---
title: E4_BGCLR
---

- Opcode: **0xE4**
- Short name: **BGCLR**
- Long name: Background Clear

#### Memory layout

| 0xE4 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *A*, or zero if *A* is specified as a literal.
- **const UByte** *A*: The ID of the background area to clear, as specified in the background's sprite, or the address to retrieve the value if *B* is non-zero.

#### Description

Hides all portions of background whose sprite specifies that it belongs to the background area given by *A*.
