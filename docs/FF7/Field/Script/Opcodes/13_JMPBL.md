---
title: 13_JMPBL
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 13 JMPBL

-   Opcode: **0x13**
-   Short name: **JMPBL**
-   Long name: Jump back (long)

#### Memory layout

| 0x10 | *A* |
|------|-----|

#### Arguments

-   **const UShort** *A*: Amount to jump backwards.

#### Description

Jumps backward in the current script a specified amount. The jump begins just before the jump opcode itself and then moves the current byte pointer back the specified number of bytes. Unlike [JMPB](12_JMPB.md), this jump command allows jumps longer than 0xFF bytes.
