---
title: Directory11 Field
---

[Home](../../Main%20Page.md.md) > [Xeno](../../Xeno.md) > [GameDirectoryDescription](../GameDirectoryDescription.md) > Directory11 Field

## File Format

There are pairs of two files. First one are field model textures. The
second one are model, sprites data, as well as text and script.

## First file - Textures and CLUT

## Second file - Field Data

This is uniq pack of different data. There are always 8 files in there.
All of them are compressed. The most part of header are unknown, except
few data.

| Start offset |    Size    |             Value             |
|:------------:|:----------:|:-----------------------------:|
|    0x010C    | 0x04 bytes | Length of uncompressed file 1 |
|    0x0110    | 0x04 bytes | Length of uncompressed file 2 |
|    0x0114    | 0x04 bytes | Length of uncompressed file 3 |
|    0x0118    | 0x04 bytes | Length of uncompressed file 4 |
|    0x011C    | 0x04 bytes | Length of uncompressed file 5 |
|    0x0120    | 0x04 bytes | Length of uncompressed file 6 |
|    0x0124    | 0x04 bytes | Length of uncompressed file 7 |
|    0x0128    | 0x04 bytes | Length of uncompressed file 8 |
|    0x012C    | 0x04 bytes |            Unknown            |
|    0x0130    | 0x04 bytes |       Offset to file 1        |
|    0x0134    | 0x04 bytes |       Offset to file 2        |
|    0x0138    | 0x04 bytes |       Offset to file 3        |
|    0x013C    | 0x04 bytes |       Offset to file 4        |
|    0x0140    | 0x04 bytes |       Offset to file 5        |
|    0x0144    | 0x04 bytes |       Offset to file 6        |
|    0x0148    | 0x04 bytes |       Offset to file 7        |
|    0x014C    | 0x04 bytes |       Offset to file 8        |
|    0x0150    | 0x04 bytes |     Offset to end of pack     |

There are files:

-   1\) unknown
-   2\) walkmeshes
-   3\) pack of 3d models
-   4\) sprites
-   5\) sprites animation
-   6\) entitys and scripts
-   7\) unknown
-   8\) text

**2) walkmeshes**

Contains number of walkmeshes for character and camera.

|                                 Start offset                                  |    Size    |                 Value                  |
|:-----------------------------------------------------------------------------:|:----------:|:--------------------------------------:|
|                                     0x00                                      | 0x04 bytes |          Number of walkmeshes          |
|                       0x04 + Number of walkmesh \* 0x04                       | 0x04 bytes |           Length of walkmesh           |
|                   0x04 + (Number of walkmeshes + 1) \* 0x04                   | 0x04 bytes |              End of file               |
|    0x04 + (Number of walkmeshes + 1) \* 0x04 + Number of walkmesh \* 0x08     | 0x04 bytes | Start of walkmesh triangle description |
| 0x04 + (Number of walkmeshes + 1) \* 0x04 + Number of walkmesh \* 0x08 + 0x04 | 0x04 bytes |       Start of walkmesh vertexes       |
|                                                                               |            |                                        |

Vertex array are simple.

| Start offset |    Size    |          Value          |
|:------------:|:----------:|:-----------------------:|
|     0x00     | 0x02 bytes |            X            |
|     0x02     | 0x02 bytes |            Y            |
|     0x04     | 0x02 bytes |            Z            |
|     0x06     | 0x02 bytes | Aligment zeros (0x0000) |

Each triangle descript like this

| Start offset |    Size    |                    Value                    |
|:------------:|:----------:|:-------------------------------------------:|
|     0x00     | 0x02 bytes |             A (index of vertex)             |
|     0x02     | 0x02 bytes |             B (index of vertex)             |
|     0x04     | 0x02 bytes |             C (index of vertex)             |
|     0x06     | 0x02 bytes | Access side 1 (index of triangle or 0xFFFF) |
|     0x08     | 0x02 bytes | Access side 2 (index of triangle or 0xFFFF) |
|     0x0A     | 0x02 bytes | Access side 3 (index of triangle or 0xFFFF) |
|     0x0C     | 0x02 bytes |                Unknown flags                |
