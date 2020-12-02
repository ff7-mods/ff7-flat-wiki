---
title: FF1NES
---

[Home](Main%20Page.md) > FF1NES

To understand how the data is organized for Final Fantasy 1, you must
first understand how the original NES operated.

The NES had a 6502 microprocessor, this gave the system a maximum of
65,536 bytes, or 64K of addressable memory. At the time, RAM was very
expensive, costing upwardly of one dollar per kilobyte of storage. When
Nintendo created the original NES, the game slot plugged in 32K of ROM,
split into two sections of 16K each. As games grew, "mapping"
technologies allowed the top half of 16K to be swapped out for other
sections of 16K ROM.

FF1 uses this technology to organize it's ROM. The game is split into 16
banks of 16K each. (This means the whole game is 256K in size.)

A typical NES ROM downloaded from the Internet almost always has a 10
byte header at the beginning. For our purposes, this data is going to be
thrown away. This is for two reasons.

-   This document assumes you have an original ROM dump and not
    something downloaded.
-   It messes up bank boundaries and offsets by 10 bytes, making it
    harder to point to data

The following below is a map of the ROM.

| Bank   | Data Within                             |
|--------|-----------------------------------------|
| Bank 0 | Inital values                           |
| Bank 1 | Overworld map and decompresser          |
| Bank 2 | Overworld Graphics/sprites              |
| Bank 3 | Town/Dungeon graphics                   |
| Bank 4 | Town/Dungeon maps and decompresser      |
| Bank 5 | Code                                    |
| Bank 6 | Code                                    |
| Bank 7 | Battle Graphics (Overworld)             |
| Bank 8 | Battle Graphics (Dungeon)               |
| Bank 9 | Shop/menu text/character battle/minimap |
| Bank A | Dialog                                  |
| Bank B | Bridge Crossing/Ending Event            |
| Bank C | Armor/weapon data                       |
| Bank D | Code + Crystal Graphics                 |
| Bank E | Code                                    |
| Bank F | Kernel                                  |
