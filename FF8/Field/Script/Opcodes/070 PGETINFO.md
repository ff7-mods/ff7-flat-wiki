---
title: 070 PGETINFO
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 070 PGETINFO

-   Opcode: **0x070**
-   Short name: **PGETINFO**
-   Long name: Get Party Member Worldspace Coordinates?

#### Argument

none

#### Stack

  
*Party slot*

**PGETINFO**

#### Description

Pushes the given party member's X position into temp variable 0, Y
position into temp variable 1, (and maybe z? facing?).

Temp variables can be accessed with PSHI\_L.
