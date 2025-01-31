---
title: TXZ
---

## WM0.TXZ

The following information applies specifically to WM0.TXZ, it is reasonable to assume that the rest of the TXZ files use a similar format, where WM2.TXZ and WM3.TXZ presumably holds equivalent data for the underwater and snowfield maps respectively.

### Compression

TXZ files are compressed using standard LZS compression where the first 4 bytes contain the size of the compressed data.

### TXZ archive format

Uncompressed TXZ files are divided into several different sections, to extract the different sections a header must be parsed at the beginning of the file. The first 4 bytes will tell you how many sections there are. After that follows 4 \* <number of sections> bytes containing offsets into the file for each section. A section can be assumed to end where the next section begins and the last section runs until the end of the file. Offsets do not include the first 4 bytes of the file! Add 4 to get the actual file offset for each section.

## Sections

### WM0.TXZ, section 0

Unknown format, might be a model? Looks like there's atleast one or two textures in there.

### WM0.TXZ, section 1

Texture data for direct VRAM upload, same format as section 2 but contains only a single block.

### WM0.TXZ, section 2

Texture data for the worldmap mesh (see .MAP format), starts with a table of 512 palette/texture identifiers in a format compatible with the PSX GPU, see <http://psx.rules.org/gpu.txt> for more information.

The following structure can be used to read this data:

`struct wm_texture`  
`{`  
`   unsigned int clutx:6;`  
`   unsigned int cluty:10;`  
`   unsigned int tx:4;`  
`   unsigned int ty:1;`  
`   unsigned int abr:2;`  
`   unsigned int tp:2;`  
`   unsigned int reserved:7;`  
`};`

Texture IDs are the same for the PSX and PC version which means that this table maps 1:1 to the table of PC textures which can be found here: [FF7/WorldMap_Module/TextureTable](../WorldMap_Module/TextureTable)

After this table follows a number of blocks intended for direct VRAM upload, each block has the following structure:

|            size            |              description              |
|:--------------------------:|:-------------------------------------:|
|          4 bytes           | Size of this block (including header) |
|          2 bytes           |       Destination X coordinate        |
|          2 bytes           |       Destination Y coordinate        |
|          2 bytes           |                 Width                 |
|          2 bytes           |                Height                 |
| Width \* Height \* 2 bytes |              Pixel data               |

VRAM Block

A new block can be assumed to start where the previous one ends until the end of this section is reached.

### WM0.TXZ, section 3

Unknown format, contains more blocks of VRAM data.

### WM0.TXZ, section 4

Contains the script for the overworld map, a copy of the data in wm0.ev?

### WM0.TXZ, section 5-11

These sections contain songs in standard AKAO format. Presumably the different overworld background themes are in there, don't know what else?
