---
title: CF_MMBUK
---

- Opcode: **0xCF**
- Short name: **MMBUK**
- Long name: Party Select: Character Unlock

#### Memory layout

| 0xCF | *C* |
|------|-----|

#### Arguments

- **const UByte** *C*: Character ID to unlock.

#### Description

Unocks the character given by the argument in the Party Select screen. The player will be able to move this character into or out of the party. The character IDs can be found in [MMBud](CD_MMBud).

This setting has global scope, that is, the character will still be switchable when transitioning to a new field or to the world map and using the PHS.
