---
title: 175 UNKNOWN10
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 175 UNKNOWN10

-   Opcode: **0x175**
-   Short name: **UNKNOWN10**
-   Long name: (?)

#### Argument

none

#### Stack

none

#### Description

I think this pushes the current sample time of the playing music track
(or something like that) into temporary variable 0. UNKNOWN10 is always
called just before a map transition, and after the transition, the
variables storing the result (bytes 458 and 459) are the parameter of
MUSICSKIP.
