---
title: 2D_BGSCR
---

- Opcode: **0x2D**
- Short name: **BGSCR**
- Long name: Background Scroll

#### Memory layout

| 0x2D | *B1 / B2* | *L* | *X* | *Y* |
|------|-----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve value for *X*, or zero if *X* is specified as a literal.
- **const Bit\[4\]** *B2*: Bank to retrieve value for *Y*, or zero if *Y* is specified as a literal.
- **const UByte** *L*: ID number of the layer to manipulate.
- **const Short** *X*: Speed of the scroll in the X direction; positive values indicate right-to-left scrolling.
- **const Short** *Y*: Speed of the scroll in the Y direction; positive values indicate bottom-to-top scrolling.

#### Description

Scrolls the background layer specified by *L*. This opcode will only scroll those extra layers above the standard background and foreground layers (0/1, respectively), and so should be an argument of 2 or greater. The *X* and *Y* speeds are signed; positive values scroll from right-to-left and bottom-to-top, whilst negative values scroll from left-to-right and top-to-bottom.
