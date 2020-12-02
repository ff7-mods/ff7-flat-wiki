---
title: 034 RCANIMEKEEP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 034 RCANIMEKEEP

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
