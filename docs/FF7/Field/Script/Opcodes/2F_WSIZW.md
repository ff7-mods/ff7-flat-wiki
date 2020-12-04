---
title: 2F_WSIZW
---

-   Opcode: **0x2F**
-   Short name: **WSIZW**
-   Long name: Window Resize

#### Memory layout

| 0x2F | *I* | *X* | *Y* | *W* | *H* |
|------|-----|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *I*: [WINDOW](50_WINDOW.md) ID to resize.
-   **const UShort** *X*: X-coordinate of the window.
-   **const UShort** *Y*: Y-coordinate of the window.
-   **const UShort** *W*: Width of the window.
-   **const UShort** *H*: Height of the window.

#### Description

Resizes and/or repositions the window, after it has been created with the [WINDOW](50_WINDOW.md) opcode. On the next [MESSAGE](40_MESSAGE.md) or [ASK](48_ASK.md), the window will be positioned and sized with the new properties.
