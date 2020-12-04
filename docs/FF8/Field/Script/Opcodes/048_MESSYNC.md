---
title: 048_MESSYNC
---

-   Opcode: **0x048**
-   Short name: **MESSYNC**
-   Long name: Message Window Sync

#### Argument

none

#### Stack

  
*Message Channel*

**MESSYNC**

#### Description

After [AMES](065_AMES.md) is called, the window it creates stays until either [WINCLOSE](04C_WINCLOSE.md) or **MESSYNC** is called. WINCLOSE closes the window at that point in the script, while MESSYNC waits for the player to press the OK button. This allows the script to do other things while the window is open while preventing the player from dismissing the window too early (like play sounds or animations).
