---
title: 2F WSIZW
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > 2F WSIZW

-   Opcode: **0x2F**
-   Short name: **WSIZW**
-   Long name: Window Resize

#### Memory layout

| 0x2F | *I* | *X* | *Y* | *W* | *H* |
|------|-----|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *I*: [WINDOW][] ID to resize.
-   **const UShort** *X*: X-coordinate of the window.
-   **const UShort** *Y*: Y-coordinate of the window.
-   **const UShort** *W*: Width of the window.
-   **const UShort** *H*: Height of the window.

#### Description

Resizes and/or repositions the window, after it has been created with
the [WINDOW][] opcode. On the next [MESSAGE][] or [ASK][], the window
will be positioned and sized with the new properties.

  [WINDOW]: /FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [MESSAGE]: /FF7/Field/Script/Opcodes/40%20MESSAGE.md "wikilink"
  [ASK]: /FF7/Field/Script/Opcodes/48%20ASK.md "wikilink"
