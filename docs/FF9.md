---
title: FF9
---

# Final Fantasy 9 Information

Since there isn't a PC version of this game all information relates to the PS1.

# Disk IMG Format

The game information is contained in a single file on the CD-ROM named FF9.IMG with each disk containing a file named this. FMV movies are stored in sub directories on the disk.

## [Image Root Directory](FF9/IMGRootDir)

The IMG file begins with a **root directory** that has a list of file counts and sectors.

## [Image Sub Directory](FF9/IMGSubDir)

Some directory entries contain **subdirectories**.

## [Directories and data](FF9/Dirs)

What contains directories and for what contain files

### [Directory '0'](FF9/Dirs/00)

### [Directory '1'](FF9/Dirs/01)

## [File Cluster Information](FF9/File/Data)

Some of the files are actually **data clusters** that contain multiple information these files begin with the hexadecimal number 0xDB.

### [Chunk 0x02: 3D Model data](FF9/File/0x02)

This chunk contains 3D model information: vertices, quads, triangles, texture mapping coordinates...

### [Chunk 0x03: 3D Animation](FF9/File/0x03)

This chunk contains animation sequences for 3d models...

### [Chunk 0x04: Image data(TIM\`s)](FF9/File/0x04)

This chunk contains tim-images...

### [Chunk 0x05: Scripts](FF9/File/0x05)

This chunk contains scripts files...

### [Chunk 0x0A: Field tiles](FF9/File/0x0A)

This chunk contains information about field tiles and field camera parameters...

### [Chunk 0x0B: Field walkmesh](FF9/File/0x0B)

This chunk contain field walkmesh data...

### [Chunk 0x0C: Battle scenes](FF9/File/0x0C)

This chunk contain battle scenes geometry...

### [Chunk 0x12: Contain CLUT and TPage for models](FF9/File/0x12)

This chunk contains CLUT and TPage info for models.

### [Chunk 0x1B: Pointers to other 'DB'](FF9/File/0x1B)

This chunk contains pointers to other DB structures.

# [WorldMap](FF9/WorldMap)

# [Character Tables](FF9/CharTables)

## [European & US Tables](FF9/CharTables#Character_Table_for_EU_.26_US_version)

## [Japanese Table](FF9/CharTables#Character_Table_for_JP_version)

## [Kanji Table A](FF9/CharTables#Kanji_Table_A)

## [Kanji Table B](FF9/CharTables#Kanji_Table_B)

# Sound

- [Sound](FF9/Sound)

# Tools and Patches

- [Tools and Patches](FF9/Tools)
