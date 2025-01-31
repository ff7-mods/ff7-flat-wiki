---
title: 66_SCR2DC
---

- Opcode: **0x66**
- Short name: **SCR2DC**
- Long name: Scroll to Coordinates (Smooth)

#### Memory layout

| 0x66 | *B1 / B2* | *0 / B3* | *X* | *Y* | *S* |
|------|-----------|----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Source bank 1, or zero if *X* is set as a constant value.
- **const Bit\[4\]** *B2*: Source bank 2, or zero if *Y* is set as a constant value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B4*: Source bank 3, or zero if *S* is set as a constant value.
- **const Short** *X*: X-coordinate to scroll to.
- **const Short** *Y*: Y-coordinate to scroll to.
- **const UShort** *S*: Speed to scroll; higher values scroll more slowly.

#### Description

Similar to [SCR2D](64_SCR2D), except the scroll is not instantaneous and is performed smoothly, with a slower start and ending, with speed peaking in the center of the scroll. The overall speed can be set with *S*.
