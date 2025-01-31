---
title: E3_BGROL2
---

- Opcode: **0xE3**
- Short name: **BGROL2**
- Long name: Background Roll (Reverse)

#### Memory layout

| 0xE3 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *A*, or zero if *A* is specified as a literal.
- **const UByte** *A*: The ID of the background area to roll, as specified in the background's sprite.

#### Description

Similar to [BGROL](E2_BGROL), except the roll runs backwards through layers, rather than forwards. Rolling backwards past layer 0 for the area specified results in no background being shown.
