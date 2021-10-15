---
title: Status_Effects
---

## Status Effects

There are 31 Status effects in FF7. In attacks and items they are referred to as a 32-bit longword. In Materia they are only 24-bits so the last 8 cannot be affected. In weapons and armors they are represented as an index. Weapons have a low inflict chance.

| Bit        | Index | Status       |
|------------|-------|--------------|
| 0x00000001 | 00    | Death        |
| 0x00000002 | 01    | Near Death   |
| 0x00000004 | 02    | Sleep        |
| 0x00000008 | 03    | Poison       |
| 0x00000010 | 04    | Sadness      |
| 0x00000020 | 05    | Fury         |
| 0x00000040 | 06    | Confu        |
| 0x00000080 | 07    | Silence      |
| 0x00000100 | 08    | Haste        |
| 0x00000200 | 09    | Slow         |
| 0x00000400 | 0A    | Stop         |
| 0x00000800 | 0B    | Frog         |
| 0x00001000 | 0C    | Small        |
| 0x00002000 | 0D    | Slow Numb    |
| 0x00004000 | 0E    | Petrify      |
| 0x00008000 | 0F    | Regen        |
| 0x00010000 | 10    | Barrier      |
| 0x00020000 | 11    | M.Barrier    |
| 0x00040000 | 12    | Reflect      |
| 0x00080000 | 13    | Dual         |
| 0x00100000 | 14    | Shield       |
| 0x00200000 | 15    | D.Sentence   |
| 0x00400000 | 16    | Manipulate   |
| 0x00800000 | 17    | Berserk      |
| 0x01000000 | 18    | Peerless     |
| 0x02000000 | 19    | Paralysis    |
| 0x04000000 | 1A    | Darkness     |
| 0x08000000 | 1B    | Dual Drain   |
| 0x10000000 | 1C    | DeathForce   |
| 0x20000000 | 1D    | Resist       |
| 0x40000000 | 1E    | "Lucky Girl" |
| 0x80000000 | 1F    | Imprisoned   |

If "Dual Drain" is inflicted without "Dual", the game will crash. Section 4 of Terence Fergusson's [http://www.gamefaqs.com/console/psx/file/197341/22395 Battle Mechanics FAQ](http://www.gamefaqs.com/console/psx/file/197341/22395_Battle_Mechanics_FAQ) describes each of these statuses with great detail.
