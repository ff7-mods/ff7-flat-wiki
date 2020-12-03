---
title: 11 JMPFL
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 11 JMPFL

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

  [JMPF]: ../10%20JMPF.md "wikilink"
