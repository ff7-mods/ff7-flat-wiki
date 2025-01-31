---
title: TEX_format
---

## TEX Texture Data Format for PC by [Mirex](User:Mirex "wikilink") (Edits by [Aali](../User:Aali)

FF7 PC texture consists of header, an optional palette and bitmap data. Usually data are stored like palletized picture, with bitmap pixels referencing to palette. Color 0 (in palette its usually black) is usually used as transparent color.

*Pixel values of 0 may or may not be transparent, depending on the color key status, more on that later. This also applies to non-paletted formats.*

When bit depth is 16 then data are stored as packed RGB in style RGB555, which means 5 bits per color in one 2 byte entry. I'm not sure if it is used in FF7 at all, its probably used in FF8.

*The tex format is actually very flexible and can take almost any non-paletted format as long as you describe it properly in the header.*

| Offset | Size | Description |
|----|----|----|
|  | Header |  |
| 0x00 | 4 bytes (long) | Version, must be 1, or FF7 won't load the file |
| 0x04 | 4 bytes (long) | Unknown |
| 0x08 | 4 bytes (long) | Color key flag |
| 0x0C | 4 bytes (long) | Unknown |
| 0x10 | 4 bytes (long) | Unknown |
| 0x14 | 4 bytes (long) | Minimum bits per color (D3D driver uses these to determine which texture format to convert to on load) |
| 0x18 | 4 bytes (long) | Maximum bits per color |
| 0x1C | 4 bytes (long) | Minimum alpha bits |
| 0x20 | 4 bytes (long) | Maximum alpha bits |
| 0x24 | 4 bytes (long) | Minimum bits per pixel |
| 0x28 | 4 bytes (long) | Maximum bits per pixel |
| 0x2C | 4 bytes (long) | Unknown |
| 0x30 | 4 bytes (long) | Number of palettes |
| 0x34 | 4 bytes (long) | Number of colors per palette |
| 0x38 | 4 bytes (long) | Bit depth |
| 0x3C | 4 bytes (long) | Image Width |
| 0x40 | 4 bytes (long) | Image Height |
| 0x44 | 4 bytes (long) | Pitch or bytes per row, usually ignored and assumed to be bytes per pixel \* width |
| 0x48 | 4 bytes (long) | Unknown |
| 0x4C | 4 bytes (long) | Palette flag (this indicates the presence of a palette) |
| 0x50 | 4 bytes (long) | Bits per index, always 0 for non-paletted images |
| 0x54 | 4 bytes (long) | Indexed-to-8bit flag, never used in FF7 |
| 0x58 | 4 bytes (long) | Palette size, always number of palettes \* colors per palette |
| 0x5C | 4 bytes (long) | Number of colors per palette (again, may be 0 sometimes, the other value will be used anyway) |
| 0x60 | 4 bytes (long) | Runtime data, ignored on load |
| 0x64 | 4 bytes (long) | Bits per pixel |
| 0x68 | 4 bytes (long) | Bytes per pixel, always use this to determine how much data to read, if this is 1 you read 1 byte per pixel, regardless of bit depth |
|  | Pixel format (all 0 for paletted images) |  |
| 0x6C | 4 bytes (long) | Number of red bits |
| 0x70 | 4 bytes (long) | Number of green bits |
| 0x74 | 4 bytes (long) | Number of blue bits |
| 0x78 | 4 bytes (long) | Number of alpha bits |
| 0x7C | 4 bytes (long) | Red bitmask |
| 0x80 | 4 bytes (long) | Green bitmask |
| 0x84 | 4 bytes (long) | Blue bitmask |
| 0x88 | 4 bytes (long) | Alpha bitmask |
| 0x8C | 4 bytes (long) | Red shift |
| 0x90 | 4 bytes (long) | Green shift |
| 0x94 | 4 bytes (long) | Blue shift |
| 0x98 | 4 bytes (long) | Alpha shift |
| 0x9C | 4 bytes (long) | Always 8 - Number of red bits (Not sure what the point of these fields is, they're always ignored anyway) |
| 0xA0 | 4 bytes (long) | 8 - Number of green bits |
| 0xA4 | 4 bytes (long) | 8 - Number of blue bits |
| 0xA8 | 4 bytes (long) | 8 - Number of alpha bits |
| 0xAC | 4 bytes (long) | Red max |
| 0xB0 | 4 bytes (long) | Green max |
| 0xB4 | 4 bytes (long) | Blue max |
| 0xB8 | 4 bytes (long) | Alpha max |
|  | End of pixel format |  |
| 0xBC | 4 bytes (long) | Color key array flag (this indicates the presence of a color key array) |
| 0xC0 | 4 bytes (long) | Runtime data |
| 0xC4 | 4 bytes (long) | Reference alpha (more on this later) |
| 0xC8 | 4 bytes (long) | Runtime data |
| 0xCC | 4 bytes (long) | Unknown |
| 0xD0 | 4 bytes (long) | Palette index (runtime data) |
| 0xD4 | 4 bytes (long) | Runtime data |
| 0xD8 | 4 bytes (long) | Runtime data |
| 0xDC | 4 bytes (long) | Unknown |
| 0xE0 | 4 bytes (long) | Unknown |
| 0xE4 | 4 bytes (long) | Unknown |
| 0xE8 | 4 bytes (long) | Unknown |
|  | Palette data (ignore this section if palette flag is 0) |  |
| 0xEC | Palette size \* 4 | The raw palette data, always in 32-bit BGRA format |
|  | Pixel data |  |
| Varies | Read width \* height \* "bytes per pixel" bytes of data. If there's a palette, every pixel is an index into that palette, otherwise use the pixel format specification. |  |
|  | Color key array |  |
| Varies | Number of palettes \* 1 bytes. |  |

*Color keying: If the color key flag is zero, no color keying is performed and the color key array is ignored. Otherwise, the current palette index is used to retrieve a single byte from the color key array, this is the new color key flag, zero means don't do color keying.* If there is no color key array (and the color key flag is not zero), you should always color key.

*Reference alpha: Only applies to paletted images, if the alpha value sampled from the palette is 0xFE, this value should be replaced with the reference alpha.*
