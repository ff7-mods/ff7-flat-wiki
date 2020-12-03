---
title: 019 PREQEW
---

[Home](../../../../Main%20Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 019 PREQEW

-   Opcode: **0x019**
-   Short name: **PREQEW**
-   Long name: Request party entity execution (synchronous, guaranteed)

#### Argument

The ID of the current party member Entity (0, 1 or 2).

#### Stack

..., *Priority*, *Label* =&gt; ...

#### Description

Go to the method *Label* in the entity associated with the character
**Argument** in the current party with a specified *Priority*.
