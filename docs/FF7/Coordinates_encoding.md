---
title: Coordinates_encoding
---

Coordinates on the world map are stored on 2 DWords and some basic decoding has to be done before you can manipulate them.

First DWord :

    [1F 1E 1D 1C 1B 1A 19 18:17 16 15 14 13 12 11 10:0F 0E 0D 0C 0B 0A 09 08:07 06 05 04 03 02 01 00]
    |     DIRECTION/0x10    |  OBJECT'S ID |               X COORDINATE OF THE OBJECT               |

Second DWord :

    [1F 1E 1D 1C 1B 1A 19 18:17 16 15 14 13 12 11 10:0F 0E 0D 0C 0B 0A 09 08:07 06 05 04 03 02 01 00]
    |        Z COORDINATE OF THE OBJECT       |              Y COORDINATE OF THE OBJECT             |

Notes :

- X is an unsigned value ranging from 0 to 0x47FFF
- Y is an unsigned value ranging from 0 to 0x37FFF
- Z is signed
- Direction is multiplied by 0x10 after reading from save-game, but that's not affecting anything so we can think of it as a byte value. e.g: 00: South, 40: East, 80: North, C0: West

| Value |          Object          |
|:-----:|:------------------------:|
| 0x00  |          Cloud           |
| 0x01  |           Tifa           |
| 0x02  |           Cid            |
| 0x03  |         Highwind         |
| 0x04  |      Yellow Chocobo      |
| 0x05  |       Tiny Bronco        |
| 0x06  |          Buggy           |
| 0x07  |    Cannon from Junon     |
| 0x0C  | Phoenix from Fort Condor |
| 0x0D  |        Submarine         |
| 0x0E  |       Gold Saucer        |
| 0x0F  |          Rocket          |
| 0x10  |    Rocket launch pad     |
| 0x13  |         Chocobo          |
| 0x18  |    North crater dome     |
| 0x19  |      Ancient Forest      |
| 0x1D  |          Weapon          |

**Table: Object ID**

## How to decode coordinates

Assuming *1st* and *2nd* are respectively the first and second DWords :

    X = 1st & 0x7FFFF
    Y = 2nd & 0x3FFFF
    Z = 2nd >> 0x12     // shift arithmetic right
    ID = (1st >> 0x13) & 0x1F
    DIR = (1st >> 0x14) & 0x0FF0
