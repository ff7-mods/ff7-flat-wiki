---
title: Animation_Script
---

This page contains information related to the AB animation files of battle models.

Any code less than 8Eh is treated as a raw animation index to be executed.

| Code | Arguments | Effect |
|:--:|:--:|:--:|
| 8E |  | Turns some flag on (Can only be executed once) |
| 8F |  | Unsets whatever flag 8E sets |
| 90 | byte, word | Change color \[byte\] in texture of currently used CLUT to \[word\] (Might apply to all textures or just first texture. Not sure. It was written with the understanding that it's only going to be used on Emerald Weapon's eyes. ie, it will only affect enemy slots 2-6) |
| 91 | byte | After a \[byte\] frame delay, do ??? |
| 92 |  | Suspend ATB (Cannot undo) |
| 93 |  | Fade whole screen to black (battle still continues) |
| 94 | word, word, byte | Rotate \[word0 - word1\] units in steps of \[byte\] (a unit is 360/4096 degrees) |
| 95 |  | Used for escaping |
| 96 | byte, byte | Barret's muzzle flash beginning in byte0 frames lasting for byte1 frames |
| 97 | byte, byte |  |
| 98 | byte | Displays action's name in \[byte\] frames |
| 99 | byte, word, word, byte | Used only by some of Yuffie's and Cid's Limit breaks? |
| 9A | word, word | Unused, but same as FB |
| 9B |  | Sets a flag that BD also sets (unknown effect) |
| 9C |  | Sets min;max volume to 1;127 |
| 9D | byte (0-6 inclusive) | Something to do with Tifa's limits |
| 9E |  | Pause here until all animation/damage handlers are finished. |
| 9F |  | Unused to unset flag that 9B and BD set |
| A0 | byte | Used by Carry Armor's Left Arm's 'Grab' |
| A1 | byte, byte | Do \[byte0?\] at \[byte1\] frame intervals (byte1 definitely increases frequency of damage counter appearance during multi-hit actions) |
| A2 | byte | Performs transformation a la Vincent's Limit Break set by AC and play animation script \[byte\] of new model |
| A3 | byte | Looks like it should change effect volume to \[byte\]/128, but in practice seems to mute them. |
| A4 |  | E.Skill charge effect (remains stationary on actor's position when called) |
| A5 |  | Summon charge effect (remains stationary on actor's position when called) |
| A6 |  | Return defending actor to original position (slightly different from FA) |
| A7 | byte |  |
| A8 | byte, byte | Wait for \[byte0\] frames then interpolate actor's current position back to original position in \[byte1\] frames |
| A9 |  | Used in idle animations\* (A9\[\]\[00\] this increment script pointer by 2 and execute animation on second pointer.) |
| AA |  | Continue camera scripts (if it was paused before). |
| AB | word, word | Move to position \[word0, 0\] relative to target of current action (word1 is ignored; used during "Cover") |
| AC | byte | Set character transformation to \[byte\] |
| AD | byte, word, byte, byte | AD\[joint XX\]\[distance XXXX\]\[start XX\]\[end XX\] Attach effect machinegun to given joint with given distanse from this joint which starts and ends at given number of frames. Always machingun fire. If end 0x80 byte is set then we do not add shell effect. |
| AE |  | Removes target from battle and resets some things |
| AF | byte | Used by Carry Armor's Right Arm's 'Grab' |
| B0 |  | No noticeable effect while used in a script |
| B1 |  | Almost identical to B0, still no effect |
| B2 |  | Duplicate of C9; could be considered a NOP |
| B3 |  | If actor does not have Small, loop until B2 is found (never used) |
| B4 |  | If Back attack or Pincer attack, make actor face appropriate direction. |
| B5 | word, word, word, byte, word, word | Only used by Mu and Trick Play. Something about positioning. |
| B6 | byte | Pause camera scripts and play animation \[byte\] one time. Used to smoothly finish idle animation before start of anything else. Camera paused because we want camera be sync with start of action (this is just finish animation that was already started). |
| B7 |  | Forces Death Animation (actor is still present and can function) |
| B8 |  |  |
| B9 | byte | Run init battle cam script \[byte\] |
| BA | word | Forces idle rotation to \[word0\]? |
| BB |  | DUMMY; treated like animation script (might crash) |
| BC | byte | Set idle cam index to \[byte\] |
| BD | word, word |  |
| BE | byte | Queue sound to be played and target reaction in \[byte\] frames (for multiple strike actions \[unless Frog status?\]) (after wait time ends execute hurt action, effect, sound. This will NOT display damage and barriers effect.) |
| BF | byte, byte |  |
| C0 |  | DUMMY; treated like animation script (might crash) |
| C1 |  | Unconditional "Jump to first C9 from start of script" |
| C2 | byte | Queue damage display in \[byte\] frames (does not play sound) |
| C3 |  |  |
| C4 | word, byte | In each of the next \[byte\] frames, move \[word\] units along the X-axis |
| C5 |  | Sets the wait timer to a predetermined amount (15 by default) |
| C6 | byte | Sets the predetermined wait time (see C5) to \[byte\] |
| C7 | word, byte | Force enemy in relative formation position \[word\] to perform their \[byte\] animation script |
| C8 | word, word, byte | Set actor's position to \[word0,word1\] in \[byte\] frames |
| C9 |  | Jump destination |
| CA |  | While background load thread is active, jump to C9 (used to load additional magic effect from separate files) |
| CB | byte, word, byte, byte, byte, byte, byte |  |
| CC | byte | Travel from current position to location that goes between center of enemy party(?) in \[byte\] frames |
| CD |  | Jump Destination (CE only); DUMMY; treated like animation script (might crash) |
| CE | byte | If actor is enemy jump to CD (Used for frog status) |
| CF | word, word, word, byte, byte | Move to \[word0,word1,word2\] relative to target in \[byte1\] frames. (byte0 ignored?) |
| D0 | word, byte (0-7 inclusive) | Move to position \[word, 0\] relative to target in either 5 (if byte is \< 4) or 8 (if byte \> 3 and \< 7) or 0 (otherwise) frames |
| D1 | word, word, byte | Move to position \[word0, word1\] relative to target in \[byte\] frames |
| D2 |  | DUMMY; treated like animation script (might crash) |
| D3 |  | DUMMY; treated like animation script (might crash) |
| D4 | word, byte | Move to position \[word0,0\] relative to self in \[byte\] frames |
| D5 | word, word, word, byte, byte | Move to \[word0,word1,word2\] relative to self in \[byte1\] frames. (byte0 ignored?) |
| D6 | byte | Delay for \[byte\] frames, then do ??? (similar to 91, but does something else) |
| D7 | byte, byte | After \[byte0\] delay, play sound \[byte1\] (only used with Grangalan and probably deprecated in favor of D8) |
| D8 | byte, word | After \[byte\] delay, play sound with attackers settings \[word\] |
| D9 |  | DUMMY; treated like animation script (might crash) |
| DA | byte | Set animation index to \[byte\] and force command to be magic (UNUSED) |
| DB | word, byte, byte | Like 96 and AD without the first byte (UNUSED) |
| DC | byte, word | Set some value with \[byte\] as an index (0-1 inclusive) to \[word\] (Eagle Gun is the only one that uses this) |
| DD | byte, byte | Directly related to DC. Sets some data for an upcoming Effect. |
| DE | byte, byte | Nearly identical to DD, but uses different data to set the same data that DC uses. |
| DF |  | Calculates an angle from the actor to the center of the opposing team's formation. |
| E0 |  | Limit charge effect (remains stationary on actor's position when called) |
| E1 |  |  |
| E2 |  |  |
| E3 |  |  |
| E4 |  |  |
| E5 |  | Reset actor's standing position |
| E6 |  | Magic charge effect (remains stationary on actor's position when called) |
| E7 | byte |  |
| E8 |  | start load requested effect during attack (attack type id and attack id are used to determinate what effect to load). |
| E9 | word, byte |  |
| EA |  | Display Action's name |
| EB |  |  |
| EC |  | If effect not loaded we will call this opcode until it does. For magic, summon, limit, enemy skill and enemy attack we execute loaded effect. All effects are hardcoded so they can do whatever they want (play sounds, display damage, request hurt for target and so on). |
| ED |  |  |
| EE |  | Run Idle Animation script |
| EF |  | DUMMY; treated like animation script (might crash) |
| F0 |  | set effect (foot_dust). |
| F1 |  |  |
| F2 |  |  |
| F3 |  | decrement wait time until 0, then continue script |
| F4 | byte | Set frames to wait \[byte\] |
| F5 | byte |  |
| F6 |  | play die effect (depends on die type) if unit is dead. Used in enemy hurt actions. |
| F7 | byte | Play sound effect, queue reaction, and display damage \[byte\] frames from this point. This will display damage and barriers effect. |
| F8 | byte | Advance texture animation (among other things?) |
| F9 |  |  |
| FA |  | Return actor to previous position |
| FB | word, word | Move to \[word, word\] position relative to target |
| FC |  | set direction for targets (delayed) and attacker acording to situation. |
| FD | word, word, word |  |
| FE | byte | If byte is C0h, End of script. |
| FF |  | Duplicate of EE |
|  |  |  |

NOTES: A9 - This skips the next byte and causes it to play the animation in the byte afterwards before moving the script pointer to the third byte. It looks like this does some "clear state" action every time the idle script is executed, but the idle scripts all cause loops so this is executed after returning from any other animation. Most enemy idle scripts are

`A9 C9 00 C1`

while a few enemies and all playable character's idle scripts read

`00 FE C0`

They seem to translate to the same thing.
