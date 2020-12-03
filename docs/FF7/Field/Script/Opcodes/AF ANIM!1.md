---
title: AF ANIM!1
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > AF ANIM!1

-   Opcode: **0xAF**
-   Short name: **ANIM!1**
-   Long name: Wait While Animate/Stay

#### Memory layout

| 0xAF | *A* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *A*: Animation ID for this entity's field object.
-   **const UByte** *S*: Speed the animation is played at. Higher
    numbers indicate slower animations.

#### Description

Similarly to [ANIME1][], **ANIM!1** plays the animation found at ID *A*
in this entity's field object, at the speed marked by *S*. However, when
the animation is completed, the field object stays posed in the last
frame of the animation.

Script execution is not halted whilst the animation plays.

Makou Reactor Description: Play animation \#%1 of the field model
(speed=%2, type=1)

  [ANIME1]: A3%20ANIME1.md "wikilink"
