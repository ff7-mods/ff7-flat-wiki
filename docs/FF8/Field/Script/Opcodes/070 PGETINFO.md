---
title: 070 PGETINFO
---

[Home](../../../../Main Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 070 PGETINFO

-   Opcode: **0x070**
-   Short name: **PGETINFO**
-   Long name: Get Party Member Worldspace Coordinates?

#### Argument

none

#### Stack

  
*Party slot*

**PGETINFO**

#### Description

Pushes the given party member's X position into temp variable 0, Y position into temp variable 1, (and maybe z? facing?).

Temp variables can be accessed with PSHI\_L.
