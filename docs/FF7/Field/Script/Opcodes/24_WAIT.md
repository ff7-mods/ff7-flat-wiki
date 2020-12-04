---
title: 24_WAIT
---

[Home](../../../../index.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 24 WAIT

-   Opcode: **0x24**
-   Short name: **WAIT**
-   Long name: Wait

#### Memory layout

| 0x24 | *A* |
|------|-----|

#### Arguments

-   **const UShort** *A*: Amount (number of frames) to wait.

#### Description

Pauses current script execution for a specific amount of time. Rather than a specific time value in milliseconds/seconds, the amount specifies the number of frames that must be drawn before execution resumes. Since the game runs at 30fps, WAIT(0x1E) (or WAIT(30) in decimal) will pause script execution for 1 second, WAIT(0x96) will pause for 5 seconds, and so on.
