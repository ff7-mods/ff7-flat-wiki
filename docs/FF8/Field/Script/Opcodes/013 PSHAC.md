---
title: 013 PSHAC
---

[Home](../../../../Main%20Page.md.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 013 PSHAC

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

  [CTURN]: 090%20CTURN.md "wikilink"
