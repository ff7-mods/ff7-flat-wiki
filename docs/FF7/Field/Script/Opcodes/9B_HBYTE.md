---
title: 9B_HBYTE
---

- Opcode: **0x9B**
- Short name: **HBYTE**
- Long name: High Byte

#### Memory layout

| 0x9B | *D / S* | *DA* | *SA* |
|------|---------|------|------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank.
- **const Bit\[4\]** *S*: Source bank.
- **const UByte** *DA*: Destination address.
- **const UShort** *SA*: Source address, *or* the word given as a literal, if source bank is zero.

#### Description

Retrieves the high byte of a two-byte word from the source bank and address, and places the byte value into the destination bank and address. If the source bank is zero, then the final two arguments are actually a given two-byte word value, and the high byte value is retrieved from this word instead of from a memory address.
