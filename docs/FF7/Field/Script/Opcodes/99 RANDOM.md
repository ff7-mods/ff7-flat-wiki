---
title: 99 RANDOM
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 99 RANDOM

-   Opcode: **0x99**
-   Short name: **RANDOM**
-   Long name: Random

#### Memory layout

| 0x99 | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Destination bank.
-   **const UByte** *A*: Destination address.

#### Description

Places a random 8-bit value into the destination bank and address
specified. If you specify a 16-bit bank, only the lower byte is
randomised.
