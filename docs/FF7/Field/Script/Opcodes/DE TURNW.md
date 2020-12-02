---
title: DE TURNW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > DE TURNW

-   Opcode: **0xDE**
-   Short name: **TURNW**
-   Long name: Wait for Turn

#### Memory layout

| 0xDE |
|------|

#### Arguments

None.

#### Description

Halts execution of the current script for a preceding turn to complete.
When the object has fully turned, execution continues. This works fine,
exept TURN, TURNGEN and TURA is waitable opcode itself, so this is
ignored. Perhaps this is deprecated opcode.
