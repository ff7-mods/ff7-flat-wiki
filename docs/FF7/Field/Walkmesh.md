---
title: Walkmesh
---

### Section 5: Walkmesh ([Kero](../../User:Kero)

![Wutai Walkmesh]({{site.baseurl}}/assets/Field_Wutai.jpg)

Every every offset is here relative, 00 is at the start of section 5 (after length indicator).

Section 5 of field files is a stored walkmesh. A walkmesh is a mesh of polygons on which characters move, telling the engine for example how high it is, and using this the character can, for example, cross bridges with the real feeling that in the middle he is at a higher place than on the sides. It has very simple structure.

| Offset | Name | Data Type | Length | Description |
|----|----|----|----|----|
| 0x0000 | NoS | DWORD | 0x04 | Number of Sectors |
| 0x0004 | Sector Pool (SP) | DWORD | 24 \* NoS | The data pool of Secots |
| 0x0004 + 24 \* NoS | Sector Access Pool (SAP) | WORD\[3\] | 6 \* NoS | ID of triangle of each Edge |

#### Section 5 Header

Startofs 0x00 Length 0x04

The walkmesh information is preceeded by a DWORD (4 bytes) unsigned int, named **NoS**, short for the Number of Sectors in the walkmesh.

#### Sector pool

Startofs 0x04 Length NoS\*24

`typedef struct {`  
`   short x,y,z,res;        // short is a 2 byte signed integer`  
`} vertex_3s;           // 3s == 3 short although there are 4 this is for 32 bit data alignment in PSX`

`typedef struct {`  
`   vertex_3s v[3];     // a triangle has 3 vertices`  
`} sect_t;          // Sector Type`

The pool consists of sectors, which are in fact triangles, each with their vertices position. For each sector there are 3 vertices (3 vertex_3s). Res is always equal to v\[0\].z (it is just a padding value). The polygons are 'wound' clockwise, this makes determining if a point is within a triangle easier.

#### Access pool

Startofs 0x04 + NoS\*24 Length NoS\*6

`typedef {`  
`   short acces1,acces2,acces3;`  
`}`

The access pool is an array of access data (ID's of triangles in the Mesh) in the mesh, the ID is the triangle you should be in if you cross that edge.

acces1 is for line from vertex 0 to 1 acces2 is for line from vertex 1 to 2 acces3 is for line from vertex 2 to 0

If the edge value is 0xFFFF, than this edge cannot be crossed (it's blocked). The access pool and sector pool have the same number of entries, thus you use the same index value for both pools of data to access the data for the same triangle. The access data merely informs one that if the PC object crosses this line the object should be in the indentified triangle. FF7 will halt running if you are not in the **access** specified triangle.
