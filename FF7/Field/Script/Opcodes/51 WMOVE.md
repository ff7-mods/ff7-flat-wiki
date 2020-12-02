---
title: 51 WMOVE
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 51 WMOVE

-   Opcode: **0x51**
-   Short name: **WMOVE**
-   Long name: Window Move

#### Memory layout

| 0x51 | *I* | *X* | *Y* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *I*: [WINDOW][] ID to resize.
-   **const Short** *X*: X-translation of the window.
-   **const Short** *Y*: Y-translation of the window.

#### Description

Repositions the window, with the given ID, and a (x,y) translation. The
window will be repositioned the next time a [MESSAGE][] or [ASK][],
referencing this window, is issued.

  [WINDOW]: FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [MESSAGE]: FF7/Field/Script/Opcodes/40%20MESSAGE.md "wikilink"
  [ASK]: FF7/Field/Script/Opcodes/48%20ASK.md "wikilink"
