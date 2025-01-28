---
title: B4_TURNGEN
---

- Opcode: **0xB4**
- Short name: **TURNGEN**
- Long name: Generate Turn

#### Memory layout

| 0xB4 | *00 / B2* | *Final rotation* | *Rotate side type* | *Steps in rotation* | *Type of steps calculation* |
|----|----|----|----|----|----|

#### Arguments

- **const Byte** *B2*: Bank to retrieve Final rotation, or zero if specifying *Final rotation* as a literal value.
- **const Byte** *Final rotation*: Rotation value to which model will be rotated.
- **const Byte** *Rotate side type*: Specify how model will be rotated. (0 - clockwise/ 1 - anti-clockwise/ 2 - closest)
- **const Byte** *Steps in rotation*: Set number of steps in rotation.
- **const Byte** *Type of steps calculation*: Specify how to calculate rotation step by step. (1 - linear/ 2 - smooth.).

#### Description

This opcode will be called until turn is over and then continue script execution.
