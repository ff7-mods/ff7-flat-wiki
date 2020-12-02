---
title: 05C MAPJUMPO
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 05C MAPJUMPO

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
