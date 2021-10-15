---
title: 13A_CARDGAME
---

-   Opcode: **0x13A**
-   Short name: **CARDGAME**
-   Long name: Card Game

#### Argument

none

#### Stack

  
Deck ID

Known rules

Region rules

Rare card chance

Unknown1

Unknown2

Unknown3

**CARDGAME**

#### Description

Starts a game of Triple Triad against the specified deck.

"Region rules" are the rules for the region you're in, and "known rules" are the ones you're spreading from elsewhere. There should be a copy of the "cardgamemaster" entity on the scene to handle all this - call "\[region\]\_maeshori0" before the game, then pass byte vars 292 and 293 into this, and finally call "\[region\]\_shori0" afterwards.

"Rare card chance" is a percentage chance (0-100) that the opponent will play a rare card if they have one.

Not known what the remaining 3 numbers do yet. Presumably the range of common cards they'll use is included. Maybe some AI characteristics like thinking time.
