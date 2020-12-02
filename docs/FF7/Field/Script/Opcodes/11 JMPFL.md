---
title: 11 JMPFL
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 11 JMPFL

-   Opcode: **0x11**
-   Short name: **JMPFL**
-   Long name: Jump forward (long)

#### Memory layout

| 0x11 | *A* |
|------|-----|

#### Arguments

-   **const UShort** *A*: Amount to jump forward.

#### Description

Jumps forward in the current script a specified amount. The jump begins
just after the jump opcode itself and then skips the specified number of
bytes. Unlike [JMPF][], this jump command allows jumps longer than 0xFF
bytes.

  [JMPF]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/10%20JMPF.md "wikilink"
