---
title: WorldMap_Module
---

## Preamble

The following was originaly described by Tonberry, in qhimm's forum. It was completed by Ficedula sometimes later, who reversed texture data.

Additions in *italics* by Aali

### Two formats

BOT and MAP files are similar; BOT files are redundant and look like optimized versions of the corresponding MAP files.

*MAP file follows the structure described below and is used to load single blocks on demand. BOT file contains the same blocks but arranged to speed up initial load time by storing each block and 3 of its neighboring blocks together. For instance, the data stored for the first 2 blocks is (numbers refer to the MAP layout below): 0,1,9,10 1,2,10,11. This pattern repeats up to block \#62. Replacement blocks 63-68 are divided in groups for each replacement, i.e. block 64 and 65 are part of the same group since they both belong to the Ultima Weapon crater. These groups are then stored using the same algorithm as above, each 4-block group containing a replaced block is written out again. 1-block replacements thus add 4\*4 blocks to the .BOT file while 2-block replacements add 6\*4 blocks. Replacements are to be made **in order**, when writing the data for the Ultima Weapon crater the Temple of the Ancients should be gone and so on. All of this adds up to 63\*4 + 4\*4 + 6\*4 + 4\*4 + 6\*4 = 332 blocks.*

### Content

- WM0 is the above water map.
- WM2 is the underwater (submarine) map.
- WM3 is the snowstorm map.

## MAP Format

### File Structure

A worldmap file is divided in sections of 0xB800 bytes, each section representing a square block of the map.

#### Map Block

Each block consists in 16 meshes, organized in a grid-like fashion:

|     |     |     |     |
|-----|-----|-----|-----|
| 0   | 1   | 2   | 3   |
| 4   | 5   | 6   | 7   |
| 8   | 9   | 10  | 11  |
| 12  | 13  | 14  | 15  |

Map Block mesh arrangement

A block is recorded following the structure (all pointers are expressed in bytes relative to offset 0 of block):

*Pointers have to be aligned to 4-byte boundaries, FF7 ignores the last two bits when reading the file.*

For each m in 16 meshes:

|  size   |              description              |
|:-------:|:-------------------------------------:|
| 4 bytes | Pointer to compressed data for mesh m |

Followed by, for each m in 16 meshes:

|   size   |        description         |
|:--------:|:--------------------------:|
| variable | Compressed data for mesh m |

The data for each mesh is independently compressed using LZSS, so the first 4 bytes are the size in bytes of the compressed data and the rest is the compressed data itself.

#### WM0.MAP

wm0.map contains 68 blocks. The first 63 of them are arranged in a grid-like fashion, made of 7 rows of 9 columns, like this:

|     |     |     |     |     |     |     |     |     |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   |
| 9   | 10  | 11  | 12  | 13  | 14  | 15  | 16  | 17  |
| 18  | 19  | 20  | 21  | 22  | 23  | 24  | 25  | 26  |
| 27  | 28  | 29  | 30  | 31  | 32  | 33  | 34  | 35  |
| 36  | 37  | 38  | 39  | 40  | 41  | 42  | 43  | 44  |
| 45  | 46  | 47  | 48  | 49  | 50  | 51  | 52  | 53  |
| 54  | 55  | 56  | 57  | 58  | 59  | 60  | 61  | 62  |
|     |     |     |     |     |     |     |     |     |

wm0.map block arrangement

The last 5 meshes 63, 64, 65, 66, 67 and 68 replaces meshes 50, 41, 42, 60, 47 and 48 (respectively), according to the story of the game.

### Mesh Structure

A worldmap mesh is recorded like this:

#### Header

|  size   |     description     |
|:-------:|:-------------------:|
| 2 bytes | Number of triangles |
| 2 bytes | Number of vertices  |

Header Structure

`typedef struct`  
`{`  
`  uint16 NumberOfTriangles;`  
`  uint16 NumberOfVertices;`  
`} WorldMeshHeader;`

#### Triangle

