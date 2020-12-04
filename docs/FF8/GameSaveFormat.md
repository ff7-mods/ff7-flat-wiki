---
title: GameSaveFormat
---

By myst6re.

## The save format

PC steam version: Offsets start from at 384 (0x0180). File is compressed with LZS.

| Offset | Size                | Data                                                                                |
|--------|---------------------|-------------------------------------------------------------------------------------|
| 0x0000 | 2 bytes             | Checksum                                                                            |
| 0x0002 | 2 bytes             | Always 0x08FF                                                                       |
| 0x0004 | 2 bytes             | **Preview:** Location ID                                                            |
| 0x0006 | 2 bytes             | **Preview:** 1st character's current HP                                             |
| 0x0008 | 2 bytes             | **Preview:** 1st character's max HP                                                 |
| 0x000A | 2 bytes             | **Preview:** save count                                                             |
| 0x000C | 4 bytes             | **Preview:** Amount of Gil                                                          |
| 0x0020 | 4 bytes             | **Preview:** Total number of seconds played                                         |
| 0x0024 | 1 byte              | **Preview:** 1st character's level                                                  |
| 0x0025 | 1 byte              | **Preview:** 1st character's portrait                                               |
| 0x0026 | 1 byte              | **Preview:** 2nd character's portrait                                               |
| 0x0027 | 1 byte              | **Preview:** 3rd character's portrait                                               |
| 0x0028 | 12 bytes            | **Preview:** Squall's name (0x00 terminated)                                        |
| 0x0034 | 12 bytes            | **Preview:** Rinoa's name (0x00 terminated)                                         |
| 0x0040 | 12 bytes            | **Preview:** Angelo's name (0x00 terminated)                                        |
| 0x004C | 12 bytes            | **Preview:** Boko's name (0x00 terminated)                                          |
| 0x0058 | 4 bytes             | **Preview:** Current Disk (0 based)                                                 |
| 0x005C | 4 bytes             | **Preview:** Current save (last saved game)                                         |
| 0x0060 | 68 bytes            | **Guardian Forces:** Quetzalcoatl                                                   |
| 0x00A4 | 68 bytes            | **Guardian Forces:** Shiva                                                          |
| 0x00E8 | 68 bytes            | **Guardian Forces:** Ifrit                                                          |
| 0x012C | 68 bytes            | **Guardian Forces:** Siren                                                          |
| 0x0170 | 68 bytes            | **Guardian Forces:** Brothers                                                       |
| 0x01B4 | 68 bytes            | **Guardian Forces:** Diablos                                                        |
| 0x01F8 | 68 bytes            | **Guardian Forces:** Carbuncle                                                      |
| 0x023C | 68 bytes            | **Guardian Forces:** Leviathan                                                      |
| 0x0280 | 68 bytes            | **Guardian Forces:** Pandemonia                                                     |
| 0x02C4 | 68 bytes            | **Guardian Forces:** Cerberus                                                       |
| 0x0308 | 68 bytes            | **Guardian Forces:** Alexander                                                      |
| 0x034C | 68 bytes            | **Guardian Forces:** Doomtrain                                                      |
| 0x0390 | 68 bytes            | **Guardian Forces:** Bahamut                                                        |
| 0x03D4 | 68 bytes            | **Guardian Forces:** Cactuar                                                        |
| 0x0418 | 68 bytes            | **Guardian Forces:** Tonberry                                                       |
| 0x045C | 68 bytes            | **Guardian Forces:** Eden                                                           |
| 0x04A0 | 152 bytes           | **Characters:** Squall                                                              |
| 0x0538 | 152 bytes           | **Characters:** Zell                                                                |
| 0x05D0 | 152 bytes           | **Characters:** Irvine                                                              |
| 0x0668 | 152 bytes           | **Characters:** Quistis                                                             |
| 0x0700 | 152 bytes           | **Characters:** Rinoa                                                               |
| 0x0798 | 152 bytes           | **Characters:** Selphie                                                             |
| 0x0830 | 152 bytes           | **Characters:** Seifer                                                              |
| 0x08C8 | 152 bytes           | **Characters:** Edea                                                                |
| 0x0960 | 400 bytes           | Shops                                                                               |
| 0x0AF0 | 20 bytes            | Configuration                                                                       |
| 0x0B04 | 4 bytes             | Party (0xFF terminated)                                                             |
| 0x0B08 | 4 bytes             | Known weapons                                                                       |
| 0x0B0C | 12 bytes            | Griever name (FF8 text format)                                                      |
| 0x0B18 | 2 bytes             | Unknown (always 7966?)                                                              |
| 0x0B1A | 2 bytes             | Unknown                                                                             |
| 0x0B1C | 4 bytes             | Amount of Gil                                                                       |
| 0x0B20 | 4 bytes             | Amount of Gil (Laguna)                                                              |
| 0x0B24 | 2 bytes             | **Limit Break** Quistis                                                             |
| 0x0B26 | 2 bytes             | **Limit Break** Zell                                                                |
| 0x0B28 | 1 byte              | **Limit Break** Irvine                                                              |
| 0x0B29 | 1 byte              | **Limit Break** Selphie                                                             |
| 0x0B2A | 1 byte              | **Limit Break** Angelo completed                                                    |
| 0x0B2B | 1 byte              | **Limit Break** Angelo known                                                        |
| 0x0B2C | 8 bytes             | **Limit Break** Angelo points                                                       |
| 0x0B34 | 32 bytes            | **Items** battle order                                                              |
| 0x0B54 | 396 bytes           | **Items** 198 items (Item ID and Quantity)                                          |
| 0x0CE0 | 4 bytes             | Game time                                                                           |
| 0x0CE4 | 4 bytes             | Countdown                                                                           |
| 0x0CE8 | 4 bytes             | Unknown                                                                             |
| 0x0CEC | 4 bytes             | **Battle:** victory count                                                           |
| 0x0CF0 | 2 bytes             | Unknown                                                                             |
| 0x0CF2 | 2 bytes             | **Battle:** battle escaped                                                          |
| 0x0CF4 | 4 bytes             | Unknown                                                                             |
| 0x0CF8 | 4 bytes             | **Battle:** Tonberry killed count                                                   |
| 0x0CFC | 4 bytes             | **Battle:** Tonberry Sr killed (yeah, this is a boolean)                            |
| 0x0D00 | 4 bytes             | Unknown                                                                             |
| 0x0D04 | 4 bytes             | **Battle:** First "Bug" battle (R1 tip)                                             |
| 0x0D08 | 4 bytes             | **Battle:** First "Bomb" battle (Elemental tip)                                     |
| 0x0D0C | 4 bytes             | **Battle:** First "T-Rex" battle (Mental tip)                                       |
| 0x0D10 | 4 bytes             | **Battle:** First "Irvine" battle (Irvine's limit break tip)                        |
| 0x0D14 | 8 bytes             | **Battle:** Magic drawn once                                                        |
| 0x0D1C | 20 bytes            | **Battle:** Ennemy scanned once                                                     |
| 0x0D30 | 1 byte              | **Battle:** Renzokuken auto                                                         |
| 0x0D31 | 1 byte              | **Battle:** Renzokuken indicator                                                    |
| 0x0D32 | 1 byte              | **Battle:** dream/Odin/Phoenix/Gilgamesh/Angelo disabled/Angel Wing enabled/???/??? |
| 0x0D33 | 16 bytes            | Tutorial infos                                                                      |
| 0x0D43 | 1 byte              | SeeD test level                                                                     |
| 0x0D44 | 4 bytes             | Unknown                                                                             |
| 0x0D48 | 4 bytes             | Party (last byte always = 255)                                                      |
| 0x0D4C | 4 bytes             | Unknown                                                                             |
| 0x0D50 | 2 bytes             | Module (1= field, 2= worldmap, 3= battle)                                           |
| 0x0D52 | 2 bytes             | Current field                                                                       |
| 0x0D54 | 2 bytes             | Previous field                                                                      |
| 0x0D56 | 3\*2 bytes (signed) | Coord X (party1, party2, party3)                                                    |
| 0x0D5C | 3\*2 bytes (signed) | Coord Y (party1, party2, party3)                                                    |
| 0x0D62 | 3\*2 bytes          | Triangle ID (party1, party2, party3)                                                |
| 0x0D68 | 3\*1 bytes          | Direction (party1, party2, party3)                                                  |
| 0x0D6B | 1 byte              | *Padding*                                                                           |
| 0x0D6C | 4 bytes             | Unknown                                                                             |
| 0x0D70 | 256 + 1024 bytes    | [Field vars](Variables.md)                                              |
| 0x1270 | 128 bytes           | Worldmap (TODO)                                                                     |
| 0x12F0 | 128 bytes           | Triple Triad (TODO)                                                                 |
| 0x1370 | 64 bytes            | Chocobo World (TODO)                                                                |

  

### Guardian Forces

The checksum calculation starts here.

There are 16 G-F: Quetzalcoatl, Shiva, Ifrit, Siren, Brothers, Diablos, Carbuncle, Leviathan, Pandemonia, Cerberus, Alexander, Doomtrain, Bahamut, Cactuar, Tonberry, Eden.  
For each G-F:

| Offset | Size     | Data                                                                       |
|--------|----------|----------------------------------------------------------------------------|
| 0x00   | 12 bytes | Name (0x00 terminated)                                                     |
| 0x0C   | 4 bytes  | Experience                                                                 |
| 0x10   | 1 byte   | Unknown                                                                    |
| 0x11   | 1 byte   | Exists                                                                     |
| 0x12   | 2 bytes  | HP                                                                         |
| 0x14   | 16 bytes | Complete abilities (1 bit = 1 ability completed, 9 bits unused)            |
| 0x24   | 24 bytes | APs (1 byte = 1 ability of the GF, 2 bytes unused)                         |
| 0x3C   | 2 bytes  | Number of kills                                                            |
| 0x3E   | 2 bytes  | Number of KOs                                                              |
| 0x41   | 1 byte   | Learning ability                                                           |
| 0x42   | 3 bytes  | Forgotten abilities (1 bit = 1 ability of the GF forgotten, 2 bits unused) |

### Characters

Squall, Zell, Irvine, Quistis, Rinoa, Selphie, Seifer, Edea. For each character:

| Offset | Size          | Data                                         |
|--------|---------------|----------------------------------------------|
| 0x00   | 2 bytes       | Current HPs                                  |
| 0x02   | 2 bytes       | Max HPs                                      |
| 0x04   | 4 bytes       | Experience                                   |
| 0x08   | 1 byte        | Model ID                                     |
| 0x09   | 1 byte        | Weapon ID                                    |
| 0x0A   | 1 byte        | STR                                          |
| 0x0B   | 1 byte        | VIT                                          |
| 0x0C   | 1 byte        | MAG                                          |
| 0x0D   | 1 byte        | SPR                                          |
| 0x0E   | 1 byte        | SPD                                          |
| 0x0F   | 1 byte        | LCK                                          |
| 0x10   | 2\*32 bytes   | Magics                                       |
| 0x50   | 3 bytes       | Commands                                     |
| 0x53   | 1 byte        | *Padding or unused command*                  |
| 0x54   | 4 bytes       | Abilities                                    |
| 0x58   | 2 bytes       | Junctionned GFs                              |
| 0x5A   | 1 byte        | Unknown                                      |
| 0x5B   | 1 byte        | Alternative model (Normal, SeeD, Soldier...) |
| 0x5C   | 1 byte        | Junction HP                                  |
| 0x5D   | 1 byte        | Junction STR                                 |
| 0x5E   | 1 byte        | Junction VIT                                 |
| 0x5F   | 1 byte        | Junction MAG                                 |
| 0x60   | 1 byte        | Junction SPR                                 |
| 0x61   | 1 byte        | Junction SPD                                 |
| 0x62   | 1 byte        | Junction EVA                                 |
| 0x63   | 1 byte        | Junction HIT                                 |
| 0x64   | 1 byte        | Junction LCK                                 |
| 0x65   | 1 byte        | Junction elemental attack                    |
| 0x66   | 1 byte        | Junction mental attack                       |
| 0x67   | 4 bytes       | Junction elemental defense                   |
| 0x6B   | 4 bytes       | Junction mental defense                      |
| 0x6F   | 1 byte        | Unknown (padding?)                           |
| 0x70   | 16 \* 2 bytes | Compatibility with GFs                       |
| 0x90   | 2 bytes       | Number of kills                              |
| 0x92   | 2 bytes       | Number of KOs                                |
| 0x94   | 1 byte        | Exists                                       |
| 0x95   | 1 byte        | Unknown                                      |
| 0x96   | 1 byte        | Mental Status                                |
| 0x97   | 1 byte        | Unknown                                      |

### Worldmap

1.  TODO

### Triple Triad

1.  TODO

### Chocobo World

| Offset | Size               | Data                                                                                                           |
|--------|--------------------|----------------------------------------------------------------------------------------------------------------|
| 0x00   | 1 byte (bit field) | Enabled / In world / MiniMog found / Demon King defeated / Koko kidnapped / Hurry! / Koko met / Event Wait off |
| 0x01   | 1 byte             | Level                                                                                                          |
| 0x02   | 1 byte             | Current HP                                                                                                     |
| 0x03   | 1 byte             | Max HP                                                                                                         |
| 0x04   | 2 bytes            | Weapon (4 bit = 1 weapon)                                                                                      |
| 0x06   | 1 byte             | Rank                                                                                                           |
| 0x07   | 1 byte             | Move                                                                                                           |
| 0x08   | 4 bytes            | Save count                                                                                                     |
| 0x0C   | 2 bytes            | id related                                                                                                     |
| 0x0E   | 6 bytes            | Unknown                                                                                                        |
| 0x14   | 1 byte             | Item Class A count                                                                                             |
| 0x15   | 1 byte             | Item Class B count                                                                                             |
| 0x16   | 1 byte             | Item Class C count                                                                                             |
| 0x17   | 1 byte             | Item Class D count                                                                                             |
| 0x18   | 16 bytes           | Unknown                                                                                                        |
| 0x28   | 4 bytes            | Associated save ID                                                                                             |
| 0x2C   | 1 byte             | Unknown                                                                                                        |
| 0x2D   | 1 byte             | Boko Attack (star count: 0 = ChocoFire, 1 = ChocoFlare, 2 = ChocoMeteor, 3 = ChocoBocle)                       |
| 0x2E   | 1 byte             | Unknown                                                                                                        |
| 0x2F   | 1 byte             | Home walking                                                                                                   |
| 0x30   | 16 bytes           | Unknown (unused?)                                                                                              |
