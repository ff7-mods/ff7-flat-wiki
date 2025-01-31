---
title: 5D_CMTRA
---

- Opcode: **0x5D**
- Short name: **CMTRA**
- Long name: Check Materia

#### Memory layout

| 0x5D | *B1 / B2* | *B3 / B4* | *B5* | *T* | *AP* | *U* | *A* |
|------|-----------|-----------|------|-----|------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *T* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B3*: Source bank 3, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B4*: Source bank 4, or zero if this unit of *AP* is set as a constant value.
- **const UByte** *B5*: Bank to store *A*.
- **const UByte** *T*: [Type of materia](../Materia_ID) to check, or source address 1.
- **const UByte\[3\]** *AP*: Amount of AP the checked materia must have, or source addresses 2, 3 and 4.
- **const UByte** *U*: Unknown.
- **const UByte** *A*: Address to store amount of materia found.

#### Description

Places the amount of materia with specified type and AP into the bank and address specified.

#### Important Note

This opcode is **not** implemented in the PC version of the game, nor used in the PlayStation version.
