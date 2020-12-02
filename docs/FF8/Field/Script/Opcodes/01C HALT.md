---
title: 01C HALT
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 01C HALT

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
