---
title: 4B BTLTB
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > 4B BTLTB

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
