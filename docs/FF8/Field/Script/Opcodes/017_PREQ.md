---
title: 017_PREQ
---

-   Opcode: **0x017**
-   Short name: **PREQ**
-   Long name: Request party entity execution

#### Argument

The ID of the current party member Entity (0, 1 or 2).

#### Stack

..., *Priority*, *Label* =&gt; ...

#### Description

Go to the method *Label* in the entity associated with the character **Argument** in the current party with a specified *Priority*.
