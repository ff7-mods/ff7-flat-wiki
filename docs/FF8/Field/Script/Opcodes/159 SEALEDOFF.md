---
title: 159 SEALEDOFF
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF8](/ff7-flat-wiki/FF8.md) > [Field](/ff7-flat-wiki/FF8/Field.md) > [Script](/ff7-flat-wiki/FF8/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF8/Field/Script/Opcodes.md) > 159 SEALEDOFF

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

  [byte 334]: /ff7-flat-wiki/FF8/Variables.md "wikilink"
