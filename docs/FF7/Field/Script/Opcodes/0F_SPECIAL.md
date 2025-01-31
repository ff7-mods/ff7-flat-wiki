---
title: 0F_SPECIAL
---

- Opcode: **0x0F**
- Short name: **SPECIAL**
- Long name: Special Opcode (Multibyte sequence)

#### Memory layout

| 0x0F | *SUBOP* | *...* |
|------|---------|-------|

#### Arguments

- **const UByte** *SUBOP*: Special suboperation for field script execution.
- **const UByte** *...*: 0 or more arguments, depending on the subop.

#### Description

Special is a multibyte opcode extension, mostly for game specific opcodes to FF7. The first argument specifies the type of operation and must be from the values listed below; the number of arguments after this must also match the number of arguments for the operation type.

#### Subcodes by Category

##### Kernel

[`F5 ARROW`](0F_SPECIAL/F5_ARROW)  
[`F6 PNAME`](0F_SPECIAL/F6_PNAME)  
[`F7 GMSPD`](0F_SPECIAL/F7_GMSPD)  
[`F8 SMSPD`](0F_SPECIAL/F8_SMSPD)  
[`FB BTLCK`](0F_SPECIAL/FB_BTLCK)  
[`FC MVLCK`](0F_SPECIAL/FC_MVLCK)  
[`FD SPCNM`](0F_SPECIAL/FD_SPCNM)  
[`FE RSGLB`](0F_SPECIAL/FE_RSGLB)

##### Inventory

[`F9 FLMAT`](0F_SPECIAL/F9_FLMAT)  
[`FA FLITM`](0F_SPECIAL/FA_FLITM)  
[`FF CLITM`](0F_SPECIAL/FF_CLITM)

#### Subcodes by Opcode

[`F5 ARROW`](0F_SPECIAL/F5_ARROW)  
[`F6 PNAME`](0F_SPECIAL/F6_PNAME)  
[`F7 GMSPD`](0F_SPECIAL/F7_GMSPD)  
[`F8 SMSPD`](0F_SPECIAL/F8_SMSPD)  
[`F9 FLMAT`](0F_SPECIAL/F9_FLMAT)  
[`FA FLITM`](0F_SPECIAL/FA_FLITM)  
[`FB BTLCK`](0F_SPECIAL/FB_BTLCK)  
[`FC MVLCK`](0F_SPECIAL/FC_MVLCK)  
[`FD SPCNM`](0F_SPECIAL/FD_SPCNM)  
[`FE RSGLB`](0F_SPECIAL/FE_RSGLB)  
[`FF CLITM`](0F_SPECIAL/FF_CLITM)
