---
title: CB_IFPRTYQ
---

- Opcode: **0xCB**
- Short name: **IFPRTYQ**
- Long name: If Party Member

#### Memory layout

| 0xCB | *C* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *C*: [Character ID](../../Character_ID) to check.
- **const UByte** *A*: Amount to jump if comparison is false.

#### Description

Checks whether the character, given as the first argument, is in the current party of three. If so, the script immediately following this opcode and argument list will execute; otherwise, the script pointer is advanced by the second argument and execution continues.
