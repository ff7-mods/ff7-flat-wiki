---
title: 36 WSPCL
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 36 WSPCL

-   Opcode: **0x36**
-   Short name: **WSPCL**
-   Long name: Window Special (Numerical Display)

#### Memory layout

| 0x36 | *W* | *T* | *X* | *Y* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *W*: [WINDOW][] ID to apply the change to.
-   **const UByte** *T*: Type of display.
-   **const UByte** *X*: X-coordinate of the numerical display, relative
    to the top-left of the window.
-   **const UByte** *Y*: Y-coordinate of the numerical display, relative
    to the top-left of the window.

#### Description

Creates a numerical display inside the given window. The display can be
either in the form of a clock, or a scoreboard with six digits. This
only creates the numerical display; to actually show it, a [MESSAGE][]
or [ASK][] command needs to be issued. Using a blank line of dialog will
allow you to create a numerical display in the top-left of the window
without field dialog hidden behind it. Alternatively, dialog can be
shown along with the display by placing the display in an appropriate
area of the window.

To set the time for the clock variant, [STTIM][] is used. To set the
number for the numerical display, [WNUMB][] is used.

#### Display types

| ID  | Display Type     |
|-----|------------------|
| 0   | None             |
| 1   | Clock (00:00)    |
| 2   | Numeric (000000) |
|     |                  |

  [WINDOW]: 50%20WINDOW.md "wikilink"
  [MESSAGE]: 40%20MESSAGE.md "wikilink"
  [ASK]: 48%20ASK.md "wikilink"
  [STTIM]: 38%20STTIM.md "wikilink"
  [WNUMB]: 37%20WNUMB.md "wikilink"
