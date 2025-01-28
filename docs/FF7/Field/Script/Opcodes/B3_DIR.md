---
title: B3_DIR
---

- Opcode: **0xB3**
- Short name: **DIR**
- Long name: Direction

#### Memory layout

| 0xB3 | *B* | *D* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve direction value, or zero if it is specified as a literal value.
- **const UByte** *D*: Direction to face, or address if *B* is non-zero.

#### Description

Instantaneously turns the field object for this entity to the direction specified by *D*. The direction is in the standard direction format for the game.
