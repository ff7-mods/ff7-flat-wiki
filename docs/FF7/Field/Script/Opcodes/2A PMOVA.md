---
title: 2A PMOVA
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 2A PMOVA

-   Opcode: **0x2A**
-   Short name: **PMOVA**
-   Long name: Move to Party Member

#### Memory layout

| 0x2A | *P* |
|------|-----|

#### Arguments

-   **const UByte** *P*: Party member to move towards (0 to 2).

#### Description

Makes the field object/character that the script's entity is assigned
to, move/walk to the party member specified by *P*. When the object
reaches its destination, script execution continues.
