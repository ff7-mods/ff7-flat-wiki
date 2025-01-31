---
title: Palette
---

### Section 4: Palette ([Terence Fergusson](User:Terence_Fergusson "wikilink") & [myst6re](../../User:Myst6re)

The following is an overview of the palette data.

#### Section 4 Format

| Offset | Size | Description |
|----|----|:--:|
| 0x00 | 4 bytes | Length (Repeat of previous length header) |
| 0x04 | 2 bytes | PalX |
| 0x06 | 2 bytes | PalY |
| 0x08 | 2 bytes | Number of colors in palette |
| 0x0A | 2 bytes | Number of palettes |
| 0x0C | (Number of palettes) \* (Number of colors in palette) \* 2 | Palette data |

After the first length indicator comes another integer, also indicating length. Useless, but it's there.  
Then two bytes; palX, useful for the PS version only (always 0).  
Then two bytes again; palY, useful for the PS version only (always 480).  
Then two bytes; number of colors in the palette (always 256).  
Then two bytes; number of palettes.  
Then the actual palette data.

Each palette entry is a 16-bit color. This is unusual - normally palettes store as high quality data as possible, usually 24/32 bit. However since FF7 only ever runs in 16 bit I guess there isn't much point storing any other kind of data. Actually, the data is 15-bit (1 mask bit, 5-bit Blue, 5-bit Green and 5-bit Red).

| Palette Data |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| Mask | Blue |  |  |  |  | Green |  |  |  |  | Red (LSB) |  |  |  |  |
| m | <font color="blue"> b </font> | <font color="blue"> b </font> | <font color="blue"> b </font> | <font color="blue"> b </font> | <font color="blue"> b </font> | <font color="green"> g </font> | <font color="green"> g </font> | <font color="green"> g </font> | <font color="green"> g </font> | <font color="green"> g </font> | <font color="red"> r </font> | <font color="red"> r </font> | <font color="red"> r </font> | <font color="red"> r </font> | <font color="red"> r </font> |

Palettes generally contain a number of colors that's a multiple of 256. This is because the palette is split up into 256-color 'pages' internally. So the first color is page 0/color 0. Color 256 is page 1/color 0. Color 628 is page 2/color 116. You'll see why in the [background](Background) section.
