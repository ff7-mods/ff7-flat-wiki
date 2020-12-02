---
title: DB FCFIX
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > DB FCFIX

-   Opcode: **0xDB**
-   Short name: **FCFIX**
-   Long name: Character rotatability

#### Memory layout

| 0xDB | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: 1 - lock.

#### Description

If rotation is locked it will not be changed during movement. And some
other events. You still can set it directly using DIR.
