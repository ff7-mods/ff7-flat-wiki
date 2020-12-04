---
title: 53_WREST
---

-   Opcode: **0x53**
-   Short name: **WREST**
-   Long name: Window Reset

#### Memory layout

| 0x53 | *N* |
|------|-----|

#### Arguments

-   **const UByte** *N*: The ID of the window to reset.

#### Description

Resets the given window, including the following parameters:

-   Position and size, set by [WMOVE](51_WMOVE.md), [WSIZW](2F_WSIZW.md), [WROW](55_WROW.md) or even the initial values set by [WINDOW](50_WINDOW.md);
-   Background type, set by [WMODE](52_WMODE.md);
-   Numerical displays, set by [WSPCL](36_WSPCL.md);
-   Message parameters, set by [MPARA](41_MPARA.md) and [MPRA2](42_MPRA2.md).

The reset window has a position of approximately (5,5), with a width and height of approximately (0x130, 0x45).
