---
title: D6 TLKR2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > D6 TLKR2

-   Opcode: **0xD6**
-   Short name: **TLKR2**
-   Long name: Talk Range (16-bit)

#### Memory layout

| 0xC6 | *B* | *T* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *T*, or zero if *T* is
    specified as a literal value.
-   **const UShort** *T*: Range value.

#### Description

Similar to [TALKR][], but allows a two-byte range value to be used.

  [TALKR]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/C5%20TALKR.md "wikilink"
