---
title: BD ASPED
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > BD ASPED

-   Opcode: **0xBD**
-   Short name: **ASPED**
-   Long name: Animation Speed

#### Memory layout

| 0xBD | *B* | *S* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve direction value, or zero if it
    is specified as a literal value.
-   **const UShort** *S*: Speed of animation.

#### Description

Set global model animation speed. Lager the value - faster all animation
played by this model.

Default value = 16 -&gt; relative animation time scale 1

ASPED 8 -&gt; relative animation time scale 0.5

ASPED 32 -&gt; relative animation time scale 2
