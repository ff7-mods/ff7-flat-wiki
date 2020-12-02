---
title: FA MVIEF
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > FA MVIEF

-   Opcode: **0xFA**
-   Short name: **MVIEF**
-   Long name: Movie Frame

#### Memory layout

| 0xFA | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store result; should be a 16-bit bank.
-   **const UByte** *A*: Address to store result.

#### Description

Stores the frame number of the current [MOVIE][] that is being
displayed, in the bank and address specified.

  [MOVIE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/F9%20MOVIE.md "wikilink"
