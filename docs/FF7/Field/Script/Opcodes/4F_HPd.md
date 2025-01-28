---
title: 4F_HPd
---

- Opcode: **0x4F**
- Short name: **HPd**
- Long name: HP Down

#### Memory layout

| 0x4F | *B* | *P* | *V* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve value for decreasing, or zero if the amount is specified by a constant in *V*.
- **const UByte** *P*: Party member whose HP will decrease (0 to 2).
- **const UShort** *V*: Value to decrease HP by, or address to retrieve value from if *B* is non-zero.

#### Description

Decreases the HP of the party member specified by *P* by the amount *V*. If *B* is non-zero, then the value to decrease by is retrieved from bank *B* and address *V*.
