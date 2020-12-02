---
title: 3A GOLDd
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 3A GOLDd

-   Opcode: **0x3A**
-   Short name: **GOLDd**
-   Long name: Gil Down

#### Memory layout

| 0x3A | *0* | *A* |
|------|-----|-----|

| 0x3A | *B / 0* | *A* | *0* |
|------|---------|-----|-----|

#### Arguments

Decrease by a constant amount:

-   **const UByte** *0*: Zero.
-   **const ULong** *A*: Amount to increase.

Decrease by an amount found in memory:

-   **const Bit\[4\]** *B*: Source bank.
-   **const UByte** *A*: Source address.
-   **const UByte\[3\]** *0*: Three zero bytes.

#### Description

Decreases the amount of gil by a constant amount, or by an amount found
in the source bank *B* and address *A*.

The total gil is capped below by 0; attempts to decrement further will
fail.
