---
title: 45 MPu
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 45 MPu

-   Opcode: **0x45**
-   Short name: **MPu**
-   Long name: MP Up

#### Memory layout

| 0x45 | *B* | *P* | *V* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve value for increasing, or zero
    if the amount is specified by a constant in *V*.
-   **const UByte** *P*: Party member whose MP will increase (0 to 2).
-   **const UShort** *V*: Value to increase MP by, or address to
    retrieve value from if *B* is non-zero.

#### Description

Increases the MP of the party member specified by *P* by the amount *V*.
If *B* is non-zero, then the value to increase by is retrieved from bank
*B* and address *V*.
