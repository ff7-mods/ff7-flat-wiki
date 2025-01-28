---
title: D5_COS
---

- Opcode: **0xD5**
- Short name: **COS**
- Long name: COS Calculation

#### Memory layout

| 0xD5 | *B1 / B2* | *B3 / B4* | *D* | *M* | *A* | *S* |
|------|-----------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Destination bank.
- **const Bit\[4\]** *B2*: Bank to retrieve *M*, or zero if *M* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *A*, or zero if *A* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *S*, or zero if *S* is specified as a literal value.
- **const UByte** *D*: Destination address.
- **const UByte** *M*: Multiplicand, or address to retrieve value if *B2* is non-zero.
- **const UByte** *A*: Addition, or address to retrieve value if *B3* is non-zero.
- **const UByte** *S*: Variable for cos angle, or source address to retrieve value if *B4* is non-zero.

#### Description

`Var[B1][D] = ( ( Math.cos(Var[B4][S]) * M) + A) >> 12`

Creates a variable from the another variable, with COS, a multiplicand and an addition factor
