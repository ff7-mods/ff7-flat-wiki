---
title: 4B_BTLTB
---

- Opcode: **0x4B**
- Short name: **BTLTB**
- Long name: Battle Table

#### Memory layout

| 0x4B | *I* |
|------|-----|

#### Arguments

- **const UByte** *I*: ID of the encounter table to use, either 0 (standard) or 1.

#### Description

Switches between the two sets of encounter data that may exist in a field file, depending on the ID given.
