---
title: D0_LINE
---

- Opcode: **0xD0**
- Short name: **LINE**
- Long name: Line Definition

#### Memory layout

| 0xD0 | *XA* | *YA* | *ZA* | *XB* | *YB* | *ZB* |
|------|------|------|------|------|------|------|

#### Arguments

- **const Short** *XA*: X-coordinate of the first point of the line.
- **const Short** *YA*: Y-coordinate of the first point of the line.
- **const Short** *ZA*: Z-coordinate of the first point of the line.
- **const Short** *XB*: X-coordinate of the second point of the line.
- **const Short** *YB*: Y-coordinate of the second point of the line.
- **const Short** *ZB*: Z-coordinate of the second point of the line.

#### Description

Defines a line on the walkmesh that, when crossed by a playable character, causes one of the entity's scripts to be executed. These are similar to the triggers in [Section 8](FF7/Field/3D_Related "wikilink"). All the lines in the current field can be turned on or off by using the [LINON](D1_LINON) opcode.

#### Additional Detail

There are generally 6 scripts (other than the init and main) if the entity is a LINE (taken from Makou Reactor):

- script index 2 -\> S1 - \[OK\]
- script index 3 -\> S2 - Move
- script index 4 -\> S3 - Move
- script index 5 -\> S4 - Go
- script index 6 -\> S5 - Go 1x
- script index 7 -\> S6 - Go away

Here is a JSON file containing a little more details on the occurrences, frequencies and combinations of the LINE op code usage: <https://github.com/dangarfield/ff7-fenrir/blob/master/workings-out/output/line-occurences.json>

**S1 - \[OK\]**

Appears to be the same as the S2 - Move, in that it is triggered on proximity, but it is also triggered with the CIRCLE button. If you hold the circle, it is only triggered once as apposed the directional movements as mentioned above.

**S2 - Move**

Triggered EVERY time an input key is pressed when the character will be in close proximity to the line. If the line is near a wall and a direction key is pressed but the player does not move but they are in proximity to the line, the Move command will be called every time (eg each frame)

It is not dependent on cross the line in either direction, appears to be purely proximity to the line. Once this has been triggered, moving the character away from the line had no effect, the operations are still queued and played until a return is met.

**S3 - Move**

Appears to be the same as the S2 - Move, but the proximity is VERY close to the line.

Once this has been triggered, moving the character away from the line had no effect, the operations are still queued and played until a return is met.

**S4 - Go**

Whilst the character is in proximity of the line (irrespective of the buttons pressed), this action is triggered. Appears to be the same distances as S2 - Move. Eg, if you stand on a line that simply plans a sound and returns, the sound will play every frame.

**S5 - Go 1x**

Whilst the character is in proximity of the line (irrespective of the buttons pressed), this action is triggered ONCE. If the character travels away from the proximity of the line then back towards it, this is triggered once more.

Once this has been triggered, moving the character away from the line had no effect, the operations are still queued and played until a return is met.

**S6 - Go away**

After the character has been in proximity of line and exits the immediate proximity (but is still within an outer proximity) this script is triggered.

**Concurrency**

Only one script can be running per entity at any one time. Eg, if there is a line with Go and Go away, but the Go takes 120 frames, and by the time the script has finished, the player in now longer within the outer boundary to trigger the Go away script. The Go script returns and the Go away script is not triggered.

It appears as though the priority for running the scripts is as follows:

- S5 - Go 1x
- S4 - Go
- S2 - Move
- S3 - Move
- S1 - \[OK\]
- S6 - Go away
