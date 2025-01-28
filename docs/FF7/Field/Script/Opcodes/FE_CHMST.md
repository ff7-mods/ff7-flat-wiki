---
title: FE_CHMST
---

- Opcode: **0xFE**
- Short name: **CHMST**
- Long name: Check Music

#### Memory layout

| 0xFE | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store boolean.
- **const UByte** *A*: Address to store boolean.

#### Description

Stores a boolean value (0 for false, 1 for true) in the bank and address specified, indicating whether music is currently playing.
