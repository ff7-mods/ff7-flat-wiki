---
title: 0F_SPECIAL
---

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

[`F5`` ``ARROW`](FF7/Field/Script/Opcodes/0F_SPECIAL/F5_ARROW "wikilink")  
[`F6`` ``PNAME`](FF7/Field/Script/Opcodes/0F_SPECIAL/F6_PNAME "wikilink")  
[`F7`` ``GMSPD`](FF7/Field/Script/Opcodes/0F_SPECIAL/F7_GMSPD "wikilink")  
[`F8`` ``SMSPD`](FF7/Field/Script/Opcodes/0F_SPECIAL/F8_SMSPD "wikilink")  
[`FB`` ``BTLCK`](FF7/Field/Script/Opcodes/0F_SPECIAL/FB_BTLCK "wikilink")  
[`FC`` ``MVLCK`](FF7/Field/Script/Opcodes/0F_SPECIAL/FC_MVLCK "wikilink")  
[`FD`` ``SPCNM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FD_SPCNM "wikilink")  
[`FE`` ``RSGLB`](FF7/Field/Script/Opcodes/0F_SPECIAL/FE_RSGLB "wikilink")

##### Inventory

[`F9`` ``FLMAT`](FF7/Field/Script/Opcodes/0F_SPECIAL/F9_FLMAT "wikilink")  
[`FA`` ``FLITM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FA_FLITM "wikilink")  
[`FF`` ``CLITM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FF_CLITM "wikilink")

#### Subcodes by Opcode

[`F5`` ``ARROW`](FF7/Field/Script/Opcodes/0F_SPECIAL/F5_ARROW "wikilink")  
[`F6`` ``PNAME`](FF7/Field/Script/Opcodes/0F_SPECIAL/F6_PNAME "wikilink")  
[`F7`` ``GMSPD`](FF7/Field/Script/Opcodes/0F_SPECIAL/F7_GMSPD "wikilink")  
[`F8`` ``SMSPD`](FF7/Field/Script/Opcodes/0F_SPECIAL/F8_SMSPD "wikilink")  
[`F9`` ``FLMAT`](FF7/Field/Script/Opcodes/0F_SPECIAL/F9_FLMAT "wikilink")  
[`FA`` ``FLITM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FA_FLITM "wikilink")  
[`FB`` ``BTLCK`](FF7/Field/Script/Opcodes/0F_SPECIAL/FB_BTLCK "wikilink")  
[`FC`` ``MVLCK`](FF7/Field/Script/Opcodes/0F_SPECIAL/FC_MVLCK "wikilink")  
[`FD`` ``SPCNM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FD_SPCNM "wikilink")  
[`FE`` ``RSGLB`](FF7/Field/Script/Opcodes/0F_SPECIAL/FE_RSGLB "wikilink")  
[`FF`` ``CLITM`](FF7/Field/Script/Opcodes/0F_SPECIAL/FF_CLITM "wikilink")
