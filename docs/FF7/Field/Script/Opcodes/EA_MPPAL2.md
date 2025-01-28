---
title: EA_MPPAL2
---

- Opcode: **0xEA**
- Short name: **MPPAL2**
- Long name: Multiply Palette

#### Memory layout

| 0xEA | *B1/B2* | *B3/B4* | *B5/0* | *Source palette array id* | *Destination palette array id* | *Multiply Blue* | *Multiply Green* | *Multiply Red* | *Size* |
|----|----|----|----|----|----|----|----|----|----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for source palette array id.
- **const Bit\[4\]** *B2*: Bank for destination palette array id.
- **const Bit\[4\]** *B3*: Bank for multiply blue colour.
- **const Bit\[4\]** *B4*: Bank for multiply green colour.
- **const Bit\[4\]** *B5*: Bank for multiply red colour.
- **const UByte** *Source palette array id*: Source palette array id. Take data from here and multiply it by BRG colour.
- **const UByte** *Destination palette array id*: Destination palette array id. Here we store data after multiplication
- **const UByte** *Multiply Blue*: Blue value for multiplying.
- **const UByte** *Multiply Green*: green value for multiplying.
- **const UByte** *Multiply Red*: Red value for multiplying.
- **const UByte** *Size*: Size of palette data to multiply + 1.

#### Description

Multiply stored palette by some colour.
