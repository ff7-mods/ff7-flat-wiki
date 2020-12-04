---
title: 51_WMOVE
---

-   Opcode: **0x51**
-   Short name: **WMOVE**
-   Long name: Window Move

#### Memory layout

| 0x51 | *I* | *X* | *Y* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *I*: [WINDOW](50_WINDOW.md) ID to resize.
-   **const Short** *X*: X-translation of the window.
-   **const Short** *Y*: Y-translation of the window.

#### Description

Repositions the window, with the given ID, and a (x,y) translation. The window will be repositioned the next time a [MESSAGE](40_MESSAGE.md) or [ASK](48_ASK.md), referencing this window, is issued.
