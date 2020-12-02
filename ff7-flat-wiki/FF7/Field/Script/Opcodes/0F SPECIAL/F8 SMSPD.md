---
title: F8 SMSPD
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > [0F SPECIAL](/ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL.md) > F8 SMSPD

-   Opcode: **0x0FF8**
-   Short name: **SPECIAL: SMSPD**
-   Long name: Special: Set Field Message Speed

#### Memory layout

| 0x0F | 0xF8 | 0   | S   |
|------|------|-----|-----|

#### Arguments

-   **const UByte** *0*: A single zero byte.
-   **const UByte** *S*: Field message speed.

#### Description

Sets the Field Message speed, as found in the Config menu. The valid
range is from 0 (the slowest setting) to FF (the fastest setting).
