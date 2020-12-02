---
title: AD FMOVE
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > AD FMOVE

-   Opcode: **0xA9**
-   Short name: **CMOVE**
-   Long name: Move Object (No Animation)

#### Memory layout

| 0xA9 | *B1 / B2* | *X* | *Y* |
|------|-----------|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: Bank to retrieve X-coordinate, or zero if
    it is specified as a literal value.
-   **const Bit\[4\]** *B2*: Bank to retrieve Y-coordinate, or zero if
    it is specified as a literal value.
-   **const Short** *X*: X-coordinate, or lower byte specifying an
    address for the value if *B1* is non-zero.
-   **const Short** *Y*: Y-coordinate, or lower byte specifying an
    address for the value if *B2* is non-zero.

#### Description

Similar to [MOVE][], but the field object won't play its animation
whilst it moves. Field object will be rotated according to movement.

  [MOVE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/A8%20MOVE.md "wikilink"
