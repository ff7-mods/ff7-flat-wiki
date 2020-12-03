---
title: 5A CKITM
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 5A CKITM

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

  [Item ID]: ../../Item%20ID.md "wikilink"
