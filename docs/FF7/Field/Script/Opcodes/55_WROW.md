---
title: 55_WROW
---

- Opcode: **0x55**
- Short name: **WROW**
- Long name: Window Rows

#### Memory layout

| 0x55 | *N* | *R* |
|------|-----|-----|

#### Arguments

- **const UByte** *N*: The ID of the [WINDOW](50_WINDOW) whose height will be set.
- **const UByte** *R*: Number of rows of text that should fit in this window.

#### Description

Sets the height of the window with ID *N*, by adjusting it to fit a specified number of rows of text, as given by *R*. If the dialog does not fit after adjusting the height of the window, the player will be able to scroll the dialog in the window by pressing \[OK\] to see the proceeding lines of text. When all text has scrolled, the window will close as normal.
