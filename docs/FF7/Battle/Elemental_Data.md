---
title: Elemental_Data
---

## Elemental Data

There are 16 elements in FF7. They are usually stored as a bitmask, but are instead stored as an index in the case of materia.

|  Bit   | Index | Element         |     |
|:------:|-------|-----------------|-----|
| 0x0001 | 00h   | Fire            |     |
| 0x0002 | 01h   | Ice             |     |
| 0x0004 | 02h   | Bolt            |     |
| 0x0008 | 03h   | Earth           |     |
| 0x0010 | 04h   | Poison          |     |
| 0x0020 | 05h   | Gravity         |     |
| 0x0040 | 06h   | Water           |     |
| 0x0080 | 07h   | Wind            |     |
| 0x0100 | 08h   | Holy            |     |
| 0x0200 | 09h   | Restorative     |     |
| 0x0400 | 0Ah   | Cut             |     |
| 0x0800 | 0Bh   | Hit             |     |
| 0x1000 | 0Ch   | Punch           |     |
| 0x2000 | 0Dh   | Shoot           |     |
| 0x4000 | 0Eh   | Shout           |     |
| 0x8000 | 0Fh   | "Hidden/Ultima" |     |

  
NOTES:  
The battle text (part 26 of the [KERNEL.BIN](../Kernel/Kernel.bin) refers to "Ice" as "Cold" and "Bolt" as "Lightning".  
The names of elements 09h - 0Eh are not ever mentioned in the game. However, they are stored as battle text for the purpose of sensing.  
"Hidden/Ultima" has no name mentioned in the battle text.  
"Hidden/Ultima" is on only a few enemy exclusive attacks including Ultima Weapon's Ultima Beam. Elements 0Ah - 0Eh are considered Physical elements (though not enforced as such) and show up on physical attacks. Non-elemental attacks, such as Bahamuts' Flares, have no elements selected.
