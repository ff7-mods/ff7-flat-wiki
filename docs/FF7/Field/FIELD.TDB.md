---
title: FIELD.TDB
---

## Format for Field.TDB

[Cyberman](User:Cyberman "wikilink") 21:45, 10 Jan 2007 (CST) Field.TDB is an [LZS compressed](../LZS_format) file the first DWORD of which is it's compressed size.

After decompression the file contains the following header

| Size | Type   | Description     |
|------|--------|-----------------|
| 4    | uint32 | Total Data Size |
| 2    | uint16 | Image Count     |
| 2    | uint16 | Palette Count   |
| 4    | uint32 | Image Offset    |
| 4    | uint32 | Palette Offset  |

FILED.TDB header

`typedef struct`  
`{`  
` uint32 FileSize;`  
` uint16 ImageCount;`  
` uint16 PaletteCount;`  
` uint32 ImageOffset;`  
` uint32 PaletteOffset;`  
`} TDB_TextureHeader;`

Images follow they are 32x32x 4 bits (or 512 bytes each) Palettes are next, which are B5G5R5 format, uint16 format. 16 colors per palette. Therefore each palette is 32bytes in length.

Palettes are not selected from this file but from the BSX files for models.
