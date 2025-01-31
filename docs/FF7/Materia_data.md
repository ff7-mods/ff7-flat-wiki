---
title: Materia_data
---

## KERNEL.BIN - Section 9: Materia data format

This section contains the Materia data. Each record is 20 bytes long.

| Offset | Length | Description |  |  |
|:--:|----|----|----|----|
| 0x00 | 8 bytes | Level-up AP limits | Multiples of 100 (4x WORD) |  |
| 0x08 | 1 byte | Equip Effect | \[See table below\] |  |
| 0x09 | 3 bytes | [Status Effects](Battle/Status_Effects). Only first 24. |  |  |
| 0x0C | 1 byte | [Element Index](Battle/Elemental_Data) |  |  |
| 0x0D | 1 byte | [Materia Type](Materia_Types) |  |  |
| 0x0E | 1 byte | Materia attributes | \[See Above\] |  |
| 0x0F | 1 byte | Materia attributes | \[See Above\] |  |
| 0x10 | 1 byte | Materia attributes | \[See Above\] |  |
| 0x11 | 1 byte | Materia attributes | \[See Above\] |  |
| 0x12 | 1 byte | Materia attributes | \[See Above\] |  |
| 0x13 | 1 byte | Materia attributes | \[See Above\] |  |

#### Equip Effects

|       Byte        | STR | VIT | MAG | MDEF\* | DEX | LUCK | MAXHP | MAXMP |
|:-----------------:|:---:|:---:|:---:|:------:|:---:|:----:|:-----:|:-----:|
|       0x00        |     |     |     |        |     |      |       |       |
|       0x01        | -02 | -01 | +02 |  +01   |     |      | -05%  | +05%  |
|       0x02        | -04 | -02 | +04 |  +02   |     |      | -10%  | +10%  |
|       0x03        |     |     |     |        | +02 | -02  |       |       |
|       0x04        | -01 | -01 | +01 |  +01   |     |      |       |       |
|       0x05        | +01 | +01 | -01 |  -01   |     |      |       |       |
|       0x06        |     | +01 |     |        |     |      |       |       |
|       0x07        |     |     |     |        |     | +01  |       |       |
|       0x08        |     |     |     |        |     | -01  |       |       |
|       0x09        |     |     |     |        | -02 |      |       |       |
|       0x0A        |     |     |     |        | +02 |      |       |       |
|       0x0B        | -01 |     | +01 |        |     |      | -02%  | +02%  |
|       0x0C        |     |     | +01 |        |     |      | -02%  | +02%  |
|       0x0D        |     |     | +01 |  +01   |     |      | -05%  | +05%  |
|       0x0E        |     |     | +02 |  +02   |     |      | -10%  | +10%  |
|       0x0F        |     |     | +04 |  +04   |     |      | -10%  | +15%  |
|       0x10        |     |     | +08 |  +08   |     |      | -10%  | +20%  |
| 0x11<sup>+</sup>  |     |     |     |        |     |      |       |       |
| 0x12<sup>+</sup>  |     |     |     |        |     |      |       |       |
| 0x13<sup>+</sup>  |     |     |     |        |     |      |       |       |
| 0x14<sup>+</sup>  |     |     |     |        |     |      |       |       |
| 0x15<sup>++</sup> | +1  | +2  | +4  |   +8   | +16 | +32  | +64%  | +128% |

  *\** Although the Materia equip menu will claim that certain materia increase the Magic Def stat, they really increase Spirit.  
  <sup>+</sup> These are valid bonus values in the PC version, but they're unused.  
  <sup>++</sup> This value is allowable in the PC version although technically a memory leak.
