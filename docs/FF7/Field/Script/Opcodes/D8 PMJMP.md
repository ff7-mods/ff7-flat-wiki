---
title: D8 PMJMP
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > D8 PMJMP

-   Opcode: **0xD8**
-   Short name: **PMJMP**
-   Long name: Prepare Field Change

#### Memory layout

| 0xD8 | *I* |
|------|-----|

#### Arguments

-   **const UShort** *I*: [Field ID][] of the map to prepare to jump to.

#### Description

Prepare to jump to the field indicated by *I*. Use before making the
[map jump][].

  [Field ID]: ../../Field%20List.md "wikilink"
  [map jump]: 60%20MAPJUMP.md "wikilink"
