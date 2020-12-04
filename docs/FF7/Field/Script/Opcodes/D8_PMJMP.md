---
title: D8_PMJMP
---

[Home](../../../../index.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > D8 PMJMP

-   Opcode: **0xD8**
-   Short name: **PMJMP**
-   Long name: Prepare Field Change

#### Memory layout

| 0xD8 | *I* |
|------|-----|

#### Arguments

-   **const UShort** *I*: [Field ID](../../Field_List.md) of the map to prepare to jump to.

#### Description

Prepare to jump to the field indicated by *I*. Use before making the [map jump](60_MAPJUMP.md).
