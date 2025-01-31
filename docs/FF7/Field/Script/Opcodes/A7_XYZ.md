---
title: A7_XYZ
---

- Opcode: **0xA7**
- Short name: **XYZ**
- Long name: Place Object (No I)

#### Memory layout

| 0xA7 | *B1 / B2* | *B3 / 0* | *X* | *Y* | *Z* |
|------|-----------|----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *X*, or zero if *X* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *Y*, or zero if *Y* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *Z*, or zero if *Z* is specified as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Short** *X*: X-coordinate of the field object, or address of X-coordinate if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate of the field object, or address of Y-coordinate if *B2* is non-zero.
- **const Short** *Z*: Z-coordinate of the field object, or address of Z-coordinate if *B3* is non-zero.

#### Description

Similar to [XYZI](A5_XYZI), but does not specify a triangle ID. This lack of triangle ID may cause problems if the field object is set to move from its set position.
