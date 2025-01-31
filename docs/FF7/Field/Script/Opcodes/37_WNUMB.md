---
title: 37_WNUMB
---

- Opcode: **0x37**
- Short name: **WNUMB**
- Long name: Set Number

#### Memory layout

| 0x37 | *B1 / B2* | *W* | *N* | *C* |
|------|-----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve lower two bytes of number, or zero if number is given as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve higher two bytes of number, or zero if number is given as a literal value.
- **const UByte** *W*: Window ID whose numerical display will be set.
- **const ULong** *N*: A four-byte number to set the numerical display. If *B1* or *B2* are non-zero, this value is split into two two-byte values, indicating the address to find the number value in banks *B1* and *B2*, respectively.
- **const UByte** *C*: The number of digits to display, from 1 to 8.

#### Description

Sets the numerical display, as found in the [WSPCL](FF7/Field/Script/Opcodes/36_WSPCL "wikilink") opcode. The number may be set with a specified value or retrieved from two 16-bit values, and the number of digits to show is specified with *C*. Unlike the other special window setting function, [STTIM](FF7/Field/Script/Opcodes/38_STTIM "wikilink"), the [WINDOW](50_WINDOW) ID must be given for this opcode.

If the value does not fit in the specified number of digits for the display, the higher units are not displayed.
