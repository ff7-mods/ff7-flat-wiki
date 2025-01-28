---
title: F3_MUSVT
---

- Opcode: **0xF3**
- Short name: **MUSVT**
- Long name: Music Video Tape Segment

#### Memory layout

| *id* |
|------|

#### Arguments

- **const UByte** *id*: Integer referencing the music file reference as loaded in the field scripts.

#### Description

Pauses current music. Plays the music file as referenced in the AKAO segment of the flevel field script. Subsequent replaying of the main field music is does by checking if the MUSVT is still playing (CHMST) and then unpause (with a slight volume fade in) through the MUSIC op code.

Example use: Junon Locker room when practicing for the march, and Cloud does his special move, the fanfare music comes on, then normal music is resumed.
