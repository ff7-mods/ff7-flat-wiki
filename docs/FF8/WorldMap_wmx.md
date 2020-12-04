---
title: WorldMap_wmx
---

By MaKiPL, Updated 27.5.2016 by Halfer. All thanks goes to Halfer, for rich research progress on world map file. This wiki page is also based on Blue's wmx2obj source code.

## General

Wmx.obj is world map geometry model only. Contains 835 segments, does not contain textures nor additional info like general header or pointers. Collision is calculated directly from faces. Towns and places on map are part of world map and are created the same way as mountains, ground etc. File size is 0x9000\*835. Every 0x9000 a next segments starts.

Segment = contains 16 blocks

Block = contains geometry

One segment is 0x9000 or 36864 bytes long. There are 16 blocks in a segment. In theory, a segment can hold 16 blocks which each hold 0x900 bytes of data.

1-768 segments are final world map. 769-835 are story based segments like Balamb garden stationary, no Esthar, No cities in DISC4.

## Segment

Segment starts with a header (consist offsets for every block). After segment's header blocks data appears.

  

| Offset | Length   | Description |
|--------|----------|-------------|
| 0      | 68 bytes | Header data |
| 68     | varies   | Block data  |

  

### Header data

| Offset | Length            | Description                                       |
|--------|-------------------|---------------------------------------------------|
| 0      | 4 bytes           | group ID                                          |
| 4      | 64 (16 \* uint32) | Offsets to blocks position. 4 bytes every offset! |

Group ID can be one of theses values:

`0: Trabia`  
`1: Balamb + Fisherman's Horizon`  
`2: Esthar West`  
`3: Esthar South East + Laboratory`  
`4: Mordor + Esthar North`  
`5: Centra`  
`6: Galbadia borders (Deling City, Timber, Dollet, Winhill...)`  
`7: Galbadia middle (GGU, Prison, highlands...)`  
`255: Seas`

## Block

### Block data

General structure of a block

| Offset                                 | Length                                       | Description |
|----------------------------------------|----------------------------------------------|-------------|
| 0                                      | 4 Bytes                                      | Header      |
| 4                                      | Polygon count \* polygon length (see header) | Polygons    |
| Header + Polygons                      | Vertice count \* vertice length (see header) | Vertices    |
| Header + Polygons + Vertices           | Normal count \* normal length (see header)   | Normals     |
| Header + Polygons + Vertices + Normals | 4 Bytes                                      | Padding     |

**Header** (4 Bytes):

| Offset | Length | Description    |
|--------|--------|----------------|
| 0      | Byte   | Polygon count  |
| 1      | Byte   | Vertices count |
| 2      | Byte   | Normals count  |
| 3      | Byte   | (Padding)      |

**Polygon** (16 bytes):

| Offset | Length      | Description               |
|--------|-------------|---------------------------|
| 0      | Byte        | F1 (Triangle 1)           |
| 1      | Byte        | F2 (Triangle 1)           |
| 2      | Byte        | F3 (Triangle 1)           |
| 3      | Byte        | N1 (Normal Indice for F1) |
| 4      | Byte        | N2 (Normal Indice for F2) |
| 5      | Byte        | N3 (Normal Indice for F3) |
| 6      | Byte        | U1                        |
| 7      | Byte        | V1                        |
| 8      | Byte        | U2                        |
| 9      | Byte        | V2                        |
| 10     | Byte        | U3                        |
| 11     | Byte        | V3                        |
| 12     | 4 BIT/4 BIT | Texture Page/CLUT id      |
| 13     | Byte        | Ground type               |
| 14     | Byte        | Unknown                   |
| 15     | Byte        | Unknown                   |

**Vertex and Normal** (8 bytes):

| Offset | Length | Description |
|--------|--------|-------------|
| 0      | short  | X           |
| 2      | short  | -Z          |
| 4      | short  | Y           |
| 6      | short  | (Padding)   |

## Block explained

Final Fantasy 8's world map is pretty much sea all around. One sea block or as I like to call it water block is made of 32 polygons, which are always triangles. The data is pretty straight forward to read with the above information. One thing to note is, that there is only 1 normal which points upwards in water block.

In FF8's world data, a segment location is predefined in currently unknown place (in engine or wmset.obj) and there are horizontally 32 and vertically 24 segments to form the world map. Each block in segments follows to same logic with 4x4 grid instead of 32x24. The first block starts from the upper left corner of the segment.

Each block have their own local bounding box, which the vertice values follow. A blocks origin is always predefined to start from upper left corner of its bounding box. This bounding box is always a size of 2048x2048 units (up and down limit is not known). This means that 2048 units or 0x800 is the local max for vertices coordinate before it overlaps with next blocks bounding box. There are no limitation to overlapping, you can extend a blocks geometry out of its bounding box and even out of the local segment. However, the collision is always calculated from the block which bounding box you are in, so extending a blocks geometry out of its bounding box doesn't make it collidable in overlapping block.
