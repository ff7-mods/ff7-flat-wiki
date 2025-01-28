---
title: 56_GWCOL
---

- Opcode: **0x56**
- Short name: **GWCOL**
- Long name: Get Window Colour

#### Memory layout

| 0x56 | *B1 / B2* | *B3 / B4* | *C* | *R* | *G* | *B* |
|------|-----------|-----------|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *C*, or zero if it specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to store *R*.
- **const Bit\[4\]** *B3*: Bank to store *G*.
- **const Bit\[4\]** *B4*: Bank to store *B*.
- **const UByte** *C*: Corner to check, or address to retrieve value if *B1* is non-zero.
- **const UByte** *R*: Address to store red component in bank *B2*.
- **const UByte** *G*: Address to store green component in bank *B3*.
- **const UByte** *B*: Address to store blue component in bank *B4*.

#### Description

Gets the colour used in the gradient for windows in which text is displayed, into the banks and address specified.

#### Corner ID

| ID  | Corner       |
|-----|--------------|
| 0   | Top Left     |
| 1   | Bottom Left  |
| 2   | Top Right    |
| 3   | Bottom Right |
|     |              |
