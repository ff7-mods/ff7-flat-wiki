---
title: E2 BGROL
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > E2 BGROL

-   Opcode: **0xE2**
-   Short name: **BGROL**
-   Long name: Background Roll

#### Memory layout

| 0xE2 | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *A*, or zero if *A* is
    specified as a literal.
-   **const UByte** *A*: The ID of the background area to roll, as
    specified in the background's sprite.

#### Description

Turns on the next numerical layer in the background area specified by
*A*. For example, if background area 3 is currently set to [display
layer][] 1 for that particular area, a call to BGROL(0,3) will display
layer 2 for that area. If an invalid layer is given, or the background
rolls past the last layer for this area, no background is displayed by
this opcode.

  [display layer]: E0%20BGON.md "wikilink"
