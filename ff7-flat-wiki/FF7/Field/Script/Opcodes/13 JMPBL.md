---
title: 13 JMPBL
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 13 JMPBL

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

  [JMPB]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/12%20JMPB.md "wikilink"
