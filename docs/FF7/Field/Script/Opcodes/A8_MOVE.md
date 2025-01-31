---
title: A8_MOVE
---

- Opcode: **0xA8**
- Short name: **MOVE**
- Long name: Move Object

#### Memory layout

| 0xA8 | *B1 / B2* | *X* | *Y* |
|------|-----------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve X-coordinate, or zero if it is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve Y-coordinate, or zero if it is specified as a literal value.
- **const Short** *X*: X-coordinate, or lower byte specifying an address for the value if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate, or lower byte specifying an address for the value if *B2* is non-zero.

#### Description

Makes the field object, associated with the entity this opcode's script resides in, walk (or move gradually) to the point specified by the coordinates, at the speed previously specified by [MSPED](B2_MSPED). The object's standard walk animation is used, found with animation ID 1 in the field object associated with this entity.
