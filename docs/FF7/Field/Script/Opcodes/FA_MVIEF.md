---
title: FA_MVIEF
---

- Opcode: **0xFA**
- Short name: **MVIEF**
- Long name: Movie Frame

#### Memory layout

| 0xFA | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store result; should be a 16-bit bank.
- **const UByte** *A*: Address to store result.

#### Description

Stores the frame number of the current [MOVIE](F9_MOVIE) that is being displayed, in the bank and address specified.
