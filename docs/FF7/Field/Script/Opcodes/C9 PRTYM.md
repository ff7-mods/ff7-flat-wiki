---
title: C9 PRTYM
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > C9 PRTYM

-   Opcode: **0xC9**
-   Short name: **PRTYM**
-   Long name: Party Remove

#### Memory layout

| 0xC9 | *C* |
|------|-----|

#### Arguments

-   **const UByte** *C*: Character ID to remove.

#### Description

Moves the specified character out of your party, if they are currently
in it to begin with. If not, this has no effect.

#### Character IDs

| ID  | Character |
|-----|-----------|
| 0   | Cloud     |
| 1   | Tifa      |
| 2   | Barret    |
| 3   | Aeris     |
| 4   | Red XIII  |
| 5   | Yuffie    |
| 6   | Cait Sith |
| 7   | Cid       |
| 8   | Vincent   |
|     |           |
