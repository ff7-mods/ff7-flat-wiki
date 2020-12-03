---
title: 05F SETMESSPEED
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 05F SETMESSPEED

-   Opcode: **0x05F**
-   Short name: **SETMESSPEED**
-   Long name: Set Message Speed

#### Argument

none

#### Stack

  
*Message Channel*

*Speed (always 6144)*

**SETMESSPEED**

#### Description

Sets message speed.

This is only used twice and both in the same place: During the Ragnarok
scene right before the dialogue goes to "auto-play" mode and that
dreadful song starts. Because it's never called anywhere else, it's safe
to assume that it's field-specific. In other words, changing areas
"resets" the message speed.
