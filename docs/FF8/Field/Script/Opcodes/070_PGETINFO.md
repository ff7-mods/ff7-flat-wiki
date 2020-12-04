---
title: 070_PGETINFO
---

-   Opcode: **0x070**
-   Short name: **PGETINFO**
-   Long name: Get Party Member Worldspace Coordinates?

#### Argument

none

#### Stack

  
*Party slot*

**PGETINFO**

#### Description

Pushes the given party member's X position into temp variable 0, Y position into temp variable 1, (and maybe z? facing?).

Temp variables can be accessed with PSHI\_L.
