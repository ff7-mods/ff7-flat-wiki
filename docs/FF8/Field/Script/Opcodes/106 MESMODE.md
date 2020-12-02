---
title: 106 MESMODE
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 106 MESMODE

-   Opcode: **0x106**
-   Short name: **MESMODE**
-   Long name: Message Mode

#### Argument

none

#### Stack

  
*Message Channel*

*Message Window Behavior*

*(color?)*

**MESMODE**

#### Description

Sets all future messages sent to this channel to behave differently.
Behaviors:

  
0: Regular message with opaque background window

1: Translucent window background

2: No window background

The last parameter controls the color of text displayed in messages.
0=black, 4096=white. Haven't played around with it much.
