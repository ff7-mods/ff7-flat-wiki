---
title: 53 WREST
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 53 WREST

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

  [WMOVE]: FF7/Field/Script/Opcodes/51%20WMOVE.md "wikilink"
  [WSIZW]: FF7/Field/Script/Opcodes/2F%20WSIZW.md "wikilink"
  [WROW]: FF7/Field/Script/Opcodes/55%20WROW.md "wikilink"
  [WINDOW]: FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [WMODE]: FF7/Field/Script/Opcodes/52%20WMODE.md "wikilink"
  [WSPCL]: FF7/Field/Script/Opcodes/36%20WSPCL.md "wikilink"
  [MPARA]: FF7/Field/Script/Opcodes/41%20MPARA.md "wikilink"
  [MPRA2]: FF7/Field/Script/Opcodes/42%20MPRA2.md "wikilink"
