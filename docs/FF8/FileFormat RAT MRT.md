---
title: FileFormat RAT MRT
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > FileFormat RAT MRT

By myst6re.

## Field Rate and battle Formations (Encounter)

### Battle formations

MRT file contains 4 \* two bytes. Each two bytes is a battle formation
ID.

### Battle rate

RAT file contains 4 bytes. Each byte is the battle frequency, they are
always equal, but only the first is used by the game.  
If rate equal zero, there is no encounter, if rate equal 255, there are
often battles. Known values: 4, 6, 8, 10, 12 and 16.
