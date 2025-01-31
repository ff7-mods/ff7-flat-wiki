---
title: 40_MESSAGE
---

- Opcode: **0x40**
- Short name: **MESSAGE**
- Long name: Message display

#### Memory layout

| 0x40 | *N* | *D* |
|------|-----|-----|

#### Arguments

- **const UByte** *N*: The ID of the window to use.
- **const UByte** *D*: The zero-based index of the [dialog](..) that will be displayed.

#### Description

Displays a dialog in the [WINDOW](50_WINDOW) that has previously been initialised to display this dialog.
