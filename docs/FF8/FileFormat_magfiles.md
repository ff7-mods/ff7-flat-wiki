---
title: FileFormat_magfiles
---

By MaKiPL

------------------------------------------------------------------------

There is no unified format for MAG files. Every file has their own naming, even extension. You can't really distinguish them.

Files starting with 10 00 00 00 09 00 00 00 are obviously TIM texture. Files starting with null 4 bytes are in most cases "Packed magic file"

## Packed magic file

| Offset | Description                                  |
|--------|----------------------------------------------|
| 0x00   | Probably always null                         |
| 0x04   | Probably bones/animation data                |
| 0x08   | Unknown (used to determinate texture size\*) |
| 0x0C   | Geometry pointer                             |
| 0x10   | SCOT pointer                                 |
| 0x14   | Texture pointer                              |

## G.F. Sequence

<http://forums.qhimm.com/index.php?topic=15056.0>

## Environment objects

**I'm aware it's chaotic**, like no tables and etc. but it's **up-to-date** information First, recognize file:

1.Jump to pointer at 0xC \[Global\]

2.This int indicates pointer count. Example: 10 00 00 00 is 16 pointers

3.If pointer is 00 00 00 00, just ignore it and move forward

4.After noting all pointers that are not 00 00 00 00 (therefore inspecting Count\*4 bytes) just jump to selected one \[Relative jump from count int\]

5.See third int (8th byte) for UNKNOWN(POLYGON TYPES see below) \[Relative jump from 03 00 00 00\]

6.Read int at 20th byte for VERTICES offset \[Relative jump from 03 00 00 00\]

7.Read int at 24th byte for VERTICES COUNT \[Vertex is 8 bytes! X Z Y W, where W is probably weight byte \[as in OBJ specification\] and is normally unused (as usual, even in casual OBJ files)\]

Example: 09 00 9f 01 means there's 9f 01 (415) polygons of type 0x9. Therefore: 28\*415=11620 bytes to next polygon type or vertices if FF FF FF FF.

GF Environment (stages like Cerberus gate; Alexander backdrop and etc.) geometry contains many polygon types (sic!). Every single polygon type is different than other.

`       private int[] _knownPolygons = new int[] `  
`       {`  
`           0x2,`  
`           0x6,`  
`           0x7,`  
`           0x8,`  
`           0x9,`  
`           0xC,`  
`           0x10,`  
`           0x12,`  
`           0x11,`  
`           0x13,`  
`       };`

0xC points to geometry section. If \*0xC (pointers to geometries) is == 0, then file has no geometry (it is possible. Some files are only texture, some only geometry, some are only animation and some are everything). There should be no single case where the number of models in file exceed 12.

`0xC:`  
` PointersToModel:`  
`    Example object (let's call it modOffset)`

`uint _objCount = *modOffset;`  
`ushort _vertexCount = *(modOffset + 24);`  
`ushort _verticesOffset = *(modOffset + 20);`

