---
title: D6 TLKR2
permalink: D6 TLKR2.html
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > D6 TLKR2

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

  [TALKR]: C5%20TALKR.md "wikilink"
