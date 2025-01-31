---
title: Encounters
---

## Introduction

World map random encounter data is stored in the "enc_w.bin" file in the world_xx.lgp archive (on the PC version). Battles are selected based on the [region](FF7/WorldMap_Module#Regions "wikilink") and [walkmap type](FF7/WorldMap_Module#Walkmap "wikilink") of the [current triangle](../WorldMap_Module#Triangle).

**NOTE: The enc_w.bin file contains only data for first 16 regions. Any region later than that will receive encounters from region 16.**

Additionally Hill Side type battle will use the table for Grass type, and Gold Saucer Desert type will use the table for Desert type.

## Random encounter mechanics

For each region the enc_w.bin file contains 4 sets of encounters for different walkmap types. Which four are these will be used is decided using a lookup table (stored at address **0x96dea0** on PC), that maps regions to one of four walkmap types for each of four encounter sets.

| Region                 | Type 1 | Type 2        | Type 3                | Type 4    |
|------------------------|--------|---------------|-----------------------|-----------|
| Midgar Area            | Grass  | Wasteland     | <unused>              | Beach     |
| Grasslands Area        | Grass  | <unused>      | <unused>              | Beach     |
| Junon Area             | Grass  | Wasteland     | Forest                | Beach     |
| Corel Area             | Grass  | Mountain Pass | <unused>              | Beach     |
| Gold Saucer Area       | Grass  | Wasteland     | Desert                | Beach     |
| Gongaga Area           | Grass  | <unused>      | Jungle                | Beach     |
| Cosmo Area             | Grass  | Wasteland     | Canyon                | Beach     |
| Nibel Area             | Grass  | <unused>      | Forest                | Beach     |
| Rocket Launch Pad Area | Grass  | <unused>      | Forest                | Beach     |
| Wutai Area             | Grass  | Wasteland     | Wutai Bridge          | Beach     |
| Woodlands Area         | Grass  | Wasteland     | Jungle                | Beach     |
| Icicle Area            | Grass  | Snow          | Snowfield (Wasteland) | Beach     |
| Mideel Area            | Grass  | Wasteland     | Jungle                | Beach     |
| North Corel Area       | Grass  | <unused>      | Desert                | Riverside |
| Cactus Island          | Grass  | <unused>      | Desert                | <unused>  |
| Goblin Island\*        | Grass  | <unused>      | Forest                | <unused>  |

Region to walkmap type look-up table

*Note: The types marked as <unused> are stored as 00 (Grass) in the table, the reason they're unused is because Grass is always Type 1 and so if the player is on Grass the other types will not be considered*

After deciding whether a random battle should occur the game first performs the Mystery Ninja check. For each of 16 regions it consults a lookup table (**0x96dee0** on PC) for a chance (out of 256) if a Yuffie fight should start.

| Region                 | Chance          |
|------------------------|-----------------|
| Junon Area             | 12.5% (32/256)  |
| Gongaga Area           | 25% (64/256)    |
| Nibel Area             | 25% (64/256)    |
| Rocket Launch Pad Area | 99.6% (255/256) |
| Woodlands Area         | 50% (128/256)   |
| Mideel Area            | 50% (128/256)   |
| Goblin Island\*        | 50% (128/256)   |

Yuffie encounter chances per region

*\* this also includes all following regions (Round Island being the only one where encounters are possible)*

If that check succeeds the game checks whether player is either on Forest or Jungle type triangle and if Yuffie is available for fightning (based on bit 1 from variable **0x0D29** from the [Savemap Memory Bank 3](../Savemap#Save_Memory_Bank_3.2F4). If this succeeds too game determines which battle scene to use based on Cloud's level, using the 1st table stored in enc_w.bin.

Next are checks for Chocobo fights. If the [current triangle](../WorldMap_Module#Triangle).

Finally the game does separate checks for special battles (back, side and pincer attacks) and if they fail it will pick one from the 6 normal random battles.

For more in-depth information consult Terence Fergusson's excellent [Enemy Mechanics FAQ](https://gamefaqs.gamespot.com/ps/197341-final-fantasy-vii/faqs/31903) document (section 3.1 has a detailed write-up on all the above).

## enc_w.bin file format

### Overview

The enc_w.bin file is divided into three sections:

| Offset | Size       | Description               |
|--------|------------|---------------------------|
| 0x00   | 32 bytes   | Yuffie encounter mapping  |
| 0x20   | 128 bytes  | Chocobo encounter ratings |
| 0xA0   | 2048 bytes | Random encounter table    |

The format of each of these sections is as follows:

### Yuffie encounter mapping

Contains 8 records, each 4 bytes long, that maps Cloud's current level to battle's Scene ID that will be started.

| Offset | Size    | Description   |
|--------|---------|---------------|
| 0x00   | 2 bytes | Cloud's Level |
| 0x02   | 2 bytes | Scene ID      |

### Chocobo rating mapping

32 records, each 4 bytes long, mapping the scene ID to the rating of the chocobo if caught.

| Offset | Size    | Description                                       |
|--------|---------|---------------------------------------------------|
| 0x00   | 2 bytes | Chocobo battle scene ID                           |
| 0x02   | 2 bytes | Chocobo rating (1 = wonderful, ..., 8 = terrible) |

### Random encounter table

This section is 2048 bytes long and contains 16 sections for each region (as mentioned before regions 17 and later will receive encounters from region 16).

Each section contains 4 sets of 32-byte blocks for each walkmap type (see above on how walkmap types are decided) that are as follows:

| Offset | Size     | Description                          |
|--------|----------|--------------------------------------|
| 0x00   | 1 byte   | Encounters active? (0 = no, 1 = yes) |
| 0x01   | 1 byte   | Encounter rate                       |
| 0x02   | 12 bytes | Normal encounters                    |
| 0x0E   | 4 bytes  | Back attack encounters               |
| 0x12   | 2 bytes  | Side attack encounters               |
| 0x14   | 2 bytes  | Both sides encounters                |
| 0x16   | 8 bytes  | Chocobo encounters                   |
| 0x1E   | 2 bytes  | Padding (Always 00's)                |

Each encounter record is 2 bytes long, with the first byte being the encounter ID and the second byte being the encounter rate (only the first six bits are used).
