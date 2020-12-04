---
title: DB_FCFIX
---

[Home](../../../../index.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > DB FCFIX

-   Opcode: **0xDB**
-   Short name: **FCFIX**
-   Long name: Character rotatability

#### Memory layout

| 0xDB | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: 1 - lock.

#### Description

If rotation is locked it will not be changed during movement. And some other events. You still can set it directly using DIR.