<table>
<caption>For each triangle t in <em>number of triangles</em></caption>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>size</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Index of vertex 0 of triangle t</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Index of vertex 1 of triangle t</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Index of vertex 2 of triangle t</p></td>
</tr>
<tr>
<td style="text-align: center;"><p><em>5 bits (lowest)</em></p></td>
<td style="text-align: center;"><p><em>Walkmap status of triangle t (see below)</em></p></td>
</tr>
<tr>
<td style="text-align: center;"><p><em>3 bits</em></p></td>
<td style="text-align: center;"><p><em>Mesh function ID to trigger when this triangle is stepped on.<br />
Values 0-2 mean no script is attached to this triangle.<br />
For values 3+ subtract 3 from this value and this will give you the mesh function ID to trigger.</em></p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate u in texture for vertex 0</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate v in texture for vertex 0</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate u in texture for vertex 1</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate v in texture for vertex 1</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate u in texture for vertex 2</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Coordinate v in texture for vertex 2</p></td>
</tr>
<tr>
<td style="text-align: center;"><p><em>9 bits (lowest)</em></p></td>
<td style="text-align: center;"><p><em>Texture (see below)</em></p></td>
</tr>
<tr>
<td style="text-align: center;"><p><em>1 bit</em></p></td>
<td style="text-align: center;"><p><em>Chocobo tracks flag (if 1 then a chocobo fight can happen on this triangle)</em></p></td>
</tr>
<tr>
<td style="text-align: center;"><p><em>6 bits</em></p></td>
<td style="text-align: center;"><p><em>Region (message ID that will be displayed in menus and savegames, see below)</em></p></td>
</tr>
</tbody>
</table>

`typedef struct`  
`{`  
` uint8 Vertex0Index;`  
` uint8 Vertex1Index;`  
` uint8 Vertex2Index;`  
` `*`uint8 WalkabilityInfo:5;`*  
` `*`uint8 MeshFuncId:3;`*  
` uint8 uVertex0, vVertex0;`  
` uint8 uVertex1, vVertex1;`  
` uint8 uVertex2, vVertex2;`  
` `*`uint16 TextureInfo:9;`*  
` `*`uint16 ChocoboTracks:1;`*  
` `*`uint16 Region:6;`*  
`} WorldMeshTriangle;`

#### Vertex

| size | description |
|:--:|:--:|
| 2 bytes | Coordinate x of vertex v (signed) |
| 2 bytes | Coordinate y of vertex v (signed) |
| 2 bytes | Coordinate z of vertex v (signed) |
| 2 bytes | (Unknown: Coordinate w of vertex v?) *Never used for anything in the PC version.* |

For each vertex v in *number of vertices*

`typedef struct`  
`{`  
`  int16 X, Y, Z;`  
`  uint16 Unused; // fill to fit structure to 32bit boundry`  
`} VertexType;`

#### Normal

| size | description |
|:--:|:--:|
| 2 bytes | Coordinate x of normal for vertex v |
| 2 bytes | Coordinate y of normal for vertex v |
| 2 bytes | Coordinate z of normal for vertex v |
| 2 bytes | (Unknown: Coordinate w of normal for vertex v? "Always 0") *Never used for anything in the PC version.* |

For each vertex v in *number of vertices*

`typedef struct`  
`{`  
`  int16 X, Y, Z;`  
`  uint16 Unused; // fill to fit structure to 32bit boundry`  
`} NormalType;`

structures added by [Cyberman](../User:Cyberman)

### Regions

