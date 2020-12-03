---
title: 013 PSHAC
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 013 PSHAC

-   Opcode: **0x013**
-   Short name: **PSHAC**
-   Long name: Push actor code???

#### Argument

ID of the entity to reference

#### Stack

none

#### Description

Push the entity ID of an actor onto the stack. This is always used
before a call to [CTURN][] to set which character will be faced. IDK
what happens when you try to use literals for CTURN or why this function
is necessary.

  [CTURN]: FF8/Field/Script/Opcodes/090%20CTURN.md "wikilink"
