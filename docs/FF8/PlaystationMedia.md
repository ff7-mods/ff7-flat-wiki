---
title: PlaystationMedia
---

[Home](Main%20Page.md) > [FF8](FF8.md) > PlaystationMedia

By myst6re

# FF8DISCX.IMG File Format

Almost all of the game files are hidden in the FF8DISCX.IMG (with X=disc
number) file.

## Root Files

In the case of a Japanese iso, the file begins directly with a list of
file location and size, with the following format:

| Offset | Size | Data                                                               |
|--------|------|--------------------------------------------------------------------|
| 0      | 4    | Location of file in sectors (relative to the start of the **iso**) |
| 4      | 4    | Size of file in bytes                                              |

In the case of a PAL iso, there are 5 unknown sectors (a sector = 2048
bytes in data, 2352 bytes in disk) before this list of files.

**Notes:**

-   I do not have the American iso, please fix this article if you can.
-   We do not know how many files there are in the list, neither file
    names!
-   Each file in FF8DISCX.IMG are relative to the start of the **iso**!

| ID           | Filename (from PC version)                             | Notes                             |
|--------------|--------------------------------------------------------|-----------------------------------|
| 0            | ? + packcode.bin                                       | Contains a font file (tim format) |
| 2            | [field.bin][]                                          | LZSed                             |
| 3            | wm2field.tbl                                           | size= 72\*24 bytes                |
| 4            | ? + mmagic.bin + mitem.bin + areames.dc1 + ?           |                                   |
| 7            | ? + pet\_exp.bin + ?                                   |                                   |
| 9            | ? + mwepon.bin + mwepon.msg + shop.bin + price.bin + ? |                                   |
| 11           | ? + mmag.bin + mthomas.bin                             |                                   |
| 12           | ? + magsort.bin                                        |                                   |
| 15           | ? + mmag2.bin + cyocobo.bin                            |                                   |
| 16           | ? + cardanm.sp2                                        |                                   |
| 17           | ? + mtmag.bin                                          |                                   |
| 21           | mngrp.bin                                              |                                   |
| 22           | init.out                                               |                                   |
| 23           | Triple Triad (in ff8.exe in PC version)                | Some Triple Triad tims (LZSed)    |
| 25           | battle.bin (not present in PC version)                 |                                   |
| 26           | world.bin (not present in PC version)                  |                                   |
| 30 -&gt; 127 | AKAO files (music)                                     |                                   |
| 128          | kernel.bin                                             |                                   |
| 129          | sysfnt.tdw                                             |                                   |
| 130          | icon.tim                                               |                                   |
| 131          | namedic.tim                                            |                                   |

  

## Field Files

In the list of root files, the third file is in fact the "FIELD.BIN".
This file is [LZS][] compressed, and contains some informations, like
the list of field files position and size.

Find the file list is approximate, I am trying to find some bytes:
"\\x04\\x00\\x05\\x24\\x18\\x00\\xbf\\x8f\\x14\\x00\\xb1\\x8f\\x10\\x00\\xb0\\x8f\\x20\\x00\\xbd\\x27\\x08\\x00\\xe0\\x03\\x00\\x00\\x00\\x00"
(size=28), normally, there is the list right after this sequence of
bytes, and before the "\\x00\\x00\\x01\\x00\\x02\\x00\\x03\\x00"
(size=8) sequence.

Order of files (sorted by id):

-   D000.[MCH][] -&gt; D075.MCH files \[id=0 -&gt; id=76\]
-   Field files (MIM, DAT and LZK) \[id=77 -&gt; id=last\]

There are three LZSed files for each field: EXAMPLE.MIM, EXAMPLE.DAT and
EXAMPLE.LZK (Extension names \*.MIM, \*.DAT and \*.LZK found in PC
version, field.fs &gt; mapdata.fs &gt; map1.bak). If you want to convert
Playstation fields to PC fields format, this is a concatenation of some
PC files.

### First file (\*.MIM)

| Offset               | Size     | Data                             |
|----------------------|----------|----------------------------------|
| 0                    | 4        | Location of section 3 in PSX RAM |
| 4                    | 4        | Location of section 4 in PSX RAM |
| 8                    | 4        | [Unknown data \[PVP][1]\]        |
| 12                   | 438272   | [Background data \[MIM][2]\]     |
| 438284 (section 3)   | *Varies* | [Font data \[TDW][3]\]           |
| *Varies* (section 4) | *Varies* | [Particle Image Data \[PMP][4]\] |

### Second file (\*.DAT)

| Offset | Size     | Data                                   | Section Data                     |
|--------|----------|----------------------------------------|----------------------------------|
| 0      | 4        | Location of section 1 in PSX RAM       | [Triggers & gateways \[INF][5]\] |
| 4      | 4        | Location of section 2 in PSX RAM       | [Camera \[CA][6]\]               |
| 8      | 4        | Location of section 3 in PSX RAM       | [Walkmesh \[ID][7]\]             |
| 12     | 4        | Location of section 4 in PSX RAM       | [Background infos \[MAP][8]\]    |
| 16     | 4        | Location of section 5 in PSX RAM       | [Movie cam \[MSK][9]\]           |
| 20     | 4        | Location of section 6 in PSX RAM       | [Battle rate \[RAT][10]\]        |
| 24     | 4        | Location of section 7 in PSX RAM       | [Battle formations \[MRT][10]\]  |
| 28     | 4        | Location of section 8 in PSX RAM       | Sounds/AKAOs                     |
| 32     | 4        | Location of section 9 in PSX RAM       | [Texts \[MSD][11]\]              |
| 36     | 4        | Location of section 10 in PSX RAM      | [Particle Infos \[PMD][12]\]     |
| 40     | 4        | Location of section 11 in PSX RAM      | [Scripts \[JSM][13]\]            |
| 44     | 4        | Location of the end of file in PSX RAM |                                  |
| 48     | *varies* | Triggers and gateways                  |                                  |
| ...    | ...      | ...                                    | ...                              |

### Third file (\*.LZK)

Almost like the [chara.one][] file. The main difference is that the
models data are compressed.

  [field.bin]: #user-content-field-files "wikilink"
  [LZS]: FF7/LZS%20format.md "wikilink"
  [MCH]: FF8/FileFormat%20MCH.md "wikilink"
  [1]: FF8/FileFormat%20PVP.md "wikilink"
  [2]: FF8/FileFormat%20MIM.md "wikilink"
  [3]: FF8/FileFormat%20TDW.md "wikilink"
  [4]: FF8/FileFormat%20PMP.md "wikilink"
  [5]: FF8/FileFormat%20INF.md "wikilink"
  [6]: FF8/FileFormat%20CA.md "wikilink"
  [7]: FF7/Field/Camera%20Matrix.md "wikilink"
  [8]: FF8/FileFormat%20MAP.md "wikilink"
  [9]: FF8/FileFormat%20MSK.md "wikilink"
  [10]: FF8/FileFormat%20RAT%20MRT.md "wikilink"
  [11]: FF8/FileFormat%20MSD.md "wikilink"
  [12]: FF8/FileFormat%20PMD.md "wikilink"
  [13]: FF8/FileFormat%20JSM.md "wikilink"
  [chara.one]: FF8/FileFormat%20ONE.md "wikilink"
