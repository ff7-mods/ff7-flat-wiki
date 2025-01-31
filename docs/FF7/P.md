---
title: P
---

This page describes format of P files.

'P file' is a binary file containing data which form 3D model. File specifies model's vertices, polygons, colors, texture coordinates and model sub-groups. File does not specify references to the texture files, animations, model skeleton or anything else.

P-files are used as parts of field models, battle models, battle locations on PC version of FF7.

*Feel free to add more information.*

![Ff7field3dfiles.png]({{site.baseurl}}/assets/Ff7field3dfiles.png)

------------------------------------------------------------------------

## "P" Polygon File Format

This is a short diagram of the file structure

`.p-File`  
`   |`  
`   +- Header`  
`   |`  
`   +- Vertices[]`  
`   |`  
`   +- Normals[]`  
`   |`  
`   +- Unknown1[]`  
`   |`  
`   +- Texture Coords[]`  
`   |`  
`   +- Vertice Colors[]`  
`   |`  
`   +- Polygon Colors[]`  
`   |`  
`   +- Edges[]`  
`   |`  
`   +- Polygons[]`  
`   |`  
`   +- Unknown2[]`  
`   |`  
`   +- Unknown3[]`  
`   |`  
`   +- Hundreds[]`  
`   |`  
`   +- Groups[]`  
`   |`  
`   +- BoundingBoxes[]`  
`   |`  
`   +- Normal Index Table[]`  
  
`[] = a variable-sized array`

  

------------------------------------------------------------------------

### .P File Header

The .p files have a 128-Byte-long Header. The following is the known structure of the header.

| Off | 00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 0A | 0B | 0C | 0D | 0E | 0F |
|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
| 00 | Version |  |  |  | 01 | 00 | 00 | 00 | VertexType |  |  |  | NumVertices |  |  |  |
| 10 | NumNormals |  |  |  | NumUnknown1 |  |  |  | NumTexCoords |  |  |  | NumVertexColors |  |  |  |
| 20 | NumEdges |  |  |  | NumPolygons |  |  |  | NumUnknown2 |  |  |  | NumUnknown3 |  |  |  |
| 30 | NumHundreds |  |  |  | NumGroups |  |  |  | NumBoundingBoxes |  |  |  | NormIndexTableFlag |  |  |  |

**Table 1: P File header**

All Values, that can be read out in this part of the header are 4-Byte-Integers

This 64 bytes long header is followed by 64 bytes of runtime data which are to be skipped.

`typedef struct`  
`{`  
`     long Version;`  
`     long off04;`  
`     long VertexType;`  
`     long NumVertices;`  
`     long NumNormals;`  
`     long NumUnknown1;`  
`     long NumTexCs;`  
`     long NumVertexColors;`  
`     long NumEdges;`  
`     long NumPolys;`  
`     long NumUnknown2;`  
`     long NumUnknown3;`  
`     long NumHundreds;`  
`     long NumGroups;`  
`     long NumBoundingBoxes;`  
`     long NormIndexTableFlag;`  
`     long runtime_data[16];`  
`} `  
`t_p_header;`

Here are the meanings of values from header:

|  |  |
|----|----|
| VertexType | Specifies the type of vertices this file contains, should always be 1 (which translates into LVERTEX in the D3D driver) 0 translates into VERTEX, which looks the same as LVERTEX but is never used in the original FF7 data. 2 translates into TLVERTEX, you don't want this unless you know exactly what it does. |
| NumVerts | Number of Vertices |
| NumNormals | Number of Normals (always 0 in Battle files) |
| NumTexCs | Number of Texture Coords |
| NumVertexColors | Number of Vertex Colors |
| NumEdges | Number of Edges |
| NumPolys | Number of Polygons |
| NumHundreds | Number of Hundreds (Someone should really come up with a better name for this) |
| NumGroups | Number of Groups |
| NumBoundingBoxes | Number of Bounding Boxes |

  

### Vertices

Vertices are stored as array of structure â€˜vertexâ€™ below, which is triplet of float numbers. Numbers specify point in 3D space. Size of this array is specified in header. Size of vertex section is ( 12 \* NumVertices ). Section is allways present in the file.

`struct s_vertex {`  
`    float              x, y, z;`  
`}  vertex;`

// structure size = 12 bytes

  

### Vertex normals

Same format as vertices. Though, each of coordinate means vertex normal orientation instead of position. Size of this section is ( 12 \* NumNormals ).

  

### Unknown1

Same format as vertices. No idea what this is used for. Size of this section is ( 12 \* NumUnknown1 ).

  

### Texture coordinates

Array of vertex texture coordinates. Size of this section is ( 8 \* NumTexCoords ). Texture coord references are to be read through group information.

  

