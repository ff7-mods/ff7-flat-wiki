---
title: 71_BTLON
---

- Opcode: **0x71**
- Short name: **BTLON**
- Long name: Battle Switch

#### Memory layout

| 0x71 | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: Switch battles on/off (0/1, respectively).

#### Description

Turns random encounters on or off for this field. Note that if a field does not have any [Encounter Data](../../Encounter) set in its field file, battles will not occur regardless of the argument passed with this opcode.
