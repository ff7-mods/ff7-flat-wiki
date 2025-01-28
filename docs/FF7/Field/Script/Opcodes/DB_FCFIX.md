---
title: DB_FCFIX
---

- Opcode: **0xDB**
- Short name: **FCFIX**
- Long name: Character rotatability

#### Memory layout

| 0xDB | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: 1 - lock.

#### Description

If rotation is locked it will not be changed during movement. And some other events. You still can set it directly using DIR.
