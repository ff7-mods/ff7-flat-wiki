---
title: 01D SET
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 01D SET

-   Opcode: **0x01D**
-   Short name: **SET**
-   Long name: Set position

#### Argument

Walkmesh triangle ID.

#### Stack

  
*XCoord*

*YCoord*

**SET**

#### Description

Place this entity's model at XCoord, YCoord standing on the given
walkmesh triangle. Unlike SET3, this function will place the event on
the walkable terrain (the ZCoord is interpolated from the walkmesh).
