---
title: FC_MVLCK
---

- Opcode: **0x0FFC**
- Short name: **SPECIAL: MVLCK**
- Long name: Special: Movie Lock

#### Memory layout

| 0x0F | 0xFC | *B* |
|------|------|-----|

- **const UByte** *B*: Movie lock on/off (1/0, respectively).

#### Description

Enables or disables the playing of movies; if the movie lock is set to on (1), movies will not be played with the [MOVIE](../F9_MOVIE) opcode.
