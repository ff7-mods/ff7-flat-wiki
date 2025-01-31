---
title: Tile_Map
---

## Background Tile Map

--[Cyberman](User:Cyberman "wikilink") 17:17, 27 Nov 2006 (CST) & --[Myst6re](../../../User:Myst6re)

The background tile map information on the PSX is actually stored in 2 files. The graphic tiles are in a MIM file with the same name as the DAT file. Both are needed to view the background data completely. This section covers just the Tile Map information and not how to decode the MIM data. The Tile Map consists of 5 subsections. The header for the tile map consists of 4 offsets which are relative to the begining of the section. The first section always starts at offset 0x0010, it is not in the header.

| Offset | Size  | Description                          |
|--------|-------|--------------------------------------|
| 0x0000 | DWORD | 1st layer Information (Section 2)    |
| 0x0004 | DWORD | Texture Page Data (Section 3)        |
| 0x0008 | DWORD | Sprite Layer Information (Section 4) |
| 0x000C | DWORD | 3th Layer Information (Section 5)    |

  

### Section 1

A list of data structures (size == 6 or 2 bytes). The first UINT16 indicates layer or not a layer.

`struct {`  
` UINT16 Type;`  
` UINT16 TilePos;`  
` UINT16 TileCount;`  
`} Section1LayerChange;`  
`Type 0x7FFE is a sprite use Section 3 to find it's texture page.`  
`Type 0x7FFF is the End of layer information Data Record.`

### Section 2

A series of Layer 1 tile data structures (basic background information)

`struct {`  
` INT16 DestinationX;`  
` INT16 DestinationY;`  
` UINT8 TexPageSourceX;`  
` UINT8 TexPageSourceY;`  
` UINT16 TileClutData;`  
`} Layer1Tile;`

Destination X and Y are signed, this is used for the walkmesh information and the center of the background field. The only used portion of the tile data is:

`{`  
` unsigned ZZ1:6;`  
` unsigned ClutNumber;`  
` unsigned ZZ2:6;`  
`} TileClutData;`

### Section 3

A list of UINT16, bit fields, because the ordering of fields within such an object are unspecifiable in the C and C++ standards (IE the compilor can choose any way which it may be done the standard doesn't care), this structure will be shown (a BIT?) differently.

`{`  
`  unsigned ZZ:7; // 7 MSB`  
`  unsigned deph:2;`  
`  unsigned blending_mode:2;`  
`  unsigned page_y:1;`  
`  unsigned page_x:4; // 4 LSB`  
`} SpriteTP_Blend;`

### Section 4

This section consists of the sprite data (2d data that is either non static or can be walked behind).

`struct {`  
` INT16 DestinationX;`  
` INT16 DestinationY;`  
` UINT8 TexPageSourceX;`  
` UINT8 TexPageSourceY;`  
` UINT16 TileClutData;`  
` UINT16 SpriteTP_Blend;`  
` UINT16 Group; // 12 lsb bits only`  
` UINT8 Parameter;`  
` UINT8 State;`  
`} SpriteTile;`

Destination X and Y are signed, this is used for the walkmesh information and the center of the background field.

Tile Color Lookup Table Data

`{`  
` unsigned ZZ1:6;`  
` unsigned ClutNumber;`  
` unsigned ZZ2:6;`  
`} TileClutData;`

Sprite Texture Page and Blending Mode data

`{`  
`  unsigned ZZ:7; // 7 MSB`  
`  unsigned deph:2;`  
`  unsigned blending_mode:2;`  
`  unsigned page_y:1;`  
`  unsigned page_x:4; // 4 LSB`  
`} SpriteTP_Blend;`

Parameter structure

`{`  
`  unsigned blending:1; // MSB`  
`  unsigned param_id:7; // LSB`  
`} Parameter;`

### Section 5

This section looks like section 4, it is used for additional layers. For SpriteTP_Blend infos, you must use section 3.

`struct {`  
` INT16 DestinationX;`  
` INT16 DestinationY;`  
` UINT8 TexPageSourceX;`  
` UINT8 TexPageSourceY;`  
` UINT16 TileClutData;`  
` UINT8 Parameter;`  
` UINT8 State;`  
`} SpriteTile2;`
