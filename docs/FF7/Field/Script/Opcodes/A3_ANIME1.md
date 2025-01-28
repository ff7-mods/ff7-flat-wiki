---
title: A3_ANIME1
---

- Opcode: **0xA3**
- Short name: **ANIME1**
- Long name: Wait While Animate/Return

#### Memory layout

| 0xA3 | *A* | *S* |
|------|-----|-----|

#### Arguments

- **const UByte** *A*: Animation ID for this entity's field object.
- **const UByte** *S*: Speed the animation is played at. Real model animation speed divide by this to calculate real play speed.

#### Description

Plays the animation found at ID *A* in this entity's field object, at the speed marked by *S*. When the animation is completed, the field object returns to its original state.

The current script's execution is halted whilst the animation is played, and continues when the animation has completed.

Makou Reactor Description: Play animation \#%1 of the field model and reset to previous state (speed=%2)
