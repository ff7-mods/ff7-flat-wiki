---
title: D7_SLDR2
---

[Home](../../../../index.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > D7 SLDR2

-   Opcode: **0xD7**
-   Short name: **SLDR2**
-   Long name: Solid Range (16-bit)

#### Memory layout

| 0xD7 | *B* | *R* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is specified as a literal value.
-   **const UShort** *R*: Range value.

#### Description

Similar to [SLIDR](C6_SLIDR.md), but allows a two-byte range value to be used.
