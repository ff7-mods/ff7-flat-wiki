---
title: 5B_SMTRA
---

- Opcode: **0x5B**
- Short name: **SMTRA**
- Long name: Set Materia

#### Memory layout

| 0x5B | *B1 / B2* | *B3 / B4* | *T* | *AP* |
|------|-----------|-----------|-----|------|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *T* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B3*: Source bank 3, or zero if this unit of *AP* is set as a constant value.
- **const Bit\[4\]** *B4*: Source bank 4, or zero if this unit of *AP* is set as a constant value.
- **const UByte** *T*: [Type of materia](../Materia_ID) to add, or source address 1.
- **const UByte\[3\]** *AP*: Amount of AP the newly added materia will have, or source addresses 2, 3 and 4.

#### Description

Adds a new piece of materia to the materia inventory. This is either done by explicitly providing the materia type and AP value, in which case the first two bytes are zero, or by retrieving these values from memory. Both setting the values explicitly and retrieving from memory can be used together in one call by setting the correct bytes to zero; to see an example, please check below.

If *B1* is non-zero, then *T* specifies the address to be used with *B1* to find the value for materia type. If *B2*, *B3* or *B4* are non-zero, these three bytes specify the addresses to retrieve the values for this unit. *B2* and the first AP byte specifies the lowest-unit (16^1) hex value to retrieve, corresponding to 0-16 gil; *B3* and the second AP byte specifies the middle-unit (16^2) hex value to retrieve; *B4* and the third AP byte the highest-unit (16^3) hex value.

#### Example

The following example adds a piece of Slash All materia (ID: 0xE) using the following parameters:

- Materia ID retrieved from memory bank 6, address 1D;
- 16^1 set explicitly with a constant value;
- 16^2 set explicitly with a constant value;
- 16^3 retrieved from memory bank 6, address 1B.

`SETWORD(60,1B,1,0)`  
`SETWORD(60,1D,E,0)`  
`SMTRA(60,06,1D,3,2,1B)`

This equates to: (3\*16^1) + (2\*16^2) + (1\*16^3) == 0x010203 == 66051 AP.
