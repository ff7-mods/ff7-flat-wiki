---
title: Kernel.bin
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Kernel](FF7/Kernel.md) > Kernel.bin

## Important Files

|   PSX Version    |        PC Version        |
|:----------------:|:------------------------:|
| /INIT/KERNEL.BIN | /DATA/KERNEL/KERNEL.BIN  |
|                  | /DATA/KERNEL/KERNEL2.BIN |

## The KERNEL.BIN Archive

The file KERNEL.BIN archive is in [BIN-GZIP format][]. It consists of 27
gziped sections concatenated together with a 6 byte header for each.
This file is the same both on the PC and PSX versions. This holds all
the static data and menu text for the game, with a look up table at the
beginning of the section. The first 9 sections of data (i.e. The
non-text related items) are in typical BIN file archive format. Sections
10-27 are [FF Text files][]. The text sections have a header of pointers
at the beginning of each section and point to a text block below.

The KERNEL.BIN file consists of the following sections.

| File | Data                          | Offset |
|------|-------------------------------|--------|
| 1    | [Command data][]              | 0x0006 |
| 2    | [Attack data][]               | 0x0086 |
| 3    | [Battle and growth data][]    | 0x063A |
| 4    | [Initialization data][]       | 0x0F7F |
| 5    | [Item data][]                 | 0x111B |
| 6    | [Weapon data][]               | 0x137A |
| 7    | [Armor data][]                | 0x1A30 |
| 8    | [Accessory data][]            | 0x1B73 |
| 9    | [Materia data][]              | 0x1C11 |
| 10   | Command descriptions          | 0x1F32 |
| 11   | Magic descriptions            | 0x2199 |
| 12   | Item descriptions             | 0x28D4 |
| 13   | Weapon descriptions           | 0x2EE2 |
| 14   | Armor descriptions            | 0x307B |
| 15   | Accessory descriptions        | 0x315F |
| 16   | Materia descriptions          | 0x3384 |
| 17   | Key Item descriptions         | 0x3838 |
| 18   | Command Names                 | 0x3BE2 |
| 19   | Magic Names                   | 0x3CCA |
| 20   | Item Names                    | 0x4293 |
| 21   | Weapon Names                  | 0x4651 |
| 22   | Armor Names                   | 0x4B02 |
| 23   | Accessory Names               | 0x4C4B |
| 24   | Materia Names                 | 0x4D90 |
| 25   | Key Item Names                | 0x5040 |
| 26   | Battle and Battle-Screen Text | 0x5217 |
| 27   | Summon Attack Names           | 0x5692 |

## The KERNEL2.BIN Archive

On the PC version there exists a secondary kernel archive called
KERNEL2.BIN. This archive contains only sections 10-27 (Text data) of
KERNEL.BIN. The data was ungzipped from the original archive,
concatenated together, and then LZSed into a single archive with a 4
byte header giving the length of the file.

The maximum allotted storage space on the PC version for all un-LZSed
data in the kernel2.bin is 27KB (27648 bytes). This means that the total
size of the extracted files (text and pointers) must be less than this.

  [BIN-GZIP format]: Low%20level%20libraries.md#BIN-GZIP%20Type%20Archives
    "wikilink"
  [FF Text files]: ../FF%20Text.md "wikilink"
  [Command data]: ../Command%20data.md "wikilink"
  [Attack data]: ../Attack%20data.md "wikilink"
  [Battle and growth data]: ../Battle%20and%20growth%20data.md "wikilink"
  [Initialization data]: ../Character%20starting%20stats.md "wikilink"
  [Item data]: ../Item%20data.md "wikilink"
  [Weapon data]: ../Weapon%20data.md "wikilink"
  [Armor data]: ../Armor%20data.md "wikilink"
  [Accessory data]: ../Accessory%20data.md "wikilink"
  [Materia data]: ../Materia%20data.md "wikilink"
