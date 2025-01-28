---
title: 99_RANDOM
---

- Opcode: **0x99**
- Short name: **RANDOM**
- Long name: Random

#### Memory layout

| 0x99 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Destination bank.
- **const UByte** *A*: Destination address.

#### Description

Places a random 8-bit value into the destination bank and address specified. If you specify a 16-bit bank, only the lower byte is randomised.
