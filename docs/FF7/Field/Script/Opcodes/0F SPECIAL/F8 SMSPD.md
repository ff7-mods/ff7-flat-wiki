---
title: F8 SMSPD
---

[Home](../../../../../Main Page.md) > [FF7](../../../../../FF7.md) > [Field](../../../../Field.md) > [Script](../../../Script.md) > [Opcodes](../../Opcodes.md) > [0F SPECIAL](../0F SPECIAL.md) > F8 SMSPD

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

Sets the Field Message speed, as found in the Config menu. The valid range is from 0 (the slowest setting) to FF (the fastest setting).
