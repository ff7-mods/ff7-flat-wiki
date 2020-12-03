---
title: DE_TURNW
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > DE TURNW

-   Opcode: **0xDE**
-   Short name: **TURNW**
-   Long name: Wait for Turn

#### Memory layout

| 0xDE |
|------|

#### Arguments

None.

#### Description

Halts execution of the current script for a preceding turn to complete. When the object has fully turned, execution continues. This works fine, exept TURN, TURNGEN and TURA is waitable opcode itself, so this is ignored. Perhaps this is deprecated opcode.
