---
title: 68 SCR2DL
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 68 SCR2DL

-   Opcode: **0x68**
-   Short name: **SCR2DC**
-   Long name: Scroll to Coordinates (Linear)

#### Memory layout

| 0x68 | *B1 / B2* | *0 / B3* | *X* | *Y* | *S* |
|------|-----------|----------|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: Source bank 1, or zero if *X* is set as a constant value.
-   **const Bit\[4\]** *B2*: Source bank 2, or zero if *Y* is set as a constant value.
-   **const Bit\[4\]** *0*: Zero.
-   **const Bit\[4\]** *B4*: Source bank 3, or zero if *S* is set as a constant value.
-   **const Short** *X*: X-coordinate to scroll to.
-   **const Short** *Y*: Y-coordinate to scroll to.
-   **const UShort** *S*: Speed to scroll; higher values scroll more slowly.

#### Description

Similar to [SCR2D](64 SCR2D.md), except the scroll to the coordinates is linear; that is, the speed is constant throughout the duration of the screen scroll.
