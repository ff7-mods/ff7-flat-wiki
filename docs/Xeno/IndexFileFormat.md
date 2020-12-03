---
title: IndexFileFormat
---

[Home](../Main Page.md) > [Xeno](../Xeno.md) > IndexFileFormat

The original file structure was deleted from the disk, exept two start files: SLUS\_xxx.xx and SYSTEM.CNF, but after game starts file structure restores and game works whith it.

The file that holds all file structure are the very first on the disk (no matter english or japanese copy of game). It starts from 24 sector and has size of 16 sectors.

## File Format

The file consists of repeated 7 bytes block that contents start sectors and length for directories and files.

|                                                    Start sector                                                     |                                           Length                                           |
|:-------------------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------------------------------:|
|                                               Offset 0x00 Length 0x03                                               |                                  Offset 0x03 Length 0x04                                   |
|                                                      Directory                                                      |                                                                                            |
|              Start sector is the same as the sector of the first file. It doesn't interest us anyway.               | Length must be greater than 0xff000000. We don't know purpose of the directory Length yet. |
|                                                        File                                                         |                                                                                            |
|                                              Start sector of the file.                                              |                           Length must be lesser than 0xff000000.                           |
|                                                       Others                                                        |                                                                                            |
| There are some free spaces sometimes. They are filled with zeros, so we need to skip it. Its purpose are not known. |                                                                                            |
|                                                      0x000000.                                                      |                                        0x00000000.                                         |
|                                                     End of Disk                                                     |                                                                                            |
|                                                      0xFFFFFF.                                                      |                                        0x00000000.                                         |
