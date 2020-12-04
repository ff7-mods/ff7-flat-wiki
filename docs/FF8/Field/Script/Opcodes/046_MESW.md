---
title: 046_MESW
---

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

Popup a message window, and wait for the player to dismiss it before continuing. The size of the message window can be set with [WINSIZE](04B_WINSIZE.md).

This is never used anywhere in the game, but it works. It was replaced by AMESW, which has built-in position and size parameters.
