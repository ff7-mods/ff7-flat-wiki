---
title: B2 MSPED
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > B2 MSPED

-   Opcode: **0xB2**
-   Short name: **MSPED**
-   Long name: Movement Speed (16-bit)

#### Memory layout

| 0xD7 | *B* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is
    specified as a literal value.
-   **const UShort** *S*: Speed value (8-bit fixed point).

#### Description

Set speed of movement for MOVE-type opcodes.

Default value = 1024 -&gt; relative movement time scale 1

MSPED 512 -&gt; relative movement time scale 0.5

MSPED 2048 -&gt; relative movement time scale 2
