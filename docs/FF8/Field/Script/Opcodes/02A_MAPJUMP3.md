---
title: 02A_MAPJUMP3
---

-   Opcode: **0x02A**
-   Short name: **MAPJUMP3**
-   Long name: Jump to map

#### Argument

Walkmesh ID

#### Stack

  
*Field Map ID*

*XCoord*

*YCoord*

*ZCoord*

*(angle?)*

**MAPJUMP3**

#### Description

Jump the player to the field with the given ID at the specified coordinates. Last parameter is probably the angle to face, because it's never above 360 (the highest I've found is 240). Interestingly, the last parameter is always even, and except for the values 6 and 10, it's always a multiple of 4 in the game.
