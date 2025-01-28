---
title: 95_INC
---

- Opcode: **0x95**
- Short name: **INC**
- Long name: Increment (8-bit)

#### Memory layout

| 0x95 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Destination bank.
- **const UByte** *A*: Address.

#### Description

Increments the 8-bit value found at bank **B**, address **A**. If the value is 0xFF, it will roll over to 0x00. If you specify a 16-bit bank, only the lower byte will be incremented, and if the lower byte is 0xFF, the higher byte will be unaffected whilst the lower byte will return to 0x00.
