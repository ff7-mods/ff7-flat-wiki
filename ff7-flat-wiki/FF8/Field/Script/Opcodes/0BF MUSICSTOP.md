---
title: 0BF MUSICSTOP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 0BF MUSICSTOP

-   Opcode: **0x0BF**
-   Short name: **MUSICSTOP**
-   Long name: Stop Music

#### Argument

none

#### Stack

  
*0 or 1*

**MUSICSTOP**

#### Description

Presumably stops the music from playing. There are some points where
MUSICSTOP is called twice in a row like this:

  
PSHN\_L 1

MUSICSTOP

PSHN\_L 0

MUSICSTOP
