---
title: 36 WSPCL
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 36 WSPCL

-   Opcode: **0x36**
-   Short name: **WSPCL**
-   Long name: Window Special (Numerical Display)

#### Memory layout

| 0x36 | *W* | *T* | *X* | *Y* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *W*: [WINDOW](50 WINDOW.md) ID to apply the change to.
-   **const UByte** *T*: Type of display.
-   **const UByte** *X*: X-coordinate of the numerical display, relative to the top-left of the window.
-   **const UByte** *Y*: Y-coordinate of the numerical display, relative to the top-left of the window.

#### Description

Creates a numerical display inside the given window. The display can be either in the form of a clock, or a scoreboard with six digits. This only creates the numerical display; to actually show it, a [MESSAGE](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink") or [ASK](48 ASK.md) command needs to be issued. Using a blank line of dialog will allow you to create a numerical display in the top-left of the window without field dialog hidden behind it. Alternatively, dialog can be shown along with the display by placing the display in an appropriate area of the window.

To set the time for the clock variant, [STTIM](FF7/Field/Script/Opcodes/38_STTIM "wikilink") is used. To set the number for the numerical display, [WNUMB](37 WNUMB.md) is used.

#### Display types

| ID  | Display Type     |
|-----|------------------|
| 0   | None             |
| 1   | Clock (00:00)    |
| 2   | Numeric (000000) |
|     |                  |
