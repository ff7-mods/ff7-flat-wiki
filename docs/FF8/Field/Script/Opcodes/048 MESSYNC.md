---
title: 048 MESSYNC
permalink: 048 MESSYNC.html
---

[Home](../../../../Main%20Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 048 MESSYNC

-   Opcode: **0x048**
-   Short name: **MESSYNC**
-   Long name: Message Window Sync

#### Argument

none

#### Stack

  
*Message Channel*

**MESSYNC**

#### Description

After [AMES][] is called, the window it creates stays until either
[WINCLOSE][] or **MESSYNC** is called. WINCLOSE closes the window at
that point in the script, while MESSYNC waits for the player to press
the OK button. This allows the script to do other things while the
window is open while preventing the player from dismissing the window
too early (like play sounds or animations).

  [AMES]: 065%20AMES.md "wikilink"
  [WINCLOSE]: 04C%20WINCLOSE.md "wikilink"
