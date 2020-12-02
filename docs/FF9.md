---
title: FF9
---

[Home](/ff7-flat-wiki/Main%20Page.md) > FF9

# Final Fantasy 9 Information

Since there isn't a PC version of this game all information relates to
the PS1.

# Disk IMG Format

The game information is contained in a single file on the CD-ROM named
FF9.IMG with each disk containing a file named this. FMV movies are
stored in sub directories on the disk.

## [Image Root Directory][]

The IMG file begins with a **root directory** that has a list of file
counts and sectors.

## [Image Sub Directory][]

Some directory entries contain **subdirectories**.

## [Directories and data][]

What contains directories and for what contain files

### [Directory '0'][]

### [Directory '1'][]

## [File Cluster Information][]

Some of the files are actually **data clusters** that contain multiple
information these files begin with the hexadecimal number 0xDB.

### [Chunk 0x02: 3D Model data][]

This chunk contains 3D model information: vertices, quads, triangles,
texture mapping coordinates...

### [Chunk 0x03: 3D Animation][]

This chunk contains animation sequences for 3d models...

### [Chunk 0x04: Image data(TIM\`s)][]

This chunk contains tim-images...

### [Chunk 0x05: Scripts][]

This chunk contains scripts files...

### [Chunk 0x0A: Field tiles][]

This chunk contains information about field tiles and field camera
parameters...

### [Chunk 0x0B: Field walkmesh][]

This chunk contain field walkmesh data...

### [Chunk 0x0C: Battle scenes][]

This chunk contain battle scenes geometry...

### [Chunk 0x12: Contain CLUT and TPage for models][]

This chunk contains CLUT and TPage info for models.

### [Chunk 0x1B: Pointers to other 'DB'][]

This chunk contains pointers to other DB structures.

# [WorldMap][]

# [Character Tables][]

## [European & US Tables][]

## [Japanese Table][]

## [Kanji Table A][]

## [Kanji Table B][]

# Sound

-   [Sound][]

# Tools and Patches

-   [Tools and Patches][]

  [Image Root Directory]: /ff7-flat-wiki/FF9/IMGRootDir.md "wikilink"
  [Image Sub Directory]: /ff7-flat-wiki/FF9/IMGSubDir.md "wikilink"
  [Directories and data]: /ff7-flat-wiki/FF9/Dirs.md "wikilink"
  [Directory '0']: /ff7-flat-wiki/FF9/Dirs/00.md "wikilink"
  [Directory '1']: /ff7-flat-wiki/FF9/Dirs/01.md "wikilink"
  [File Cluster Information]: /ff7-flat-wiki/FF9/File/Data.md "wikilink"
  [Chunk 0x02: 3D Model data]: /ff7-flat-wiki/FF9/File/0x02.md "wikilink"
  [Chunk 0x03: 3D Animation]: /ff7-flat-wiki/FF9/File/0x03.md "wikilink"
  [Chunk 0x04: Image data(TIM\`s)]: /ff7-flat-wiki/FF9/File/0x04.md "wikilink"
  [Chunk 0x05: Scripts]: /ff7-flat-wiki/FF9/File/0x05.md "wikilink"
  [Chunk 0x0A: Field tiles]: /ff7-flat-wiki/FF9/File/0x0A.md "wikilink"
  [Chunk 0x0B: Field walkmesh]: /ff7-flat-wiki/FF9/File/0x0B.md "wikilink"
  [Chunk 0x0C: Battle scenes]: /ff7-flat-wiki/FF9/File/0x0C.md "wikilink"
  [Chunk 0x12: Contain CLUT and TPage for models]: /ff7-flat-wiki/FF9/File/0x12.md
    "wikilink"
  [Chunk 0x1B: Pointers to other 'DB']: /ff7-flat-wiki/FF9/File/0x1B.md "wikilink"
  [WorldMap]: /ff7-flat-wiki/FF9/WorldMap.md "wikilink"
  [Character Tables]: /ff7-flat-wiki/FF9/CharTables.md "wikilink"
  [European & US Tables]: /ff7-flat-wiki/FF9/CharTables.md#Character%20Table%20for%20EU%20.26%20US%20version
    "wikilink"
  [Japanese Table]: /ff7-flat-wiki/FF9/CharTables.md#Character%20Table%20for%20JP%20version
    "wikilink"
  [Kanji Table A]: /ff7-flat-wiki/FF9/CharTables.md#Kanji%20Table%20A "wikilink"
  [Kanji Table B]: /ff7-flat-wiki/FF9/CharTables.md#Kanji%20Table%20B "wikilink"
  [Sound]: /ff7-flat-wiki/FF9/Sound.md "wikilink"
  [Tools and Patches]: /ff7-flat-wiki/FF9/Tools.md "wikilink"
