---
title: 019 PREQEW
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 019 PREQEW

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
