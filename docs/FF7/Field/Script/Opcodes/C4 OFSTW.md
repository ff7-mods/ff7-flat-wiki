---
title: C4 OFSTW
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > C4 OFSTW

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

  [OFST]: ../C3%20OFST.md "wikilink"
