---
title: BA ANIM!2
permalink: BA ANIM!2.html
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > BA ANIM!2

-   Opcode: **0xBA**
-   Short name: **ANIM!2**
-   Long name: Animate/Stay

#### Memory layout

| 0xBA | *A* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *A*: Animation ID for this entity's field object.
-   **const UByte** *S*: Speed the animation is played at. Higher
    numbers indicate slower animations.

#### Description

Similarly to [ANIME2][], plays the animation found at ID *A* in this
entity's field object, at the speed marked by *S*. However, in contrast,
the field object stays posed in the last frame of the animation played.

The current script's execution is halted whilst the animation is played,
and continues when the animation has completed.

Makou Reactor Description: Play animation \#%1 of the field model
(speed=%2, type=2)

  [ANIME2]: AE%20ANIME2.md "wikilink"
