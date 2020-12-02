---
title: 015 REQSW
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 015 REQSW

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