Each triangle has a region ID that corresponds with the region name showed in the menu and stored in the save files. The names are loaded from the \`mes\` file and are 0-indexed. Below is the English list of valid region names and their IDs:

|  id  |           name           |
|:----:|:------------------------:|
| *0*  |      *Midgar Area*       |
| *1*  |    *Grasslands Area*     |
| *2*  |       *Junon Area*       |
| *3*  |       *Corel Area*       |
| *4*  |    *Gold Saucer Area*    |
| *5*  |      *Gongaga Area*      |
| *6*  |       *Cosmo Area*       |
| *7*  |       *Nibel Area*       |
| *8*  | *Rocket Launch Pad Area* |
| *9*  |       *Wutai Area*       |
| *10* |     *Woodlands Area*     |
| *11* |      *Icicle Area*       |
| *12* |      *Mideel Area*       |
| *13* |    *North Corel Area*    |
| *14* |     *Cactus Island*      |
| *15* |     *Goblin Island*      |
| *16* |      *Round Island*      |
| *17* |          *Sea*           |
| *18* |   *Bottom of the Sea*    |
| *19* |        *Glacier*         |

### Walkmap

*Each triangle can have one of the 32 different walkmap types described below.*

| code | type | description |
|:--:|:--:|:--:|
| *0* | *Grass* | *Most things can go here.* |
| *1* | *Forest* | *No landing here, but anything else goes.* |
| *2* | *Mountain* | *Chocobos and flying machines only.* |
| *3* | *Sea* | *Deep water, only gold chocobo and submarine can go here.* |
| *4* | *River Crossing* | *Buggy, tiny bronco and water-capable chocobos.* |
| *5* | *River* | *Tiny bronco and chocobos.* |
| *6* | *Water* | *Shallow water, same as above.* |
| *7* | *Swamp* | *Midgar zolom can only move in swamp areas.* |
| *8* | *Desert* | *No landing.* |
| *9* | *Wasteland* | *Found around Midgar, Wutai and misc other. No landing.* |
| *10* | *Snow* | *Leaves footprints, no landing.* |
| *11* | *Riverside* | *Beach-like area where river and land meet.* |
| *12* | *Cliff* | *Sharp drop, usually where the player can be on either side.* |
| *13* | *Corel Bridge* | *Tiny bridge over the waterfall from Costa del Sol to Corel.* |
| *14* | *Wutai Bridge* | *Rickety rope bridges south of Wutai.* |
| *15* | *Unused* | *Doesn't seem to be used anywhere in the original data.* |
| *16* | *Hill side* | *This is the tiny walkable part at the foot of a mountain.* |
| *17* | *Beach* | *Where land and shallow water meets.* |
| *18* | *Sub Pen* | *Only place where you can enter/exit the submarine.* |
| *19* | *Canyon* | *The ground in cosmo canyon has this type, walkability seems to be the same as wasteland.* |
| *20* | *Mountain Pass* | *The small path through the mountains connecting Costa del Sol and Corel.* |
| *21* | *Unknown* | *Present around bridges and the Northern Crater, may have some special meaning.* |
| *22* | *Waterfall* | *River type where the tiny bronco can't go.* |
| *23* | *Unused* | *Doesn't seem to be used anywhere in the original data.* |
| *24* | *Gold Saucer Desert* | *Special desert type for the golden saucer.* |
| *25* | *Jungle* | *Walkability same as forest, used in southern parts of the map.* |
| *26* | *Sea (2)* | *Special type of deep water, only used in one small spot next to HP-MP cave, possibly related to the underwater map/submarine.* |
| *27* | *Northern Cave* | *Inside part of the crater, where you can land the highwind.* |
| *28* | *Gold Saucer Desert Border* | *Narrow strip of land surrounding the golden saucer desert. Probably related to the "quicksand" script.* |
| *29* | *Bridgehead* | *Small area at both ends of every bridge. May have some special meaning.* |
| *30* | *Back Entrance* | *Special type that can be set unwalkable from the script.* |
| *31* | *Unused* | *Doesn't seem to be used anywhere in the original data.* |

### Texture

The lower 9 bits contain a texture number (0-511, but only 0-281 appear to be used). *Unfortunately, knowing which texture to use is not enough, the UV coordinates found in the mesh data are (presumably) the original PSX VRAM coordinates, so to get the real coordinates you must subtract a texture-specific offset from each of the UV pairs. A complete table with every texture, its original size and offsets can be found [here](WorldMap_Module/TextureTable). Sometimes you will end up with negative values after subtracting the offsets, this is normal, the texture should be assumed to repeat itself indefinitely in all directions.*
