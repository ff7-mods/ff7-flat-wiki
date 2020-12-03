---
title: Field ID
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > Field ID

## Purpose

Field IDs are used internally by scripts to reference fields, for
example with the [MAPJUMP][] and [LSTMP][] opcodes.

## Field Table

| ID     | Field Name | Description                                                                                           |
|--------|------------|-------------------------------------------------------------------------------------------------------|
| 0x000  | dummy      | World Map - Dummy Room (not used)                                                                     |
| 0x001  | wm0        | World Map - Outside Midgar                                                                            |
| 0x002  | wm1        | World Map - Outside Kalm                                                                              |
| 0x003  | wm2        | World Map - Outside Chocobo Farm                                                                      |
| 0x004  | wm3        | World Map - Outside Mithryl Mine (Midgar side)                                                        |
| 0x005  | wm4        | World Map - Outside Mithryl Mine (Junon side)                                                         |
| 0x006  | wm5        | World Map - Outside Condor                                                                            |
| 0x007  | wm6        | World Map - Outside Junon                                                                             |
| 0x008  | wm7        | World Map - Outside Temple of the Ancients                                                            |
| 0x009  | wm8        | World Map - Outside Old Man's House (receive Mythril)                                                 |
| 0x00A  | wm9        | World Map - Outside Weapon Seller                                                                     |
| 0x00B  | wm10       | World Map - Outside Mideel                                                                            |
| 0x00C  | wm11       | World Map - Outside Materia Cave (Quadra Magic)                                                       |
| 0x00D  | wm12       | World Map - Outside Costa Del Sol                                                                     |
| 0x00E  | wm13       | World Map - Outside Mt. Coral                                                                         |
| 0x00F  | wm14       | World Map - Outside North Coral                                                                       |
| 0x010  | wm15       | World Map - Outside Corel Prison/Desert (In desert, can't move without buggy)                         |
| 0x011  | wm16       | World Map - Outside Gongaga                                                                           |
| 0x012  | wm17       | World Map - Outside Cosmo Canyon                                                                      |
| 0x013  | wm18       | World Map - Outside Nibelheim (Town Side)                                                             |
| 0x014  | wm19       | World Map - Outside Rocket Town (South Side)                                                          |
| 0x015  | wm20       | World Map - Outside Lucrecia's Cave                                                                   |
| 0x016  | wm21       | World Map - Outside Materia Cave (HP&lt;-&gt;MP Materia)                                              |
| 0x017  | wm22       | World Map - Outside Wutai                                                                             |
| 0x018  | wm23       | World Map - Outside Materia Cave (Mime Materia)                                                       |
| 0x019  | wm24       | World Map - Outside Bone Village                                                                      |
| 0x01A  | wm25       | World Map - Outside Corel Valley Cave (Icicle Area)                                                   |
| 0x01B  | wm26       | World Map - Outside Icicle Inn (South Side)                                                           |
| 0x01C  | wm27       | World Map - Outside Chocobo Sage's House                                                              |
| 0x01D  | wm28       | World Map - Outside Materia Cave (Knights of the Round Materia)                                       |
| 0x01E  | wm29       | World Map - Outside Underwater Reactor                                                                |
| 0x01F  | wm30       | World Map - Outside Gelnika                                                                           |
| 0x020  | wm31       | World Map - Midgar Zolom in Tree, between Marsh and Mythril mine (Relative to last world coordinates) |
| 0x021  | wm32       | World Map - Mystery Ninja Encounter (Relative to last world coordinates)                              |
| 0x022  | wm33       | World Map - Yuffie's Betrayal, South of Western Continent (Relative to last world coordinates)        |
| 0x023  | wm34       | World Map - Yuffie's Betrayal, South of Western Continent (Relative to last world coordinates)        |
| 0x024  | wm35       | World Map Event - Ship pulls out of Junon                                                             |
| 0x025  | wm36       | World Map Event - Ship pulls into Costa Del Sol                                                       |
| 0x026  | wm37       | World Map Event - Ship goes from Junon to Costa Del Sol                                               |
| 0x027  | wm38       | World Map Event - Ship goes from Costa Del Sol to Junon                                               |
| 0x028  | wm39       | World Map - Tiny Bronco Starting point (when obtained)                                                |
| 0x029  | wm40       | World Map - Highwind starting point (when obtained)                                                   |
| 0x02A  | wm41       | World Map - Underwater - North Area (unknown)                                                         |
| 0x02B  | wm42       | World Map - Outside Nibelheim (Mt. Nibel Side)                                                        |
| 0x02C  | wm43       | World Map - Outside Mt. Nibel (Nibelheim Side)                                                        |
| 0x02D  | wm44       | World Map - Leaving Highwind (Relative to last coordinates)                                           |
| 0x02E  | wm45       | World Map - Outside Mt. Nibel (West Side)                                                             |
| 0x02F  | wm46       | World Map - Outside Icicle Inn (North Side)                                                           |
| 0x030  | wm47       | World Map - Outside Great Glacier                                                                     |
| 0x031  | wm48       | World Map - Outside Rocket Town (North Side)                                                          |
| 0x032  | wm49       | World Map - Entering Highwind (Relative to last world coordinates)                                    |
| 0x033  | wm50       | World Map - Entering Highwind (Relative to last world coordinates)                                    |
| 0x034  | wm51       | World Map - Entering Highwind (Relative to last world coordinates)                                    |
| 0x035  | wm52       | World Map - Diamond Weapon Battle Location (Relative to last world coordinates)                       |
| 0x036  | wm53       | World Map - Submarine Starting point (when obtained)                                                  |
| 0x037  | wm54       | World Map - Outside Ancient Forset                                                                    |
| 0x038  | wm55       | World Map - Outside Underwater Key of the Ancients                                                    |
| 0x039  | wm56       | World Map - Outside Sleeping Forest                                                                   |
| 0x03A  | wm57       | World Map - Valley, City of Ancients entrance                                                         |
| 0x03B  | wm58       | World Map - Northern Crater (Relative to last known coordinates)                                      |
| 0x03C  | wm59       | World Map - Snow Maze                                                                                 |
| 0x03D  | wm60       | World Map - Snow Maze                                                                                 |
| 0x03E  | wm61       | World Map - Snow Maze                                                                                 |
| 0x03F  | wm62       | World Map - Snow Maze                                                                                 |
| 0x040  | wm63       | World Map - Snow Maze - Outside Materia Cave (All)                                                    |
| 0x0041 | startmap   |                                                                                                       |
| 0x0042 | fship\_1   |                                                                                                       |
| 0x0043 | fship\_12  |                                                                                                       |
| 0x0044 | fship\_2   |                                                                                                       |
| 0x0045 | fship\_22  |                                                                                                       |
| 0x0046 | fship\_23  |                                                                                                       |
| 0x0047 | fship\_24  |                                                                                                       |
| 0x0048 | fship\_25  |                                                                                                       |
| 0x0049 | fship\_3   |                                                                                                       |
| 0x004A | fship\_4   |                                                                                                       |
| 0x004B | fship\_42  |                                                                                                       |
| 0x004C | fship\_5   |                                                                                                       |
| 0x004D | hill       |                                                                                                       |
| 0x004E | zz1        |                                                                                                       |
| 0x004F | zz2        |                                                                                                       |
| 0x0050 | zz3        |                                                                                                       |
| 0x0051 | zz4        |                                                                                                       |
| 0x0052 | zz5        |                                                                                                       |
| 0x0053 | zz6        |                                                                                                       |
| 0x0054 | zz7        |                                                                                                       |
| 0x0055 | zz8        |                                                                                                       |
| 0x0056 | sea        |                                                                                                       |
| 0x0057 | sky        |                                                                                                       |
| 0x0058 | qa         |                                                                                                       |
| 0x0059 | qb         |                                                                                                       |
| 0x005A | qc         |                                                                                                       |
| 0x005B | qd         |                                                                                                       |
| 0x005C | qe         |                                                                                                       |
| 0x005D | blackbg1   |                                                                                                       |
| 0x005E | blackbg2   |                                                                                                       |
| 0x005F | blackbg3   |                                                                                                       |
| 0x0060 | blackbg4   |                                                                                                       |
| 0x0061 | blackbg5   |                                                                                                       |
| 0x0062 | blackbg6   |                                                                                                       |
| 0x0063 | blackbg7   |                                                                                                       |
| 0x0064 | blackbg8   |                                                                                                       |
| 0x0065 | blackbg9   |                                                                                                       |
| 0x0066 | blackbga   |                                                                                                       |
| 0x0067 | blackbgb   |                                                                                                       |
| 0x0068 | blackbgc   |                                                                                                       |
| 0x0069 | blackbgd   |                                                                                                       |
| 0x006A | blackbge   |                                                                                                       |
| 0x006B | blackbgf   |                                                                                                       |
| 0x006C | blackbgg   |                                                                                                       |
| 0x006D | blackbgh   |                                                                                                       |
| 0x006E | blackbgi   |                                                                                                       |
| 0x006F | blackbgj   |                                                                                                       |
| 0x0070 | blackbgk   |                                                                                                       |
| 0x0071 | whitebg1   |                                                                                                       |
| 0x0072 | whitebg2   |                                                                                                       |
| 0x0073 | whitebg3   |                                                                                                       |
| 0x0074 | md1stin    |                                                                                                       |
| 0x0075 | md1\_1     |                                                                                                       |
| 0x0076 | md1\_2     |                                                                                                       |
| 0x0077 | nrthmk     |                                                                                                       |
| 0x0078 | nmkin\_1   |                                                                                                       |
| 0x0079 | elevtr1    |                                                                                                       |
| 0x007A | nmkin\_2   |                                                                                                       |
| 0x007B | nmkin\_3   |                                                                                                       |
| 0x007C | nmkin\_4   |                                                                                                       |
| 0x007D | nmkin\_5   |                                                                                                       |
| 0x007E | southmk1   |                                                                                                       |
| 0x007F | southmk2   |                                                                                                       |
| 0x0080 | smkin\_1   |                                                                                                       |
| 0x0081 | smkin\_2   |                                                                                                       |
| 0x0082 | smkin\_3   |                                                                                                       |
| 0x0083 | smkin\_4   |                                                                                                       |
| 0x0084 | smkin\_5   |                                                                                                       |
| 0x0085 | md8\_1     |                                                                                                       |
| 0x0086 | md8\_2     |                                                                                                       |
| 0x0087 | md8\_3     |                                                                                                       |
| 0x0088 | md8\_4     |                                                                                                       |
| 0x0089 | md8brdg    |                                                                                                       |
| 0x008A | cargoin    |                                                                                                       |
| 0x008B | tin\_1     |                                                                                                       |
| 0x008C | tin\_2     |                                                                                                       |
| 0x008D | tin\_3     |                                                                                                       |
| 0x008E | tin\_4     |                                                                                                       |
| 0x008F | rootmap    |                                                                                                       |
| 0x0090 | mds7st1    |                                                                                                       |
| 0x0091 | mds7st2    |                                                                                                       |
| 0x0092 | mds7st3    |                                                                                                       |
| 0x0093 | mds7st32   |                                                                                                       |
| 0x0094 | mds7\_w1   |                                                                                                       |
| 0x0095 | mds7\_w2   |                                                                                                       |
| 0x0096 | mds7\_w3   |                                                                                                       |
| 0x0097 | mds7       |                                                                                                       |
| 0x0098 | mds7\_im   |                                                                                                       |
| 0x0099 | min71      |                                                                                                       |
| 0x009A | mds7pb\_1  |                                                                                                       |
| 0x009B | mds7pb\_2  |                                                                                                       |
| 0x009C | mds7plr1   |                                                                                                       |
| 0x009D | mds7plr2   |                                                                                                       |
| 0x009E | pillar\_1  |                                                                                                       |
| 0x009F | pillar\_2  |                                                                                                       |
| 0x00A0 | pillar\_3  |                                                                                                       |
| 0x00A1 | tunnel\_1  |                                                                                                       |
| 0x00A2 | tunnel\_2  |                                                                                                       |
| 0x00A3 | tunnel\_3  |                                                                                                       |
| 0x00A4 | sbwy4\_1   |                                                                                                       |
| 0x00A5 | sbwy4\_2   |                                                                                                       |
| 0x00A6 | sbwy4\_3   |                                                                                                       |
| 0x00A7 | sbwy4\_4   |                                                                                                       |
| 0x00A8 | sbwy4\_5   |                                                                                                       |
| 0x00A9 | sbwy4\_6   |                                                                                                       |
| 0x00AA | mds5\_5    |                                                                                                       |
| 0x00AB | mds5\_4    |                                                                                                       |
| 0x00AC | mds5\_3    |                                                                                                       |
| 0x00AD | mds5\_2    |                                                                                                       |
| 0x00AE | min51\_1   |                                                                                                       |
| 0x00AF | min51\_2   |                                                                                                       |
| 0x00B0 | mds5\_dk   |                                                                                                       |
| 0x00B1 | mds5\_1    |                                                                                                       |
| 0x00B2 | mds5\_w    |                                                                                                       |
| 0x00B3 | mds5\_i    |                                                                                                       |
| 0x00B4 | mds5\_m    |                                                                                                       |
| 0x00B5 | church     |                                                                                                       |
| 0x00B6 | chrin\_1a  |                                                                                                       |
| 0x00B7 | chrin\_1b  |                                                                                                       |
| 0x00B8 | chrin\_2   |                                                                                                       |
| 0x00B9 | chrin\_3a  |                                                                                                       |
| 0x00BA | chrin\_3b  |                                                                                                       |
| 0x00BB | eals\_1    |                                                                                                       |
| 0x00BC | ealin\_1   |                                                                                                       |
| 0x00BD | ealin\_12  |                                                                                                       |
| 0x00BE | ealin\_2   |                                                                                                       |
| 0x00BF | mds6\_1    |                                                                                                       |
| 0x00C0 | mds6\_2    |                                                                                                       |
| 0x00C1 | mds6\_22   |                                                                                                       |
| 0x00C2 | mds6\_3    |                                                                                                       |
| 0x00C3 | mrkt2      |                                                                                                       |
| 0x00C4 | mkt\_w     |                                                                                                       |
| 0x00C5 | mkt\_mens  |                                                                                                       |
| 0x00C6 | mkt\_ia    |                                                                                                       |
| 0x00C7 | mktinn     |                                                                                                       |
| 0x00C8 | mkt\_m     |                                                                                                       |
| 0x00C9 | mkt\_s1    |                                                                                                       |
| 0x00CA | mkt\_s2    |                                                                                                       |
| 0x00CB | mkt\_s3    |                                                                                                       |
| 0x00CC | mktpb      |                                                                                                       |
| 0x00CD | mrkt1      |                                                                                                       |
| 0x00CE | colne\_1   |                                                                                                       |
| 0x00CF | colne\_2   |                                                                                                       |
| 0x00D0 | colne\_3   |                                                                                                       |
| 0x00D1 | colne\_4   |                                                                                                       |
| 0x00D2 | colne\_5   |                                                                                                       |
| 0x00D3 | colne\_6   |                                                                                                       |
| 0x00D4 | colne\_b1  |                                                                                                       |
| 0x00D5 | colne\_b3  |                                                                                                       |
| 0x00D6 | mrkt3      |                                                                                                       |
| 0x00D7 | onna\_1    |                                                                                                       |
| 0x00D8 | onna\_2    |                                                                                                       |
| 0x00D9 | onna\_3    |                                                                                                       |
| 0x00DA | onna\_4    |                                                                                                       |
| 0x00DB | onna\_5    |                                                                                                       |
| 0x00DC | onna\_52   |                                                                                                       |
| 0x00DD | onna\_6    |                                                                                                       |
| 0x00DE | mrkt4      |                                                                                                       |
| 0x00DF | wcrimb\_1  |                                                                                                       |
| 0x00E0 | wcrimb\_2  |                                                                                                       |
| 0x00E1 | md0        |                                                                                                       |
| 0x00E2 | roadend    |                                                                                                       |
| 0x00E3 | sinbil\_1  |                                                                                                       |
| 0x00E4 | sinbil\_2  |                                                                                                       |
| 0x00E5 | blinst\_1  |                                                                                                       |
| 0x00E6 | blinst\_2  |                                                                                                       |
| 0x00E7 | blinst\_3  |                                                                                                       |
| 0x00E8 | blinele    |                                                                                                       |
| 0x00E9 | eleout     |                                                                                                       |
| 0x00EA | blin1      |                                                                                                       |
| 0x00EB | blin2      |                                                                                                       |
| 0x00EC | blin2\_i   |                                                                                                       |
| 0x00ED | blin3\_1   |                                                                                                       |
| 0x00EE | blin59     |                                                                                                       |
| 0x00EF | blin60\_1  |                                                                                                       |
| 0x00F0 | blin60\_2  |                                                                                                       |
| 0x00F1 | blin61     |                                                                                                       |
| 0x00F2 | blin62\_1  |                                                                                                       |
| 0x00F3 | blin62\_2  |                                                                                                       |
| 0x00F4 | blin62\_3  |                                                                                                       |
| 0x00F5 | blin63\_1  |                                                                                                       |
| 0x00F6 | blin63\_t  |                                                                                                       |
| 0x00F7 | blin64     |                                                                                                       |
| 0x00F8 | blin65\_1  |                                                                                                       |
| 0x00F9 | blin65\_2  |                                                                                                       |
| 0x00FA | blin66\_1  |                                                                                                       |
| 0x00FB | blin66\_2  |                                                                                                       |
| 0x00FC | blin66\_3  |                                                                                                       |
| 0x00FD | blin66\_4  |                                                                                                       |
| 0x00FE | blin66\_5  |                                                                                                       |
| 0x00FF | blin66\_6  |                                                                                                       |
| 0x0100 | blin67\_1  |                                                                                                       |
| 0x0101 | blin671b   |                                                                                                       |
| 0x0102 | blin67\_2  |                                                                                                       |
| 0x0103 | blin67\_3  |                                                                                                       |
| 0x0104 | blin673b   |                                                                                                       |
| 0x0105 | blin67\_4  |                                                                                                       |
| 0x0106 | blin68\_1  |                                                                                                       |
| 0x0107 | blin68\_2  |                                                                                                       |
| 0x0108 | blin69\_1  |                                                                                                       |
| 0x0109 | blin69\_2  |                                                                                                       |
| 0x010A | blin70\_1  |                                                                                                       |
| 0x010B | blin70\_2  |                                                                                                       |
| 0x010C | blin70\_3  |                                                                                                       |
| 0x010D | blin70\_4  |                                                                                                       |
| 0x010E | niv\_w     |                                                                                                       |
| 0x010F | nvmin1\_1  |                                                                                                       |
| 0x0110 | nvmin1\_2  |                                                                                                       |
| 0x0111 | nivinn\_1  |                                                                                                       |
| 0x0112 | nivinn\_2  |                                                                                                       |
| 0x0113 | nivinn\_3  |                                                                                                       |
| 0x0114 | niv\_cl    |                                                                                                       |
| 0x0115 | trackin    |                                                                                                       |
| 0x0116 | trackin2   |                                                                                                       |
| 0x0117 | nivgate    |                                                                                                       |
| 0x0118 | nivgate2   |                                                                                                       |
| 0x0119 | nivgate3   |                                                                                                       |
| 0x011A | nivl       |                                                                                                       |
| 0x011B | nivl\_2    |                                                                                                       |
| 0x011C | nivl\_3    |                                                                                                       |
| 0x011D | nivl\_4    |                                                                                                       |
| 0x011E | niv\_ti1   |                                                                                                       |
| 0x011F | niv\_ti2   |                                                                                                       |
| 0x0120 | niv\_ti3   |                                                                                                       |
| 0x0121 | niv\_ti4   |                                                                                                       |
| 0x0122 | nivl\_b1   |                                                                                                       |
| 0x0123 | nivl\_b12  |                                                                                                       |
| 0x0124 | nivl\_b2   |                                                                                                       |
| 0x0125 | nivl\_b22  |                                                                                                       |
| 0x0126 | nivl\_e1   |                                                                                                       |
| 0x0127 | nivl\_e2   |                                                                                                       |
| 0x0128 | nivl\_e3   |                                                                                                       |
| 0x0129 | sinin1\_1  |                                                                                                       |
| 0x012A | sinin1\_2  |                                                                                                       |
| 0x012B | sinin2\_1  |                                                                                                       |
| 0x012C | sinin2\_2  |                                                                                                       |
| 0x012D | sinin3     |                                                                                                       |
| 0x012E | sininb1    |                                                                                                       |
| 0x012F | sininb2    |                                                                                                       |
| 0x0130 | sininb31   |                                                                                                       |
| 0x0131 | sininb32   |                                                                                                       |
| 0x0132 | sininb33   |                                                                                                       |
| 0x0133 | sininb41   |                                                                                                       |
| 0x0134 | sininb42   |                                                                                                       |
| 0x0135 | sininb51   |                                                                                                       |
| 0x0136 | sininb52   |                                                                                                       |
| 0x0137 | mtnvl2     |                                                                                                       |
| 0x0138 | mtnvl3     |                                                                                                       |
| 0x0139 | mtnvl4     |                                                                                                       |
| 0x013A | mtnvl5     |                                                                                                       |
| 0x013B | mtnvl6     |                                                                                                       |
| 0x013C | mtnvl6b    |                                                                                                       |
| 0x013D | nvdun1     |                                                                                                       |
| 0x013E | nvdun2     |                                                                                                       |
| 0x013F | nvdun3     |                                                                                                       |
| 0x0140 | nvdun31    |                                                                                                       |
| 0x0141 | nvdun4     |                                                                                                       |
| 0x0142 | nvmkin1    |                                                                                                       |
| 0x0143 | nvmkin21   |                                                                                                       |
| 0x0144 | nvmkin22   |                                                                                                       |
| 0x0145 | nvmkin23   |                                                                                                       |
| 0x0146 | nvmkin31   |                                                                                                       |
| 0x0147 | nvmkin32   |                                                                                                       |
| 0x0148 | elm\_wa    |                                                                                                       |
| 0x0149 | elm\_i     |                                                                                                       |
| 0x014A | elmpb      |                                                                                                       |
| 0x014B | elminn\_1  |                                                                                                       |
| 0x014C | elminn\_2  |                                                                                                       |
| 0x014D | elmin1\_1  |                                                                                                       |
| 0x014E | elmin1\_2  |                                                                                                       |
| 0x014F | elm        |                                                                                                       |
| 0x0150 | elmin2\_1  |                                                                                                       |
| 0x0151 | elmin2\_2  |                                                                                                       |
| 0x0152 | elmin3\_1  |                                                                                                       |
| 0x0153 | elmin3\_2  |                                                                                                       |
| 0x0154 | elmtow     |                                                                                                       |
| 0x0155 | elmin4\_1  |                                                                                                       |
| 0x0156 | elmin4\_2  |                                                                                                       |
| 0x0157 | farm       |                                                                                                       |
| 0x0158 | frmin      |                                                                                                       |
| 0x0159 | frcyo      |                                                                                                       |
| 0x015A | trap       |                                                                                                       |
| 0x015B | fr\_e      |                                                                                                       |
| 0x015C | sichi      |                                                                                                       |
| 0x015D | psdun\_1   |                                                                                                       |
| 0x015E | psdun\_2   |                                                                                                       |
| 0x015F | psdun\_3   |                                                                                                       |
| 0x0160 | psdun\_4   |                                                                                                       |
| 0x0161 | condor1    |                                                                                                       |
| 0x0162 | condor2    |                                                                                                       |
| 0x0163 | convil\_1  |                                                                                                       |
| 0x0164 | convil\_2  |                                                                                                       |
| 0x0165 | convil\_3  |                                                                                                       |
| 0x0166 | convil\_4  |                                                                                                       |
| 0x0167 | junon      |                                                                                                       |
| 0x0168 | junonr1    |                                                                                                       |
| 0x0169 | junonr2    |                                                                                                       |
| 0x016A | junonr3    |                                                                                                       |
| 0x016B | junonr4    |                                                                                                       |
| 0x016C | jun\_wa    |                                                                                                       |
| 0x016D | jun\_i1    |                                                                                                       |
| 0x016E | jun\_m     |                                                                                                       |
| 0x016F | junmin1    |                                                                                                       |
| 0x0170 | junmin2    |                                                                                                       |
| 0x0171 | junmin3    |                                                                                                       |
| 0x0172 | junonl1    |                                                                                                       |
| 0x0173 | junonl2    |                                                                                                       |
| 0x0174 | junonl3    |                                                                                                       |
| 0x0175 | jun\_w     |                                                                                                       |
| 0x0176 | jun\_a     |                                                                                                       |
| 0x0177 | jun\_i2    |                                                                                                       |
| 0x0178 | juninn     |                                                                                                       |
| 0x0179 | junpb\_1   |                                                                                                       |
| 0x017A | junpb\_2   |                                                                                                       |
| 0x017B | junpb\_3   |                                                                                                       |
| 0x017C | junmin4    |                                                                                                       |
| 0x017D | junmin5    |                                                                                                       |
| 0x017E | jundoc1a   |                                                                                                       |
| 0x017F | jundoc1b   |                                                                                                       |
| 0x0180 | junair     |                                                                                                       |
| 0x0181 | junair2    |                                                                                                       |
| 0x0182 | junin1     |                                                                                                       |
| 0x0183 | junin1a    |                                                                                                       |
| 0x0184 | junele1    |                                                                                                       |
| 0x0185 | junin2     |                                                                                                       |
| 0x0186 | junin3     |                                                                                                       |
| 0x0187 | junele2    |                                                                                                       |
| 0x0188 | junin4     |                                                                                                       |
| 0x0189 | junin5     |                                                                                                       |
| 0x018A | junin6     |                                                                                                       |
| 0x018B | junin7     |                                                                                                       |
| 0x018C | junbin1    |                                                                                                       |
| 0x018D | junbin12   |                                                                                                       |
| 0x018E | junbin21   |                                                                                                       |
| 0x018F | junbin22   |                                                                                                       |
| 0x0190 | junbin3    |                                                                                                       |
| 0x0191 | junbin4    |                                                                                                       |
| 0x0192 | junbin5    |                                                                                                       |
| 0x0193 | junmon     |                                                                                                       |
| 0x0194 | junsbd1    |                                                                                                       |
| 0x0195 | subin\_1a  |                                                                                                       |
| 0x0196 | subin\_1b  |                                                                                                       |
| 0x0197 | subin\_2a  |                                                                                                       |
| 0x0198 | subin\_2b  |                                                                                                       |
| 0x0199 | subin\_3   |                                                                                                       |
| 0x019A | subin\_4   |                                                                                                       |
| 0x019B | junone2    |                                                                                                       |
| 0x019C | junone3    |                                                                                                       |
| 0x019D | junone4    |                                                                                                       |
| 0x019E | junone5    |                                                                                                       |
| 0x019F | junone6    |                                                                                                       |
| 0x01A0 | junone7    |                                                                                                       |
| 0x01A1 | spgate     |                                                                                                       |
| 0x01A2 | spipe\_1   |                                                                                                       |
| 0x01A3 | spipe\_2   |                                                                                                       |
| 0x01A4 | semkin\_1  |                                                                                                       |
| 0x01A5 | semkin\_2  |                                                                                                       |
| 0x01A6 | semkin\_8  |                                                                                                       |
| 0x01A7 | semkin\_3  |                                                                                                       |
| 0x01A8 | semkin\_4  |                                                                                                       |
| 0x01A9 | semkin\_5  |                                                                                                       |
| 0x01AA | semkin\_6  |                                                                                                       |
| 0x01AB | semkin\_7  |                                                                                                       |
| 0x01AC | ujunon1    |                                                                                                       |
| 0x01AD | ujunon2    |                                                                                                       |
| 0x01AE | ujunon3    |                                                                                                       |
| 0x01AF | prisila    |                                                                                                       |
| 0x01B0 | ujun\_w    |                                                                                                       |
| 0x01B1 | jumin      |                                                                                                       |
| 0x01B2 | ujunon4    |                                                                                                       |
| 0x01B3 | ujunon5    |                                                                                                       |
| 0x01B4 | ship\_1    |                                                                                                       |
| 0x01B5 | ship\_2    |                                                                                                       |
| 0x01B6 | shpin\_22  |                                                                                                       |
| 0x01B7 | shpin\_2   |                                                                                                       |
| 0x01B8 | shpin\_3   |                                                                                                       |
| 0x01B9 | del1       |                                                                                                       |
| 0x01BA | del12      |                                                                                                       |
| 0x01BB | del2       |                                                                                                       |
| 0x01BC | delinn     |                                                                                                       |
| 0x01BD | delpb      |                                                                                                       |
| 0x01BE | delmin1    |                                                                                                       |
| 0x01BF | delmin12   |                                                                                                       |
| 0x01C0 | delmin2    |                                                                                                       |
| 0x01C1 | del3       |                                                                                                       |
| 0x01C2 | ncorel     |                                                                                                       |
| 0x01C3 | ncorel2    |                                                                                                       |
| 0x01C4 | ncorel3    |                                                                                                       |
| 0x01C5 | ncoin1     |                                                                                                       |
| 0x01C6 | ncoin2     |                                                                                                       |
| 0x01C7 | ncoin3     |                                                                                                       |
| 0x01C8 | ncoinn     |                                                                                                       |
| 0x01C9 | ropest     |                                                                                                       |
| 0x01CA | mtcrl\_0   |                                                                                                       |
| 0x01CB | mtcrl\_1   |                                                                                                       |
| 0x01CC | mtcrl\_2   |                                                                                                       |
| 0x01CD | mtcrl\_3   |                                                                                                       |
| 0x01CE | mtcrl\_4   |                                                                                                       |
| 0x01CF | mtcrl\_5   |                                                                                                       |
| 0x01D0 | mtcrl\_6   |                                                                                                       |
| 0x01D1 | mtcrl\_7   |                                                                                                       |
| 0x01D2 | mtcrl\_8   |                                                                                                       |
| 0x01D3 | mtcrl\_9   |                                                                                                       |
| 0x01D4 | corel1     |                                                                                                       |
| 0x01D5 | corel2     |                                                                                                       |
| 0x01D6 | corel3     |                                                                                                       |
| 0x01D7 | jail1      |                                                                                                       |
| 0x01D8 | jailin1    |                                                                                                       |
| 0x01D9 | jail2      |                                                                                                       |
| 0x01DA | jailpb     |                                                                                                       |
| 0x01DB | jailin2    |                                                                                                       |
| 0x01DC | jailin3    |                                                                                                       |
| 0x01DD | jailin4    |                                                                                                       |
| 0x01DE | jail3      |                                                                                                       |
| 0x01DF | jail4      |                                                                                                       |
| 0x01E0 | dyne       |                                                                                                       |
| 0x01E1 | desert1    |                                                                                                       |
| 0x01E2 | desert2    |                                                                                                       |
| 0x01E3 | corelin    |                                                                                                       |
| 0x01E4 | astage\_a  |                                                                                                       |
| 0x01E5 | astage\_b  |                                                                                                       |
| 0x01E6 | jet        |                                                                                                       |
| 0x01E7 | jetin1     |                                                                                                       |
| 0x01E8 | bigwheel   |                                                                                                       |
| 0x01E9 | bwhlin     |                                                                                                       |
| 0x01EA | bwhlin2    |                                                                                                       |
| 0x01EB | ghotel     |                                                                                                       |
| 0x01EC | ghotin\_1  |                                                                                                       |
| 0x01ED | ghotin\_4  |                                                                                                       |
| 0x01EE | ghotin\_2  |                                                                                                       |
| 0x01EF | ghotin\_3  |                                                                                                       |
| 0x01F0 | gldst      |                                                                                                       |
| 0x01F1 | gldgate    |                                                                                                       |
| 0x01F2 | gldinfo    |                                                                                                       |
| 0x01F3 | coloss     |                                                                                                       |
| 0x01F4 | coloin1    |                                                                                                       |
| 0x01F5 | coloin2    |                                                                                                       |
| 0x01F6 | clsin2\_1  |                                                                                                       |
| 0x01F7 | clsin2\_2  |                                                                                                       |
| 0x01F8 | clsin2\_3  |                                                                                                       |
| 0x01F9 | games      |                                                                                                       |
| 0x01FA | games\_1   |                                                                                                       |
| 0x01FB | games\_2   |                                                                                                       |
| 0x01FC | mogu\_1    |                                                                                                       |
| 0x01FD | chorace    |                                                                                                       |
| 0x01FE | chorace2   |                                                                                                       |
| 0x01FF | crcin\_1   |                                                                                                       |
| 0x0200 | crcin\_2   |                                                                                                       |
| 0x0201 | gldelev    |                                                                                                       |
| 0x0202 | gonjun1    |                                                                                                       |
| 0x0203 | gonjun2    |                                                                                                       |
| 0x0204 | gnmkf      |                                                                                                       |
| 0x0205 | gnmk       |                                                                                                       |
| 0x0206 | gongaga    |                                                                                                       |
| 0x0207 | gon\_wa1   |                                                                                                       |
| 0x0208 | gon\_wa2   |                                                                                                       |
| 0x0209 | gon\_i     |                                                                                                       |
| 0x020A | gninn      |                                                                                                       |
| 0x020B | gomin      |                                                                                                       |
| 0x020C | goson      |                                                                                                       |
| 0x020D | cos\_btm   |                                                                                                       |
| 0x020E | cos\_btm2  |                                                                                                       |
| 0x020F | cosmo      |                                                                                                       |
| 0x0210 | cosmo2     |                                                                                                       |
| 0x0211 | cosin1     |                                                                                                       |
| 0x0212 | cosin1\_1  |                                                                                                       |
| 0x0213 | cosin2     |                                                                                                       |
| 0x0214 | cosin3     |                                                                                                       |
| 0x0215 | cosin4     |                                                                                                       |
| 0x0216 | cosin5     |                                                                                                       |
| 0x0217 | cosmin2    |                                                                                                       |
| 0x0218 | cosmin3    |                                                                                                       |
| 0x0219 | cosmin4    |                                                                                                       |
| 0x021A | cosmin6    |                                                                                                       |
| 0x021B | cosmin7    |                                                                                                       |
| 0x021C | cos\_top   |                                                                                                       |
| 0x021D | bugin1a    |                                                                                                       |
| 0x021E | bugin1b    |                                                                                                       |
| 0x021F | bugin1c    |                                                                                                       |
| 0x0220 | bugin2     |                                                                                                       |
| 0x0221 | bugin3     |                                                                                                       |
| 0x0222 | gidun\_1   |                                                                                                       |
| 0x0223 | gidun\_2   |                                                                                                       |
| 0x0224 | gidun\_4   |                                                                                                       |
| 0x0225 | gidun\_3   |                                                                                                       |
| 0x0226 | seto1      |                                                                                                       |
| 0x0227 | rckt2      |                                                                                                       |
| 0x0228 | rckt3      |                                                                                                       |
| 0x0229 | rkt\_w     |                                                                                                       |
| 0x022A | rkt\_i     |                                                                                                       |
| 0x022B | rktinn1    |                                                                                                       |
| 0x022C | rktinn2    |                                                                                                       |
| 0x022D | rckt       |                                                                                                       |
| 0x022E | rktsid     |                                                                                                       |
| 0x022F | rktmin1    |                                                                                                       |
| 0x0230 | rktmin2    |                                                                                                       |
| 0x0231 | rcktbas1   |                                                                                                       |
| 0x0232 | rcktbas2   |                                                                                                       |
| 0x0233 | rcktin1    |                                                                                                       |
| 0x0234 | rcktin2    |                                                                                                       |
| 0x0235 | rcktin3    |                                                                                                       |
| 0x0236 | rcktin4    |                                                                                                       |
| 0x0237 | rcktin5    |                                                                                                       |
| 0x0238 | rcktin6    |                                                                                                       |
| 0x0239 | rcktin7    |                                                                                                       |
| 0x023A | rcktin8    |                                                                                                       |
| 0x023B | pass       |                                                                                                       |
| 0x023C | yougan     |                                                                                                       |
| 0x023D | yougan2    |                                                                                                       |
| 0x023E | yougan3    |                                                                                                       |
| 0x023F | uta\_wa    |                                                                                                       |
| 0x0240 | uta\_im    |                                                                                                       |
| 0x0241 | utmin1     |                                                                                                       |
| 0x0242 | utmin2     |                                                                                                       |
| 0x0243 | uutai1     |                                                                                                       |
| 0x0244 | utapb      |                                                                                                       |
| 0x0245 | yufy1      |                                                                                                       |
| 0x0246 | yufy2      |                                                                                                       |
| 0x0247 | hideway1   |                                                                                                       |
| 0x0248 | hideway2   |                                                                                                       |
| 0x0249 | hideway3   |                                                                                                       |
| 0x024A | tower5     |                                                                                                       |
| 0x024B | uutai2     |                                                                                                       |
| 0x024C | uttmpin1   |                                                                                                       |
| 0x024D | uttmpin2   |                                                                                                       |
| 0x024E | uttmpin3   |                                                                                                       |
| 0x024F | uttmpin4   |                                                                                                       |
| 0x0250 | datiao\_1  |                                                                                                       |
| 0x0251 | datiao\_2  |                                                                                                       |
| 0x0252 | datiao\_3  |                                                                                                       |
| 0x0253 | datiao\_4  |                                                                                                       |
| 0x0254 | datiao\_5  |                                                                                                       |
| 0x0255 | datiao\_6  |                                                                                                       |
| 0x0256 | datiao\_7  |                                                                                                       |
| 0x0257 | datiao\_8  |                                                                                                       |
| 0x0258 | jtempl     |                                                                                                       |
| 0x0259 | jtemplb    |                                                                                                       |
| 0x025A | jtmpin1    |                                                                                                       |
| 0x025B | jtmpin2    |                                                                                                       |
| 0x025C | kuro\_1    |                                                                                                       |
| 0x025D | kuro\_2    |                                                                                                       |
| 0x025E | kuro\_3    |                                                                                                       |
| 0x025F | kuro\_4    |                                                                                                       |
| 0x0260 | kuro\_5    |                                                                                                       |
| 0x0261 | kuro\_6    |                                                                                                       |
| 0x0262 | kuro\_7    |                                                                                                       |
| 0x0263 | kuro\_8    |                                                                                                       |
| 0x0264 | kuro\_82   |                                                                                                       |
| 0x0265 | kuro\_9    |                                                                                                       |
| 0x0266 | kuro\_10   |                                                                                                       |
| 0x0267 | kuro\_11   |                                                                                                       |
| 0x0268 | kuro\_12   |                                                                                                       |
| 0x0269 | bonevil    |                                                                                                       |
| 0x026A | slfrst\_1  |                                                                                                       |
| 0x026B | slfrst\_2  |                                                                                                       |
| 0x026C | anfrst\_1  |                                                                                                       |
| 0x026D | anfrst\_2  |                                                                                                       |
| 0x026E | anfrst\_3  |                                                                                                       |
| 0x026F | anfrst\_4  |                                                                                                       |
| 0x0270 | anfrst\_5  |                                                                                                       |
| 0x0271 | sango1     |                                                                                                       |
| 0x0272 | sango2     |                                                                                                       |
| 0x0273 | sango3     |                                                                                                       |
| 0x0274 | sandun\_1  |                                                                                                       |
| 0x0275 | sandun\_2  |                                                                                                       |
| 0x0276 | lost1      |                                                                                                       |
| 0x0277 | losin1     |                                                                                                       |
| 0x0278 | losin2     |                                                                                                       |
| 0x0279 | losin3     |                                                                                                       |
| 0x027A | lost2      |                                                                                                       |
| 0x027B | lost3      |                                                                                                       |
| 0x027C | losinn     |                                                                                                       |
| 0x027D | loslake1   |                                                                                                       |
| 0x027E | loslake2   |                                                                                                       |
| 0x027F | loslake3   |                                                                                                       |
| 0x0280 | blue\_1    |                                                                                                       |
| 0x0281 | blue\_2    |                                                                                                       |
| 0x0282 | white1     |                                                                                                       |
| 0x0283 | white2     |                                                                                                       |
| 0x0284 | hekiga     |                                                                                                       |
| 0x0285 | whitein    |                                                                                                       |
| 0x0286 | ancnt1     |                                                                                                       |
| 0x0287 | ancnt2     |                                                                                                       |
| 0x0288 | ancnt3     |                                                                                                       |
| 0x0289 | ancnt4     |                                                                                                       |
| 0x028A | snw\_w     |                                                                                                       |
| 0x028B | sninn\_1   |                                                                                                       |
| 0x028C | sninn\_2   |                                                                                                       |
| 0x028D | sninn\_b1  |                                                                                                       |
| 0x028E | snow       |                                                                                                       |
| 0x028F | snmin1     |                                                                                                       |
| 0x0290 | snmin2     |                                                                                                       |
| 0x0291 | snmayor    |                                                                                                       |
| 0x0292 | hyou1      |                                                                                                       |
| 0x0293 | hyou2      |                                                                                                       |
| 0x0294 | hyou3      |                                                                                                       |
| 0x0295 | icedun\_1  |                                                                                                       |
| 0x0296 | icedun\_2  |                                                                                                       |
| 0x0297 | hyou4      |                                                                                                       |
| 0x0298 | hyou5\_1   |                                                                                                       |
| 0x0299 | hyou5\_2   |                                                                                                       |
| 0x029A | hyou5\_3   |                                                                                                       |
| 0x029B | hyou5\_4   |                                                                                                       |
| 0x029C | hyou6      |                                                                                                       |
| 0x029D | hyoumap    |                                                                                                       |
| 0x029E | move\_s    |                                                                                                       |
| 0x029F | move\_i    |                                                                                                       |
| 0x02A0 | move\_f    |                                                                                                       |
| 0x02A1 | move\_r    |                                                                                                       |
| 0x02A2 | move\_u    |                                                                                                       |
| 0x02A3 | move\_d    |                                                                                                       |
| 0x02A4 | hyou7      |                                                                                                       |
| 0x02A5 | hyou8\_1   |                                                                                                       |
| 0x02A6 | hyou8\_2   |                                                                                                       |
| 0x02A7 | hyou9      |                                                                                                       |
| 0x02A8 | hyou10     |                                                                                                       |
| 0x02A9 | hyou11     |                                                                                                       |
| 0x02AA | hyou12     |                                                                                                       |
| 0x02AB | hyou13\_1  |                                                                                                       |
| 0x02AC | hyou13\_2  |                                                                                                       |
| 0x02AD | hyou14     |                                                                                                       |
| 0x02AE | gaiafoot   |                                                                                                       |
| 0x02AF | holu\_1    |                                                                                                       |
| 0x02B0 | holu\_2    |                                                                                                       |
| 0x02B1 | gaia\_1    |                                                                                                       |
| 0x02B2 | gaiin\_1   |                                                                                                       |
| 0x02B3 | gaiin\_2   |                                                                                                       |
| 0x02B4 | gaia\_2    |                                                                                                       |
| 0x02B5 | gaiin\_3   |                                                                                                       |
| 0x02B6 | gaia\_31   |                                                                                                       |
| 0x02B7 | gaia\_32   |                                                                                                       |
| 0x02B8 | gaiin\_4   |                                                                                                       |
| 0x02B9 | gaiin\_5   |                                                                                                       |
| 0x02BA | gaiin\_6   |                                                                                                       |
| 0x02BB | gaiin\_7   |                                                                                                       |
| 0x02BC | crater\_1  |                                                                                                       |
| 0x02BD | crater\_2  |                                                                                                       |
| 0x02BE | trnad\_1   |                                                                                                       |
| 0x02BF | trnad\_2   |                                                                                                       |
| 0x02C0 | trnad\_3   |                                                                                                       |
| 0x02C1 | trnad\_4   |                                                                                                       |
| 0x02C2 | trnad\_51  |                                                                                                       |
| 0x02C3 | trnad\_52  |                                                                                                       |
| 0x02C4 | trnad\_53  |                                                                                                       |
| 0x02C5 | woa\_1     |                                                                                                       |
| 0x02C6 | woa\_2     |                                                                                                       |
| 0x02C7 | woa\_3     |                                                                                                       |
| 0x02C8 | itown1a    |                                                                                                       |
| 0x02C9 | itown12    |                                                                                                       |
| 0x02CA | itown1b    |                                                                                                       |
| 0x02CB | itown2     |                                                                                                       |
| 0x02CC | ithill     |                                                                                                       |
| 0x02CD | itown\_w   |                                                                                                       |
| 0x02CE | itown\_i   |                                                                                                       |
| 0x02CF | itown\_m   |                                                                                                       |
| 0x02D0 | ithos      |                                                                                                       |
| 0x02D1 | itmin1     |                                                                                                       |
| 0x02D2 | itmin2     |                                                                                                       |
| 0x02D3 | life       |                                                                                                       |
| 0x02D4 | life2      |                                                                                                       |
| 0x02D5 | zmind1     |                                                                                                       |
| 0x02D6 | zmind2     |                                                                                                       |
| 0x02D7 | zmind3     |                                                                                                       |
| 0x02D8 | zcoal\_1   |                                                                                                       |
| 0x02D9 | zcoal\_2   |                                                                                                       |
| 0x02DA | zcoal\_3   |                                                                                                       |
| 0x02DB | md8\_5     |                                                                                                       |
| 0x02DC | md8\_6     |                                                                                                       |
| 0x02DD | md8\_b1    |                                                                                                       |
| 0x02DE | md8\_b2    |                                                                                                       |
| 0x02DF | sbwy4\_22  |                                                                                                       |
| 0x02E0 | tunnel\_4  |                                                                                                       |
| 0x02E1 | tunnel\_5  |                                                                                                       |
| 0x02E2 | md8brdg2   |                                                                                                       |
| 0x02E3 | md8\_32    |                                                                                                       |
| 0x02E4 | canon\_1   |                                                                                                       |
| 0x02E5 | canon\_2   |                                                                                                       |
| 0x02E6 | md\_e1     |                                                                                                       |
| 0x02E7 | xmvtes     |                                                                                                       |
| 0x02E8 | las0\_1    |                                                                                                       |
| 0x02E9 | las0\_2    |                                                                                                       |
| 0x02EA | las0\_3    |                                                                                                       |
| 0x02EB | las0\_4    |                                                                                                       |
| 0x02EC | las0\_5    |                                                                                                       |
| 0x02ED | las0\_6    |                                                                                                       |
| 0x02EE | las0\_7    |                                                                                                       |
| 0x02EF | las0\_8    |                                                                                                       |
| 0x02F0 | las1\_1    |                                                                                                       |
| 0x02F1 | las1\_2    |                                                                                                       |
| 0x02F2 | las1\_3    |                                                                                                       |
| 0x02F3 | las1\_4    |                                                                                                       |
| 0x02F4 | las2\_1    |                                                                                                       |
| 0x02F5 | las2\_2    |                                                                                                       |
| 0x02F6 | las2\_3    |                                                                                                       |
| 0x02F7 | las2\_4    |                                                                                                       |
| 0x02F8 | las3\_1    |                                                                                                       |
| 0x02F9 | las3\_2    |                                                                                                       |
| 0x02FA | las3\_3    |                                                                                                       |
| 0x02FB | las4\_0    |                                                                                                       |
| 0x02FC | las4\_1    |                                                                                                       |
| 0x02FD | las4\_2    |                                                                                                       |
| 0x02FE | las4\_3    |                                                                                                       |
| 0x02FF | las4\_4    |                                                                                                       |
| 0x0300 | lastmap    |                                                                                                       |
| 0x0301 | fallp      |                                                                                                       |
| 0x0302 | m\_endo    |                                                                                                       |
| 0x0303 | hill2      |                                                                                                       |
| 0x0304 | bonevil2   |                                                                                                       |
| 0x0305 | junone22   |                                                                                                       |
| 0x0306 | rckt32     |                                                                                                       |
| 0x0307 | jtemplc    |                                                                                                       |
| 0x0308 | fship\_26  |                                                                                                       |
| 0x0309 | las4\_42   |                                                                                                       |
| 0x030A | tunnel\_6  |                                                                                                       |
| 0x030B | md8\_52    |                                                                                                       |
| 0x030C | sininb34   |                                                                                                       |
| 0x030D | mds7st33   |                                                                                                       |
| 0x030E | midgal     |                                                                                                       |
| 0x030F | sininb35   |                                                                                                       |
| 0x0310 | nivgate4   |                                                                                                       |
| 0x0311 | sininb36   |                                                                                                       |
| 0x0312 | ztruck     |                                                                                                       |
|        |            |                                                                                                       |

  [MAPJUMP]: Script/Opcodes/60%20MAPJUMP.md "wikilink"
  [LSTMP]: Script/Opcodes/6E%20LSTMP.md "wikilink"
