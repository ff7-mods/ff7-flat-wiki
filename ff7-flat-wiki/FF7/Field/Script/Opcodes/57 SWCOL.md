---
title: 57 SWCOL
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 57 SWCOL

-   Opcode: **0x57**
-   Short name: **SWCOL**
-   Long name: Set Window Colour

#### Memory layout

| 0x57 | *B1 / B2* | *B3 / B4* | *C* | *R* | *G* | *B* |
|------|-----------|-----------|-----|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: Bank to retrieve *C*, or zero if it
    specified as a literal value.
-   **const Bit\[4\]** *B2*: Bank to retrieve *R*, or zero if it
    specified as a literal value.
-   **const Bit\[4\]** *B3*: Bank to retrieve *G*, or zero if it
    specified as a literal value.
-   **const Bit\[4\]** *B4*: Bank to retrieve *B*, or zero if it
    specified as a literal value.
-   **const UByte** *C*: Corner to set colour, or address to retrieve
    value if *B1* is non-zero.
-   **const UByte** *R*: Red value of the corner, or address to retrieve
    red component if *B2* is non-zero.
-   **const UByte** *G*: Green value of the corner, or address to
    retrieve green component if *B3* is non-zero.
-   **const UByte** *B*: Blue value of the corner, or address to
    retrieve blue component if *B4* is non-zero.

#### Description

Sets the colour for a particular corner of the gradient used in windows
for displaying text.

#### Corner ID

| ID  | Corner       |
|-----|--------------|
| 0   | Top Left     |
| 1   | Bottom Left  |
| 2   | Top Right    |
| 3   | Bottom Right |
|     |              |
