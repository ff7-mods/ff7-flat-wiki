---
title: D4_SIN
---

- Opcode: **0xD4**
- Short name: **SIN**
- Long name: SIN Calculation

#### Memory layout

| 0xD4 | *B1 / B2* | *B3 / B4* | *D* | *M* | *A* | *S* |
|------|-----------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Destination bank.
- **const Bit\[4\]** *B2*: Bank to retrieve *M*, or zero if *M* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *A*, or zero if *A* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *S*, or zero if *S* is specified as a literal value.
- **const UByte** *D*: Destination address.
- **const UByte** *M*: Multiplicand, or address to retrieve value if *B2* is non-zero.
- **const UByte** *A*: Addition, or address to retrieve value if *B3* is non-zero.
- **const UByte** *S*: Variable for sin angle, or source address to retrieve value if *B4* is non-zero.

#### Description

`Var[B1][D] = ( ( Math.sin(Var[B4][S]) * M) + A) >> 12`

Creates a variable from the another variable, with SIN, a multiplicand and an addition factor
