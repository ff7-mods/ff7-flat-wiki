---
title: AB_TURA
---

- Opcode: **0xAB**
- Short name: **TURA**
- Long name: Turn to entity

#### Memory layout

| 0xB4 | *Entity id* | *Rotate side type* | *Steps in rotation* |
|------|-------------|--------------------|---------------------|

#### Arguments

- **const Bit\[4\]** *Entity id*: Entity id to which model we calculate direction during first opcode call.
- **const Short** *Rotate side type*: Specify how model will be rotated. (0 - clockwise/ 1 - anti-clockwise/ 2 - closest)
- **const Short** *Steps in rotation*: Set number of steps in rotation.

#### Description

Rotation calculated line in TUGNGEN, except end direction calculated during first opcode call. Rotation always calculated smoothly. Like in TURNGEN(XX,XX,XX,XX,02); This opcode will be called until turn is over and then continue script execution.
