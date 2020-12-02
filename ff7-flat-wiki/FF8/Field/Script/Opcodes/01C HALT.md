---
title: 01C HALT
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 01C HALT

-   Opcode: **0x01C**
-   Short name: **HALT**
-   Long name: Halt

#### Argument

Always 0.

#### Stack

No change.

#### Description

Exits the current script and all scripts that are waiting on it. To end
only the current script, use RET instead.
