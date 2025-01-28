---
title: 3B_CHGLD
---

- Opcode: **0x3B**
- Short name: **CHGLD**
- Long name: Check Gil

#### Memory layout

| 0x3B | *B1 / B2* | *A1* | *A2* |
|------|-----------|------|------|

#### Arguments

- **const Bit\[4\]** *B1*: Destination bank 1.
- **const Bit\[4\]** *B2*: Destination bank 2.
- **const UByte** *A1*: Destination address 1.
- **const UByte** *A2*: Destination address 2.

#### Description

Copies the amount of gil the party has into the destination addresses. As the gil amount is a four-byte value, the arguments require two destination addresses to place two two-byte values into. Address 1 takes the lower two bytes of the gil amount, while address 2 takes the higher two bytes.
