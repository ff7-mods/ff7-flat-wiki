---
title: 05C MAPJUMPO
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 05C MAPJUMPO

-   Opcode: **0x05C**
-   Short name: **MAPJUMPO**
-   Long name: Map jump

#### Argument

none

#### Stack

  
*Field Map ID*

*Walkmesh ID*

**MAPJUMPO**

#### Description

Jump the player to the field with the given ID and starting on the given
walkmesh triangle. The walkmesh is almost always 0 because MAPJUMPO is
intended to be used for teleporting the player into a cutscene, and the
cutscenes place the characters where they need to be on initialization,
so it doesn't matter where they're initially teleported.
