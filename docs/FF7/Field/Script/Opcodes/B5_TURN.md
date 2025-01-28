---
title: B5_TURN
---

- Opcode: **0xB5**
- Short name: **TURN**
- Long name: Generate Turn

#### Memory layout

| 0xB4 | *00 / B2* | *Final rotation* | *ignored* | *Steps in rotation* | *Type of steps calculation* |
|----|----|----|----|----|----|

#### Arguments

- **const Bit\[4\]** *B2*: Bank to retrieve Final rotation, or zero if specifying *Final rotation* as a literal value.
- **const Bute** *Final rotation*: Rotation value to which model will be rotated.
- **const Short** *ignored*: Although this is set in script it is compleatly ignored by opcode.
- **const Short** *Steps in rotation*: Set number of steps in rotation.
- **const UShort** *Type of steps calculation*: Specify how to calculate rotation step by step. (1 - linear/ 2 - smooth.).

#### Description

This is deprecated opcode, only 4 field in game use it. This opcode do turn the same way as TURNGEN, but go to specify direction without modification. So if current direction is 0 (top) and target direction is 255 (top left) it will rotate all way clockwise and you can't do anything about 0 direction. This opcode will be called until turn is over and then continue script execution.
