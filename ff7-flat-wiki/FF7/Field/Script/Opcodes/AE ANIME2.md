---
title: AE ANIME2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > AE ANIME2

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

  [ANIME1]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/A3%20ANIME1.md "wikilink"
