---
title: A5_XYZI
---

- Opcode: **0xA5**
- Short name: **XYZI**
- Long name: Place Object

#### Memory layout

| 0xA5 | *B1 / B2* | *B3 / B4* | *X* | *Y* | *Z* | *I* |
|------|-----------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *X*, or zero if *X* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *Y*, or zero if *Y* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *Z*, or zero if *Z* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *I*, or zero if *I* is specified as a literal value.
- **const Short** *X*: X-coordinate of the field object, or address of X-coordinate if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate of the field object, or address of Y-coordinate if *B2* is non-zero.
- **const Short** *Z*: Z-coordinate of the field object, or address of Z-coordinate if *B3* is non-zero.
- **const UShort** *I*: ID of the walkmesh triangle, or address of value if *B4* is non-zero.

#### Description

Places the field object for this entity on the walkmesh at the coordinates given. This variant of object placement allows the Z-coordinate of the object to be specified, as well as the ID of the walkmesh triangle on which the object is being placed.
