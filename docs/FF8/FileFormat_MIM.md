---
title: FileFormat_MIM
---

By Aali.

# MIM Files

MIM files in the PC version of FF8 are a bit different from the MIM files found in the PSX version of FF7, there are no headers, no size information anywhere, the format seems to be fixed to two different types. Type 1 (the most common) has 24 palettes and 13 128x256 texture pages, while type 2 has 16 palettes and only 12 textures.

## Palettes

The first section contains the palettes, either 24 or 16 palettes of 256 colors in native PSX format (R5G5B5 with one mask bit) for a total of 0x2000 or 0x3000 bytes. For type 1, the first 8 palettes are always the same, a repeating pattern of some basic colors, these palettes are never used, only the remaining 16 palettes can be accessed from the MAP file(?)

## Image Data

The actual image data can be read as a single 256 pixels high image, 1664 pixels wide (0x68000 bytes) for type 1, 1536 pixels wide (0x60000 bytes) for type 2. One byte is one pixel and pixel values of 0 are transparent. FF8 splits the image into multiple textures, each one 128x256, this is not necessary on modern hardware.

The image contained in the MIM file is just a jumble of 16x16 tiles, to draw them properly you have to read the tile data from the [.map](FileFormat_MAP.md) file.
