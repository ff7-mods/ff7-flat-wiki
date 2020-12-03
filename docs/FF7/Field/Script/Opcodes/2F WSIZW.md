---
title: 2F WSIZW
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 2F WSIZW

-   Opcode: **0x2F**
-   Short name: **WSIZW**
-   Long name: Window Resize

#### Memory layout

| 0x2F | *I* | *X* | *Y* | *W* | *H* |
|------|-----|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *I*: [WINDOW](50 WINDOW.md) ID to resize.
-   **const UShort** *X*: X-coordinate of the window.
-   **const UShort** *Y*: Y-coordinate of the window.
-   **const UShort** *W*: Width of the window.
-   **const UShort** *H*: Height of the window.

#### Description

Resizes and/or repositions the window, after it has been created with the [WINDOW](FF7/Field/Script/Opcodes/50_WINDOW "wikilink") opcode. On the next [MESSAGE](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink") or [ASK](48 ASK.md), the window will be positioned and sized with the new properties.
