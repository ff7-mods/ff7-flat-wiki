---
title: 49_MENU
---

- Opcode: **0x49**
- Short name: **MENU**
- Long name: Menu

#### Memory layout

| 0x49 | *B* | *T* | *E* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank for parameter, or zero if *P* is specified as a literal value.
- **const UByte** *T*: Type of menu, or special event.
- **const UByte** *P*: Parameter to the menu, or address of parameter value, if *B* is non-zero.

#### Description

MENU has two uses. Its primary function is to display a menu or other special screen; these menus range from the character name entry screen, to a shop, and even the staff credit display. The type of display can be found in the first table below.

The other function is to provide a set of special events that would normally be accomplished through a set of opcodes, but are instead coded directly into a MENU call. These events are provided in the second table.

Some types of menu are erroneous or produce erratic behaviour, and were most likely used for testing. As such, they are not listed here.

#### Standard Menu Types

| ID  | Menu Type            |
|-----|----------------------|
| 5   | FF7 Credits          |
| 6   | Character Name Entry |
| 7   | Party Select         |
| 8   | Shop                 |
| 9   | Main Menu            |
| E   | Save Screen          |

#### Special Event Types

| ID  | Event Type                                  |
|-----|---------------------------------------------|
| F   | Yuffie's Materia Steal (Remove All Materia) |
| 12  | Remove Cloud's Materia                      |
| 13  | Restore Cloud's Materia                     |

#### Parameters

- Character Name Entry: Parameter indicates the name of the character to edit, and follows the standard Character IDs, as well as 0x64 to indicate the Chocobo naming screen.
