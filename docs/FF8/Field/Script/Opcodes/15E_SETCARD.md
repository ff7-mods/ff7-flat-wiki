---
title: 15E_SETCARD
---

-   Opcode: **0x15E**
-   Short name: **SETCARD**
-   Long name: Set Card

#### Argument

none

#### Stack

  
Deck ID

Card ID

**SETCARD**

#### Description

Moves a card to the specified deck. Sets the first temp variable to 0 if successful.

Rare cards (level 8+) are unique, moving from deck to deck.

If you give the player (deck 240) a non-rare card, it adds one to their collection (max 100). If you give anyone else a non-rare card it *removes* one from the player's collection.
