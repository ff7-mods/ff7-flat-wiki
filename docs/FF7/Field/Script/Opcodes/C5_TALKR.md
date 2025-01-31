---
title: C5_TALKR
---

- Opcode: **0xC5**
- Short name: **TALKR**
- Long name: Talk Range

#### Memory layout

| 0xC6 | *B* | *T* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *T*, or zero if *T* is specified as a literal value.
- **const UByte** *T*: Range value.

#### Description

Increases the talk range (or rather, button range) for this field object. Larger values mean that the distance between the playable character and the field object in question is increased, so that the button press script for the object's field entity is activated by a button press that is further away than normal.

For ranges larger than one byte, [TLKR2](D6_TLKR2) may be used.
