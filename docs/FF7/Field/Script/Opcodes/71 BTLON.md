---
title: 71 BTLON
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 71 BTLON

-   Opcode: **0x71**
-   Short name: **BTLON**
-   Long name: Battle Switch

#### Memory layout

| 0x71 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch battles on/off (0/1, respectively).

#### Description

Turns random encounters on or off for this field. Note that if a field
does not have any [Encounter Data][] set in its field file, battles will
not occur regardless of the argument passed with this opcode.

  [Encounter Data]: /ff7-flat-wiki/FF7/Field/Encounter.md "wikilink"
