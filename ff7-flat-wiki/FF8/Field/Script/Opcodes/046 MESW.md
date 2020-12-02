---
title: 046 MESW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 046 MESW

-   Opcode: **0x046**
-   Short name: **MESW**
-   Long name: Display Message and Wait

#### Argument

none

#### Stack

  
*Message channel*

*Message ID*

**MESW**

#### Description

Popup a message window, and wait for the player to dismiss it before
continuing. The size of the message window can be set with [WINSIZE][].

This is never used anywhere in the game, but it works. It was replaced
by AMESW, which has built-in position and size parameters.

  [WINSIZE]: /ff7-flat-wiki/FF8/Field/Script/Opcodes/04B%20WINSIZE.md "wikilink"
