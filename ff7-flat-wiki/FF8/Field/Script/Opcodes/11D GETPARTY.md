---
title: 11D GETPARTY
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 11D GETPARTY

-   Opcode: **0x11D**
-   Short name: **GETPARTY**
-   Long name: Get characetr in party slot

#### Argument

none

#### Stack

  
*Party Slot*

**GETPARTY**

#### Description

Pushes the ID of the character in the given slot to temporary variable
0. Has weird results when passed a parameter of 3 or greater (so don't
do it!).
