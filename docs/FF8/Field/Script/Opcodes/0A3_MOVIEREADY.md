---
title: 0A3_MOVIEREADY
---

-   Opcode: **0x0A3**
-   Short name: **MOVIEREADY**
-   Long name: Prepare Movie

#### Argument

none

#### Stack

  
*Movie ID*

*(?)*

**MOVIEREADY**

#### Description

Prepares a FMV movie to be played with [MOVIE](04F_MOVIE.md). The second parameter is either 0 or 1, but I have no idea what it does.

The movie that plays depends on which disc is currently active.

| Movie ID | Disc 1 Description       | Disc 2 Description                | Disc 3 Description            | Disc 4 Description         |
|----------|--------------------------|-----------------------------------|-------------------------------|----------------------------|
| 0        | Balamb Garden explore    | Squall's Cell                     | Esthar Decloaks               | Rinoa and Adel             |
| 1        | Quistis Appears          | Prison Desert Overlook            | Esthar Elevator 1             | Time Compression           |
| 2        | Zell Appears             | Prison Submerges 1                | Esthar Leave (car)            | Ultimecia's Castle         |
| 3        | Dollet Intro             | Prison Submerges 2                | Esthar Arrive (car)           | Showdown with Ultimecia    |
| 4        | Selphie Appears          | Missile Launch                    | Presidential Palace leave?    | Ending 1 (Squall in Limbo) |
| 5        | Dollet Tower Transform   | Missile Base Explodes 1           | Presidential Palace enter?    | Credits 2 (Balcony)        |
| 6        | X-ATM Steps on a Car     | Missile Base Explodes 2           | Pandora Lab Elevator down     | Ending and Credits         |
| 7        | Dollet Escape            | Missiles in Clouds                | Space Pod Launch              |                            |
| 8        | Ballroom - Shooting Star | Missiles over Water               | Space Pods exit atmosphere    |                            |
| 9        | Ballroom Dance           | MD Machine Startup                | Space Station enter           |                            |
| 10       | Timber Train 1           | Garden Ring Energizes             | Closeup of Moon 1             |                            |
| 11       | Timber Train 2           | Missile Impact                    | Closeup of Moon 2             |                            |
| 12       | Timber TV Distortion     | Missiles Destroy Garden (unused)  | LP over Esthar                |                            |
| 13       | Timber TV Camera Tilt    | Flying Garden Overlook            | LP Over Tears' Point          |                            |
| 14       | Enter Galbadia Garden    | Flying Garden Overlook (w/ Rinoa) | Monsters falling off Moon     |                            |
| 15       | Irvine Appears           | Garden over Balamb                | Adel's Tomb                   |                            |
| 16       | Enter Deling City        | Garden Crashes into Ocean         | Escape Pods Launch            |                            |
| 17       | Edea Appears             | Garden in Ocean                   | Rinoa in Space 1              |                            |
| 18       | Edea Approaches Podium   | White SeeD Ship                   | Rinoa in Space 2              |                            |
| 19       | Crowd Cheers             | Crash into FH                     | Rinoa in Space 3              |                            |
| 20       | Iguions Attack           | FH Overlook                       | Rinoa in Space - Ring         |                            |
| 21       | Parade Starts            | G-Garden through Binocs           | Rinoa Life Support            |                            |
| 22       | Parade 1                 | G-Garden through Forest           | View of Lunar Cry             |                            |
| 23       | Parade 2                 | Garden Showdown                   | Ragnarok Conveniently Appears |                            |
| 24       | Carousel Raises          | G-Cyclist Attack                  | Board Ragnarok                |                            |
| 25       | Gateway Trap             | Rinoa Falls                       | Ragnarok Hatch Open           |                            |
| 26       | Irvine's Shot            | After Rinoa Falls                 | Unlock Rinoa's Tomb           |                            |
| 27       | Squall Assaults Edea     | G-Garden pre-Ram                  | Enter LP 1                    |                            |
| 28       | Seifer and Edea          | G-Garden Ram                      | Ragnarok with Adel's Tomb     |                            |
| 29       | Wounded                  | G-Mechs Launch                    | Enter LP 2                    |                            |
| 30       | Liberi Fatali            | Another Ram                       | Lunar Cry                     |                            |
| 31       |                          | Balamb Ram                        | Lunar Cry Begins              |                            |
| 32       |                          | Escape Hatch                      |                               |                            |
| 33       |                          | Paratrooper fight                 |                               |                            |
