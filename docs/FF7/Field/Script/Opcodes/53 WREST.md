---
title: 53 WREST
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 53 WREST

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

-   Position and size, set by [WMOVE][], [WSIZW][], [WROW][] or even the
    initial values set by [WINDOW][];
-   Background type, set by [WMODE][];
-   Numerical displays, set by [WSPCL][];
-   Message parameters, set by [MPARA][] and [MPRA2][].

The reset window has a position of approximately (5,5), with a width and
height of approximately (0x130, 0x45).

  [WMOVE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/51%20WMOVE.md "wikilink"
  [WSIZW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/2F%20WSIZW.md "wikilink"
  [WROW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/55%20WROW.md "wikilink"
  [WINDOW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [WMODE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/52%20WMODE.md "wikilink"
  [WSPCL]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/36%20WSPCL.md "wikilink"
  [MPARA]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/41%20MPARA.md "wikilink"
  [MPRA2]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/42%20MPRA2.md "wikilink"
