---
title: 3A_GOLDd
---

- Opcode: **0x3A**
- Short name: **GOLDd**
- Long name: Gil Down

#### Memory layout

| 0x3A | *0* | *A* |
|------|-----|-----|

| 0x3A | *B / 0* | *A* | *0* |
|------|---------|-----|-----|

#### Arguments

Decrease by a constant amount:

- **const UByte** *0*: Zero.
- **const ULong** *A*: Amount to increase.

Decrease by an amount found in memory:

- **const Bit\[4\]** *B*: Source bank.
- **const UByte** *A*: Source address.
- **const UByte\[3\]** *0*: Three zero bytes.

#### Description

Decreases the amount of gil by a constant amount, or by an amount found in the source bank *B* and address *A*.

The total gil is capped below by 0; attempts to decrement further will fail.
