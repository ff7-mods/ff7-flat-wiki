---
title: D7 SLDR2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > D7 SLDR2

-   Opcode: **0xD7**
-   Short name: **SLDR2**
-   Long name: Solid Range (16-bit)

#### Memory layout

| 0xD7 | *B* | *R* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is
    specified as a literal value.
-   **const UShort** *R*: Range value.

#### Description

Similar to [SLIDR][], but allows a two-byte range value to be used.

  [SLIDR]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/C6%20SLIDR.md "wikilink"
