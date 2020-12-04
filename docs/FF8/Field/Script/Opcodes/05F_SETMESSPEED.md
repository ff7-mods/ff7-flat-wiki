---
title: 05F_SETMESSPEED
---

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

This is only used twice and both in the same place: During the Ragnarok scene right before the dialogue goes to "auto-play" mode and that dreadful song starts. Because it's never called anywhere else, it's safe to assume that it's field-specific. In other words, changing areas "resets" the message speed.
