---
title: 34_PDIRA
---

- Opcode: **0x34**
- Short name: **PDIRA**
- Long name: Face Party Member

#### Memory layout

| 0x34 | *C* |
|------|-----|

#### Arguments

- **const UByte** *C*: Character ID to face.

#### Description

Instantly turns the field object to face the party member specified by **C**. In contrast to [PTURA](FF7/Field/Script/Opcodes/35_PTURA "wikilink"), the turn is not gradual, and the parameter is not a party member ID (from 0 for the first to 2 for the third in the party), but a Character ID (like in [MMBud](CD_MMBud). If the specified character ID is not in your party, the field object will turn to the main character.
