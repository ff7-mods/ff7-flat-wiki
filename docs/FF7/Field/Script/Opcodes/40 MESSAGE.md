---
title: 40 MESSAGE
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 40 MESSAGE

-   Opcode: **0x40**
-   Short name: **MESSAGE**
-   Long name: Message display

#### Memory layout

| 0x40 | *N* | *D* |
|------|-----|-----|

#### Arguments

-   **const UByte** *N*: The ID of the window to use.
-   **const UByte** *D*: The zero-based index of the [dialog][] that
    will be displayed.

#### Description

Displays a dialog in the [WINDOW][] that has previously been initialised
to display this dialog.

  [dialog]: /ff7-flat-wiki/FF7/Field/Script.md "wikilink"
  [WINDOW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
