---
title: 069_BATTLE
---

-   Opcode: **0x069**
-   Short name: **BATTLE**
-   Long name: Start a battle

#### Argument

none

#### Stack

  
*[Encounter ID](../../../Encounter_Codes.md)*

*Battle Flags*

**BATTLE**

#### Description

Begin a battle with the given encounter id.

#### Battle Flags

  
+0: Regular battle.

+1: No escape?

+2: Disable victory fanfare (battle music keeps playing after win/loss)

+4: Inherit countdown timer from field.

+8: No Item/XP Gain?

+16: Use current music as battle music.

+32: Force preemptive attacked

+64: Force back attack

+128: unknown
