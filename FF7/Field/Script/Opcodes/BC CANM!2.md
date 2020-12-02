---
title: BC CANM!2
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > BC CANM!2

-   Opcode: **0xBC**
-   Short name: **CANM!2**
-   Long name: Particial Animation.

#### Memory layout

| 0xAF | *A* | *F* | *L* | *S* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *A*: Animation ID for this entity's field object.
-   **const UByte** *F*: First frame of animation.
-   **const UByte** *L*: Last frame of animation.
-   **const UByte** *S*: Relative speed of animation. Real model
    animation speed divide by this to calculate real play speed.

#### Description

Exactly the same as [ANIM!2][], but allow set first and last frame of
given animation.

Makou Reactor Description: Play partially the animation \#%1 of the
field model (first frame=%2, last frame=%3, speed=%4)

  [ANIM!2]: FF7/Field/Script/Opcodes/BA%20ANIM!2.md "wikilink"
