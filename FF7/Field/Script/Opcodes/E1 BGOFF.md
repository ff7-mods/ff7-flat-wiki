---
title: E1 BGOFF
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > E1 BGOFF

-   Opcode: **0xE1**
-   Short name: **BGOFF**
-   Long name: Background Off

#### Memory layout

| 0xE1 | *B1 / B2* | *A* | *L* |
|------|-----------|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: Bank to retrieve *A*, or zero if *A* is
    specified as a literal.
-   **const Bit\[4\]** *B2*: Bank to retrieve *L*, or zero if *L* is
    specified as a literal.
-   **const UByte** *A*: The ID of the background area to manipulate, as
    specified in the background's sprite.
-   **const UByte** *L*: The ID of the layer of *L* to hide (turn off),
    as specified in the background's sprite.

#### Description

Similar to [BGON][], only this opcode turns *off* the portion of
background whose [background sprite][] specifies it as belonging to the
scripted area and layer specified.

  [BGON]: FF7/Field/Script/Opcodes/E0%20BGON.md "wikilink"
  [background sprite]: FF7/Field/Sprite.md "wikilink"
