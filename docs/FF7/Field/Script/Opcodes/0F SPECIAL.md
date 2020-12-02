---
title: 0F SPECIAL
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 0F SPECIAL

-   Opcode: **0x0F**
-   Short name: **SPECIAL**
-   Long name: Special Opcode (Multibyte sequence)

#### Memory layout

| 0x0F | *SUBOP* | *...* |
|------|---------|-------|

#### Arguments

-   **const UByte** *SUBOP*: Special suboperation for field script
    execution.
-   **const UByte** *...*: 0 or more arguments, depending on the subop.

#### Description

Special is a multibyte opcode extension, mostly for game specific
opcodes to FF7. The first argument specifies the type of operation and
must be from the values listed below; the number of arguments after this
must also match the number of arguments for the operation type.

#### Subcodes by Category

##### Kernel

[`F5`` ``ARROW`][]  
[`F6`` ``PNAME`][]  
[`F7`` ``GMSPD`][]  
[`F8`` ``SMSPD`][]  
[`FB`` ``BTLCK`][]  
[`FC`` ``MVLCK`][]  
[`FD`` ``SPCNM`][]  
[`FE`` ``RSGLB`][]

##### Inventory

[`F9`` ``FLMAT`][]  
[`FA`` ``FLITM`][]  
[`FF`` ``CLITM`][]

#### Subcodes by Opcode

[`F5`` ``ARROW`][]  
[`F6`` ``PNAME`][]  
[`F7`` ``GMSPD`][]  
[`F8`` ``SMSPD`][]  
[`F9`` ``FLMAT`][]  
[`FA`` ``FLITM`][]  
[`FB`` ``BTLCK`][]  
[`FC`` ``MVLCK`][]  
[`FD`` ``SPCNM`][]  
[`FE`` ``RSGLB`][]  
[`FF`` ``CLITM`][]

  [`F5`` ``ARROW`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/F5%20ARROW.md
    "wikilink"
  [`F6`` ``PNAME`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/F6%20PNAME.md
    "wikilink"
  [`F7`` ``GMSPD`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/F7%20GMSPD.md
    "wikilink"
  [`F8`` ``SMSPD`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/F8%20SMSPD.md
    "wikilink"
  [`FB`` ``BTLCK`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FB%20BTLCK.md
    "wikilink"
  [`FC`` ``MVLCK`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FC%20MVLCK.md
    "wikilink"
  [`FD`` ``SPCNM`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FD%20SPCNM.md
    "wikilink"
  [`FE`` ``RSGLB`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FE%20RSGLB.md
    "wikilink"
  [`F9`` ``FLMAT`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/F9%20FLMAT.md
    "wikilink"
  [`FA`` ``FLITM`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FA%20FLITM.md
    "wikilink"
  [`FF`` ``CLITM`]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL/FF%20CLITM.md
    "wikilink"
