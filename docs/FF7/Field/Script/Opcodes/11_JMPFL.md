---
title: 11_JMPFL
---

- Opcode: **0x11**
- Short name: **JMPFL**
- Long name: Jump forward (long)

#### Memory layout

| 0x11 | *A* |
|------|-----|

#### Arguments

- **const UShort** *A*: Amount to jump forward.

#### Description

Jumps forward in the current script a specified amount. The jump begins just after the jump opcode itself and then skips the specified number of bytes. Unlike [JMPF](10_JMPF), this jump command allows jumps longer than 0xFF bytes.
