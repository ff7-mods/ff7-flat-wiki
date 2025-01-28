---
title: 0E_DSKCG
---

- Opcode: **0x0E**
- Short name: **DSKCG**
- Long name: Disk Change Screen

#### Memory layout

| 0x0E | *D* |
|------|-----|

#### Arguments

- **const UByte** *D*: Disk number.

#### Description

Shows the Disk Change screen if the current disk in the drive does not match the argument given. The current script is halted until the correct disk is inserted. When the correct disk is inserted, the field fades back into view and execution continues as normal. If the disk is subsequently ejected on this field, the field is instantly hidden, and a one-line dialog box is shown asking the user to re-insert the disk where it again waits for the disk to be inserted.

If a disk number outside the range 1 to 4 is specified, an image will show, as with normal disk change screens, but no text will display to identify which disk to insert.
