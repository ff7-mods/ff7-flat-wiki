---
title: 0CA SEPOSTRANS
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 0CA SEPOSTRANS

-   Opcode: **0x0CA**
-   Short name: **SEPOSTRANS**
-   Long name: Sound Effect Pan Transition

#### Argument

none

#### Stack

  
*Sound channel*

*Frame count*

*Final pan (0-255)*

**SEPOSTRANS**

#### Description

Transitions the pan of the sound in *sound channel* over *frame count*.
0=left, 255=right.
