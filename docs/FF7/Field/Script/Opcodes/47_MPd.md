---
title: 47_MPd
---

- Opcode: **0x47**
- Short name: **MPd**
- Long name: MP Down

#### Memory layout

| 0x47 | *B* | *P* | *V* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve value for decreasing, or zero if the amount is specified by a constant in *V*.
- **const UByte** *P*: Party member whose MP will decrease (0 to 2).
- **const UShort** *V*: Value to decrease MP by, or address to retrieve value from if *B* is non-zero.

#### Description

Decreases the MP of the party member specified by *P* by the amount *V*. If *B* is non-zero, then the value to decrease by is retrieved from bank *B* and address *V*.
