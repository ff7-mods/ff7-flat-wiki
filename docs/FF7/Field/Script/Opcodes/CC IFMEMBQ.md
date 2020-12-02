---
title: CC IFMEMBQ
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > CC IFMEMBQ

-   Opcode: **0xCC**
-   Short name: **IFMEMBQ**
-   Long name: If Party Member Available

#### Memory layout

| 0xCC | *C* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *C*: [Character ID][] to check.
-   **const UByte** *A*: Amount to jump if comparison is false.

#### Description

Checks whether the character, given as the first argument, is globally
enabled; that is, the character has been enabled using [MMBud][]. If so,
the script immediately following this opcode and argument list will
execute; otherwise, the script pointer is advanced by the second
argument and execution continues.

  [Character ID]: /FF7/Field/Character%20ID.md "wikilink"
  [MMBud]: /FF7/Field/Script/Opcodes/CD%20MMBud.md "wikilink"
