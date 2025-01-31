---
title: B1_CANM!1
---

- Opcode: **0xB1**
- Short name: **CANM!1**
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

Exactly the same as [ANIM!1](AF_ANIM!1), but allow set first and last frame of given animation.

Makou Reactor Description: Play partially the animation \#%1 of the field model (first frame=%2, last frame=%3, speed=%4)
