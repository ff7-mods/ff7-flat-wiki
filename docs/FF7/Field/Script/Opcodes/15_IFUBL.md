---
title: 15_IFUBL
---

- Opcode: **0x15**
- Short name: **IFUBL**
- Long name: If (Unsigned Byte, Long Jump)

#### Memory layout

| 0x15 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: First memory bank to access.
- **const Bit\[4\]** *B2*: Second memory bank to access.
- **const UByte** *A*: Address, from the first bank, of the value to retrieve.
- **const UByte** *V*: Unsigned value to compare the retrieved value to, or address from the second bank of the value to retrieve.
- **const UByte** *C*: Type of comparison to perform.
- **const UShort** *E*: Amount to jump if the comparison does not hold.

#### Description

This is similar to the [IFUB](14_IFUB) opcode, but it allows a jump of more than 0xFF if the comparison does not hold. This opcode is used if the 'if' block will be longer than 0xFF.
