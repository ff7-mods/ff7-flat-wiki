---
title: E3 BGROL2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > E3 BGROL2

-   Opcode: **0xE3**
-   Short name: **BGROL2**
-   Long name: Background Roll (Reverse)

#### Memory layout

| 0xE3 | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *A*, or zero if *A* is
    specified as a literal.
-   **const UByte** *A*: The ID of the background area to roll, as
    specified in the background's sprite.

#### Description

Similar to [BGROL][], except the roll runs backwards through layers,
rather than forwards. Rolling backwards past layer 0 for the area
specified results in no background being shown.

  [BGROL]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/E2%20BGROL.md "wikilink"