### Vertex colors

Vertex colors are stored as array of colors, each color is specified by four bytes. Color is in B8G8R8A8 format, that means that first byte specifies Blue, second specifies Green, third specifies Red and fourth specifies Alpha. Alpha byte has usually value â€˜255â€™, so its at full opacity. Size of this section is ( 4 \* NumVertexColors ).

  

### Polygon colors

Polygon colors are stored in the same manner as vertex colors. Size of this section is ( 4 \* NumPolygons ).

  

### Edges

Specifies edges, not really useful. Each index has value in range 0 .. NumVertices. Size of this section is ( 4 \* NumEdges ).

  

### Polygons

Array of polygon definitions. I know only meaning of values which specify vertex indexes. Vertex indexes canâ€™t be used directly to select vertices, you have first to read group information, there you will find information on which polygons and vertices you should be used to form a model part. Polygons have group-relative indexes to vertices (that means that in each group these indexes start from 0 ). Size of this section is ( 24 \* NumPolygons ).

`struct {`  
`    unsigned short     zero, VertexIndex[3], NormalIndex[3], EdgeIndex[3], u[2];`  
`} Ppolygon;`

| Off | 00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 0A | 0B | 0C | 0D | 0E | 0F |
|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
| 00 | 00 00 |  | VertexIndex1 |  | VertexIndex2 |  | VertexIndex3 |  | NormalIndex1 |  | NormalIndex2 |  | NormalIndex3 |  | EdgeIndex1 |  |
| 10 | EdgeIndex2 |  | EdgeIndex3 |  | u1 |  | u2 |  |  |  |  |  |  |  |  |  |

**Table 1: Structure of single polygon data**

  

### Unknown2

(Probably)Same format as polygons. No idea what this is used for. Size of this section is ( 24 \* NumUnknown2 ).

  

### Unknown3

No idea what this is used for. Size of this section is ( 3 \* NumUnknown3 ).

  

### Hundreds

Complex structure that specifies render state (texturing, blend modes, culling, filtering, depth testing, depth masking, shademode etc) Contact me (Aali) for more information.

  

### Groups

| Off | 00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 0A | 0B | 0C | 0D | 0E | 0F |
|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|----|
| 00 | PrimitiveType |  |  |  | PolygonStartIndex |  |  |  | NumPolygons |  |  |  | VerticesStartIndex |  |  |  |
| 10 | NumVertices |  |  |  | EdgeStartIndex |  |  |  | NumEdges |  |  |  | ? |  |  |  |
| 20 | ? |  |  |  | ? |  |  |  | ? |  |  |  | TexCoordStartIndex |  |  |  |
| 30 | AreTexturesUsed |  |  |  | TextureNumber |  |  |  |  |  |  |  |  |  |  |  |

**Table 1: Structure of single 'groups' record**

  

`struct {`  
`   unsigned long    PrimitiveType;`  
`   unsigned long    PolygonStartIndex;`  
`   unsigned long    NumPolygons;`  
`   unsigned long    VerticesStartIndex;`  
`   unsigned long    NumVertices;`  
`   unsigned long    EdgeStartIndex;`  
`   unsigned long    NumEdges;`  
`   unsigned long    u1;`  
`   unsigned long    u2;`  
`   unsigned long    u3;`  
`   unsigned long    u4;`  
`   unsigned long    TexCoordStartIndex;`  
`   unsigned long    AreTexturesUsed;`  
`   unsigned long    TextureNumber;`  
`} group; `  
`// also called pool56, size is 56 bytes`

Section contains array of group information. Each group specifies group of polygons. To read this groupâ€™s geometry you have to read polygons from polygon segment. First polygon is one with index *group.PolygonStartIndex*, number of polygons is defined by *group.NumPolygons*. Polygon has indexes of vertices. These indexes are group-relative and that means that you have to add *group.VerticesStartIndex* to each vertex index. Itâ€™s the same with vertex texture coords. Their indexes are group-relative too, to each index you have to add *group.TexCoordStartIndex*.

If *group.textures_used* is equal 1 then texture is applied on all polygons of current group. If its 0 there is no texture. If its 1 then *group.TextureNumber* defines which texture to use on polygons. Though, texture name is not specified inside the P-file, it is specified in HRC or DA file, which loads model as a whole ( it points to texture files, P-files, animation files etc.) Size of this section is ( 56 \* NumGroups ).

### Bounding box

Six 4-byte floats in order max( x, y, z ), min( x, y, z ). Sometimes just zeroes. Size of this section is 24 bytes \* NumBoundingBoxes.

  

### Normal index table

Not used anywhere. Size of this section is ( 4 \* NumVertices ).
