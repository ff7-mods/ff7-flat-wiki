---
title: 60_MAPJUMP
---

- Opcode: **0x60**
- Short name: **MAPJUMP**
- Long name: Change Field

#### Memory layout

| 0x60 | *I* | *X* | *Y* | *Z* | *D* |
|------|-----|-----|-----|-----|-----|

#### Arguments

- **const UShort** *I*: [Field ID](../../Field_List) of the map to jump to.
- **const Short** *X*: X-coordinate of the player on the next field.
- **const Short** *Y*: Y-coordinate of the player on the next field.
- **const Short** *Z*: Z-coordinate of the player on the next field.
- **const UByte** *D*: Direction the character will be facing on the next field, in the standard game format.

#### Description

Switches fields to the one indicated by *I*, and places the character at the coordinates and direction specified. This is an alternative to using a [gateway](FF7/Field/3D_Related "wikilink"), and can complement their usage as it allows for more than 12 gateways by simulating their behaviour through a [LINE](D0_LINE) which, when crossed, executes a MAPJUMP.
