---
title: 085 CTURNL
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 085 CTURNL

-   Opcode: **0x085**
-   Short name: **CTURNL**
-   Long name: Turn Character

#### Argument

none

#### Stack

  
*Angle to face*

*Duration of turn* (frames)

**CTURNL**

#### Description

Turns this entity.

Note that Final Fantasy 8 uses 256 degree circles. Degrees 0 and 256 are
defined as down, 64 right, 128 up, 192 left.

It's unknown how this is any different from [CTURNR][].

  [CTURNR]: /ff7-flat-wiki/FF8/Field/Script/Opcodes/084%20CTURNR.md "wikilink"
