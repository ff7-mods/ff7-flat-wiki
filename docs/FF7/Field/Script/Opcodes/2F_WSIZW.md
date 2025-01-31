---
title: 2F_WSIZW
---

- Opcode: **0x2F**
- Short name: **WSIZW**
- Long name: Window Resize

#### Memory layout

| 0x2F | *I* | *X* | *Y* | *W* | *H* |
|------|-----|-----|-----|-----|-----|

#### Arguments

- **const UByte** *I*: [WINDOW](50_WINDOW) ID to resize.
- **const UShort** *X*: X-coordinate of the window.
- **const UShort** *Y*: Y-coordinate of the window.
- **const UShort** *W*: Width of the window.
- **const UShort** *H*: Height of the window.

#### Description

Resizes and/or repositions the window, after it has been created with the [WINDOW](50_WINDOW) opcode. On the next [MESSAGE](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink") or [ASK](FF7/Field/Script/Opcodes/48_ASK "wikilink"), the window will be positioned and sized with the new properties.
