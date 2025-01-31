---
title: Script
---

## Script Engine

### Instructions & Stack

The Worldmap scripting engine for FF7 is very different from the field scripting format. It is a stack based language and for the most part instructions are the same size (16 bits), instead of having their parameters encoded into the instruction they take a predefined number of items off the stack and operate on that data. There are a few instructions that incorporate another word (16 bits) of immediate data, such instructions are clearly marked in the [opcode list](Script/Opcodes).

The stack itself is global, there is only one stack which is shared between all scripts that are currently running. It is 8 levels deep, that is to say a maximum of 8 different items can be on the stack at any given time. A given item on the stack is not evaluated until it is popped off the stack, which can be a little unintuitive. For example, pushing the current X position of the player does not actually read the players position at that time, only when the value is actually used will it be fetched from the player entity. In practice this is not an issue because the script itself would have to change the position in between pushing the value and using it. Refer to the section below for an explanation of why that is the case.

### Contexts

The script engine uses cooperative multitasking to run different scripts in parallel, the state of each script is contained in a separate context. On each frame, the game will loop over every active context and run it until it either returns or enters a waiting state. This means that scripts cannot run too long or they will slow down the game, an infinite loop will lock up the game completely. This also means that from the scripts point of view, nothing will happen until it returns or enters a wait state, the game is not running and no other script can run during this time.

### Entities & Models

The Worldmap module operates on a fixed set of models, each having a specific model ID.

| Model ID |          Name          |
|:--------:|:----------------------:|
|    0     |         Cloud          |
|    1     |          Tifa          |
|    2     |          Cid           |
|    3     |        Highwind        |
|    4     |      Wild Chocobo      |
|    5     |      Tiny Bronco       |
|    6     |         Buggy          |
|    7     |      Junon Canon       |
|    8     |       Cargo Ship       |
|    9     | Highwind's propellers  |
|    10    |     Diamond Weapon     |
|    11    |    Ultimate Weapon     |
|    12    |  Fort Condor's Condor  |
|    13    |       Submarine        |
|    14    |      Gold Saucer       |
|    15    |  Rocket Town's Rocket  |
|    16    | Rocket Town Launch Pad |
|    17    |     Sunken Gelnika     |
|    18    |   Underwater Reactor   |
|    19    |        Chocobo         |
|    20    |      Midgar Canon      |
|    21    |        Unknown         |
|    22    |        Unknown         |
|    23    |        Unknown         |
|    24    |  North Crater Barrier  |
|    25    |     Ancient Forest     |
|    26    |  Key of the Ancients   |
|    27    |        Unknown         |
|    28    |     Red Submarine      |
|    29    |      Ruby Weapon       |
|    30    |     Emerald Weapon     |

Type = 1, Model function

Each model that is currently loaded into the map also has an entity associated with it, this is the state of the model and holds information such as its position, rotation, current animation etc. Most instructions operate on the current active entity, which can be changed with the [330](Script/Opcodes/330) opcode. The current active entity can also change as a side effect of certain instructions, all known cases are documented in the opcode descriptions but the list is not complete. The variable holding the current active entity is a global variable that resets every frame, if a script enters a wait state the current active entity is undefined when executing resumes.

