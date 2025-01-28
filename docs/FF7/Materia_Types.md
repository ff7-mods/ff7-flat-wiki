---
title: Materia_Types
---

## Types

Materia is separated into five categories of functions in the game: "Command", "Magic", "Summon", "Independent", and "Support". Graphically they are yellow, green, red, blue, and purple respectively. The materia type is determined by a single byte value that is separated into two parts. The upper nybble will be considered the sub-type and the lower nybble is the base type. For base types the values will yield the following results:

| Base | Materia Type            |
|------|-------------------------|
| X0   | Independent             |
| X1   | Independent             |
| X2   | Command                 |
| X3   | Command                 |
| X4   | Independent             |
| X5   | Support                 |
| X6   | Command                 |
| X7   | Command                 |
| X8   | Command                 |
| X9   | Magic                   |
| XA   | Magic                   |
| XB   | Summon                  |
| XC   | Summon                  |
| XD   | Independent<sup>1</sup> |
| XE   | Independent<sup>1</sup> |
| XF   | Independent<sup>1</sup> |

  
Each of these Base Types have a set of sub-types that provide different functions. They are used to determine what function to provide, usually based on the Materia's attribute list. These sub-types have the following functions when equipped:  
(If sub-type is listed as 'X' then any sub-type will produce that effect. Other sub-types have no function. Battle effects not mentioned.)

| Independent Types: |  |  |  |
|----|----|----|----|
| 00 | Function based on Attribute 1 |  |  |
|   | 0Ch | Character's flags ORd with 1 and MateriaHandler set to 11 (Underwater) |  |
|  | 62h | Character's flags ORd with 8 and MateriaHandler set to 11 (HP\<-\>MP) |  |
| 20<sup>2</sup> | Increases Stat Bonus value based on attribute list<sup>2A</sup> and AP level and sets MateriaHandler to 4 |  |  |
| 30<sup>3</sup> | Character's flags ORd with 4 and MateriaHandler set to 12 |  |  |
| 40 | Same as 20, but sets MateriaHandler to 0Dh (EXP Plus) |  |  |
| 21<sup>4</sup> | Enables effect Attribute 1 with a magnitude based on attribute list and AP Level |  |  |
| 41 | Enables effect Attribute 1 with a magnitude based on attribute list and AP Level |  |  |
| X4 | If 0xC06914 is non-0 after getting AP level then set MateriaHandler to 0Bh (Mega-All) |  |  |
|   |  |  |  |
| Command Types: |  |  |  |
| 12 | Replace first command (Attack) based on attribute list and AP Level |  |  |
| X3 | Subtype not important. Only Primary Attributes allowed are 15h, 16h, 17h |  |  |
|   | 15h | Replaces Magic with WMagic |  |
|  | 16h | Replaces Summon with WSummon |  |
|  | 17h | Replaces Item with WItem |  |
| X6 | Add Command based on attribute list and AP Level |  |  |
| X7 | Add Command 0Dh (E.Skill) |  |  |
| X8 | Add Command 5 (Steal), 6 (Sense), 7 (Coin), 9 (Morph), Ah (D.Blow), Bh (Manip), Ch (Mime) |  |  |
|   |  |  |  |
| Support Types: |  |  |  |
| 25 | Attribute 1 must be between 54h - 64h inclusive. Just sets the MateriaHandler to a specific value |  |  |
|   | Attribute 1 Value | MateriaHandler | Materia |
|  | 54h | 0Fh | Command Counter |
|  | 55h | 0Fh | Magic Counter |
|  | 56h | 10h | Sneak Attack |
|  | 57h | Ignored |  |
|  | 58h | 10h | MP Turbo |
|  | 59h | 10h | MP Absorb |
|  | 5Ah | 10h | HP Absorb |
|  | 5Bh | Ignored |  |
|  | 5Ch | 10h | Added Cut |
|  | 5Dh | 10h | Steal As Well |
|  | 5Eh | 10h | Elemental |
|  | 5Fh | 10h | Added Effect |
|  | 60h | Ignored |  |
|  | 61h | Ignored |  |
|  | 62h | Ignored |  |
|  | 63h | Ignored |  |
|  | 64h | 10h | (Unused) |
| 35 | Like 25, but only Attribute 1 values 51h, 57h, and 63h are used. |  |  |
|   | 51h | 0Fh | All |
|  | 57h | 10h | Final Attack |
|  | 63h | 0Fh | Quadra Magic |
|   |  |  |  |
| Magic Types: |  |  |  |
| X9 | Add Command 2 (Magic) and Enable magics based on attribute list and AP Level |  |  |
| XA | Add Command 2 (Magic) and Enable magics with index 0-37h inclusive<sup>5</sup> |  |  |
|   |  |  |  |
| Summon Types: |  |  |  |
| XB | Add Command 3 (Summon) and enables attack at Attribute 1 for use 'AP Level' times (Ignores other Attributes) |  |  |
| XC | Add Command 3 (Summon) and enables attacks with index 38h - 47h inclusive |  |  |

  
1 - There are no XD, XE or XF type materias in the game. They are graphically represented as Independent but have no effect.  

2 - Various in-battle conditions (Cover/Counter) and stat increases  
:2A - 0=Strength; 1=Vitality; 2=Magic; 3=Spirit; 4=Speed; 5=Luck; 6=Attack; 7=Defense; 8=MHP; 9=MMP; 10=EXP; higher than 10 results in memory leaks

3 - ONLY works with Materia Index 0Ch (Long Range). Attribute List is ignored  

4 - Although Enemy Away's first attribute shares a value with Enemy Lure (1), it is handled differently based on index to alter a different memory address from Enemy Lure.

5 - Shield is the last magic attack with an index of 35h. The Magic menu prevents access to attacks 36h & 37h  

## Materia Handler

These are the values assigned to each materia type:

| Handler Value | Type                                      |
|---------------|-------------------------------------------|
| 00            | None                                      |
| 01            | Magic Materia (excluding Master Magic)    |
| 02            | Summon Materia (excluding Master Summon)  |
| 03            | Base 6                                    |
| 04            | 20                                        |
| 05            | Master Command                            |
| 06            | Master Magic                              |
| 07            | Master Summon                             |
| 08            | E.Skill                                   |
| 09            | 41                                        |
| 0A            | 21                                        |
| 0B            | Mega-All                                  |
| 0C            | None                                      |
| 0D            | EXP Plus                                  |
| 0E            | W-Materia                                 |
| 0F            | some 25 & 35                              |
| 10            | some 25 & 35                              |
| 11            | 00                                        |
| 12            | Specifically CounterAttack and Long Range |
| 13            | Base 2                                    |

It primarily (exclusively?) tells the menu loader which texts to bring up when a menu is loaded.
