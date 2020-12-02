---
title: 159 SEALEDOFF
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 159 SEALEDOFF

-   Opcode: **0x159**
-   Short name: **SEALEDOFF**
-   Long name: Enable Sealed Options (Ultimecia's Castle)

#### Argument

none

#### Stack

  
*Option flags*

**SEALEDOFF**

#### Description

Enables features of the game pertaining to the last dungeon's mechanic
(items, saving, etc).

Whether or not these are enabled/disabled is stored in [byte 334][].
0=Sealed, 1=Unsealed

Flags:

  
1\. Items

2\. Magic

4\. GF

8\. Draw

16\. Command Ability

32\. Limit Break

64\. Resurrection

128\. Save

  [byte 334]: /FF8/Variables.md "wikilink"
