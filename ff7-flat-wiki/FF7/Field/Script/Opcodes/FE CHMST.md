---
title: FE CHMST
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > FE CHMST

-   Opcode: **0xFE**
-   Short name: **CHMST**
-   Long name: Check Music

#### Memory layout

| 0xFE | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store boolean.
-   **const UByte** *A*: Address to store boolean.

#### Description

Stores a boolean value (0 for false, 1 for true) in the bank and address
specified, indicating whether music is currently playing.
