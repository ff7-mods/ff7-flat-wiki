---
title: 51_WMOVE
---

- Opcode: **0x51**
- Short name: **WMOVE**
- Long name: Window Move

#### Memory layout

| 0x51 | *I* | *X* | *Y* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *I*: [WINDOW](50_WINDOW) ID to resize.
- **const Short** *X*: X-translation of the window.
- **const Short** *Y*: Y-translation of the window.

#### Description

Repositions the window, with the given ID, and a (x,y) translation. The window will be repositioned the next time a [MESSAGE](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink") or [ASK](48_ASK), referencing this window, is issued.
