---
title: CC_IFMEMBQ
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > CC IFMEMBQ

-   Opcode: **0xCC**
-   Short name: **IFMEMBQ**
-   Long name: If Party Member Available

#### Memory layout

| 0xCC | *C* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *C*: [Character ID](../../Character_ID.md) to check.
-   **const UByte** *A*: Amount to jump if comparison is false.

#### Description

Checks whether the character, given as the first argument, is globally enabled; that is, the character has been enabled using [MMBud](CD_MMBud.md). If so, the script immediately following this opcode and argument list will execute; otherwise, the script pointer is advanced by the second argument and execution continues.
