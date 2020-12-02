---
title: C4 OFSTW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > C4 OFSTW

-   Opcode: **0xC4**
-   Short name: **OFSTW**
-   Long name: Wait for Offset

#### Memory layout

| 0xC4 |
|------|

#### Arguments

None.

#### Description

Halts current script execution until a previous [OFST][] has completed.
This is only of use if the offset type is not instantaneous.

  [OFST]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/C3%20OFST.md "wikilink"
