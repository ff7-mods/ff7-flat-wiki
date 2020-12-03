---
title: 6C_FADEW
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 6C FADEW

-   Opcode: **0x6C**
-   Short name: **FADEW**
-   Long name: Wait for fade

#### Memory layout

| 0x6C |
|------|

#### Arguments

None.

#### Description

Halts execution of the current script for a preceding [FADE](6B_FADE.md) command, issued by any entity, to fully complete before continuing execution. If no FADE has been issued by any entity, or previous FADE calls have already completed, the FADEW call is ignored.
