---
title: 60 MAPJUMP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 60 MAPJUMP

-   Opcode: **0x60**
-   Short name: **MAPJUMP**
-   Long name: Change Field

#### Memory layout

| 0x60 | *I* | *X* | *Y* | *Z* | *D* |
|------|-----|-----|-----|-----|-----|

#### Arguments

-   **const UShort** *I*: [Field ID][] of the map to jump to.
-   **const Short** *X*: X-coordinate of the player on the next field.
-   **const Short** *Y*: Y-coordinate of the player on the next field.
-   **const Short** *Z*: Z-coordinate of the player on the next field.
-   **const UByte** *D*: Direction the character will be facing on the
    next field, in the standard game format.

#### Description

Switches fields to the one indicated by *I*, and places the character at
the coordinates and direction specified. This is an alternative to using
a [gateway][], and can complement their usage as it allows for more than
12 gateways by simulating their behaviour through a [LINE][] which, when
crossed, executes a MAPJUMP.

  [Field ID]: /ff7-flat-wiki/FF7/Field/Field%20List.md "wikilink"
  [gateway]: /ff7-flat-wiki/FF7/Field/3D%20Related.md "wikilink"
  [LINE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/D0%20LINE.md "wikilink"
