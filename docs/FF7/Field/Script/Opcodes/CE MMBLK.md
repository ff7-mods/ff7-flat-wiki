---
title: CE MMBLK
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > CE MMBLK

-   Opcode: **0xCE**
-   Short name: **MMBLK**
-   Long name: Party Select: Character Lock

#### Memory layout

| 0xCE | *C* |
|------|-----|

#### Arguments

-   **const UByte** *C*: Character ID to lock.

#### Description

Locks the character given by the argument in the Party Select screen.
The player will not be able to move this character into or out of the
party. The character IDs can be found in [MMBud][].

This setting has global scope, that is, the character will still be
locked when transitioning to a new field or to the world map and using
the PHS.

  [MMBud]: FF7/Field/Script/Opcodes/CD%20MMBud.md "wikilink"
