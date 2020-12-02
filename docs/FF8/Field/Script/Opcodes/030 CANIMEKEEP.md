---
title: 030 CANIMEKEEP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 030 CANIMEKEEP

-   Opcode: **0x030**
-   Short name: **CANIMEKEEP**
-   Long name: Controlled animation, keep last frame

#### Argument

Model Animation ID

#### Stack

  
*Last frame of animation*

*First frame of animation*

**CANIMEKEEP**

#### Description

Play the range of frames of an animation, then freeze the model on the
last frame played. Pauses script until animation finishes. Used to make
a character perform "half an animation" and then finish the animation
later in a script.
