---
title: 0F SPECIAL
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 0F SPECIAL

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

[`F5`` ``ARROW`](0F SPECIAL/F5 ARROW.md)  
[`F6`` ``PNAME`](0F SPECIAL/F6 PNAME.md)  
[`F7`` ``GMSPD`](0F SPECIAL/F7 GMSPD.md)  
[`F8`` ``SMSPD`](0F SPECIAL/F8 SMSPD.md)  
[`FB`` ``BTLCK`](0F SPECIAL/FB BTLCK.md)  
[`FC`` ``MVLCK`](0F SPECIAL/FC MVLCK.md)  
[`FD`` ``SPCNM`](0F SPECIAL/FD SPCNM.md)  
[`FE`` ``RSGLB`](0F SPECIAL/FE RSGLB.md)

##### Inventory

[`F9`` ``FLMAT`](0F SPECIAL/F9 FLMAT.md)  
[`FA`` ``FLITM`](0F SPECIAL/FA FLITM.md)  
[`FF`` ``CLITM`](0F SPECIAL/FF CLITM.md)

#### Subcodes by Opcode

[`F5`` ``ARROW`](0F SPECIAL/F5 ARROW.md)  
[`F6`` ``PNAME`](0F SPECIAL/F6 PNAME.md)  
[`F7`` ``GMSPD`](0F SPECIAL/F7 GMSPD.md)  
[`F8`` ``SMSPD`](0F SPECIAL/F8 SMSPD.md)  
[`F9`` ``FLMAT`](0F SPECIAL/F9 FLMAT.md)  
[`FA`` ``FLITM`](0F SPECIAL/FA FLITM.md)  
[`FB`` ``BTLCK`](0F SPECIAL/FB BTLCK.md)  
[`FC`` ``MVLCK`](0F SPECIAL/FC MVLCK.md)  
[`FD`` ``SPCNM`](0F SPECIAL/FD SPCNM.md)  
[`FE`` ``RSGLB`](0F SPECIAL/FE RSGLB.md)  
[`FF`` ``CLITM`](0F SPECIAL/FF CLITM.md)
