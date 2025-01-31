---
title: DA_AKAO2
---

- Opcode: **0xDA**
- Short name: **AKAO2**
- Long name: Sound Operation (word param1)

#### Memory layout

| 0xF2 | *B1 / B2* | *B3 / B4* | *0 / B6* | *Op* | *Param1* | *Param2* | *Param3* | *Param4* | *Param5* |
|----|----|----|----|----|----|----|----|----|----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *Param1*, or zero if *Param1* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *Param2*, or zero if *Param2* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve *Param3*, or zero if *Param3* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve *Param4*, or zero if *Param4* is specified as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B6*: Bank to retrieve *Param5*, or zero if *Param5* is specified as a literal value.
- **const UByte** *Op*: Operation to perform.
- **const UShort** *Param1*: Parameter 1.
- **const UShort** *Param2*: Parameter 2.
- **const UShort** *Param3*: Parameter 3.
- **const UShort** *Param4*: Parameter 4.
- **const UShort** *Param5*: Parameter 5.

#### Description

Perform an operation described by *Op*, and uses the parameters depending on the operation.

[Opcode list](F2_AKAO#Operation_list)
