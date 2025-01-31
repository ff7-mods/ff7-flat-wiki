---
title: C3_OFST
---

- Opcode: **0xC3**
- Short name: **OFST**
- Long name: Offset Object

#### Memory layout

| 0xC3 | *B1 / B2* | *B3 / B4* | *T* | *X* | *Y* | *Z* | *S* |
|------|-----------|-----------|-----|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve X offset, or zero if *X* is specified as a literal.
- **const Bit\[4\]** *B2*: Bank to retrieve Y offset, or zero if *Y* is specified as a literal.
- **const Bit\[4\]** *B3*: Bank to retrieve Z offset, or zero if *Z* is specified as a literal.
- **const Bit\[4\]** *B4*: Bank to retrieve speed, or zero if *S* is specified as a literal.
- **const UByte** *T*: Type of movement.
- **const Short** *X*: X offset amount, relative to current position, or address to find X offset, if *B1* is non-zero.
- **const Short** *Y*: Y offset amount, relative to current position, or address to find Y offset, if *B2* is non-zero.
- **const Short** *Z*: Z offset amount, relative to current position, or address to find Z offset, if *B3* is non-zero.
- **const UShort** *S*: Step-count of the offset movement, if type is non-zero, or address to find speed, if *B4* is non-zero.

#### Description

Offsets the field object, belonging to the entity whose script this opcode resides in, by a certain amount. After being offset, the character continues to be constrained in movement as defined by the walkmesh's shape, but at a certain distance away from the normal walkmesh position. Other field objects are unaffected, and their position or movements are maintained on the walkmesh's original position.

If B1, B2, B3 or B4 is non-zero, then the value for that particular component is taken from memory using the corresponding bank and address specified, rather than as a literal value. Both retrieved values and literals can be used for different components. If using *T*, *X*, *Y* or *S* as addresses, the lower byte should hold the address whilst the higher byte should be zero.

The amount to offset is specified relative to the current position. If **T**ype is specified, the object moves gradually from its current point to the offset position; this can be used to simulate movements such as elevators. Any type outside the range in the table will cause the offset not to occur.

If the object is set to move gradually, then the number of steps to use to reach the destination can be set. The current step is incremented by one as the movement progresses. The ratio of the current step to total steps is used to determine the current progress through the movement, so the greater the number of steps, the slower the object moves toward its target offset.

In the case of linear movement, a simple linear interpolation is used :

`  current position = start position + total distance * current step / total steps.`

In the case of smooth movement, a cosine function is used to simulate "ease-in" and "ease-out" of the perceived speed :

`  current position = start position + total distance * ((cos(π * current step / total steps + π) + 1) / 2)`

For the sake of speed, the above calculations are done using look-up tables and fixed-point arithmetic.

Script execution may also be halted until the gradual offset has been completed. For this, see [OFSTW](C4_OFSTW).

#### Movement Types

| ID  | Movement Type             |
|-----|---------------------------|
| 0   | Instantaneous             |
| 1   | Linear (No acceleration)  |
| 2   | Cosine (ease-in/ease-out) |
|     |                           |
