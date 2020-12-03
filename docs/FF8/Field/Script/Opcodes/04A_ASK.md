---
title: 04A_ASK
---

[Home](../../../../Main_Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 04A ASK

-   Opcode: **0x04A**
-   Short name: **ASK**
-   Long name: Ask

#### Argument

none

#### Stack

  
*Message Channel*

*Field message ID*

*Line of first option*

*Line of last option*

*Line of default option*

*Line of cancel option*

**ASK**

#### Description

Opens a field message window and lets player choose a single line. ASK saves the chosen line index into a temp variable which you can retrieve with PSHI\_L 0.

[AASK](06F_AASK.md) is an upgrade that also lets you set the window position.
