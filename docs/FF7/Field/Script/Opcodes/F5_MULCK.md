---
title: F5_MULCK
---

- Opcode: **0xF5**
- Short name: **MULCK**
- Long name: Music Lock

#### Memory layout

| 0xF5 | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: Lock on/off (1/0, respectively).

#### Description

Locks the [MUSIC](F0_MUSIC) to the current selection. Subsequent calls to change the music will fail unless a corresponding MULCK set to 0 is executed.
