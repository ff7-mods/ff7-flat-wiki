---
title: 5C_DMTRA
---

- Opcode: **0x5C**
- Short name: **DMTRA**
- Long name: Delete Materia

#### Memory layout

| 0x5C | *B1 / B2* | *B3 / B4* | *T* | *AP* | *A* |
|------|-----------|-----------|-----|------|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *T* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B3*: Source bank 3, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B4*: Source bank 4, or zero if this unit of *AP* is set as a constant value.
- **const UByte** *T*: [Type of materia](../Materia_ID) to remove, or source address 1.
- **const UByte\[3\]** *AP*: Amount of AP the deleted materia must have, or source addresses 2, 3 and 4.
- **const UByte** *A*: Amount to delete.

#### Description

Deletes a quantity of materia with the given type and AP.

#### Important Note

This opcode does not appear to function correctly in the PC version of the game. In addition, it is only used once, in the [Debug Rooms](../../../Debug_Rooms).
