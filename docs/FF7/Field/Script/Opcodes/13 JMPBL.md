---
title: 13 JMPBL
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > 13 JMPBL

-   Opcode: **0x13**
-   Short name: **JMPBL**
-   Long name: Jump back (long)

#### Memory layout

| 0x10 | *A* |
|------|-----|

#### Arguments

-   **const UShort** *A*: Amount to jump backwards.

#### Description

Jumps backward in the current script a specified amount. The jump begins
just before the jump opcode itself and then moves the current byte
pointer back the specified number of bytes. Unlike [JMPB][], this jump
command allows jumps longer than 0xFF bytes.

  [JMPB]: /FF7/Field/Script/Opcodes/12%20JMPB.md "wikilink"
