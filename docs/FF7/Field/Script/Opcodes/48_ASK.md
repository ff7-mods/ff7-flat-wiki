---
title: 48_ASK
---

- Opcode: **0x48**
- Short name: **ASK**
- Long name: Ask Question

#### Memory layout

| 0x48 | *Bank* | *Win* | *Mess* | *First* | *Last* | *Addr* |
|------|--------|-------|--------|---------|--------|--------|

#### Arguments

- **const UByte** *Bank*: Bank to put line number selected.
- **const UByte** *Win*: Window ID to place the question in. (Initialized with WINDOW)
- **const UByte** *Mess*: Which dialog to display from dialog table.
- **const UByte** *First*: Line from dialog where the first question is.
- **const UByte** *Last*: Line from dialog where the last question is.
- **const UByte** *Addr*: Address in bank where line selected is written.

#### Description

The ASK command opens a window with a set of choices to be picked with the "selector finger". If ASK is called on an open window ID, the window will shrink closed and re-open with the new data.
