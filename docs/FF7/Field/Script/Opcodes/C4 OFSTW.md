---
title: C4 OFSTW
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > C4 OFSTW

-   Opcode: **0xC4**
-   Short name: **OFSTW**
-   Long name: Wait for Offset

#### Memory layout

| 0xC4 |
|------|

#### Arguments

None.

#### Description

Halts current script execution until a previous [OFST](C3 OFST.md) has completed. This is only of use if the offset type is not instantaneous.
