---
title: 019 PREQEW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 019 PREQEW

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
