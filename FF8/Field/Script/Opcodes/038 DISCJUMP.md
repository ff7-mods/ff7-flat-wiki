---
title: 038 DISCJUMP
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 038 DISCJUMP

-   Opcode: **0x038**
-   Short name: **DISCJUMP**
-   Long name: Disc change and map jump

#### Argument

Walkmesh ID

#### Stack

  
*Field Map ID*

*XCoord*

*YCoord*

*ZCoord*

*(angle?)*

**DISCJUMP**

#### Description

Same as [MAPJUMP3][], but also initiate a [DISC][] switch.

  [MAPJUMP3]: FF8/Field/Script/Opcodes/02A%20MAPJUMP3.md "wikilink"
  [DISC]: FF8/Field/Script/Opcodes/11F%20DISC.md "wikilink"
