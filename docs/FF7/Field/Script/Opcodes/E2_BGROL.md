---
title: E2_BGROL
---

- Opcode: **0xE2**
- Short name: **BGROL**
- Long name: Background Roll

#### Memory layout

| 0xE2 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *A*, or zero if *A* is specified as a literal.
- **const UByte** *A*: The ID of the background area to roll, as specified in the background's sprite.

#### Description

Turns on the next numerical layer in the background area specified by *A*. For example, if background area 3 is currently set to [display layer](E0_BGON) will display layer 2 for that area. If an invalid layer is given, or the background rolls past the last layer for this area, no background is displayed by this opcode.
