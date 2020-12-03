---
title: Materia Types
---

[Home](Main%20Page.md) > [FF7](FF7.md) > Materia Types

## Types

Materia is separated into five categories of functions in the game:
"Command", "Magic", "Summon", "Independent", and "Support". Graphically
they are yellow, green, red, blue, and purple respectively. The materia
type is determined by a single byte value that is separated into two
parts. The upper nybble will be considered the sub-type and the lower
nybble is the base type. For base types the values will yield the
following results:

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

  
Each of these Base Types have a set of sub-types that provide different
functions. They are used to determine what function to provide, usually
based on the Materia's attribute list. These sub-types have the
following functions when equipped:  
(If sub-type is listed as 'X' then any sub-type will produce that
effect. Other sub-types have no function. Battle effects not mentioned.)

| Independent Types:                                     |
|--------------------------------------------------------|
| 00                                                     |
|                                                        |
| 62h                                                    |
| 20<sup>2</sup>                                         |
| 30<sup>3</sup>                                         |
| 40                                                     |
| 21<sup>4</sup>                                         |
| 41                                                     |
| X4                                                     |
| style="background:rgb(255,255,255);" colspan = "4"\|   |
| Command Types:                                         |
| 12                                                     |
| X3                                                     |
|                                                        |
| 16h                                                    |
| 17h                                                    |
| X6                                                     |
| X7                                                     |
| X8                                                     |
| style="background:rgb(255,255,255);" colspan = "4"\|   |
| Support Types:                                         |
| 25                                                     |
|                                                        |
| 54h                                                    |
| 55h                                                    |
| 56h                                                    |
| 57h                                                    |
| 58h                                                    |
| 59h                                                    |
| 5Ah                                                    |
| 5Bh                                                    |
| 5Ch                                                    |
| 5Dh                                                    |
| 5Eh                                                    |
| 5Fh                                                    |
| 60h                                                    |
| 61h                                                    |
| 62h                                                    |
| 63h                                                    |
| 64h                                                    |
| 35                                                     |
|                                                        |
| 57h                                                    |
| 63h                                                    |
| style="background:rgb(255,255,255);" colspan = "4"\|   |
| Magic Types:                                           |
| X9                                                     |
| XA                                                     |
| style="background:rgb(255,255,255);" colspan = "4"\|   |
| Summon Types:                                          |
| XB                                                     |
| XC                                                     |

  
1 - There are no XD, XE or XF type materias in the game. They are
graphically represented as Independent but have no effect.  

2 - Various in-battle conditions (Cover/Counter) and stat increases  
:2A - 0=Strength; 1=Vitality; 2=Magic; 3=Spirit; 4=Speed; 5=Luck;
6=Attack; 7=Defense; 8=MHP; 9=MMP; 10=EXP; higher than 10 results in
memory leaks

3 - ONLY works with Materia Index 0Ch (Long Range). Attribute List is
ignored  

4 - Although Enemy Away's first attribute shares a value with Enemy Lure
(1), it is handled differently based on index to alter a different
memory address from Enemy Lure.

5 - Shield is the last magic attack with an index of 35h. The Magic menu
prevents access to attacks 36h & 37h  

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

It primarily (exclusively?) tells the menu loader which texts to bring
up when a menu is loaded.
