---
title: A2 DFANM
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > A2 DFANM

-   Opcode: **0xA2**
-   Short name: **DFANM**
-   Long name: Animate, Loop

#### Memory layout

| 0xA2 | *A* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *A*: Animation ID for this entity's field object.
-   **const UByte** *S*: Speed the animation is played at. Higher
    numbers indicate slower animations.

#### Description

Plays the animation given by *A* at the speed *S*. The animation loops
(plays, completes, then rewinds and plays again) until another animation
is played, either using any animation opcode, or an opcode indirectly
changes the animation being played, such as [MOVE][].

Makou Reactor Description: Play loop animation \#%1 of the field model
(speed=%2)

  [MOVE]: FF7/Field/Script/Opcodes/A8%20MOVE.md "wikilink"
