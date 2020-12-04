---
title: 0BF_MUSICSTOP
---

-   Opcode: **0x0BF**
-   Short name: **MUSICSTOP**
-   Long name: Stop Music

#### Argument

none

#### Stack

  
*0 or 1*

**MUSICSTOP**

#### Description

Presumably stops the music from playing. There are some points where MUSICSTOP is called twice in a row like this:

  
PSHN\_L 1

MUSICSTOP

PSHN\_L 0

MUSICSTOP
