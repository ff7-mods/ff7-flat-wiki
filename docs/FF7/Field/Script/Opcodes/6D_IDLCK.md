---
title: 6D_IDLCK
---

- Opcode: **0x6D**
- Short name: **IDLCK**
- Long name: Triangle Boundary

#### Memory layout

| 0x6D | *I* | *S* |
|------|-----|-----|

#### Arguments

- **const UShort** *I*: Triangle ID.
- **const UByte** *S*: Switch boundary off/on (0/1, respectively).

#### Description

Dynamically turns on or off the boundary status for the set of edges marked by the triangle ID *I*. If the boundary status is switched to on, the player will not be able to cross the edges of the triangle given. If switched to off, the player may walk freely through the same edges.
