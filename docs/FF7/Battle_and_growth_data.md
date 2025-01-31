---
title: Battle_and_growth_data
---

### Kernel.bin section 3

This file contains a bunch of information about character growth and battles. Table below explains it all (credits go to Terence F. for this).

#### General data layout

| Offset | Length | Description |
|:--:|:--:|:--:|
| 0x0000 | 56 bytes | Character data: Cloud ([see below](#character-data-record) |
| 0x0038 | 56 bytes | Character data: Barret |
| 0x0070 | 56 bytes | Character data: Tifa |
| 0x00A8 | 56 bytes | Character data: Aeris |
| 0x00E0 | 56 bytes | Character data: Red XIII |
| 0x0118 | 56 bytes | Character data: Yuffie |
| 0x0150 | 56 bytes | Character data: Cait Sith |
| 0x0188 | 56 bytes | Character data: Vincent |
| 0x01C0 | 56 bytes | Character data: Cid |
| 0x01F8 | 12 x 1 byte | Random bonus to primary stats |
| 0x0204 | 12 x 1 byte | Random bonus % to HP |
| 0x0210 | 12 x 1 byte | Random bonus % to MP |
| 0x021C | 37 x 16 bytes | Primary stat curve 0 - 36 ([see below](#stat-curve-record) |
| 0x046C | 9 x 16 bytes | HP stat curve 37 - 45 (Base \* 40) |
| 0x04FC | 9 x 16 bytes | MP stat curve 46 - 54 (Base \* 2) |
| 0x058C | 9 x 16 bytes | EXP stat curve 55 - 63 (Gradient is quadratic, no Base) |
| 0x61C | 1508 bytes | Character AI data ([see below](#character-ai-data) |
| 0xC00 | 540 bytes | FF padding |
| 0xE1C | 256 bytes | Random number look-up table (all numbers from 0-255 are here) |
| 0xF1C | 64 bytes | Scene.bin look-up table ([see below](#scene.bin-look-up-file) |
| 0xF5C | 56 bytes | Spell order from Magic menu in battles ([see below](#magic-order) |
|  |  |  |

**Table 1: Section 3 of kernel.bin description**

#### Character data record

| Offset | Length  |               Function               |
|:------:|:-------:|:------------------------------------:|
|  0x00  | 1 byte  |       Strength Level-Up Curve        |
|  0x01  | 1 byte  |       Vitality Level-Up Curve        |
|  0x02  | 1 byte  |         Magic Level-Up Curve         |
|  0x03  | 1 byte  |        Spirit Level-Up Curve         |
|  0x04  | 1 byte  |       Dexterity Level-Up Curve       |
|  0x05  | 1 byte  |         Luck Level-Up Curve          |
|  0x06  | 1 byte  |          HP Level-Up Curve           |
|  0x07  | 1 byte  |          MP Level-Up Curve           |
|  0x08  | 1 byte  |      Experience Level-Up Curve       |
|  0x09  | 1 byte  |             FF (padding)             |
|  0x0A  | 1 byte  |            Starting Level            |
|  0x0B  | 1 byte  |             FF (padding)             |
|  0x0C  | 1 byte  |          Limit Command 1-1           |
|  0x0D  | 1 byte  |          Limit Command 1-2           |
|  0x0E  | 1 byte  |      Limit Command 1-3 (UNUSED)      |
|  0x0F  | 1 byte  |          Limit Command 2-1           |
|  0x10  | 1 byte  |          Limit Command 2-2           |
|  0x11  | 1 byte  |      Limit Command 2-3 (UNUSED)      |
|  0x12  | 1 byte  |          Limit Command 3-1           |
|  0x13  | 1 byte  |          Limit Command 3-2           |
|  0x14  | 1 byte  |      Limit Command 3-3 (UNUSED)      |
|  0x15  | 1 byte  |          Limit Command 4-1           |
|  0x16  | 1 byte  |      Limit Command 4-2 (UNUSED)      |
|  0x17  | 1 byte  |      Limit Command 4-3 (UNUSED)      |
|  0x18  | 2 bytes |   Kills required for Limit Level 2   |
|  0x1A  | 2 bytes |   Kills required for Limit Level 3   |
|  0x1C  | 2 bytes |     Uses required for Limit 1-2      |
|  0x1E  | 2 bytes | Uses required for Limit 1-3 (UNUSED) |
|  0x20  | 2 bytes |     Uses required for Limit 2-2      |
|  0x22  | 2 bytes | Uses required for Limit 2-3 (UNUSED) |
|  0x24  | 2 bytes |     Uses required for Limit 3-2      |
|  0x26  | 2 bytes | Uses required for Limit 3-3 (UNUSED) |
|  0x28  | 4 bytes |     HP Divisor for Limit Level 1     |
|  0x2C  | 4 bytes |     HP Divisor for Limit Level 2     |
|  0x30  | 4 bytes |     HP Divisor for Limit Level 3     |
|  0x34  | 4 bytes |     HP Divisor for Limit Level 4     |
|        |         |                                      |

#### Stat curve record

Each entry is 16 bytes long and contains eight pairs of Gradients and Bases (1 byte each) for eight different level groups:

`2-11   12-21   22-31   32-41   42-51   52-61   62-81   82-99`

The general formula for primary stats to follow is:

`Stat Difference = Rnd(1..8) + Base + Floor(Gradient * [Level Attained] / 100) - Current Stat`

This difference is capped at 11 and the value located at &\[0x01F8 + Stat Difference\] is added to that Stat.  
  
HP and MP use a similar system, but a different formula:

`HP Baseline = Base * 40 +  (Level - 1) * Gradient`  
`MP Baseline = Base * 40 + [(Level - 1) * Gradient / 10]`  
  
`Difference = Rnd(1..8) + [100 * Baseline / Current Stat] - 100`

In the above formulas, Base is a signed byte (between -128 and 127) so Base \* 40 can range between -5120 and 5080.  
Again, this difference is capped at 11 and the appropriate points are increased by (Base is now treated as an unsigned byte):

`(&[0x204 + Difference] / 100) * Base for HP`  
`(&[0x210 + Difference] / 100) * [Level * Gradient / 10] - [(Level - 1) * Gradient / 10] for MP`

where &\[x\] is the value located at the address of this section  
  
The Experience level curves are 16 bytes long, although only eight bytes of each are used. Experience is calculated on a need-to-level basis. This means that the total Experience needed for each character to reach the next level is calculated and stored in memory.

`Needed XP = [Mod * ((Lvl-1) ^ 2) / 10]`

Where Mod is the value of the byte at the point in the curve based on the level to attain. So with a Mod of 70, to get to level 13 from level 12, a character would need:

`70 * ((13-1) ^ 2) /10 `  
`70 * (144 / 10)`  
`70 * Floor( 14.4 )`  
`980 additional XP`

The savemap contains information about the needed XP to get to the next level for each character so it can be assumed that the game only performs this calculation at level up and changes the needed XP stat accordingly and compares that against the total XP the character has to determine when the next level occurs.  
To calculate the total XP needed for a given level:

`XP = 0`  
`For I = 1 to Lvl-1`  
`  XP = XP + [Mod * (I ^ 2) / 10]`  
`Next I`

The Mod only needs to be assigned based on the character's current level.

#### Character AI data

Section contains 24-byte header representing 2-bytes per script block (1 per character?). Each number is an offset from the beginning of this block to the actual AI data. Each script block follows the same AI data found in the [Battle Scenes](FF7/Battle/Battle_scenes#AI_Data "wikilink"). A basic disassembly of the characters' scripts can be found [here](http://forums.qhimm.com/index.php?topic=7928.msg97889#msg97889)

#### Scene.bin Look-up Table

In order to understand the purpose of this table we must understand the structure of the compressed and packed [scene.bin](Battle/Battle_scenes) file. It is divided into blocks of 8K in size. Each of these blocks begins with an array of pointers that point to a compressed array of bytes that contain a single scene file. There can be between 1 and 16 inclusive scenes in each of these blocks.

There is no direct indication of how many scenes are in each block other than searching through all the headers to find the desired one. It would take a noticeable amount of time to search through each block when the greater valued formations are requested. The working solution to this is a look up table that would tell the scene retrieval method which block contains the desired scene. Enter the Scene Look-Up Table (hereafter abbreviated SLUT because I can :) ).

When a specific formation ID is requested, the Scene File that contains it can be determined like this:

`Scene File = ( Formation ID AND FFFC ) >> 2`

So, for example, we know that formation 134h would be in scene 4Dh.

Without searching through all the blocks as noted above, this table serves to indicate what the first scene is in each block of 8K. When a formation is to be loaded, the containing scene file is retrieved as mentioned above then the SLUT is looped through to find the lowest value greater than the requested scene then uses the value BEFORE that.

`Example`  
`Unmodded SLUT:`  
`00 0C 12 19 21 27 2D 35 3D 49 51 5A ...etc`  
  
`Desired scene is 4D. 51 is first in that list greater than 4D. Value to the left of that is used (49).`

Then we know that the 10th block in the scene.bin contains the scene and formation we're looking for. The rest of the details of what happens next don't matter. This is all that involves the SLUT.

This needs to be checked/updated each time the scene.bin is compressed and repacked. If not it can lead to errors and out-of-place formations being used.

As an example, if a modder changes the one of the scenes in the first block it may not be able to fit together in an 8K block of compressed space with all its original "brothers." The last scene in this block is then kicked out of that block and into the next. Now each scene in the next block is off by one file. This will domino onward displacing scene after scene until a block with enough padding can absorb a new scene without going over the 8K limit.

So if formation 31h is requested it will see that formation is part of scene 0Ch which is the first scene of block three. But since one of the scenes from block 1 became the first scene in block 2, the game will load the second formation in the first scene which won't match the one we're really looking for. The solution is to change the second byte in the SLUT to 0Bh which will correctly indicate that the desired scene is actually the second scene of block two.

Also consider if scene 0Bh were requested. The scene retrieval mentioned above leads the game to conclude that scene 0Bh is in the first block. However, when it tries to loop through the pointers in the block, it will find a null pointer. Then an error beyond your imagination will occur: the game will crash!! D: (not verified, but probably around 0x5D116B)

Both [http://forums.qhimm.com/index.php?topic=7186.0 Hojo](http://forums.qhimm.com/index.php?topic=7186.0_Hojo "wikilink") and [http://forums.qhimm.com/index.php?topic=8481.0 Proud Clod](http://forums.qhimm.com/index.php?topic=8481.0_Proud_Clod) will examine this SLUT automatically and make changes accordingly. The moral of the above story is use one of these programs when altering the scene.bin and let them take action accordingly on the KERNEL.BIN.

Bonus Info: Since there are only 64 bytes allotted to this table, there must be no more than 64 blocks in a scene.bin file which indirectly limits its size to 64 \* 8K or 512K.

#### Magic Order

This segment of data tells the game in what order to load the attacks into which Magic section. There are four Magic sections: Restore, Attack, Indirect, and Special. The first three can be reorganized in the battle's magic menu. When the first 56 attacks are loaded, these bytes tell the game which section and what order to be loaded in:

[`AAA:BBBBB`](../AAA:BBBBB)  
`AAA - Section`  
`BBBBB - Index within section of attack loaded`

The Magic menu will only display sections 0 - 3 (Summons are section 4, E.Skills are section 5, etc.). The sections are then displayed sequentially in the field magic menu and in the order specified in the battle menu.

Eg: The fourth attack in [Attack data](Attack_data) is Regen. The fourth byte in this data segment is 08. This means load Regen into section 0 at position 8.

NOTES:

- If a value is repeated, that attack will override the previous listing.
- The final two bytes are NULL (0xFF) so the game moves the Attack pointer ahead to load the summon attacks(?).
  - Even if these were not NULL, they would be ignored.
