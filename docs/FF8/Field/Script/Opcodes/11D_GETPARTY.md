---
title: 11D_GETPARTY
---

[Home](../../../../Main_Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 11D GETPARTY

-   Opcode: **0x11D**
-   Short name: **GETPARTY**
-   Long name: Get characetr in party slot

#### Argument

none

#### Stack

  
*Party Slot*

**GETPARTY**

#### Description

Pushes the ID of the character in the given slot to temporary variable 0. Has weird results when passed a parameter of 3 or greater (so don't do it!).
