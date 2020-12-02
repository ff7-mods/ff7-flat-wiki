---
title: DB FCFIX
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > DB FCFIX

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
