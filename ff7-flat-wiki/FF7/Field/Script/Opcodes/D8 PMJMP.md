---
title: D8 PMJMP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > D8 PMJMP

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

  [Field ID]: /ff7-flat-wiki/FF7/Field/Field%20List.md "wikilink"
  [map jump]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/60%20MAPJUMP.md "wikilink"
