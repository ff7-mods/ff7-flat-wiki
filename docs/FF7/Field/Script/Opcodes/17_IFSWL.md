---
title: 17_IFSWL
---

- Opcode: **0x17**
- Short name: **IFSWL**
- Long name: If (Signed Word, Long Jump)

#### Memory layout

| 0x17 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: First memory bank to access.
- **const Bit\[4\]** *B2*: Second memory bank to access.
- **const UShort** *A*: Address, from the first bank, of the value to retrieve.
- **const Short** *V*: Unsigned value to compare the retrieved value to, or address from the second bank of the value to retrieve, if *B2* is non-zero.
- **const UByte** *C*: Type of comparison to perform.
- **const UShort** *E*: Amount to jump if the comparison does not hold.

#### Description

This is similar to the [IFSW](16_IFSW) opcode in allowing the comparison value to be negative, but in addition, allows the jump on comparison failure to be longer than 0xFF bytes.
