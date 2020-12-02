---
title: 75 PXYZI
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 75 PXYZI

-   Opcode: **0x75**
-   Short name: **PXYZI**
-   Long name: Party Member Get Position

#### Memory layout

| 0x75 | *B1 / B2* | *B3 / B4* | *P* | *X* | *Y* | *Z* | *I* |
|------|-----------|-----------|-----|-----|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: Bank to store *X*.
-   **const Bit\[4\]** *B2*: Bank to store *Y*.
-   **const Bit\[4\]** *B3*: Bank to store *Z*.
-   **const Bit\[4\]** *B4*: Bank to store *I*.
-   **const UByte** *P*: Party member to retrieve data from; range is 0
    to 2.
-   **const UByte** *X*: Address to store the X-coordinate of the party
    member.
-   **const UByte** *Y*: Address to store the Y-coordinate of the party
    member.
-   **const UByte** *Z*: Address to store the Z-coordinate of the party
    member.
-   **const UByte** *I*: Address to store the ID of the walkmesh
    triangle the party member is standing on.

#### Description

Retrieves the coordinates of the party member specified by *P*. If an
invalid party member ID is specified, zeros are stored in the four
addresses.
