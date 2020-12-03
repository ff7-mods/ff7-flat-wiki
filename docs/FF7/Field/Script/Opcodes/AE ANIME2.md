---
title: AE ANIME2
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > AE ANIME2

-   Opcode: **0xAE**
-   Short name: **ANIME2**
-   Long name: Animate/Return

#### Memory layout

| 0xAE | *A* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *A*: Animation ID for this entity's field object.
-   **const UByte** *S*: Speed the animation is played at. Real model
    animation speed divide by this to calculate real play speed.

#### Description

Similarly to [ANIME1][], the animation specified by *A* is played at
speed *S* for the current entity's field object. However, in contrast,
the current script's execution is **not** halted whilst the animation is
played.

Makou Reactor Description: Play animation \#%1 of the field model and
reset to previous state (speed=%2)

  [ANIME1]: ../A3%20ANIME1.md "wikilink"
