---
title: D7 SLDR2
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > D7 SLDR2

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

  [SLIDR]: C6%20SLIDR.md "wikilink"
