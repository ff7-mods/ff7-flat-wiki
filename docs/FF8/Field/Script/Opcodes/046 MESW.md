---
title: 046 MESW
---

[Home](../../../../Main%20Page.md.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 046 MESW

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

  [WINSIZE]: 04B%20WINSIZE.md "wikilink"
