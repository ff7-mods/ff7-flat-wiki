---
title: 9A_LBYTE
---

- Opcode: **0x9A**
- Short name: **LBYTE**
- Long name: Low Byte

#### Memory layout

| 0x9A | *D / S* | *DA* | *SA* |
|------|---------|------|------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank.
- **const Bit\[4\]** *S*: Source bank.
- **const UByte** *DA*: Destination address.
- **const UByte** *SA*: Source address.

#### Description

Retrieves the low byte of a two-byte word from the source bank and address, and places the byte value into the destination bank and address. If the source is an 8-bit bank, this will simply copy the value from source to destination; if the destination is a 16-bit bank, the high byte of the destination will remain unchanged.
