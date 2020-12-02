---
title: E5 STPAL
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > E5 STPAL

-   Opcode: **0xE5**
-   Short name: **STPAL**
-   Long name: Store Palette

#### Memory layout

| 0xE5 | *B1/B2* | *Vram palette id* | *Palette array id* | *Size* |
|------|---------|-------------------|--------------------|--------|

#### Arguments

-   **const Bit\[4\]** *B1*: Bank for palette id.
-   **const Bit\[4\]** *B2*: Bank for palette array id.
-   **const UByte** *Vram palette id*: Id of palette. All palettes
    stored starting from vram\_x = 0, vram\_y = 0x1e0, so this index is
    starting from vram\_y.
-   **const UByte** *Palette array id*: All palette stored from in
    special array 0x20 size of each item. But it just index and can be
    used lo load full 256 colours (it just takes 0x10 slots of array).
-   **const UByte** *Size*: Size of palette to copy + 1.

#### Description

Stores palette data to special array (0x80095de0 in english psx
version).
