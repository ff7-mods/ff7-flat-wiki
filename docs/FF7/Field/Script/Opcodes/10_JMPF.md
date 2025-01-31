---
title: 10_JMPF
---

- Opcode: **0x10**
- Short name: **JMPF**
- Long name: Jump forward

#### Memory layout

| 0x10 | *A* |
|------|-----|

#### Arguments

- **const UByte** *A*: Amount to jump forward.

#### Description

Jumps forward in the current script a specified amount. The jump begins just after the jump opcode itself and then skips the specified number of bytes. In the following example, the [WAIT](24_WAIT) line is skipped.

    JMPF (04)
    WAIT (70,00)
    SOLID (01)

If a jump longer than 0xFF is required, use [JMPFL](11_JMPFL) instead.
