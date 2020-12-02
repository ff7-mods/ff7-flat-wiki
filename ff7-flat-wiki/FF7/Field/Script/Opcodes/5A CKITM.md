---
title: 5A CKITM
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 5A CKITM

-   Opcode: **0x5A**
-   Short name: **CKITM**
-   Long name: Check Item

#### Memory layout

| 0x5A | *B* | *I* | *A* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store result.
-   **const UShort** *I*: [Item ID][] to check.
-   **const UByte** *A*: Address to store result.

#### Description

Copies the amount of item **I** the player has in their inventory, to
the bank and address specified.

  [Item ID]: /ff7-flat-wiki/FF7/Field/Item%20ID.md "wikilink"