Each entity is also a context (see the above section for more information about contexts) and in fact, there is no difference whatsoever between an entity and a context. The distinction is made because of the way they are treated by the scripting engine, the script state of the active entity (or any entity for that matter) cannot be modified (other than asking it to execute a function by means of the [204](Script/Opcodes/204) and conversely, the state of the model corresponding to the context cannot be modified unless it is also the current active entity. This is the default state, whenever a function begins execution the context and current active entity are always equal.

In addition to the contexts associated with the models there is also a system context, this is where execution begins when the worldmap is first loaded and it also handles events which are not specific to any model on the map. The system context is technically an entity because, again, contexts and entities are the same thing but since it does not correspond to a model, manipulating the state of the system "entity" is an error.

### Functions

As alluded to earlier, the script engine is driven by executing functions, each model has a set of functions that are executed by the game in response to certain events;

| \# | Name | Description |
|:--:|:--:|:--:|
| 0 | Enter | Called when the model is loaded |
| 1 | Exit | Called when the model is unloaded |
| 2 | Tick | Called each frame if the model is set to recieve ticks? |
| 3 | Movement? | Seems to be called for certain models that move around the map |
| 4 | Action | Called when player interacts with the model |
| 5 | Unknown |  |

This table is probably not complete.

There is also a set of 32 system functions that are executed in response to certain events. First 10 are called by the game's executable (subroutine at address 0x7640BC in the PC version), while the remaining ones are called by the WM scripts using the "[run function](Script/Opcodes/204)" opcode with Model ID parameter set to 0xFFFF.

| \# | Name | Description |
|:--:|:--:|:--:|
| 0 | Enter | Called when the worldmap is loaded |
| 1 | Exit | Called when the worldmap is unloaded |
| 2 | Tick | Called each frame (only does a check if Zolom should be reset) |
| 3 | Dummy function (copy of Function ID 2) |  |
| 4 | Dummy function (copy of Function ID 2) |  |
| 5 | Dummy function (copy of Function ID 2) |  |
| 6 | Unknown | Enter highwind interior |
| 7 | Midgar Zolom | Called when the player touches the midgar zolom in the swamp. |
| 8 | Dummy function (copy of Function ID 2) |  |
| 9 | Northern Cave landing | Checks if Highwind can land in the crater switches to Highwind Deck map |

And finally there is a set of functions which are called when the player steps on a walkmesh triangle that is designated to trigger a script. Which function is executed depends on the mesh coordinates of the player (0-35, 0-27) as well as the function ID [from the MAP file](../WorldMap_Module#Triangle) Fortunately, not all functions need to be implemented, as will become apparent in the next section, functions that do nothing do not need to be implemented at all. Most of the mesh functions handle entering field levels from the world map.

## .ev Format

### Call Table

The first 0x400 bytes of an .ev file is the call table, a mapping between functions and entry points. Each entry is 4 bytes, 2 bytes of function identifier and 2 bytes instruction pointer. Instruction pointers are in 2-byte increments from the start of the code section. The first two bits (most significant) of the function identifier defines the format of the remaining 14 bits;

|            size            | description |
|:--------------------------:|:-----------:|
|           6 bits           |   Padding   |
| 8 bits (least significant) | Function \# |

Type = 0, System function

|            size            | description |
|:--------------------------:|:-----------:|
|           6 bits           |  Model ID   |
| 8 bits (least significant) | Function \# |

Type = 1, Model function

|            size            |     description     |
|:--------------------------:|:-------------------:|
|          10 bits           | MeshX + MeshZ \* 36 |
| 4 bits (least significant) |    Walkmesh type    |

Type = 2, Mesh function

Call table entries MUST be sorted in ascending order of function identifier! Duplicate function IDs are not recommended as they can cause some very unpredictable behavior. Original FF7 data seems to duplicate the 0 identifier, it is possible that the first entry does not count? It is probably best to ignore the first entry altogether. If the game attempts to call a function for which no identifier can be found in the call table the call will simply be ignored. It is not an error to leave a function unimplemented if it does not have a use. The call table should be kept compact with all empty entries at the end with a function identifier of 0xFFFF and an instruction pointer of 0.

### Code

After the call table follows 0x6C00 bytes of code. The .exe would have to be patched to accommodate for a larger code size. The entire code section is treated as a continuous area of 16-bit values, no padding is necessary between functions and functions do not even have to be contiguous in memory (although it is highly recommended). Due to an implementation detail the first function should start at offset 1 (an instruction pointer of 0 means the context is not active), just in case it is probably a good idea to make the first instruction always be a single [return](Script/Opcodes/203) instruction.
