---
title: 04A ASK
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 04A ASK

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

Opens a field message window and lets player choose a single line. ASK
saves the chosen line index into a temp variable which you can retrieve
with PSHI\_L 0.

[AASK][] is an upgrade that also lets you set the window position.

  [AASK]: /FF8/Field/Script/Opcodes/06F%20AASK.md "wikilink"
