---
title: 066 GETINFO
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 066 GETINFO

-   Opcode: **0x066**
-   Short name: **GETINFO**
-   Long name: Get Worldspace Coordinates?

#### Argument

none

#### Stack

none

#### Description

Pushes this entity's X position into temp variable 0, Y position into
temp variable 1, (and maybe z? facing?).

Temp variables can be accessed with PSHI\_L.
