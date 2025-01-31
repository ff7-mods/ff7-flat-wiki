---
title: A2_DFANM
---

- Opcode: **0xA2**
- Short name: **DFANM**
- Long name: Animate, Loop

#### Memory layout

| 0xA2 | *A* | *S* |
|------|-----|-----|

#### Arguments

- **const UByte** *A*: Animation ID for this entity's field object.
- **const UByte** *S*: Speed the animation is played at. Higher numbers indicate slower animations.

#### Description

Plays the animation given by *A* at the speed *S*. The animation loops (plays, completes, then rewinds and plays again) until another animation is played, either using any animation opcode, or an opcode indirectly changes the animation being played, such as [MOVE](A8_MOVE).

Makou Reactor Description: Play loop animation \#%1 of the field model (speed=%2)
