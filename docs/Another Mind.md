---
title: Another Mind
---

[Home](/Main%20Page.md) > Another Mind

(The following Was ripped off of Wikipedia because I'm lazy)

Another Mind is an FMV visual Novel created by Squaresofy for Sony
PlayStation and released on November 12, 1998 in Japan. The game is
extremely obscure. The game involves a 16 year-old girl named Hitomi
Hayama who is involved in a car accident and admitted to a hospital.
Upon waking, she realizes that another mind has taken residence in her
head. The player takes on the role of this separate consciousness. The
pair are then put into the middle of a mystery that begins at the
hospital, which includes a murder, several suicide attempts, and a
bombing attempt. Hitomi frequently communicates back with the player,
and the player must convince her to perform actions rather than
commanding.

The file location data on the CD-ROM is indexed much like FF7, the
sector lookup table is called CDPOS.DAT and in the root directory.

The following are the file formats for the game. These are loacted in
the /PRGDATA folder. If the extension end in a "Z" They are compressed
in an LZS format elaborated below.

  

| Extension | Data                                |
|-----------|-------------------------------------|
| [ANZ][]   | LZS Compressed Dialog Answer Lookup |
| [BBB][]   | Unknown                             |
| [BIN][]   | Unknown                             |
| [BIZ][]   | LZS Compressed BIN file (Unknown)   |
| [DAT][]   | Sound Effects                       |
| [DCT][]   | Japanese Word Dictionary            |
| [KAT][]   | Unknown                             |
| [SNG][]   | Midi/Mod like Music Data            |
| [STR][]   | MDEC format movie file              |
| [TIZ][]   | LZS Compressed TIM file             |
| [VIB][]   | Unknown                             |
| [ZZZ][]   | LZS Compressed dialogs              |

## Compression

The compressed files are compressed with LZS with a special 2-byte
header that starts with "C3 FF" marking it as compressed.

## CDPOS.DAT

This is the master look-up table for the data files loacted in the
/PRGDATA folder. It follows the following format in little-endian
(backwards)

| Sector Offset | Data Length |
|---------------|-------------|
| 4 Bytes       | 4 Bytes     |

You must subtract one to the sector location to get the actual location
of the disk. Take, for example BUS3012.TIZ (entry 257). According to
it's ISO6996 directory entry says it starts at 0x032E78 and has a length
of 0xE00F. The entry in CDPOS.DAT shows it's location of 0x032E79 with a
length of 0xE00F. The means the ISO starts at zero, while Square starts
indexing at one(?)

  [ANZ]: /ANZ.md "wikilink"
  [BBB]: /BBB.md "wikilink"
  [BIN]: /BIN.md "wikilink"
  [BIZ]: /BIZ.md "wikilink"
  [DAT]: /DAT.md "wikilink"
  [DCT]: /DCT.md "wikilink"
  [KAT]: /KAT.md "wikilink"
  [SNG]: /SNG.md "wikilink"
  [STR]: /STR.md "wikilink"
  [TIZ]: /TIZ.md "wikilink"
  [VIB]: /VIB.md "wikilink"
  [ZZZ]: /ZZZ.md "wikilink"
