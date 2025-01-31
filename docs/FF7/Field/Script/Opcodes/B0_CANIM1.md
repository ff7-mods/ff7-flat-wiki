---
title: B0_CANIM1
---

- Opcode: **0xB0**
- Short name: **CANIM1**
- Long name: Particial Animation.

#### Memory layout

| 0xAF | *A* | *F* | *L* | *S* |
|------|-----|-----|-----|-----|

#### Arguments

- **const UByte** *A*: Animation ID for this entity's field object.
- **const UByte** *F*: First frame of animation.
- **const UByte** *L*: Last frame of animation.
- **const UByte** *S*: Relative speed of animation. Real model animation speed divide by this to calculate real play speed.

#### Description

Exactly the same as [ANIME2](AE_ANIME2), but allow set first and last frame of given animation.

Makou Reactor Description: Play partially the animation \#%1 of the field model and reset to initial state (first frame=%2, last frame=%3, speed=%4)
