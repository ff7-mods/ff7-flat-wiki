---
title: 2A_PMOVA
---

- Opcode: **0x2A**
- Short name: **PMOVA**
- Long name: Move to Party Member

#### Memory layout

| 0x2A | *P* |
|------|-----|

#### Arguments

- **const UByte** *P*: Party member to move towards (0 to 2).

#### Description

Makes the field object/character that the script's entity is assigned to, move/walk to the party member specified by *P*. When the object reaches its destination, script execution continues.