Polygon parsing based on types (C\#):

`int relativeJump = *(modOffset + 8);`  
`int *localoffset = modOffset + _relativeJump + 4;`

`               if (polygonType == 0x02)`  
`               {`  
`                   for (int i = 0; i < polygons * 20; i += 20)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 0xC)} {GetPolygon(localoffset + i + 0xE)} {GetPolygon(localoffset + i + 0x10)}\n";`  
`                   }`  
`                   safeHandle = polygons * 20;`  
`               }`

`               if (polygonType == 0x06)`  
`               {`  
`                   for (int i = 0; i < polygons * 12; i += 12)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 0x4)} {GetPolygon(localoffset + i + 0x6)} {GetPolygon(localoffset + i + 0x08)}\n";`  
`                   }`  
`                   safeHandle = polygons * 12;`  
`               }`

`               if (polygonType == 0x07)`  
`               {`  
`                   for (int i = 0; i < polygons * 20; i += 20)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 0xC)} {GetPolygon(localoffset + i + 0xE)} {GetPolygon(localoffset + i + 0x10)}\n";`  
`                   }`  
`                   safeHandle = polygons * 20;`  
`               }`

`               if (polygonType == 0x09)`  
`               {`  
`                   for (int i = 0; i < polygons * 28; i += 28)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 18)} {GetPolygon(localoffset + i + 20)} {GetPolygon(localoffset + i + 22)}\n";`  
`                   }`  
`                   safeHandle = polygons * 28;`  
`               }`

`               if (polygonType == 0x08)`  
`               {`  
`                   for (int i = 0; i < polygons * 20; i += 20)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 0xA)} {GetPolygon(localoffset + i + 0xC)} {GetPolygon(localoffset + i + 0xE)}\n";`  
`                   }`  
`                   safeHandle = polygons * 20;`  
`               }`

`               if (polygonType == 12)`  
`               {`  
`                   for (int i = 0; i < polygons * 28; i += 28)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 20)} {GetPolygon(localoffset + i + 22)} {GetPolygon(localoffset + i + 26)} {GetPolygon(localoffset + i + 24)}\n";`  
`                   }`  
`                   safeHandle = polygons * 28;`  
`               }`

`               if (polygonType == 0x12)`  
`               {`  
`                   for (int i = 0; i < polygons * 24; i += 24)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 12)} {GetPolygon(localoffset + i + 14)} {GetPolygon(localoffset + i + 18)} {GetPolygon(localoffset + i + 16)}\n";`  
`                   }`  
`                   safeHandle = polygons * 24;`  
`               }`

`               if (polygonType == 0x13)`  
`               {`  
`                   for (int i = 0; i < polygons * 36; i += 36)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 24)} {GetPolygon(localoffset + i + 26)} {GetPolygon(localoffset + i + 30)} {GetPolygon(localoffset + i + 28)}\n";`  
`                   }`  
`                   safeHandle = polygons * 36;`  
`               }`

`               if (polygonType == 0x11)`  
`               {`  
`                   for (int i = 0; i < polygons * 24; i += 24)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 16)} {GetPolygon(localoffset + i + 18)} {GetPolygon(localoffset + i + 22)} {GetPolygon(localoffset + i + 20)}\n";`  
`                   }`  
`                   safeHandle = polygons * 24;`  
`               }`

`               if (polygonType == 0x10)`  
`               {`  
`                   for (int i = 0; i < polygons * 12; i += 12)`  
`                   {`  
`                       f += $"f {GetPolygon(localoffset + i + 4)} {GetPolygon(localoffset + i + 6)} {GetPolygon(localoffset + i + 10)} {GetPolygon(localoffset + i + 8)}\n";`  
`                   }`  
`                   safeHandle = polygons * 12;`  
`               }`

`               uint isNext = *(localoffset + safeHandle);`  
`               if (isNext == 0xFFFFFFFF) //FFFFFFFF breaks the polygons reading`  
`                   break;`

Vertex:

`short x`  
`short z`  
`short y`  
`short w //rarely used, for skeleton weighting`

## Textures

1\. See 0x08, it points almost always to null data, but also indicates where to stop watching texture pointers

2\. Jump to pointer 0x14 (almost always 0x30)

3\. Note all pointers if not zero until streamPosition==\*(0x08)

4\. If no pointers, file has no texture.

5\. Jump to texture (pointer+\*(0x14)) e.g. 48+21675

6\. There's no sizes, so if there's another texture after the one you're getting, then subdivide next texture position from current position to get size and determine texture resolution. If it's the last texture, then it gets a bit tricky, as in many ways the file is not ending with texture but SCOT for example..

Texture is **8BPP** (does not contain palette/monochromatic) (one byte is all three channels in 24RGB manner)

**Texture resolution is based on size:**

| Texture byte size | Texture final resolution |
|-------------------|--------------------------|
| 0x2000            | 64x64 (or 32x32)\*       |
| 0x4000            | 128x128 (or 64x64)\*     |
| 0x8000            | 256x256 (or 128x128)\*   |
| 0x10000           | 256x256                  |

GFs uses higher texture resolution, for example 0x2000 is 64x64 instead of 32x32, but many magic texture like fire effect animation atlas texture is using the lower resolution (the one with asterisk \*, for example 0x2000 for fire atlas animation texture it's 32x32 instead of 64x64)

## SCOT

Related to sound transition effect. Structure is completely unknown.
