---
title: CB IFPRTYQ
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > CB IFPRTYQ

-   Opcode: **0xCB**
-   Short name: **IFPRTYQ**
-   Long name: If Party Member

#### Memory layout

| 0xCB | *C* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *C*: [Character ID][] to check.
-   **const UByte** *A*: Amount to jump if comparison is false.

#### Description

Checks whether the character, given as the first argument, is in the
current party of three. If so, the script immediately following this
opcode and argument list will execute; otherwise, the script pointer is
advanced by the second argument and execution continues.

  [Character ID]: ../../Character%20ID.md "wikilink"
