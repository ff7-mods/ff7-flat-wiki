---
title: 42_MPRA2
---

- Opcode: **0x42**
- Short name: **MPRA2**
- Long name: Message Parameter (16-bit)

#### Memory layout

| 0x42 | *B* | *W* | *I* | *V* |
|------|-----|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve value from, or zero if using a literal value.
- **const UByte** *W*: [WINDOW](50_WINDOW) ID for this parameter.
- **const UByte** *I*: ID of the "[Variable](../../Variable_Dialog)" dialog code that this value will replace.
- **const UShort** *V*: Value to insert into dialog, or address of value, if *B* is non-zero.

#### Description

Similar to [MPARA](41_MPARA), but allows a constant value of greater than one byte to be supplied. This does not apply if *B* is non-zero, as the address the value is retrieved from must be in the range 0 to 0xFF.
