---
title: E6_LDPAL
---

- Opcode: **0xE6**
- Short name: **LDPAL**
- Long name: Load Palette

#### Memory layout

| 0xE6 | *B1/B2* | *Palette array id* | *Vram palette id* | *Size* |
|------|---------|--------------------|-------------------|--------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for palette array id.
- **const Bit\[4\]** *B2*: Bank for palette id.
- **const UByte** *Vram palette id*: Id of palette. All palettes loaded starting from vram_x = 0, vram_y = 0x1e0, so this index is starting from vram_y.
- **const UByte** *Palette array id*: All palette loaded from in special array 0x20 size of each item. But it just index and can be used lo load full 256 colours (it just takes 0x10 slots of array).
- **const UByte** *Size*: Size of palette to copy + 1.

#### Description

Load palette from stored array back to vram.
