---
title: 175_UNKNOWN10
---

[Home](../../../../index.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 175 UNKNOWN10

-   Opcode: **0x175**
-   Short name: **UNKNOWN10**
-   Long name: (?)

#### Argument

none

#### Stack

none

#### Description

I think this pushes the current sample time of the playing music track (or something like that) into temporary variable 0. UNKNOWN10 is always called just before a map transition, and after the transition, the variables storing the result (bytes 458 and 459) are the parameter of MUSICSKIP.
