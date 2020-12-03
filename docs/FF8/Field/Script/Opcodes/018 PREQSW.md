---
title: 018 PREQSW
---

[Home](../../../../Main Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 018 PREQSW

-   Opcode: **0x018**
-   Short name: **PREQSW**
-   Long name: Request party entity execution (asynchronous execution, guaranteed)

#### Argument

The ID of the current party member Entity (0, 1 or 2).

#### Stack

..., *Priority*, *Label* =&gt; ...

#### Description

Go to the method *Label* in the entity associated with the character **Argument** in the current party with a specified *Priority*.
