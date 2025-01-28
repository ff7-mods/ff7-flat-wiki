---
title: 80_SETBYTE
---

- Opcode: **0x80**
- Short name: **SETBYTE**
- Long name: Byte Set

#### Memory layout

| 0x80 | *D / S* | *A* | *V* |
|------|---------|-----|-----|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank.
- **const Bit\[4\]** *S*: Source bank.
- **const UByte** *A*: Destination address.
- **const UByte** *V*: Value to be written/Source address.

#### Description

Writes the byte value from the source address, or the value argument itself, into the destination 8-bit bank. If the source bank **S** is zero, the value given by **V** is written directly into the destination address; otherwise, the value is retrieved from the source bank/address **S**/**V**, and then written to the destination bank/address **D**/**A**. If the destination is a 16-bit bank, the high byte of the destination will remain unchanged.
