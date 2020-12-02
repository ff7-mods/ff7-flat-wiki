---
title: 015 REQSW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 015 REQSW

-   Opcode: **0x015**
-   Short name: **REQSW**
-   Long name: Request remote execution (asynchronous execution,
    guaranteed)

#### Argument

The ID of the target Entity.

#### Stack

..., *Priority*, *Label* =&gt; ...

#### Description

Go to the method *Label* in the group **Argument** with a specified
*Priority*.
