---
title: 18_IFUW
---

- Opcode: **0x18**
- Short name: **IFUW**
- Long name: If (Unsigned Word)

#### Memory layout

| 0x18 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: First memory bank to access.
- **const Bit\[4\]** *B2*: Second memory bank to access.
- **const UShort** *A*: Address, from the first bank, of the value to retrieve.
- **const UShort** *V*: Unsigned value to compare the retrieved value to, or address from the second bank of the value to retrieve, if *B2* is non-zero.
- **const UByte** *C*: Type of comparison to perform.
- **const UByte** *E*: Amount to jump if the comparison does not hold.

#### Description

This is similar to the [IFUB](14_IFUB) opcode, but it allows the value to be larger than 0xFF.
