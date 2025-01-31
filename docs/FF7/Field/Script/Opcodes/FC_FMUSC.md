---
title: FC_FMUSC
---

- Opcode: **0xFC**
- Short name: **FMUSC**
- Long name: Field Music

#### Memory layout

| 0xFC | *I* |
|------|-----|

#### Arguments

- **const UByte** *I*: ID of the music file to play, as set in the field file.

#### Description

Sets the [MUSIC](FF7/Field/Script/Opcodes/F0_MUSIC "wikilink") that will play after the next [BATTLE](70_BATTLE) set, this opcode can be used to set regular or boss battle music for the current field's encounters, or even switched between in the script.
