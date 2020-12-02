---
title: 4B BTLTB
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 4B BTLTB

-   Opcode: **0x4B**
-   Short name: **BTLTB**
-   Long name: Battle Table

#### Memory layout

| 0x4B | *I* |
|------|-----|

#### Arguments

-   **const UByte** *I*: ID of the encounter table to use, either 0
    (standard) or 1.

#### Description

Switches between the two sets of encounter data that may exist in a
field file, depending on the ID given.
