---
title: 81_SETWORD
---

- Opcode: **0x81**
- Short name: **SETWORD**
- Long name: Word Set

#### Memory layout

| 0x81 | *D / S* | *A* | *V* |
|------|---------|-----|-----|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank.
- **const Bit\[4\]** *S*: Source bank.
- **const UByte** *A*: Destination address.
- **const Short** *V*: Value to be written/Source address.

#### Description

Writes the word value from the source address, or the value argument itself, into the destination 16-bit bank. If the source bank **S** is zero, the value given by **V** is written directly into the destination bank/address; otherwise, the value is retrieved from the source bank/address **S**/**V**, and then written to the destination bank/address **D**/**A**. If the destination is a 8-bit bank, only the low byte of the source will be written into it.
