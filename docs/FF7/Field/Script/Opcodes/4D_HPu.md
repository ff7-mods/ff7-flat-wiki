---
title: 4D_HPu
---

- Opcode: **0x4D**
- Short name: **HPu**
- Long name: HP Up

#### Memory layout

| 0x4D | *B* | *P* | *V* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve value for increasing, or zero if the amount is specified by a constant in *V*.
- **const UByte** *P*: Party member whose HP will increase (0 to 2).
- **const UShort** *V*: Value to increase HP by, or address to retrieve value from if *B* is non-zero.

#### Description

Increases the HP of the party member specified by *P* by the amount *V*. If *B* is non-zero, then the value to increase by is retrieved from bank *B* and address *V*.
