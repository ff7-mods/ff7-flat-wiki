---
title: 64_SCR2D
---

- Opcode: **0x64**
- Short name: **SCR2D**
- Long name: Scroll 2D

#### Memory layout

| 0x64 | *B1 / B2* | *X* | *Y* |
|------|-----------|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *X* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if *Y* is set as a constant value.
- **const Short** *X*: X-coordinate to scroll to, or address to find *X* if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate to scroll to, or address to find *Y* if *B2* is non-zero.

#### Description

Instantaneously scrolls the current view to the coordinates found in the arguments (or the values found at the addresses if memory banks and address are specified). The move to the new coordinates is instant; variants exist for [linear](FF7/Field/Script/Opcodes/68_SCR2DL "wikilink") and [smooth](66_SCR2DC) scrolling.
