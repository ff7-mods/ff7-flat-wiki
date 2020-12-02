---
title: 034 RCANIMEKEEP
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 034 RCANIMEKEEP

-   Opcode: **0x034**
-   Short name: **RCANIMEKEEP**
-   Long name: Resume script, controlled animation, keep last frame

#### Argument

Model Animation ID

#### Stack

  
*Last frame of animation*

*First frame of animation*

**RCANIMEKEEP**

#### Description

Play the range of frames of an animation, then freeze the model on the
last frame played. Used to make a character perform "half an animation"
and then finish the animation later in a script.
