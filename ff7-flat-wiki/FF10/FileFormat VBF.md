---
title: FileFormat VBF
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF10](/ff7-flat-wiki/FF10.md) > FileFormat VBF

Final Fantasy X stores all of its' game data in a single large archive,
called a VBF (Virtuos Big File) archive. [Virtuos][] is the developer
contracted by Square Enix to handle the FFX/X-2 HD Remaster.

### VBF header format

| Offset                                                      | Length               | Name              | Description                                           |
|-------------------------------------------------------------|----------------------|-------------------|-------------------------------------------------------|
| 0x0000                                                      | 4 bytes              | N/A               | VBF header bytes, always equal to 0x5352594b ("SRYK") |
| 0x0004                                                      | 4 bytes              | headerLength      | Length of the header block                            |
| 0x0008                                                      | 8 bytes              | numFiles          | Number of files contained in archive                  |
| 0x0010                                                      | numFiles \* 16 bytes | nameHashes        | MD5 hashes of each file name within archive           |
| The next 5 values are repeated for each file in the archive |                      |                   |                                                       |
| 0x0010 + (numFiles \* 16) + (32 \* fileIndex)               | 4 bytes              | blockListStarts   | Start offset of file in the block list                |
| 0x0014 + (numFiles \* 16) + (32 \* fileIndex)               | 4 bytes              | unknown           | Unknown value, can be left as 0 when reconstructing   |
| 0x0018 + (numFiles \* 16) + (32 \* fileIndex)               | 8 bytes              | originalSizes     | Original size of file                                 |
| 0x0020 + (numFiles \* 16) + (32 \* fileIndex)               | 8 bytes              | startOffsets      | Start offset of file data                             |
| 0x0028 + (numFiles \* 16) + (32 \* fileIndex)               | 8 bytes              | fileNameOffsets   | Offset of file name in string table                   |
| ...                                                         |                      |                   |                                                       |
| 0x0010 + (numFiles \* 48)                                   | 4 bytes              | stringTableLength | Length of the string table                            |
| 0x0014 + (numFiles \* 48)                                   | stringTableLength    | stringTable       | String table data                                     |

  [Virtuos]: https://en.wikipedia.org/wiki/Virtuos
