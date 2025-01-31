---
title: 50_WINDOW
---

- Opcode: **0x50**
- Short name: **WINDOW**
- Long name: Window creation

#### Memory layout

| 0x50 | *N* | *X* | *Y* | *W* | *H* |
|------|-----|-----|-----|-----|-----|

#### Arguments

- **const UByte** *N*: The numerical ID that the newly-created window will be associated with.
- **const UShort** *X*: X-coordinate of the window.
- **const UShort** *Y*: Y-coordinate of the window.
- **const UShort** *W*: Window width.
- **const UShort** *H*: Window height.

#### Description

Creates a window with a given ID and placement/size parameters. Windows are used to show [dialog](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink"), present [choices](48_ASK) and so on, each of which reference the window's ID to insert text. This command only initializes a window ID, but does not present itself until a dialog command is issued on it.

Adjustments are made for windows that are either too close an edge, or the width / height is too big for the screen. Eg:

`// Adjust window position if too close to an edge`  
`const MIN_WINDOW_DISTANCE = 8 // Looks about right`  
`if (x < MIN_WINDOW_DISTANCE) { x = MIN_WINDOW_DISTANCE }`  
`if (y < MIN_WINDOW_DISTANCE) { y = MIN_WINDOW_DISTANCE }`  
`if (x + w + MIN_WINDOW_DISTANCE > GAME_WIDTH) { x = GAME_WIDTH - w - MIN_WINDOW_DISTANCE }`  
`if (y + h + MIN_WINDOW_DISTANCE > GAME_HEIGHT) { y = GAME_HEIGHT - h - MIN_WINDOW_DISTANCE }`
