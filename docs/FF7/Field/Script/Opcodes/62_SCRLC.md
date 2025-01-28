---
title: 62_SCRLC
---

- Opcode: **0x62**
- Short name: **SCRLC**
- Long name: Scroll To Playable Character Stop Movement

#### Memory layout

| 0x63 | *B* | *S* | *U* | *T* |
|------|-----|-----|-----|-----|

#### Arguments

- **const UByte** *B*: PRESUME -\> Bank for the scroll speed, or zero if it is specified as a literal value. Always zero in game data
- **const UShort** *S*: Speed of the scroll, in frames, or the address to find the speed if *B* is non-zero.
- **const UByte** *U*: Unknown -\> Always zero in game data. Seems to affect the speed above.
- **const UByte** *T*: Type of scroll.

#### Description

Scrolls the current view so that the main playable character is in the center of the view. The script executes asynchronously and does not block whilst the camera movement is active but returns control to the next script operation. This is tweened over a period of *S* frames. If the main playable character also moves during this time period, the tween position is also updated to match the new playable character location. Once the camera has completed its movement, the camera NO LONGER follows the main playable character's movement. It stays in place.

#### Scroll Types

| ID | Scroll Type |
|----|----|
| 0 | No effect - Camera does not move, returns script, camera still follows the playable character is it did before |
| 1 | No effect - Camera does not move, returns script, camera still follows the playable character is it did before |
| 2 | Linear |
| 3 | Smooth (QuadraticInAndOut) |
|  |  |
