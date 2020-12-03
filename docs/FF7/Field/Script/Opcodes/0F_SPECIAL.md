---
title: 0F_SPECIAL
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 0F SPECIAL

-   Opcode: **0x0F**
-   Short name: **SPECIAL**
-   Long name: Special Opcode (Multibyte sequence)

#### Memory layout

| 0x0F | *SUBOP* | *...* |
|------|---------|-------|

#### Arguments

-   **const UByte** *SUBOP*: Special suboperation for field script execution.
-   **const UByte** *...*: 0 or more arguments, depending on the subop.

#### Description

Special is a multibyte opcode extension, mostly for game specific opcodes to FF7. The first argument specifies the type of operation and must be from the values listed below; the number of arguments after this must also match the number of arguments for the operation type.

#### Subcodes by Category

##### Kernel

[`F5`` ``ARROW`](0F_SPECIAL/F5_ARROW.md)  
[`F6`` ``PNAME`](0F_SPECIAL/F6_PNAME.md)  
[`F7`` ``GMSPD`](0F_SPECIAL/F7_GMSPD.md)  
[`F8`` ``SMSPD`](0F_SPECIAL/F8_SMSPD.md)  
[`FB`` ``BTLCK`](0F_SPECIAL/FB_BTLCK.md)  
[`FC`` ``MVLCK`](0F_SPECIAL/FC_MVLCK.md)  
[`FD`` ``SPCNM`](0F_SPECIAL/FD_SPCNM.md)  
[`FE`` ``RSGLB`](0F_SPECIAL/FE_RSGLB.md)

##### Inventory

[`F9`` ``FLMAT`](0F_SPECIAL/F9_FLMAT.md)  
[`FA`` ``FLITM`](0F_SPECIAL/FA_FLITM.md)  
[`FF`` ``CLITM`](0F_SPECIAL/FF_CLITM.md)

#### Subcodes by Opcode

[`F5`` ``ARROW`](0F_SPECIAL/F5_ARROW.md)  
[`F6`` ``PNAME`](0F_SPECIAL/F6_PNAME.md)  
[`F7`` ``GMSPD`](0F_SPECIAL/F7_GMSPD.md)  
[`F8`` ``SMSPD`](0F_SPECIAL/F8_SMSPD.md)  
[`F9`` ``FLMAT`](0F_SPECIAL/F9_FLMAT.md)  
[`FA`` ``FLITM`](0F_SPECIAL/FA_FLITM.md)  
[`FB`` ``BTLCK`](0F_SPECIAL/FB_BTLCK.md)  
[`FC`` ``MVLCK`](0F_SPECIAL/FC_MVLCK.md)  
[`FD`` ``SPCNM`](0F_SPECIAL/FD_SPCNM.md)  
[`FE`` ``RSGLB`](0F_SPECIAL/FE_RSGLB.md)  
[`FF`` ``CLITM`](0F_SPECIAL/FF_CLITM.md)
