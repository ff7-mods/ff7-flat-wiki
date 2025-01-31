---
title: Battle_model_format_(PSX)
---

## Playstation battle model format

The entire file is compressed using [LZS format](FF7/LZS_format "wikilink") and is decompressed into the playstation user memory for a battle. The file consists of several section blocks, a header, compiled HRC and model information, battle animations, a texture image in [TIM format](../PSX/TIM_format), and optional weapon models. All integers short or long are little endian based. This includes some of the [animation data](animation_format) as well.

  

### Battle model header

The header section is a sequence of little endian 32 bit unsigned integers. The first integer (entitled SectionCount) contains the number of pointers offset from the beginning of the file. The remaining integers are SectionCount number of pointers.

<table>
<tbody>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Offset<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Size<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Description<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>000000<br />
</p></td>
<td style="vertical-align: top"><p>4 bytes long<br />
</p></td>
<td style="vertical-align: top"><p>Number of Sections<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>N*4<br />
</p></td>
<td style="vertical-align: top"><p>4 bytes long<br />
</p></td>
<td style="vertical-align: top"><p>Pointer to each section of data.<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>(N+1)*4<br />
</p></td>
<td style="vertical-align: top"><p>Varies<br />
</p></td>
<td style="vertical-align: top"><p>First section of data, this is the actual 3d data for the model.<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>(N+2)*4<br />
</p></td>
<td style="vertical-align: top"><p>Varies<br />
</p></td>
<td style="vertical-align: top"><p>First animation for the model.<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>unknown<br />
</p></td>
<td style="vertical-align: top"><p>Varies<br />
</p></td>
<td style="vertical-align: top"><p>Tim image information often 4bpp sometimes 8bpp # of cluts varies<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; text-align: center; vertical-align: middle"><p>unknown<br />
</p></td>
<td style="vertical-align: top"><p>Varies<br />
</p></td>
<td style="vertical-align: top"><p>Battle weapon models for characters go here they have identical format to the first section, save they do not have textured polygons<br />
</p></td>
</tr>
</tbody>
</table>

### Battle model HRC/model information

This is the first section and consists of real model data and bone structure. Without the animation information the model CANNOT be displayed properly.

#### HRC data

This data resembles [Hierarchy files (.HRC)](../PSX/HRC):

`typedef struct`  
`{`  
`   uint16 Parent;`  
`   int16  Length;`  
`   uint32 Offset;`  
`} FF7_bone;`

Where offset is relative to the begining of the section. If Offset is 0 then the object is a **Joint** otherwise it's a bone. All FF7 bone lengths are negative.

**HRC Table structure**

<table>
<tbody>
<tr>
<td style="width: 76px; vertical-align: middle; background-color: rgb(204, 204, 204); text-align: center"><p>Offset<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Size<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Description<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000000<br />
</p></td>
<td style="vertical-align: top"><p>4 bytes long<br />
</p></td>
<td style="vertical-align: top"><p>Number of Bones<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000004<br />
</p></td>
<td style="vertical-align: top"><p>8 bytes<br />
</p></td>
<td style="vertical-align: top"><p>root bone (always 0 values)<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>000008<br />
</p></td>
<td style="vertical-align: top"><p>8*N bytes<br />
</p></td>
<td style="vertical-align: top"><p>ï¿½Bones and joints of model<br />
</p></td>
</tr>
</tbody>
</table>

**Bone Structure**

<table>
<tbody>
<tr>
<td style="width: 76px; vertical-align: middle; background-color: rgb(204, 204, 204); text-align: center"><p>Offset<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Size<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Description<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000000<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Parent Bone<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000002<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (signed)<br />
</p></td>
<td style="vertical-align: top"><p>Bone Length<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>000004<br />
</p></td>
<td style="vertical-align: top"><p>4 bytes<br />
</p></td>
<td style="vertical-align: top"><p>ï¿½Offset to bone data object is a joint if 0<br />
</p></td>
</tr>
</tbody>
</table>

#### Model information

Following the HRC Data is the model information, these are referenced by offsets in the **Bone** structure. Each bone has it's own model section specific too it. Each bone section has the following information uint32 VertexCount (int bytes), Vertices, Textured Triangle Count (Poly Count Structure), Textured Triangles, Textured Quadric Count (PCS), Textured Quadrics, Triangle Count (PCS), Triangles, Quadric Count (PCS), Quadrics. If the count of any of these is zero then the follow data is a Poly Count Structure.

All structure information is 32 bit aligned for the PSX GPU.

`typedef struct`  
`{`  
`   uint16  Count;`  
`   uint16  TexPage;`  
`} PolyCount;`

`typedef struct`  
`{`  
`   int16  X;`  
`   int16  Y;`  
`   int16  Z;`  
`   int16  Unused;`  
`} Vertex;`

`typedef struct`  
`{`  
`   uint8  Red;`  
`   uint8  Green;`  
`   uint8  Blue;`  
`   uint8  Unused;`  
`} Color;`

`typedef struct`  
`{`  
`   uint16  A;`  
`   uint16  B;`  
`   uint16  C;`  
`   uint16  D;`  
`} PolyIndices;`

`typedef struct`  
`{`  
`   PolyIndices  Vertexs;`  
`   Color        Colors[3];`  
`} ColorTriangle;`

`typedef struct`  
`{`  
`   PolyIndices  Vertexs;`  
`   Color        Colors[4];`  
`} ColorQuadric;`

`typedef struct`  
`{`  
`   PolyIndices  Vertex;`  
`   uint8        U0, V0;`  
`   unint16      Flags;`  
`   uint8        U1, V1;`  
`   uint8        U2, V2;`  
`} TexTriangle;`

`typedef struct`  
`{`  
`   PolyIndices  Vertex;`  
`   uint8        U0, V0;`  
`   unint16      Flags;`  
`   uint8        U1, V1;`  
`   uint8        U2, V2;`  
`   uint8        U3, V3;`  
`   uint16       Unused;`  
`} TexQuadric;`

The Flags field on the Textured polygons contains the texture palette offset for the [TIM](PSX/TIM_format "wikilink") texture file associated with the model. The TexPage is not used in any of the battle models however battle scenes do use this to refer another page of texture data (for 8bpp [TIM](../PSX/TIM_format).

**Bone structure data**

<table>
<tbody>
<tr>
<td style="width: 76px; vertical-align: middle; background-color: rgb(204, 204, 204); text-align: center"><p>Offset<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Size<br />
</p></td>
<td style="text-align: center; vertical-align: middle; background-color: rgb(204, 204, 204)"><p>Description<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000000<br />
</p></td>
<td style="vertical-align: top"><p>4 bytes (long)<br />
</p></td>
<td style="vertical-align: top"><p>Vertex pool size (in bytes)<br />
</p></td>
</tr>
<tr>
<td style="width: 76px; vertical-align: middle; text-align: center"><p>000004<br />
</p></td>
<td style="vertical-align: top"><p>Vertex Pool Size bytes<br />
</p></td>
<td style="vertical-align: top"><p>Vertex pool for bone structure<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>ï¿½Number of polygons<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Polygon flags (Palette)<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>N * 16 bytes<br />
</p></td>
<td style="vertical-align: top"><p>Textured Triangles if N polygons = 0 these ocupy no space<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Number of polygons quadrics&gt;<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Polygon flags (Palette)<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>N * 20 bytes<br />
</p></td>
<td style="vertical-align: top"><p>Textured Quadrics if N polygons = 0 these ocupy no space<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Number of polygons<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p><br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>N * 20 bytes<br />
</p></td>
<td style="vertical-align: top"><p>Colored vertex triangles if N polygons = 0 these ocupy no space<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p>Number of polygons<br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>2 bytes (word)<br />
</p></td>
<td style="vertical-align: top"><p><br />
</p></td>
</tr>
<tr>
<td style="vertical-align: top; text-align: center"><p>...<br />
</p></td>
<td style="vertical-align: top"><p>N * 24 bytes<br />
</p></td>
<td style="vertical-align: top"><p>Colored vertex quadrics if N polygons = 0 these ocupy no space</p></td>
</tr>
</tbody>
</table>

### Battle animations

This is identical to the PC version of FF7.

### Texture information

see [TIM format](../PSX/TIM_format)

### Weapon models

These are identical to the bone model structures, as the weapon models are treated as bones in character animation. They have NO texture data period.

  

### Example of LZS playable character battle model file breakdown, using CLOUD.LZS

\[Lazy Bastard\]: Using data from Akari's Q-Gears utilities source, information from the wiki, and my own intuition, I've mapped out CLOUD.LZS, Cloud's battle model, in entirety. It turns out that Akari's Q-Gears FF7 Battle Model Viewer/Extractor source applies to enemy models, but not to playable character models (animations, textures, and weapon 'bones' work differently). I've deliberately avoided dissecting animation data and similar data sections, as these are outlined already in the wiki, and would make this breakdown even more verbose than it already is. Anyway, without further ado:

  
  
**Header** \[at offset 0x00000000\]:

  
71 00 00 00 C8 01 00 00 70 5B 00 00

  
  
Breakdown:

71 00 00 00 - Number of sections (0x00000071)

C8 01 00 00 - Offset to Bone Description Section (0x000001C8)

70 5B 00 00 - Offset to Model Settings (0x00005B70)

  
  

- \*\* \*\*\* Header runs until Offsets to Animations, Texture, and Weapon Bone Data\*\*\*

  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Offsets to Animations, Texture, and Weapon Bone Data** \[at offset 0x0000000C\]:

  
Note: These are four-byte offsets. The first one is the offset to the 1st animation data. The last one is the offset to the last weapon bone data. There's surely a better method, but by counting the number of weapons a character has, multiplying that number by four, adding four, and going back that number of bytes from the end of the last offset in this group of offsets, you can identify the offset for the Texture Data Section (in this case, 0x0000B408, as Cloud has 16 weapons in the game). The offset before this offset is the last animation data offset. There must be some reference in the file to how many animations and how many weapons a character has, which would facilitate a simpler mapping of this data...

  
  
A8 5F 00 00 04 63 00 00 04 66 00 00 AC 6A 00 00 94 6C 00 00 FC 6D 00 00 6C 6F 00 00 C0 6F 00 00

E8 70 00 00 3C 71 00 00 74 73 00 00 04 76 00 00 08 76 00 00 9C 79 00 00 70 7A 00 00 54 7C 00 00

10 7E 00 00 68 7F 00 00 DC 80 00 00 2C 83 00 00 80 85 00 00 A0 87 00 00 78 8B 00 00 A8 8C 00 00

AC 8C 00 00 C0 8D 00 00 20 8F 00 00 A4 8F 00 00 60 90 00 00 28 91 00 00 FC 91 00 00 34 93 00 00

20 98 00 00 B4 9B 00 00 90 9E 00 00 24 A0 00 00 EC A0 00 00 68 A2 00 00 2C A3 00 00 14 A4 00 00

E0 A4 00 00 B0 A5 00 00 70 A7 00 00 74 A7 00 00 78 A7 00 00 7C A7 00 00 80 A7 00 00 84 A7 00 00

88 A7 00 00 8C A7 00 00 90 A7 00 00 94 A7 00 00 98 A7 00 00 08 A8 00 00 64 A8 00 00 84 A9 00 00

D4 A9 00 00 18 AA 00 00 58 AA 00 00 68 AA 00 00 90 AA 00 00 A0 AA 00 00 08 AB 00 00 74 AB 00 00

78 AB 00 00 34 AC 00 00 5C AC 00 00 B0 AC 00 00 F8 AC 00 00 2C AD 00 00 68 AD 00 00 C8 AD 00 00

30 AE 00 00 90 AE 00 00 64 AF 00 00 94 AF 00 00 98 AF 00 00 C4 AF 00 00 F8 AF 00 00 10 B0 00 00

34 B0 00 00 54 B0 00 00 78 B0 00 00 A8 B0 00 00 70 B1 00 00 04 B2 00 00 80 B2 00 00 C8 B2 00 00

E8 B2 00 00 30 B3 00 00 50 B3 00 00 7C B3 00 00 A0 B3 00 00 C0 B3 00 00 08 B4 00 00 68 D2 00 00

BC DB 00 00 A8 E5 00 00 F4 EE 00 00 6C F9 00 00 C4 04 01 00 EC 0F 01 00 4C 1B 01 00 4C 29 01 00

28 35 01 00 F4 3C 01 00 24 47 01 00 AC 4F 01 00 94 5D 01 00 7C 67 01 00 1C 73 01 00

  
  
  

- \*\* \*\*\* Offsets to Animations, Texture, and Weapon Bone Data runs until Bone Description Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
  
**Bone Description Section** \[at offset 0x000001C8\]:

  
Number of Bones \[at offset 0x000001C8\]:

17 00 00 00

  
  
***Individual Bone Descriptions*** \[at offset 0x000001CC\]:

  
  
Note: According to the wiki, the length of these bones (see below) is signed, not unsigned, and "all FF7 bone lengths are negative".

Note2: If 'Bone offset from Bone Description Section' is 0, bone is actually a joint (and will have no bone data in the next section, incidentally).

Note3: I discovered which bone was which by first mangling each one at a time and observing what became mangled in the game, and then by verifying using FF7vME, an app that allows you to view LZS models from FF7. I didn't bother to map out joints, although mangling them did have interesting effects, of course.

  
  
Root Bone Description \[at offset 0x000001CC\]:

  
00 00 00 00 00 00 00 00

  
Note: According to the wiki page, this bone is 'always zeroed'.

  
  
  
1st bone description \[at offset 0x000001D4\]:

  
00 00 D9 FF C4 00 00 FF

  
Breakdown:

00 00 - Parent ID

D9 FF - Bone length

C4 00 00 00 - Bone offset from Bone Description Section

  

- Pelvis

  
  
  
2nd bone description \[at offset 0x000001DC\]:

  
01 00 5D FF 68 05 00 00

  
Breakdown:

01 00 - Parent ID

5D FF - Bone Length

68 05 00 00 - Bone offset from Bone Description Section

  

- Torso

  
  
3rd bone description \[at offset 0x000001E4\]:

  
02 00 6E FF 2C 12 00 00

  
Breakdown:

02 00 - Parent ID

6E FF - Bone Length

2C 12 00 00 - Bone offset from Bone Description Section

  

- Head

  
  
  
4th bone description \[at offset 0x000001EC\]:

  
01 00 73 FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

73 FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
  
  
5th bone description \[at offset 0x000001F4\]:

  
04 00 C5 FF 00 00 00 00

  
Breakdown:

04 00 - Parent ID

C5 FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
  
  
  
6th bone description \[at offset 0x000001FC\]:

  
05 00 7B FF E0 2A 00 00

  
Breakdown:

05 00 - Parent ID

7B FF - Bone Length

E0 2A 00 00 - Bone offset from Bone Description Section

  

- Left arm, shoulder to elbow

  
  
7th bone description \[at offset 0x00000204\]:

  
06 00 8B FF 24 2F 00 00

  
Breakdown:

06 00 - Parent ID

8B FF - Bone Length

24 2F 00 00 - Bone offset from Bone Description Section

  

- Left arm, elbow to wrist

  
  
8th bone description \[at offset 0x0000020C\]:

  
07 00 AB FF 78 31 00 00

  
Breakdown:

07 00 - Parent ID

AB FF - Bone Length

78 31 00 00 - Bone offset from Bone Description Section

  

- Left arm, wrist to fingertips

  
  
9th bone description \[at offset 0x00000214\]:

  
01 00 73 FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

73 FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
  
  
10th bone description \[at offset 0x0000021C\]:

  
09 00 C5 FF 00 00 00 00

  
Breakdown:

09 00 - Parent ID

C5 FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
  
  
11th bone description \[at offset 0x00000224\]:

  
0A 00 7B FF 9C 36 00 00

  
Breakdown:

0A 00 - Parent ID

7B FF - Bone Length

9C 36 00 00 - Bone offset from Bone Description Section

  

- Right arm, shoulder to elbow

  
  
12th bone description \[at offset 0x0000022C\]:

  
0B 00 8B FF B0 3A 00 00

  
Breakdown:

0B 00 - Parent ID

8B FF - Bone Length

B0 3A 00 00 - Bone offset from Bone Description Section

  

- Right arm, elbow to wrist

  
  
13th bone description \[at offset 0x00000234\]:

  
0C 00 B4 FF 44 3C 00 00

  
Breakdown:

0C 00 - Parent ID

B4 FF - Bone Length

44 3C 00 00 - Bone offset from Bone Description Section

  

- Right arm, wrist to fingertips

  
  
14th bone description \[at offset 0x0000023C\]:

  
00 00 DB FF 00 00 00 00

  
Breakdown:

00 00 - Parent ID

DB FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
  
  
15th bone description \[at offset 0x00000244\]:

  
0E 00 EB FE 68 41 00 00

  
Breakdown:

0E 00 - Parent ID

EB FE - Bone Length

68 41 00 00 - Bone offset from Bone Description Section

  

- Left leg, hip to knee

  
  
16th bone description \[at offset 0x0000024C\]:

  
0F 00 03 FF CC 43 00 00

  
Breakdown:

0F 00 - Parent ID

03 FF - Bone Length

CC 43 00 00 - Bone offset from Bone Description Section

  
  

- Left leg, knee to top of boot

  
  
17th bone description \[at offset 0x00000254\]:

  
10 00 B3 FF 58 49 00 00

  
Breakdown:

10 00 - Parent ID

B3 FF - Bone Length

58 49 00 00 - Bone offset from Bone Description Section

  

- Left foot, back part of boot

  
  
18th bone description \[at offset 0x0000025C\]:

  
11 00 87 FF 00 4C 00 00

  
Breakdown:

11 00 - Parent ID

87 FF - Bone Length

00 4C 00 00 - Bone offset from Bone Description Section

  

- Left foot, front part of boot

  
  
19th bone description \[at offset 0x00000264\]:

  
00 00 DB FF 00 00 00 00

  
Breakdown:

00 00 - Parent ID

DB FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
20th bone description \[at offset 0x0000026C\]:

  
13 00 EB FE 88 4D 00 00

  
Breakdown:

13 00 - Parent ID

EB FE - Bone Length

88 4D 00 00 - Bone offset from Bone Description Section

  

- Right leg, hip to knee

  
  
21th bone description \[at offset 0x00000274\]:

  
14 00 03 FF EC 4F 00 00

  
Breakdown:

14 00 - Parent ID

03 FF - Bone Length

EC 4F 00 00 - Bone offset from Bone Description Section

  

- Right leg, knee to top of boot

  
  
22th bone description \[at offset 0x0000027C\]:

  
15 00 B3 FF 78 55 00 00

  
Breakdown:

15 00 - Parent ID

B3 FF - Bone Length

78 55 00 00 - Bone offset from Bone Description Section

  

- Right foot, back part of boot

  
  
23th bone description \[at offset 0x00000284\]:

  
16 00 87 FF 20 58 00 00

  
Breakdown:

16 00 - Parent ID

87 FF - Bone Length

20 58 00 00 - Bone offset from Bone Description Section

  

- Right foot, front part of boot

  
  
  

- \*\* \*\*\* Individual Bone Descriptions runs until Bone Data Section\*\*\*

  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Bone Data Section** \[at offset 0x0000028C\]

  
  
Note: These offsets are from the previous section, per bone. If a bone is actually a joint (offset of all zeroes in the previous section), there will be no data for it in this section, and it will be skipped as if it doesn't exist.

  
  
  
Bone 1 \[at offset 0x0000028C\]

  
D0 00 00 00 00 00 CD FF 2E 00 00 00 43 00 D1 FF 22 00 00 00 00 00 C2 FF F9 FF 00 00 54 00 02 00

22 00 00 00 00 00 FE FF 34 00 00 00 4F 00 02 00 F9 FF 00 00 3F 00 23 00 F9 FF 00 00 B1 FF 02 00

F9 FF 00 00 C1 FF 23 00 F9 FF 00 00 AC FF 02 00 22 00 00 00 BD FF D1 FF 22 00 00 00 42 00 06 00

D7 FF 00 00 00 00 34 00 0F 00 00 00 00 00 37 00 D7 FF 00 00 BE FF 06 00 D7 FF 00 00 3F 00 D1 FF

F9 FF 00 00 00 00 DA FF D7 FF 00 00 C1 FF D1 FF F9 FF 00 00 00 00 02 00 BD FF 00 00 37 00 E7 FF

D7 FF 00 00 31 00 26 00 D7 FF 00 00 BD FF 23 00 22 00 00 00 43 00 23 00 22 00 00 00 C9 FF E7 FF

D7 FF 00 00 00 00 21 00 2E 00 00 00 CF FF 26 00 D7 FF 00 00 00 00 25 00 00 00 00 00 30 00 00 00

C0 00 60 00 B0 00 00 00 13 0F 14 30 17 12 17 00 20 1C 2A 00 08 00 78 00 10 00 00 00 1F 18 20 30

17 12 17 00 09 04 0B 00 20 00 08 00 00 00 00 00 11 0E 12 30 1F 18 20 00 09 00 0F 00 30 00 18 00

B0 00 00 00 20 1C 2A 30 19 13 1A 00 20 1C 2A 00 48 00 40 00 A8 00 00 00 0E 09 0F 30 12 0E 17 00

17 12 17 00 50 00 20 00 00 00 00 00 0E 09 0F 30 11 0E 12 00 09 00 0F 00 58 00 30 00 A0 00 00 00

17 12 17 30 20 1C 2A 00 17 12 17 00 30 00 68 00 A0 00 00 00 20 1C 2A 30 19 14 24 00 17 12 17 00

40 00 70 00 C8 00 00 00 12 0E 17 30 12 0E 17 00 12 0E 17 00 80 00 78 00 98 00 00 00 17 12 17 30

17 12 17 00 17 12 17 00 60 00 C0 00 A8 00 00 00 17 12 17 30 13 0F 14 00 17 12 17 00 68 00 40 00

C8 00 00 00 19 14 24 30 12 0E 17 00 12 0E 17 00 88 00 80 00 B8 00 00 00 0E 09 0F 30 17 12 17 00

0E 09 0F 00 50 00 10 00 88 00 00 00 0E 09 0F 30 09 04 0B 00 0E 09 0F 00 68 00 C8 00 90 00 00 00

19 14 24 30 12 0E 17 00 12 0E 17 00 C8 00 70 00 90 00 00 00 12 0E 17 30 12 0E 17 00 12 0E 17 00

B8 00 80 00 90 00 00 00 0E 09 0F 30 17 12 17 00 17 12 27 00 80 00 98 00 90 00 00 00 17 12 17 30

17 12 17 00 17 12 27 00 98 00 58 00 A0 00 00 00 17 12 17 30 17 12 17 00 17 12 17 00 A0 00 68 00

90 00 00 00 17 12 17 30 19 14 24 00 17 12 27 00 28 00 58 00 98 00 00 00 20 1C 2A 30 17 12 17 00

17 12 17 00 08 00 28 00 78 00 00 00 1F 18 20 30 20 1C 2A 00 17 12 17 00 20 00 A8 00 C0 00 00 00

11 0E 12 30 17 12 17 00 13 0F 14 00 B0 00 20 00 C0 00 00 00 20 1C 2A 30 11 0E 12 00 13 0F 14 00

88 00 48 00 50 00 00 00 0E 09 0F 30 0E 09 0F 00 0E 09 0F 00 70 00 38 00 B8 00 00 00 12 0E 17 30

0E 09 0F 00 0E 09 0F 00 90 00 70 00 B8 00 00 00 12 0E 17 30 12 0E 17 00 0E 09 0F 00 60 00 A8 00

40 00 00 00 17 12 17 30 17 12 17 00 12 0E 17 00 B0 00 60 00 30 00 00 00 20 1C 2A 30 17 12 17 00

20 1C 2A 00 B8 00 38 00 88 00 00 00 0E 09 0F 30 0E 09 0F 00 0E 09 0F 00 48 00 88 00 38 00 00 00

0E 09 0F 30 0E 09 0F 00 0E 09 0F 00 20 00 B0 00 18 00 00 00 11 0E 12 30 20 1C 2A 00 19 13 1A 00

A8 00 20 00 48 00 00 00 17 12 17 30 11 0E 12 00 0E 09 0F 00 28 00 08 00 18 00 00 00 20 1C 2A 30

1F 18 20 00 19 13 1A 00 28 00 98 00 78 00 00 00 20 1C 2A 30 17 12 17 00 17 12 17 00 98 00 A0 00

90 00 00 00 17 12 17 30 17 12 17 00 17 12 27 00 10 00 50 00 00 00 00 00 09 04 0B 30 0E 09 0F 00

09 00 0F 00 80 00 88 00 10 00 00 00 17 12 17 30 0E 09 0F 00 09 04 0B 00 40 00 68 00 60 00 00 00

12 0E 17 30 19 14 24 00 17 12 17 00 78 00 80 00 10 00 00 00 17 12 17 30 17 12 17 00 09 04 0B 00

70 00 40 00 38 00 00 00 12 0E 17 30 12 0E 17 00 0E 09 0F 00 68 00 30 00 60 00 00 00 19 14 24 30

20 1C 2A 00 17 12 17 00 30 00 58 00 28 00 00 00 20 1C 2A 30 17 12 17 00 20 1C 2A 00 20 00 50 00

48 00 00 00 11 0E 12 30 0E 09 0F 00 0E 09 0F 00 40 00 48 00 38 00 00 00 12 0E 17 30 0E 09 13 00

0E 09 13 00 18 00 30 00 28 00 00 00 19 13 1A 30 20 1C 2A 00 20 1C 2A 00 08 00 20 00 18 00 00 00

1F 18 20 30 11 0E 12 00 19 13 1A 00 08 00 10 00 00 00 00 00 1F 18 20 30 09 04 0B 00 09 00 0F 00

00 00 00 00

  
  
  
Bone 2 \[at offset 0x00000730\]:

  
60 02 00 00 C0 FF 18 00 E1 FF 00 00 CF FF 36 00 CF FF 00 00 E3 FF 3A 00 E2 FF 00 00 CB FF 47 00

BB FF 00 00 E0 FF 3D 00 CB FF 00 00 BA FF F2 FF CA FF 00 00 BA FF 13 00 D4 FF 00 00 C0 FF F8 FF

DB FF 00 00 FA FF 49 00 B6 FF 00 00 F4 FF 3F 00 D5 FF 00 00 E4 FF 48 00 B8 FF 00 00 06 00 49 00

B6 FF 00 00 1C 00 47 00 B5 FF 00 00 0C 00 3F 00 D5 FF 00 00 31 00 36 00 CF FF 00 00 20 00 3D 00

CB FF 00 00 35 00 47 00 BB FF 00 00 47 00 F2 FF CA FF 00 00 41 00 F8 FF DB FF 00 00 46 00 13 00

D4 FF 00 00 41 00 18 00 E1 FF 00 00 1E 00 3A 00 E2 FF 00 00 CD FF 10 00 5F FF 00 00 DC FF 18 00

64 FF 00 00 CE FF 34 00 81 FF 00 00 9B FF E2 FF 9C FF 00 00 9C FF 14 00 A5 FF 00 00 F2 FF 3C 00

E0 FF 00 00 F2 FF 33 00 FF FF 00 00 F3 FF C3 FF 99 FF 00 00 FA FF C9 FF A6 FF 00 00 0D 00 C3 FF

99 FF 00 00 00 00 C5 FF 8D FF 00 00 CE FF E1 FF 58 FF 00 00 DE FF E1 FF 59 FF 00 00 0E 00 3C 00

E0 FF 00 00 0E 00 33 00 FF FF 00 00 65 00 E2 FF 9C FF 00 00 64 00 14 00 A5 FF 00 00 D6 FF 47 00

BA FF 00 00 29 00 47 00 B9 FF 00 00 18 00 35 00 84 FF 00 00 41 00 32 00 7F FF 00 00 CF FF DB FF

BB FF 00 00 06 00 C9 FF A6 FF 00 00 31 00 DB FF BB FF 00 00 DD FF FC FF 55 FF 00 00 00 00 27 00

6E FF 00 00 DD FF 35 00 83 FF 00 00 24 00 18 00 64 FF 00 00 00 00 F6 FF 52 FF 00 00 23 00 FC FF

55 FF 00 00 A8 FF F1 FF 5E FF 00 00 A8 FF 19 00 71 FF 00 00 BF FF 32 00 7F FF 00 00 22 00 E1 FF

59 FF 00 00 58 00 F1 FF 5E FF 00 00 32 00 E1 FF 59 FF 00 00 58 00 19 00 71 FF 00 00 20 00 E6 FF

D8 FF 00 00 20 00 DE FF F6 FF 00 00 40 00 F0 FF F9 FF 00 00 41 00 10 00 FF FF 00 00 19 00 2F 00

03 00 00 00 41 00 C7 FF 80 FF 00 00 00 00 FF FF 10 00 00 00 06 00 DB FF BB FF 00 00 06 00 E6 FF

D8 FF 00 00 E0 FF E6 FF D8 FF 00 00 E0 FF DE FF F6 FF 00 00 FA FF E6 FF D8 FF 00 00 FA FF DB FF

BB FF 00 00 BF FF C7 FF 80 FF 00 00 E7 FF 2F 00 03 00 00 00 C0 FF F0 FF F9 FF 00 00 C0 FF 10 00

FF FF 00 00 00 00 20 00 00 00 00 00 6C 00 00 00 E8 00 F8 00 00 01 00 00 3C 2D 37 30 28 2C 2C 00

2D 32 3C 00 F8 00 68 01 00 02 00 00 19 0A 00 30 11 09 02 00 19 0A 00 00 68 01 28 01 00 02 00 00

11 09 02 30 08 02 00 00 19 0A 00 00 C0 01 00 02 28 01 00 00 0D 05 00 30 19 0A 00 00 08 02 00 00

C8 01 00 02 C0 01 00 00 15 07 00 30 19 0A 00 00 0D 05 00 00 98 01 B8 01 C8 01 00 00 34 1B 07 30

18 09 03 00 15 07 00 00 98 01 C8 01 C0 01 00 00 34 1B 07 30 15 07 00 00 0D 05 00 00 C0 01 88 01

98 01 00 00 0D 05 00 30 37 23 14 00 34 1B 07 00 C0 01 D0 01 88 01 00 00 0D 05 00 30 20 0D 03 00

37 23 14 00 88 01 D0 01 50 01 00 00 37 1E 14 30 20 0D 03 00 37 1E 14 00 88 01 50 01 48 01 00 00

37 1E 14 30 37 1E 14 00 37 1E 14 00 40 01 50 01 80 00 00 00 23 14 00 30 37 1E 14 00 0D 07 02 00

50 01 30 01 80 00 00 00 37 1E 14 30 0F 07 03 00 0D 07 02 00 30 01 50 01 D0 01 00 00 0F 07 03 30

37 1E 14 00 20 0D 03 00 48 01 40 01 60 00 00 00 37 23 14 30 23 14 00 00 23 14 00 00 F8 00 B8 01

00 01 00 00 19 0A 00 30 18 09 03 00 10 04 00 00 50 01 40 01 48 01 00 00 37 1E 14 30 23 14 00 00

37 1E 14 00 20 00 38 01 50 00 00 00 37 32 28 30 1E 23 28 00 25 33 33 00 C0 00 B8 00 80 01 00 00

36 1D 06 30 41 28 0A 00 37 28 0A 00 B8 00 C0 00 B0 00 00 00 41 28 0A 30 36 1D 06 00 32 1B 08 00

40 01 78 00 60 00 00 00 25 32 35 30 32 2D 28 00 23 32 37 00 B0 00 70 01 B8 00 00 00 32 1B 08 30

34 17 07 00 41 28 0A 00 70 01 B0 00 08 01 00 00 34 17 07 30 32 1B 08 00 0D 07 02 00 70 01 08 01

10 01 00 00 34 17 07 30 0D 07 02 00 0F 09 00 00 E8 00 10 01 08 01 00 00 0D 07 02 30 0F 09 00 00

0D 07 02 00 10 01 E8 00 00 01 00 00 0F 09 00 30 0D 07 02 00 11 09 00 00 18 02 E0 01 D8 01 00 00

14 0F 02 30 11 09 00 00 11 09 00 00 E8 01 D8 01 E0 01 00 00 0A 02 00 30 11 09 00 00 11 09 00 00

90 00 D8 01 E8 01 00 00 19 14 00 30 11 09 00 00 0A 02 00 00 28 02 30 02 20 02 00 00 11 09 00 30

14 0F 02 00 14 0F 02 00 20 02 50 02 28 02 00 00 14 0F 02 30 14 0F 02 00 11 09 00 00 20 02 38 00

50 02 00 00 14 0F 02 30 11 09 00 00 14 0F 02 00 00 00 48 02 58 02 00 00 0D 07 02 30 1A 0F 04 00

0E 03 00 00 00 00 10 00 48 02 00 00 0D 07 02 30 37 23 0A 00 1A 0F 04 00 48 02 10 00 E0 00 00 00

1A 0F 04 30 37 23 0A 00 20 11 04 00 E0 00 10 00 D8 00 00 00 20 11 04 30 37 23 0A 00 15 0B 02 00

D8 00 10 00 48 00 00 00 15 0B 02 30 37 23 0A 00 3C 28 0A 00 A8 00 18 01 68 00 00 00 46 2D 0F 30

23 11 08 00 46 2D 0F 00 A8 00 20 01 18 01 00 00 46 2D 0F 30 23 15 04 00 23 11 08 00 20 01 A8 00

F8 01 00 00 23 15 04 30 46 2D 0F 00 2B 19 09 00 A8 00 A0 00 F8 01 00 00 46 2D 0F 30 1E 0D 00 00

2B 19 09 00 F8 01 A0 00 F0 01 00 00 2B 19 09 30 1E 0D 00 00 0E 03 00 00 28 00 20 02 58 01 00 00

12 0E 1B 30 12 0E 1B 00 12 0E 1B 00 40 02 A0 01 C8 00 00 00 19 14 23 30 1E 23 2D 00 0E 09 0F 00

C8 00 58 01 40 02 00 00 0E 09 0F 30 12 0E 1B 00 19 14 23 00 B0 01 D0 00 A8 01 00 00 3C 3C 64 30

0E 0B 13 00 2D 32 4B 00 28 00 58 01 C8 00 00 00 12 0E 1B 30 12 0E 1B 00 0E 09 0F 00 08 00 00 00

30 00 00 00 19 1E 2D 30 05 0A 14 00 09 04 13 00 20 00 10 00 08 00 00 00 12 0E 1B 30 05 0A 14 00

19 1E 2D 00 D0 00 08 00 30 00 00 00 0E 0B 13 30 19 1E 2D 00 09 04 13 00 38 01 20 00 18 00 00 00

0A 0F 19 30 0A 0F 19 00 0A 0F 19 00 90 01 10 01 B8 01 00 00 14 19 28 30 19 14 23 00 0A 0F 19 00

30 00 28 00 D0 00 00 00 09 04 13 30 12 0E 1B 00 0E 0B 13 00 18 00 08 00 D0 00 00 00 0A 0F 19 30

19 1E 2D 00 0E 0B 13 00 48 01 80 01 78 01 00 00 41 3A 69 30 41 3A 69 00 23 28 3C 00 40 02 08 01

A0 01 00 00 19 14 23 30 14 19 28 00 1E 23 2D 00 38 00 30 00 00 00 00 00 05 0A 14 30 09 04 13 00

05 0A 14 00 48 02 08 02 58 02 00 00 22 1A 2A 30 0A 05 0F 00 14 0F 23 00 50 02 58 02 08 02 00 00

0A 05 14 30 14 0F 23 00 0A 05 0F 00 28 02 50 02 08 02 00 00 0A 05 14 30 0A 06 14 00 0A 05 0F 00

E8 00 08 01 40 02 00 00 12 0E 1B 30 14 19 28 00 19 14 23 00 20 02 28 00 38 00 00 00 12 0E 1B 30

12 0E 1B 00 05 0A 14 00 D0 00 B0 01 18 00 00 00 0E 0B 13 30 3C 3C 64 00 0A 0F 19 00 48 02 F8 01

08 02 00 00 22 1A 2A 30 16 11 1B 00 0A 05 0F 00 E0 01 28 02 08 02 00 00 1E 19 28 30 0A 05 14 00

0A 05 0F 00 20 00 50 00 48 00 00 00 12 0E 1B 30 09 04 13 00 12 10 17 00 B0 00 C0 00 B0 01 00 00

2D 2D 46 30 46 3C 5F 00 3C 3C 64 00 B0 00 A0 01 08 01 00 00 2D 2D 46 30 1E 23 2D 00 14 19 28 00

58 01 E8 00 40 02 00 00 12 0E 1B 30 12 0E 1B 00 19 14 23 00 10 01 00 01 B8 01 00 00 19 14 23 30

19 14 23 00 0A 0F 19 00 38 02 F0 00 58 01 00 00 12 0E 1B 30 0E 09 0F 00 12 0E 1B 00 60 01 10 02

68 01 00 00 09 04 0F 30 12 0E 1B 00 19 14 23 00 68 00 60 00 78 00 00 00 12 10 17 30 09 04 13 00

05 0A 14 00 80 00 78 00 40 01 00 00 1C 17 23 30 05 0A 14 00 09 04 13 00 60 00 58 00 48 01 00 00

09 04 13 30 09 04 13 00 41 3A 69 00 A8 00 68 00 78 00 00 00 05 0A 14 30 12 10 17 00 05 0A 14 00

88 00 D8 01 90 00 00 00 14 10 15 30 0A 0F 14 00 0B 09 0C 00 E8 01 E0 01 08 02 00 00 19 13 1F 30

1E 14 28 00 0A 05 0F 00 F0 01 E8 01 08 02 00 00 14 0F 1E 30 19 13 1F 00 0A 05 0F 00 08 02 F8 01

F0 01 00 00 0A 05 0F 30 16 11 1B 00 14 0F 1E 00 98 00 90 00 A0 00 00 00 11 0E 18 30 0B 09 0C 00

12 0E 1B 00 48 01 78 01 88 01 00 00 41 3A 69 30 23 28 3C 00 1E 1E 37 00 70 00 80 00 30 01 00 00

23 20 32 30 11 0E 18 00 11 0E 18 00 88 00 98 00 30 01 00 00 14 10 15 30 11 0E 18 00 11 0E 18 00

70 00 30 01 98 00 00 00 23 20 32 30 11 0E 18 00 11 0E 18 00 A0 00 70 00 98 00 00 00 12 0E 1B 30

23 20 32 00 11 0E 18 00 68 01 88 00 28 01 00 00 19 14 23 30 14 10 15 00 0E 09 0F 00 D8 01 88 00

68 01 00 00 0A 0F 14 30 14 10 15 00 19 14 23 00 90 01 B8 01 98 01 00 00 14 19 28 30 0A 0F 19 00

14 1E 37 00 10 01 90 01 70 01 00 00 19 14 23 30 14 19 28 00 14 1E 37 00 B0 00 B0 01 A8 01 00 00

2D 2D 46 30 3C 3C 64 00 2D 32 4B 00 B0 00 A8 01 A0 01 00 00 2D 2D 46 30 2D 32 4B 00 1E 23 2D 00

10 00 20 00 48 00 00 00 05 0A 14 30 12 0E 1B 00 12 10 17 00 70 00 A8 00 78 00 00 00 23 20 32 30

05 0A 14 00 05 0A 14 00 80 01 40 00 50 00 00 00 41 3A 69 30 09 04 13 00 09 04 13 00 78 01 80 01

B8 00 00 00 23 28 3C 30 41 3A 69 00 1E 1E 37 00 60 01 68 01 F8 00 00 00 09 04 0F 30 19 14 23 00

09 04 0F 00 58 01 F0 00 E8 00 00 00 12 0E 1B 30 0E 09 0F 00 12 0E 1B 00 88 00 30 01 28 01 00 00

14 10 15 30 11 0E 18 00 0E 09 0F 00 D0 00 28 00 C8 00 00 00 0E 0B 13 30 12 0E 1B 00 0E 09 0F 00

A8 00 70 00 A0 00 00 00 05 0A 14 30 23 20 32 00 12 0E 1B 00 90 00 98 00 88 00 00 00 0B 09 0C 30

11 0E 18 00 14 10 15 00 78 00 80 00 70 00 00 00 05 0A 14 30 1C 17 23 00 23 20 32 00 60 00 68 00

58 00 00 00 09 04 13 30 12 10 17 00 09 04 13 00 48 00 50 00 40 00 00 00 12 10 17 30 09 04 13 00

09 04 13 00 30 00 38 00 28 00 00 00 09 04 13 30 05 0A 14 00 12 0E 1B 00 18 00 20 00 08 00 00 00

0A 0F 19 30 0A 0F 19 00 19 1E 2D 00 08 00 10 00 00 00 00 00 19 1E 2D 30 05 0A 14 00 05 0A 14 00

14 00 00 00 D8 00 18 01 E0 00 20 01 28 2D 2D 38 69 55 5A 00 28 2D 3C 00 5C 5C 6E 00 F8 00 E8 00

60 01 F0 00 28 2C 2C 38 3C 2D 37 00 38 34 24 00 23 1E 32 00 C8 01 B8 01 00 02 F8 00 15 07 00 38

18 09 03 00 19 0A 00 00 19 0A 00 00 28 01 30 01 C0 01 D0 01 08 02 00 38 0F 07 03 00 0D 05 00 00

20 0D 03 00 38 01 C0 00 50 00 80 01 0D 07 02 38 36 1D 06 00 28 14 05 00 37 28 0A 00 60 01 F0 00

10 02 38 02 08 05 01 38 08 05 01 00 0D 07 02 00 0D 07 02 00 10 02 38 02 18 02 30 02 14 0A 05 38

14 0A 05 00 14 0A 05 00 14 0A 05 00 18 02 30 02 E0 01 28 02 14 0F 02 38 14 0F 02 00 11 09 00 00

11 09 00 00 E8 01 F0 01 90 00 A0 00 0A 02 00 38 0E 03 00 00 19 14 00 00 1E 0D 00 00 58 02 50 02

00 00 38 00 0E 03 00 38 14 0F 02 00 14 0F 02 00 11 09 00 00 18 01 D8 00 68 00 48 00 23 11 08 38

15 0B 02 00 46 2D 0F 00 3C 28 0A 00 F8 01 48 02 20 01 E0 00 2B 19 09 38 1A 0F 04 00 25 15 06 00

20 11 04 00 18 00 B0 01 38 01 C0 00 0A 0F 19 38 3C 3C 64 00 0A 0F 19 00 46 3C 5F 00 58 00 40 00

48 01 80 01 09 04 13 38 09 04 13 00 41 3A 69 00 41 3A 69 00 D0 00 C8 00 A8 01 A0 01 0E 0B 13 38

0E 09 0F 00 2D 32 4B 00 1E 23 2D 00 68 00 48 00 58 00 40 00 12 10 17 38 12 10 17 00 09 04 13 00

09 04 13 00 30 02 38 02 20 02 58 01 12 0E 1B 38 12 0E 1B 00 12 0E 1B 00 12 0E 1B 00 10 02 18 02

68 01 D8 01 12 0E 1B 38 05 0A 14 00 19 14 23 00 0A 0F 14 00 70 01 90 01 B8 00 78 01 14 1E 37 38

14 19 28 00 1E 1E 37 00 23 28 3C 00 78 01 90 01 88 01 98 01 23 28 3C 38 14 19 28 00 1E 1E 37 00

14 1E 37 00

  
  
  
Bone 3 \[at offset 0x000013F4\]:

  
18 04 00 00 0C 00 4C 00 9C FF 00 00 25 00 45 00 AF FF 00 00 FF FF 56 00 B5 FF 00 00 24 00 3F 00

94 FF 00 00 1D 00 42 00 97 FF 00 00 14 00 F2 FF EC FF 00 00 13 00 F1 FF 08 00 00 00 14 00 1A 00

F0 FF 00 00 22 00 1E 00 DE FF 00 00 21 00 3A 00 D2 FF 00 00 2E 00 27 00 BC FF 00 00 EB FF 1A 00

F0 FF 00 00 EC FF 18 00 0A 00 00 00 EB FF F1 FF EC FF 00 00 EC FF F1 FF 08 00 00 00 D9 FF 45 00

B0 FF 00 00 F0 FF 4B 00 9C FF 00 00 F8 FF 48 00 88 FF 00 00 E9 FF 44 00 87 FF 00 00 EA FF 62 00

62 FF 00 00 00 00 2A 00 6A FF 00 00 E6 FF 50 00 4F FF 00 00 24 00 FB FF 6E FF 00 00 1A 00 25 00

6E FF 00 00 00 00 FB FF 6B FF 00 00 0B 00 36 00 58 FF 00 00 12 00 3F 00 7D FF 00 00 08 00 40 00

5C FF 00 00 F3 FF 22 00 65 FF 00 00 B1 FF 20 00 6F FF 00 00 DF FF 00 00 6F FF 00 00 D3 FF 33 00

7C FF 00 00 1E 00 6B 00 87 FF 00 00 24 00 58 00 8E FF 00 00 1E 00 3F 00 8D FF 00 00 1A 00 4B 00

9C FF 00 00 11 00 46 00 92 FF 00 00 19 00 4C 00 95 FF 00 00 F6 FF 59 00 56 FF 00 00 F8 FF 78 00

85 FF 00 00 F3 FF 65 00 8A FF 00 00 F9 FF 58 00 93 FF 00 00 FD FF 5D 00 90 FF 00 00 FC FF 4E 00

94 FF 00 00 ED FF 48 00 96 FF 00 00 E8 FF 4A 00 9A FF 00 00 EE FF 58 00 9D FF 00 00 F5 FF 4D 00

98 FF 00 00 EA FF 4D 00 9E FF 00 00 2B 00 39 00 B4 FF 00 00 39 00 17 00 BA FF 00 00 23 00 3C 00

C2 FF 00 00 2F 00 18 00 BE FF 00 00 C9 FF 10 00 74 FF 00 00 C6 FF 22 00 7F FF 00 00 F2 FF 3D 00

38 FF 00 00 02 00 38 00 63 FF 00 00 BF FF 7D 00 1E FF 00 00 D9 FF 5B 00 62 FF 00 00 2A 00 1F 00

6F FF 00 00 03 00 4A 00 91 FF 00 00 9A FF 27 00 C9 FF 00 00 D8 FF 3A 00 9E FF 00 00 C9 FF 31 00

9E FF 00 00 D0 FF 37 00 96 FF 00 00 C1 FF 44 00 90 FF 00 00 CC FF 43 00 A7 FF 00 00 DF FF 41 00

96 FF 00 00 DF FF 69 00 78 FF 00 00 C6 FF 22 00 88 FF 00 00 ED FF 34 00 72 FF 00 00 E0 FF 51 00

76 FF 00 00 B3 FF 34 00 56 FF 00 00 A7 FF F9 FF AD FF 00 00 B4 FF 35 00 8D FF 00 00 E2 FF 5D 00

83 FF 00 00 AE FF 3B 00 E4 FF 00 00 0A 00 47 00 8C FF 00 00 CA FF 61 00 E3 FF 00 00 2F 00 43 00

D1 FF 00 00 83 FF 03 00 89 FF 00 00 CC FF F7 FF 7F FF 00 00 00 00 D3 FF C7 FF 00 00 DC FF DC FF

C0 FF 00 00 28 00 04 00 DB FF 00 00 23 00 DC FF C0 FF 00 00 D6 FF 04 00 DB FF 00 00 FF FF D4 FF

83 FF 00 00 2D 00 EA FF 82 FF 00 00 DF FF 31 00 1D 00 00 00 CF FF 17 00 BF FF 00 00 C1 FF 25 00

AD FF 00 00 D3 FF 39 00 B4 FF 00 00 DB FF 3B 00 C2 FF 00 00 F7 FF 4C 00 D1 FF 00 00 FF FF 50 00

D0 FF 00 00 FB FF 50 00 DA FF 00 00 DD FF 3A 00 D2 FF 00 00 03 00 50 00 DA FF 00 00 07 00 4C 00

D1 FF 00 00 E5 FF 3B 00 E7 FF 00 00 FF FF 56 00 DA FF 00 00 CB FF 02 00 D9 FF 00 00 C1 FF FA FF

C9 FF 00 00 00 00 03 00 1A 00 00 00 DB FF 1B 00 DE FF 00 00 D4 FF DA FF A0 FF 00 00 C5 FF F9 FF

98 FF 00 00 CE FF 04 00 B9 FF 00 00 00 00 41 00 FB FF 00 00 00 00 C3 FF A6 FF 00 00 C4 FF 09 00

B5 FF 00 00 13 00 19 00 0A 00 00 00 38 00 18 00 94 FF 00 00 3A 00 FA FF 98 FF 00 00 57 00 F9 FF

88 FF 00 00 31 00 24 00 AB FF 00 00 26 00 3E 00 A2 FF 00 00 5D 00 F2 FF 9F FF 00 00 57 00 E1 FF

C2 FF 00 00 30 00 04 00 B9 FF 00 00 3A 00 0A 00 B5 FF 00 00 3D 00 FB FF C8 FF 00 00 34 00 02 00

D9 FF 00 00 18 00 3C 00 E7 FF 00 00 2C 00 DB FF 9F FF 00 00 FF FF 53 00 A0 FF 00 00 F7 FF 5F 00

A5 FF 00 00 F9 FF 5F 00 A4 FF 00 00 FA FF 5C 00 A6 FF 00 00 F7 FF 58 00 C0 FF 00 00 0B 00 25 00

10 00 E8 02 78 00 80 00 00 06 40 78 36 20 39 00 98 01 10 00 08 00 80 00 36 20 40 78 00 06 3A 00

F0 02 E8 02 10 00 80 00 0C 38 40 78 36 20 00 06 E8 02 F0 02 08 03 80 00 36 20 40 78 0C 38 32 39

10 00 98 01 18 03 80 00 00 06 40 78 36 20 0D 38 00 03 68 03 20 03 80 00 AB 00 00 78 B5 37 83 15

10 00 F8 02 F0 02 80 00 00 06 40 78 00 34 0C 38 00 03 10 03 68 03 80 00 AB 00 00 78 BF 00 B5 37

F8 02 10 00 18 03 80 00 00 34 40 78 00 06 0D 38 68 03 10 03 E0 03 80 00 B5 37 00 78 BF 00 E6 15

18 03 98 01 48 00 80 00 0D 38 40 78 36 20 32 39 00 00 00 00 F8 00 00 00 C0 02 88 03 D8 01 00 00

4A 37 17 30 4F 37 25 00 CA 9E 2A 00 D8 01 D0 00 B8 00 00 00 CA 9E 2A 30 E0 DB 51 00 8C 62 25 00

A8 02 90 03 E8 03 00 00 23 19 0E 30 41 2F 1C 00 30 22 17 00 A8 02 C0 03 90 03 00 00 23 19 0E 30

4A 33 1C 00 41 2F 1C 00 C0 03 A8 02 A0 02 00 00 4A 33 1C 30 23 19 0E 00 2F 1E 0A 00 90 03 88 03

C0 02 00 00 41 2F 1C 30 4F 37 25 00 4A 37 17 00 B8 00 B0 00 D8 01 00 00 8C 62 25 30 72 55 25 00

CA 9E 2A 00 88 03 18 00 D8 01 00 00 4F 37 25 30 C1 AB 41 00 CA 9E 2A 00 A8 02 70 03 90 02 00 00

23 19 0E 30 11 0C 04 00 1A 11 05 00 70 03 E8 03 B8 02 00 00 11 0C 04 30 30 22 17 00 3D 2A 17 00

C0 02 E8 03 90 03 00 00 4A 37 17 30 30 22 17 00 41 2F 1C 00 B8 02 E8 03 C0 02 00 00 3D 2A 17 30

30 22 17 00 4A 37 17 00 70 03 A8 02 E8 03 00 00 11 0C 04 30 23 19 0E 00 30 22 17 00 90 03 C0 03

A0 03 00 00 41 2F 1C 30 4A 33 1C 00 3E 28 0E 00 50 00 90 01 A0 01 00 00 57 39 13 30 2B 1D 0A 00

3D 22 0E 00 90 01 C0 03 A0 01 00 00 2B 1D 0A 30 CB 85 2D 00 42 2B 0F 00 88 01 A8 03 B0 03 00 00

CA 9E 2E 30 E0 C9 9F 00 95 6B 1C 00 90 01 A0 03 C0 03 00 00 2B 1D 0A 30 3E 28 0E 00 4A 33 1C 00

90 01 88 01 B8 03 00 00 2B 1D 0A 30 CC 86 2D 00 75 4C 1A 00 88 01 A0 03 B8 03 00 00 CA 9E 59 30

2D 22 0E 00 88 51 1C 00 18 00 88 03 A8 03 00 00 D2 BD 69 30 4F 37 25 00 E0 CF 47 00 B0 03 A0 03

88 01 00 00 97 62 21 30 3E 28 0E 00 7B 5A 2E 00 A0 03 B0 03 A8 03 00 00 2B 15 0E 30 97 62 21 00

E0 CF 47 00 A8 03 88 03 98 03 00 00 E0 CF 47 30 4F 33 20 00 D7 8C 2F 00 98 03 A0 03 A8 03 00 00

99 62 25 30 3E 28 0E 00 E0 CE 83 00 88 03 A0 03 98 03 00 00 4F 33 20 30 3E 28 0E 00 D7 8C 2F 00

20 01 20 00 00 00 00 00 2B 1D 0A 30 E0 B6 3E 00 E0 A5 87 00 D8 02 58 03 28 02 00 00 1A 15 09 30

27 1E 12 00 1E 11 0E 00 D8 02 28 02 F0 01 00 00 1A 15 09 30 2B 19 0E 00 4F 33 11 00 E0 02 D8 02

F0 01 00 00 7B 51 20 30 1A 15 09 00 4F 33 11 00 60 03 D8 02 D0 02 00 00 1E 15 00 30 1A 15 09 00

1E 15 09 00 60 03 58 03 D8 02 00 00 1E 15 00 30 27 1E 12 00 1A 15 09 00 98 02 70 03 50 03 00 00

1A 11 05 30 11 0C 04 00 1E 15 00 00 50 03 B8 02 88 02 00 00 1E 15 00 30 3D 2A 17 00 4A 33 1C 00

50 03 88 02 58 03 00 00 1E 15 00 30 4A 33 1C 00 27 1E 12 00 50 03 70 03 B8 02 00 00 1E 15 00 30

11 0C 04 00 3D 2A 17 00 88 02 B8 02 F0 00 00 00 4A 33 1C 30 3D 2A 17 00 60 49 1C 00 70 03 98 02

90 02 00 00 11 0C 04 30 1A 11 05 00 1A 11 05 00 28 02 58 03 88 02 00 00 1E 11 0E 30 27 1E 12 00

4A 33 1C 00 98 02 60 03 B0 02 00 00 1A 11 05 30 1E 15 00 00 1E 15 09 00 60 03 98 02 58 03 00 00

1E 15 00 30 1A 11 05 00 27 1E 12 00 58 03 98 02 50 03 00 00 27 1E 12 30 1A 11 05 00 1E 15 00 00

D8 02 E0 02 C8 02 00 00 1A 15 09 30 7B 51 20 00 2B 1D 0A 00 E0 02 D0 02 C8 02 00 00 66 43 16 30

59 3A 13 00 2B 1D 0A 00 D0 02 D8 02 C8 02 00 00 1E 15 09 30 1A 15 09 00 2B 1D 0A 00 A0 00 30 02

E0 00 00 00 8C 6B 2A 30 9A 7B 30 00 E0 DB 52 00 E0 00 30 02 F8 00 00 00 E0 DB 52 30 9A 7B 30 00

23 11 0E 00 F0 00 B8 02 C0 00 00 00 60 49 1C 30 3D 2A 17 00 88 62 20 00 50 02 08 02 48 02 00 00

69 44 17 30 5E 3D 15 00 7E 53 1C 00 50 02 28 02 20 02 00 00 69 44 17 30 30 19 0E 00 D2 BD 38 00

B0 00 B8 02 C0 02 00 00 72 55 25 30 3D 2A 17 00 4A 37 17 00 C0 00 A0 00 E0 00 00 00 88 62 20 30

8C 6B 2A 00 E0 DB 52 00 B0 00 C0 02 D8 01 00 00 72 55 25 30 4A 37 17 00 CA 9E 2A 00 B0 00 C0 00

B8 02 00 00 72 55 25 30 88 62 20 00 3D 2A 17 00 08 02 50 02 20 02 00 00 5E 3D 15 30 69 44 17 00

D2 BD 38 00 68 00 98 02 B0 02 00 00 23 15 0E 30 1A 11 05 00 1E 15 09 00 28 00 90 02 68 00 00 00

23 19 0E 30 1A 11 05 00 23 15 0E 00 A8 02 28 00 A0 02 00 00 23 19 0E 30 23 19 0E 00 2F 1E 0A 00

90 02 28 00 A8 02 00 00 1A 11 05 30 23 19 0E 00 23 19 0E 00 98 02 68 00 90 02 00 00 1A 11 05 30

23 15 0E 00 1A 11 05 00 98 00 90 00 D0 01 00 00 81 55 1D 30 41 2B 1C 00 53 37 12 00 90 00 20 02

38 02 00 00 D2 BD 38 30 D2 BD 38 00 E0 DB 5A 00 60 01 80 00 18 02 00 00 3B 27 0D 30 52 36 12 00

58 3A 13 00 F0 00 C0 00 E0 00 00 00 60 49 1C 30 88 62 20 00 E0 DB 52 00 F0 03 E0 01 00 00 00 00

E0 BD 69 30 23 15 12 00 E0 A5 87 00 90 00 A8 00 D0 01 00 00 41 2A 1C 30 C1 7E 2B 00 53 37 12 00

A8 00 30 01 C8 01 00 00 C1 7E 2B 30 E0 DB 51 00 E0 B1 3C 00 30 02 A0 00 90 00 00 00 9A 7B 30 30

8C 6B 2A 00 65 33 25 00 C0 00 B8 00 A0 00 00 00 88 62 20 30 8C 62 25 00 8C 6B 2A 00 A0 00 C8 00

C0 01 00 00 8C 6B 2A 30 E0 DB 4B 00 62 40 15 00 B8 00 D8 00 C8 00 00 00 8C 62 25 30 E0 B7 3E 00

E0 DB 4B 00 D0 00 C0 01 D8 00 00 00 E0 DB 51 30 62 40 15 00 E0 B7 3E 00 F0 00 F8 00 88 02 00 00

60 49 1C 30 23 19 0E 00 4A 33 1C 00 38 02 28 02 F8 00 00 00 AF 89 3C 30 2B 19 0E 00 34 22 17 00

F8 00 30 02 40 02 00 00 6A 45 17 30 9A 7B 30 00 85 57 1E 00 38 02 20 02 28 02 00 00 AF 89 3C 30

D2 BD 38 00 30 19 0E 00 A8 01 E8 00 80 02 00 00 30 22 1C 30 E0 9A 34 00 71 49 19 00 E8 00 B0 01

80 02 00 00 E0 9A 34 30 2B 1D 0A 00 71 49 19 00 B0 01 A8 01 80 02 00 00 2B 1D 0A 30 30 22 1C 00

71 49 19 00 F8 00 28 02 88 02 00 00 23 19 0E 30 1E 11 0E 00 4A 33 1C 00 F0 00 B0 01 F8 00 00 00

6C 4B 35 30 2B 1D 0A 00 1E 15 0E 00 E8 00 A8 01 F0 00 00 00 E0 9A 34 30 30 22 1C 00 60 49 1C 00

B0 01 E8 00 F8 00 00 00 2B 1D 0A 30 E0 9A 34 00 23 1E 17 00 D8 01 18 00 10 01 00 00 AF 78 2A 30

E0 D8 4A 00 E0 DB 55 00 10 01 68 02 D0 00 00 00 C1 A8 41 30 6D 44 2A 00 E0 DB 51 00 20 00 10 01

18 00 00 00 AC 90 3E 30 E0 DB 55 00 E0 D8 4A 00 20 00 28 01 18 01 00 00 E0 B6 3E 30 4C 31 10 00

68 43 17 00 18 01 10 01 20 00 00 00 68 43 17 30 E0 DB 55 00 E0 B6 3E 00 00 01 08 01 78 02 00 00

E0 DB 4B 30 E0 C2 42 00 77 52 0A 00 28 01 00 01 78 02 00 00 4C 31 10 30 AC 86 4B 00 2E 1E 0A 00

18 01 28 01 78 02 00 00 68 43 17 30 4C 31 10 00 2E 1E 0A 00 08 01 18 01 78 02 00 00 E0 C2 42 30

68 43 17 00 2E 1E 0A 00 30 01 88 00 98 00 00 00 E0 DB 51 30 39 22 17 00 81 55 1D 00 78 01 58 01

F0 03 00 00 E0 BA 3F 30 81 55 1D 00 E0 BD 69 00 00 01 00 00 68 02 00 00 E0 DB 4B 30 83 67 20 00

6D 44 2A 00 20 01 00 01 28 01 00 00 2B 1D 0A 30 AC 86 4B 00 4C 31 10 00 00 01 20 01 00 00 00 00

AC 86 4B 30 2B 1D 0A 00 E0 B8 3E 00 D0 00 38 01 88 00 00 00 E0 DB 51 30 B8 92 33 00 39 22 17 00

88 00 38 01 40 01 00 00 39 22 17 30 B8 92 33 00 4A 33 1C 00 00 00 E0 01 38 01 00 00 E0 B8 3E 30

23 15 12 00 76 55 25 00 00 00 38 01 68 02 00 00 E0 B8 3E 30 E0 DB 4B 00 60 37 20 00 38 01 E0 01

50 01 00 00 76 55 25 30 23 15 12 00 64 41 16 00 50 01 E0 01 58 01 00 00 64 41 16 30 23 15 12 00

81 55 1D 00 88 00 48 01 58 01 00 00 39 22 17 30 76 4D 1A 00 81 55 1D 00 40 01 38 01 70 02 00 00

4A 33 1C 30 B8 92 33 00 2B 1D 0A 00 38 01 50 01 70 02 00 00 76 55 25 30 64 41 16 00 AF 80 1C 00

50 01 48 01 70 02 00 00 64 41 16 30 53 37 1C 00 2B 1D 0A 00 48 01 40 01 70 02 00 00 76 4D 1A 30

4A 33 1C 00 2B 1D 0A 00 78 01 F0 03 80 00 00 00 E0 BA 3F 30 E0 BD 69 00 52 36 12 00 18 02 68 01

60 01 00 00 58 3A 13 30 82 55 1D 00 3B 27 0D 00 68 01 58 02 60 02 00 00 30 1E 17 30 85 78 30 00

40 2A 0E 00 68 01 60 02 80 01 00 00 82 55 1D 30 40 2A 0E 00 46 2D 0F 00 60 02 70 01 80 01 00 00

40 2A 0E 30 80 54 1D 00 30 1B 0F 00 58 02 70 01 60 02 00 00 E0 DB 4C 30 80 54 1D 00 40 2A 0E 00

58 02 78 01 70 01 00 00 E0 DB 4C 30 E0 BA 3F 00 80 54 1D 00 80 01 80 00 68 01 00 00 46 2D 0F 30

52 36 12 00 82 55 1D 00 80 01 78 01 80 00 00 00 46 2D 0F 30 E0 BA 3F 00 52 36 12 00 68 01 18 02

58 02 00 00 30 1E 17 30 58 3A 13 00 85 78 30 00 78 01 58 02 90 00 00 00 E0 BA 3F 30 E0 DB 4C 00

41 2B 1C 00 90 00 58 02 18 02 00 00 41 2B 1C 30 E0 DB 4C 00 58 3A 13 00 08 02 28 02 48 02 00 00

5E 3D 15 30 2B 19 0E 00 2B 19 0E 00 28 02 50 02 48 02 00 00 2B 19 0E 30 69 44 17 00 2B 19 0E 00

20 02 90 00 18 02 00 00 D2 BD 38 30 D2 BD 38 00 58 3A 13 00 38 02 40 02 30 02 00 00 9A 7B 30 30

85 57 1E 00 9A 7B 30 00 38 02 F8 00 40 02 00 00 E0 DB 5A 30 34 22 17 00 9E 6B 1C 00 90 00 38 02

30 02 00 00 41 2B 1C 30 E0 DB 5A 00 E0 DB 5A 00 08 02 00 02 28 02 00 00 5E 3D 15 30 2B 1E 17 00

2B 19 0E 00 00 02 F0 01 28 02 00 00 2B 1E 17 30 4F 33 11 00 2B 19 0E 00 18 02 08 02 20 02 00 00

58 3A 13 30 5E 3D 15 00 D2 BD 38 00 18 02 F0 01 10 02 00 00 58 3A 13 30 4F 33 11 00 32 20 0B 00

F0 01 00 02 F8 01 00 00 4F 33 11 30 80 54 1D 00 94 61 21 00 F8 01 08 02 E8 01 00 00 2B 1E 17 30

5E 3D 15 00 4F 34 11 00 10 02 08 02 18 02 00 00 32 20 0B 30 5E 3D 15 00 58 3A 13 00 10 02 F0 01

E8 01 00 00 32 20 0B 30 4F 33 11 00 4F 34 11 00 08 02 F8 01 00 02 00 00 5E 3D 15 30 2B 1E 17 00

2B 1E 17 00 F0 01 F8 01 E8 01 00 00 4F 33 11 30 2B 1E 17 00 4F 34 11 00 88 00 78 01 90 00 00 00

39 22 17 30 E0 BA 3F 00 41 2B 1C 00 58 01 78 01 88 00 00 00 81 55 1D 30 E0 BA 3F 00 39 22 17 00

D8 01 10 01 D0 00 00 00 CA 9E 2A 30 C1 A8 41 00 E0 DB 51 00 D0 01 A8 00 C8 01 00 00 53 37 12 30

C1 7E 2B 00 E0 B1 3C 00 98 00 D0 01 C8 01 00 00 81 55 1D 30 53 37 12 00 E0 B1 3C 00 30 01 98 00

C8 01 00 00 E0 DB 51 30 81 55 1D 00 E0 B1 3C 00 30 01 A8 00 A0 00 00 00 E0 DB 51 30 C1 7E 2B 00

8C 6B 2A 00 C0 01 C8 00 B8 01 00 00 62 40 15 30 E0 DB 4B 00 E0 A9 3A 00 C8 00 D8 00 B8 01 00 00

E0 DB 4B 30 E0 B7 3E 00 E0 A9 3A 00 D8 00 C0 01 B8 01 00 00 E0 B7 3E 30 62 40 15 00 E0 A9 3A 00

B0 01 F0 00 A8 01 00 00 2B 1D 0A 30 60 49 1C 00 30 22 1C 00 40 00 50 00 A0 01 00 00 76 51 20 30

57 39 13 00 3D 22 0E 00 90 01 50 00 88 01 00 00 2B 1D 0A 30 57 39 13 00 CC 86 2D 00 30 01 A0 00

D0 00 00 00 E0 DB 51 30 8C 6B 2A 00 E0 DB 51 00 78 01 80 01 70 01 00 00 E0 BA 3F 30 46 2D 0F 00

80 54 1D 00 68 01 80 00 60 01 00 00 82 55 1D 30 52 36 12 00 3B 27 0D 00 48 01 88 00 40 01 00 00

76 4D 1A 30 39 22 17 00 4A 33 1C 00 38 01 D0 00 68 02 00 00 E0 DB 4B 30 E0 DB 51 00 60 37 20 00

88 00 30 01 D0 00 00 00 39 22 17 30 E0 DB 51 00 E0 DB 51 00 28 01 20 00 20 01 00 00 4C 31 10 30

E0 B6 3E 00 2B 1D 0A 00 10 01 18 01 08 01 00 00 CB B9 55 30 68 43 17 00 E0 C2 42 00 08 01 00 01

10 01 00 00 E0 C2 42 30 E0 DB 4B 00 E0 DB 55 00 F8 00 E8 00 E0 00 00 00 23 11 0E 30 E0 9A 34 00

E0 DB 52 00 E8 00 F0 00 E0 00 00 00 E0 9A 34 30 60 49 1C 00 E0 DB 52 00 C0 01 D0 00 A0 00 00 00

62 40 15 30 E0 DB 51 00 8C 6B 2A 00 D8 00 B8 00 D0 00 00 00 E0 B7 3E 30 8C 62 25 00 E0 DB 51 00

C8 00 A0 00 B8 00 00 00 E0 DB 4B 30 8C 6B 2A 00 8C 62 25 00 B8 00 C0 00 B0 00 00 00 8C 62 25 30

88 62 20 00 72 55 25 00 A8 00 90 00 A0 00 00 00 C1 7E 2B 30 41 2A 1C 00 8C 6B 2A 00 90 00 98 00

88 00 00 00 41 2B 1C 30 81 55 1D 00 39 22 17 00 08 02 10 02 E8 01 00 00 5E 3D 15 30 32 20 0B 00

4F 34 11 00 A8 03 20 00 18 00 00 00 E0 CF 47 30 E0 B6 3E 00 D2 BD 69 00 10 01 00 01 68 02 00 00

E0 DB 55 30 E0 DB 4B 00 6D 44 2A 00 58 01 E0 01 F0 03 00 00 81 55 1D 30 23 15 12 00 E0 BD 69 00

F8 03 50 01 00 04 00 00 61 3F 15 30 64 41 16 00 E0 9C 35 00 08 04 48 01 F8 03 00 00 6C 46 18 30

76 4D 1A 00 61 3F 15 00 F8 03 00 04 10 04 00 00 61 3F 15 30 E0 9C 35 00 6D 49 12 00 00 04 08 04

10 04 00 00 E0 9C 35 30 6C 46 18 00 6D 49 12 00 08 04 F8 03 10 04 00 00 6C 46 18 30 61 3F 15 00

2C 1D 0A 00 50 01 08 04 00 04 00 00 64 41 16 30 6C 46 18 00 E0 9C 35 00 50 01 F8 03 48 01 00 00

64 41 16 30 61 3F 15 00 76 4D 1A 00 A0 03 90 01 B8 03 00 00 3E 28 0E 30 2B 1D 0A 00 75 4C 1A 00

A0 03 88 03 90 03 00 00 3E 28 0E 30 4F 37 25 00 41 2F 1C 00 00 00 08 00 F0 03 00 00 EF C4 9E 30

EF AB 8B 00 EF A5 80 00 F0 03 08 00 10 00 00 00 EF A5 80 30 EF AB 8B 00 CE 8E 72 00 08 00 20 00

A8 03 00 00 EF AB 8B 30 EF C1 9C 00 CE 9D 87 00 48 00 50 00 40 00 00 00 CC 85 6E 30 5D 2D 1B 00

32 1E 14 00 78 00 80 00 F0 03 00 00 6E 3B 29 30 62 37 24 00 EF A5 80 00 78 00 F0 03 10 00 00 00

6E 3B 29 30 EF A5 80 00 CE 8E 72 00 50 00 98 01 88 01 00 00 5D 2D 1B 30 C5 83 6A 00 D6 8E 72 00

00 03 F0 02 F8 02 00 00 62 49 29 30 7E 52 3B 00 7B 40 32 00 10 03 18 03 48 00 00 00 CC 85 6E 30

EF BC 98 00 CC 85 6E 00 88 01 98 01 08 00 00 00 D6 8E 72 30 C5 83 6A 00 EF AB 8B 00 E0 02 E8 02

D0 02 00 00 5D 3B 28 30 6B 3B 2D 00 34 21 19 00 F0 01 78 00 E0 02 00 00 46 20 16 30 6E 3B 29 00

5D 3B 28 00 80 00 78 00 18 02 00 00 62 37 24 30 6E 3B 29 00 5C 3D 21 00 08 03 00 03 20 03 00 00

5D 37 2D 30 96 63 49 00 5D 37 2D 00 F0 02 00 03 08 03 00 00 7E 52 3B 30 96 63 49 00 62 3B 2D 00

F8 02 28 03 00 03 00 00 7B 40 32 30 B4 80 63 00 4B 24 16 00 B0 02 38 03 30 03 00 00 2D 1E 19 30

46 24 16 00 2E 1B 12 00 40 03 70 00 60 00 00 00 2A 1B 12 30 33 20 16 00 2D 1E 19 00 08 03 48 03

D0 02 00 00 62 3B 2D 30 2D 1E 19 00 38 1B 12 00 58 00 20 03 68 03 00 00 17 09 04 30 5D 37 2D 00

38 20 16 00 20 03 58 00 48 03 00 00 5D 37 2D 30 17 09 04 00 2D 1E 19 00 20 03 48 03 08 03 00 00

5D 37 2D 30 2D 1E 19 00 5D 37 2D 00 D0 02 E8 02 08 03 00 00 34 21 19 30 6B 3B 2D 00 62 3B 2D 00

48 03 58 00 B0 02 00 00 2D 1E 19 30 17 09 04 00 2D 1E 19 00 B0 02 58 00 68 00 00 00 28 1E 0F 30

17 09 04 00 28 1E 0F 00 B0 02 30 03 48 03 00 00 2D 1E 19 30 2E 1B 12 00 2D 1E 19 00 E8 02 E0 02

78 00 00 00 6B 3B 2D 30 5D 3B 28 00 6E 3B 29 00 D0 02 78 03 60 03 00 00 38 1B 12 30 73 46 2D 00

24 19 0A 00 48 03 30 03 78 03 00 00 2D 1E 19 30 2E 1B 12 00 73 46 2D 00 38 03 60 03 78 03 00 00

46 24 16 30 24 19 0A 00 73 46 2D 00 38 03 B0 02 60 03 00 00 46 24 16 30 2D 1E 19 00 24 19 0A 00

78 03 30 03 38 03 00 00 73 46 2D 30 2E 1B 12 00 46 24 16 00 48 03 78 03 D0 02 00 00 2D 1E 19 30

73 46 2D 00 38 1B 12 00 78 00 F0 01 18 02 00 00 6E 3B 29 30 46 20 16 00 5C 3D 21 00 60 00 80 03

40 03 00 00 2D 1E 19 30 2D 1E 19 00 2A 1B 12 00 68 03 38 00 58 00 00 00 38 20 16 30 17 09 04 00

17 09 04 00 28 03 10 03 00 03 00 00 B4 80 63 30 B7 6E 49 00 66 43 2C 00 40 03 30 00 70 00 00 00

2A 1B 12 30 2D 1E 19 00 33 20 16 00 C8 03 40 00 A0 01 00 00 82 5F 4B 30 3C 23 1E 00 46 24 16 00

D8 03 C8 03 D0 03 00 00 33 20 0D 30 82 5F 4B 00 4F 2D 29 00 A0 02 D0 03 C0 03 00 00 2A 16 09 30

4F 2D 29 00 2D 23 19 00 C0 03 D0 03 C8 03 00 00 2D 23 19 30 4F 2D 29 00 82 5F 4B 00 D8 03 40 00

C8 03 00 00 33 20 0D 30 3C 23 1E 00 82 5F 4B 00 C8 03 A0 01 C0 03 00 00 E0 97 80 30 46 2E 25 00

2D 23 19 00 D8 03 A0 02 40 00 00 00 33 20 0D 30 2A 16 09 00 4B 29 12 00 38 00 A0 02 28 00 00 00

17 09 04 30 2A 16 09 00 2D 1E 19 00 38 00 40 00 A0 02 00 00 17 09 04 30 32 1E 14 00 2A 16 09 00

40 00 E0 03 48 00 00 00 32 1E 14 30 69 45 37 00 CC 85 6E 00 38 00 E0 03 40 00 00 00 17 09 04 30

69 45 37 00 32 1E 14 00 E0 03 38 00 68 03 00 00 69 45 37 30 17 09 04 00 38 20 16 00 50 00 48 00

98 01 00 00 5D 2D 1B 30 CC 85 6E 00 C5 83 6A 00 30 00 40 03 80 03 00 00 2D 1E 19 30 2A 1B 12 00

2D 1E 19 00 D0 03 A0 02 D8 03 00 00 4F 2D 29 30 2A 16 09 00 33 20 0D 00 28 03 F8 02 10 03 00 00

B4 80 63 30 9D 5B 45 00 CC 85 6E 00 F8 02 18 03 10 03 00 00 9D 5B 45 30 EF BC 98 00 CC 85 6E 00

10 03 48 00 E0 03 00 00 CC 85 6E 30 CC 85 6E 00 69 45 37 00 08 00 00 00 20 00 00 00 EF AB 8B 30

EF C4 9E 00 EF C1 9C 00 08 00 A8 03 88 01 00 00 EF AB 8B 30 CE 9D 87 00 D6 8E 72 00 98 01 10 00

08 00 00 00 C5 83 6A 30 CE 8E 72 00 EF AB 8B 00 10 00 98 01 18 03 00 00 CE 8E 72 30 C5 83 6A 00

EF BC 98 00 F8 02 10 00 18 03 00 00 9D 5B 45 30 CE 8E 72 00 EF BC 98 00 18 03 98 01 48 00 00 00

EF BC 98 30 C5 83 6A 00 CC 85 6E 00 10 00 E8 02 78 00 00 00 CE 8E 72 30 6B 3B 2D 00 6E 3B 29 00

F0 02 E8 02 10 00 00 00 7E 52 3B 30 6B 3B 2D 00 CE 8E 72 00 E8 02 F0 02 08 03 00 00 6B 3B 2D 30

7E 52 3B 00 62 3B 2D 00 10 00 F8 02 F0 02 00 00 CE 8E 72 30 7B 40 32 00 7E 52 3B 00 00 03 68 03

20 03 00 00 96 63 49 30 38 20 16 00 5D 37 2D 00 00 03 10 03 68 03 00 00 96 63 49 30 CC 85 6E 00

38 20 16 00 68 03 10 03 E0 03 00 00 38 20 16 30 CC 85 6E 00 69 45 37 00 05 00 00 00 48 01 08 04

58 01 50 01 76 4D 1A 38 6C 46 18 00 81 55 1D 00 64 41 16 00 38 00 28 00 80 03 30 00 17 09 04 38

2D 1E 19 00 2D 1E 19 00 2D 1E 19 00 60 00 58 00 80 03 38 00 2D 1E 19 38 17 09 04 00 2D 1E 19 00

17 09 04 00 30 00 28 00 70 00 68 00 2D 1E 19 38 2D 1E 19 00 33 20 16 00 2D 1E 19 00 70 00 68 00

60 00 58 00 33 20 16 38 2D 1E 19 00 2D 1E 19 00 17 09 04 00

  
  
  
Bone 6 \[at offset 0x00002CA8\]:

  
C8 00 00 00 1A 00 00 00 C8 FF 00 00 18 00 00 00 7C FF 00 00 00 00 E9 FF C0 FF 00 00 DD FF 25 00

25 00 00 00 12 00 28 00 24 00 00 00 E9 FF FF FF 38 00 00 00 DE FF 3D 00 EB FF 00 00 C7 FF FB FF

FC FF 00 00 1F 00 39 00 EE FF 00 00 E2 FF BF FF E6 FF 00 00 DF FF CC FF 22 00 00 00 1C 00 C9 FF

ED FF 00 00 0D 00 D5 FF 23 00 00 00 06 00 2E 00 E5 FF 00 00 D4 FF FD FF D9 FF 00 00 01 00 16 00

C0 FF 00 00 00 00 D5 FF E3 FF 00 00 21 00 FF FF 32 00 00 00 51 00 FE FF 08 00 00 00 2B 00 FD FF

EE FF 00 00 01 00 00 00 67 FF 00 00 00 00 EC FF 7C FF 00 00 ED FF 00 00 7C FF 00 00 01 00 15 00

7C FF 00 00 EB FF 00 00 C8 FF 00 00 00 00 25 00 00 00 00 00 28 00 00 00 10 00 08 00 A8 00 00 00

78 4B 3C 30 46 23 1E 00 AF 7D 5F 00 B8 00 A0 00 08 00 00 00 5A 37 2D 30 46 37 32 00 46 23 1E 00

B0 00 A0 00 B8 00 00 00 64 46 37 30 46 37 32 00 5A 37 2D 00 B0 00 A8 00 A0 00 00 00 64 46 37 30

AF 7D 5F 00 46 37 32 00 A8 00 08 00 A0 00 00 00 AF 7D 5F 30 46 23 1E 00 46 37 32 00 08 00 10 00

00 00 00 00 46 23 1E 30 78 4B 3C 00 32 19 14 00 78 00 70 00 C0 00 00 00 1E 14 0F 30 1E 14 0F 00

0F 0A 00 00 C0 00 70 00 10 00 00 00 0F 0A 00 30 1E 14 0F 00 78 4B 3C 00 10 00 70 00 80 00 00 00

78 4B 3C 30 1E 14 0F 00 14 08 0A 00 70 00 78 00 68 00 00 00 1E 14 0F 30 1E 14 0F 00 0F 0A 00 00

80 00 00 00 10 00 00 00 14 08 0A 30 32 19 14 00 78 4B 3C 00 00 00 80 00 98 00 00 00 32 19 14 30

14 08 0A 00 14 08 0A 00 68 00 00 00 98 00 00 00 0F 0A 00 30 32 19 14 00 14 08 0A 00 00 00 68 00

78 00 00 00 32 19 14 30 0F 0A 00 00 1E 14 0F 00 20 00 28 00 18 00 00 00 1C 1A 1A 30 0E 0E 0C 00

0A 0F 0F 00 18 00 38 00 30 00 00 00 0A 0F 0F 30 1C 1C 19 00 19 1E 1E 00 20 00 30 00 40 00 00 00

1C 1A 1A 30 19 1E 1E 00 19 19 16 00 38 00 50 00 48 00 00 00 1C 1C 19 30 20 19 10 00 15 16 13 00

48 00 60 00 58 00 00 00 15 16 13 30 69 7A 7A 00 1C 1A 1A 00 60 00 28 00 88 00 00 00 69 7A 7A 30

0E 0E 0C 00 87 9B 9B 00 20 00 90 00 88 00 00 00 1C 1A 1A 30 0F 0D 0E 00 87 9B 9B 00 90 00 60 00

88 00 00 00 0F 0D 0E 30 69 7A 7A 00 87 9B 9B 00 30 00 70 00 68 00 00 00 0F 0F 0A 30 0F 10 0E 00

05 0A 0F 00 98 00 40 00 68 00 00 00 04 04 03 30 19 19 16 00 05 0A 0F 00 80 00 58 00 98 00 00 00

04 04 03 30 0A 0D 0D 00 04 04 03 00 70 00 48 00 80 00 00 00 0F 10 0E 30 15 16 13 00 04 04 03 00

40 00 98 00 90 00 00 00 19 19 16 30 04 04 03 00 11 11 13 00 98 00 58 00 90 00 00 00 04 04 03 30

0A 0D 0D 00 11 11 13 00 28 00 60 00 50 00 00 00 0E 0E 0C 30 69 7A 7A 00 20 19 10 00 28 00 20 00

88 00 00 00 0E 0E 0C 30 1C 1A 1A 00 87 9B 9B 00 90 00 58 00 60 00 00 00 0F 0D 0E 30 1C 1A 1A 00

69 7A 7A 00 40 00 90 00 20 00 00 00 19 19 16 30 0F 0D 0E 00 1C 1A 1A 00 60 00 48 00 50 00 00 00

69 7A 7A 30 15 16 13 00 20 19 10 00 48 00 58 00 80 00 00 00 15 16 13 30 0A 0D 0D 00 04 04 03 00

28 00 50 00 38 00 00 00 0E 0E 0C 30 20 19 10 00 1C 1C 19 00 48 00 70 00 38 00 00 00 15 16 13 30

0F 10 0E 00 1C 1C 19 00 40 00 30 00 68 00 00 00 19 19 16 30 0F 0F 0A 00 05 0A 0F 00 30 00 20 00

18 00 00 00 19 1E 1E 30 1C 1A 1A 00 0A 0F 0F 00 18 00 28 00 38 00 00 00 0A 0F 0F 30 0E 0E 0C 00

1C 1C 19 00 70 00 30 00 38 00 00 00 0F 10 0E 30 0F 0F 0A 00 1C 1C 19 00 03 00 00 00 10 00 A8 00

C0 00 B0 00 78 4B 3C 38 AF 7D 5F 00 0F 0A 00 00 64 46 37 00 08 00 00 00 B8 00 78 00 46 23 1E 38

32 19 14 00 5A 37 2D 00 1E 14 0F 00 78 00 C0 00 B8 00 B0 00 1E 14 0F 38 0F 0A 00 00 5A 37 2D 00

64 46 37 00

  
  
  
Bone 7 \[at offset 0x000030EC\]:

  
98 00 00 00 20 00 FF FF CD FF 00 00 00 00 20 00 CD FF 00 00 E3 FF 01 00 CD FF 00 00 00 00 E2 FF

CD FF 00 00 00 00 DA FF CD FF 00 00 DB FF 00 00 CD FF 00 00 00 00 27 00 CD FF 00 00 28 00 FE FF

CD FF 00 00 F9 FF 28 00 7F FF 00 00 DB FF 00 00 7F FF 00 00 00 00 DA FF 7F FF 00 00 28 00 FD FF

7F FF 00 00 E2 FF 02 00 F1 FF 00 00 00 00 1F 00 E6 FF 00 00 00 00 E2 FF EA FF 00 00 EC FF 00 00

FB FF 00 00 00 00 00 00 0C 00 00 00 13 00 00 00 FC FF 00 00 20 00 FF FF F1 FF 00 00 00 00 25 00

00 00 00 00 08 00 00 00 78 00 70 00 60 00 00 00 64 46 37 30 C8 87 6E 00 4B 28 19 00 70 00 78 00

80 00 00 00 C8 87 6E 30 64 46 37 00 46 28 23 00 88 00 70 00 80 00 00 00 46 23 14 30 C8 87 6E 00

46 28 23 00 70 00 88 00 90 00 00 00 C8 87 6E 30 46 23 14 00 46 23 19 00 88 00 68 00 90 00 00 00

46 23 14 30 46 28 23 00 46 23 19 00 80 00 68 00 88 00 00 00 46 28 23 30 46 28 23 00 46 23 14 00

78 00 68 00 80 00 00 00 64 46 37 30 46 28 23 00 46 28 23 00 68 00 78 00 60 00 00 00 46 28 23 30

64 46 37 00 4B 28 19 00 0B 00 00 00 08 00 10 00 00 00 18 00 7E 55 45 38 51 37 2C 00 31 21 1B 00

4D 34 2A 00 28 00 30 00 20 00 38 00 14 19 28 38 14 14 19 00 91 B4 C3 00 41 50 5A 00 48 00 50 00

40 00 58 00 0F 14 14 38 19 19 1E 00 1B 1B 1B 00 1B 1B 1B 00 30 00 28 00 40 00 48 00 3C 32 3C 38

37 2D 37 00 37 2D 37 00 19 0F 19 00 38 00 30 00 58 00 40 00 0F 0A 14 38 3C 32 3C 00 14 0F 19 00

37 2D 37 00 20 00 38 00 50 00 58 00 41 50 5A 38 0F 0A 14 00 96 AF B9 00 14 0F 19 00 20 00 50 00

28 00 48 00 41 50 5A 38 8C 96 A5 00 37 2D 37 00 19 0F 19 00 90 00 68 00 00 00 08 00 23 14 0A 38

37 2D 37 00 14 14 0F 00 37 28 37 00 10 00 08 00 60 00 68 00 14 14 0F 38 37 28 37 00 2D 23 1E 00

37 2D 37 00 18 00 10 00 70 00 60 00 69 64 55 38 14 14 0F 00 A0 9B 82 00 2D 23 1E 00 00 00 18 00

90 00 70 00 14 14 0F 38 69 64 55 00 23 14 0A 00 A0 9B 82 00

  
  
  
Bone 8 \[at offset 0x00003340\]:

  
00 01 00 00 E0 FF D5 FF BF FF 00 00 DB FF DB FF C3 FF 00 00 D9 FF D4 FF C4 FF 00 00 F4 FF 20 00 A3 FF 00 00 F0 FF 1E 00 B2 FF 00 00 D6 FF 1A 00 AB FF 00 00 D3 FF DA FF C8 FF 00 00 E1 FF DB FF DA FF 00 00 F8 FF D1 FF CB FF 00 00 EA FF E2 FF CB FF 00 00 0A 00 23 00 B8 FF 00 00 F6 FF EA FF 9B FF 00 00 F2 FF E7 FF AB FF 00 00 0C 00 E1 FF AE FF 00 00 13 00 1D 00 F2 FF 00 00 F5 FF 1F 00 D8 FF 00 00 F9 FF 21 00 C1 FF 00 00 15 00 FE FF F2 FF 00 00 0F 00 DF FF C9 FF 00 00 F7 FF FF FF D3 FF 00 00 F9 FF E1 FF B8 FF 00 00 01 00 00 00 01 00 00 00 F0 FF 00 00 F2 FF 00 00 F0 FF 1D 00 F2 FF 00 00 ED FF E3 FF F2 FF 00 00 0B 00 E3 FF F2 FF 00 00 F7 FF E0 FF C9 FF 00 00 EF FF C9 FF D8 FF 00 00 EA FF F3 FF E7 FF 00 00 D8 FF 18 00 B6 FF 00 00 DA FF E7 FF B0 FF 00 00 D7 FF E9 FF A5 FF 00 00 00 00 25 00 00 00 00 00 28 00 00 00 60 00 68 00 58 00 00 00 70 70 70 30 23 28 2D 00 15 15 15 00 68 00 60 00 A0 00 00 00 23 28 2D 30 70 70 70 00 14 19 1E 00 20 00 50 00 80 00 00 00 37 3C 46 30 19 19 0F 00 1E 23 2D 00 50 00 20 00 18 00 00 00 19 19 0F 30 37 3C 46 00 19 19 0F 00 20 00 28 00 18 00 00 00 37 3C 46 30 32 28 32 00 19 19 0F 00 28 00 20 00 E8 00 00 00 32 28 32 30 37 3C 46 00 3C 37 2D 00 10 00 08 00 30 00 00 00 1C 1C 24 30 23 28 2D 00 3B 3B 3B 00 08 00 10 00 00 00 00 00 23 28 2D 30 1C 1C 24 00 15 15 15 00 48 00 00 00 40 00 00 00 14 14 1E 30 15 15 15 00 15 15 15 00 00 00 48 00 08 00 00 00 15 15 15 30 14 14 1E 00 23 28 2D 00 48 00 38 00 08 00 00 00 14 14 1E 30 19 1E 23 00 23 28 2D 00 08 00 38 00 30 00 00 00 23 28 2D 30 19 1E 23 00 3B 3B 3B 00 D8 00 90 00 40 00 00 00 23 23 23 30 09 09 09 00 03 03 03 00 78 00 70 00 B8 00 00 00 06 06 06 30 02 02 02 00 04 04 04 00 48 00 E0 00 38 00 00 00 08 08 08 30 0A 0A 0A 00 09 09 09 00 E0 00 C0 00 38 00 00 00 0A 0A 0A 30 23 23 23 00 09 09 09 00 98 00 D0 00 A0 00 00 00 03 03 03 30 04 04 04 00 03 03 03 00 D0 00 90 00 68 00 00 00 04 04 04 30 09 09 09 00 08 08 08 00 98 00 80 00 78 00 00 00 03 03 03 30 06 06 06 00 06 06 06 00 C8 00 D8 00 C0 00 00 00 1F 1F 1F 30 23 23 23 00 23 23 23 00 40 00 90 00 D0 00 00 00 03 03 03 30 09 09 09 00 04 04 04 00 D0 00 68 00 A0 00 00 00 04 04 04 30 08 08 08 00 03 03 03 00 E0 00 98 00 B0 00 00 00 0A 0A 0A 30 03 03 03 00 06 06 06 00 C0 00 E0 00 B0 00 00 00 23 23 23 30 0A 0A 0A 00 06 06 06 00 50 00 88 00 70 00 00 00 07 07 07 30 0A 0A 0A 00 02 02 02 00 88 00 90 00 C8 00 00 00 0A 0A 0A 30 09 09 09 00 1F 1F 1F 00 E0 00 D0 00 98 00 00 00 0A 0A 0A 30 04 04 04 00 03 03 03 00 E0 00 48 00 D0 00 00 00 0A 0A 0A 30 08 08 08 00 04 04 04 00 C0 00 D8 00 38 00 00 00 23 23 23 30 23 23 23 00 09 09 09 00 90 00 D8 00 C8 00 00 00 09 09 09 30 23 23 23 00 1F 1F 1F 00 40 00 D0 00 48 00 00 00 03 03 03 30 04 04 04 00 08 08 08 00 B8 00 70 00 A8 00 00 00 04 04 04 30 02 02 02 00 09 09 09 00 70 00 88 00 A8 00 00 00 02 02 02 30 0A 0A 0A 00 09 09 09 00 88 00 C8 00 A8 00 00 00 0A 0A 0A 30 1F 1F 1F 00 09 09 09 00 C8 00 C0 00 A8 00 00 00 1F 1F 1F 30 23 23 23 00 09 09 09 00 C0 00 B0 00 A8 00 00 00 23 23 23 30 06 06 06 00 09 09 09 00 B0 00 B8 00 A8 00 00 00 06 06 06 30 04 04 04 00 09 09 09 00 98 00 A0 00 80 00 00 00 03 03 03 30 03 03 03 00 06 06 06 00 88 00 68 00 90 00 00 00 0A 0A 0A 30 08 08 08 00 09 09 09 00 88 00 50 00 68 00 00 00 0A 0A 0A 30 07 07 07 00 08 08 08 00 0A 00 00 00 60 00 20 00 A0 00 80 00 70 70 70 38 37 3C 46 00 14 19 1E 00 1E 23 2D 00 60 00 F0 00 20 00 E8 00 70 70 70 38 82 82 82 00 37 3C 46 00 3C 37 2D 00 E8 00 F0 00 28 00 F8 00 3C 37 2D 38 82 82 82 00 32 28 32 00 41 32 41 00 60 00 58 00 F0 00 F8 00 70 70 70 38 15 15 15 00 82 82 82 00 41 32 41 00 58 00 18 00 F8 00 28 00 15 15 15 38 19 19 0F 00 41 32 41 00 32 28 32 00 18 00 58 00 50 00 68 00 19 19 0F 38 15 15 15 00 19 19 0F 00 23 28 2D 00 38 00 D8 00 30 00 10 00 19 1E 23 38 9B 96 8C 00 3B 3B 3B 00 50 50 4B 00 D8 00 40 00 10 00 00 00 9B 96 8C 38 15 15 15 00 50 50 4B 00 15 15 15 00 B0 00 98 00 B8 00 78 00 06 06 06 38 03 03 03 00 04 04 04 00 06 06 06 00 70 00 78 00 50 00 80 00 02 02 02 38 06 06 06 00 07 07 07 00 06 06 06 00

  
  
  
Bone 11 \[at offset 0x00003864\]:

  
C0 00 00 00 E6 FF 00 00 C8 FF 00 00 00 00 E9 FF C0 FF 00 00 E8 FF 00 00 7C FF 00 00 FF FF 12 00

1F 00 00 00 F6 FF FF FF 23 00 00 00 EE FF 23 00 F1 FF 00 00 03 00 EC FF 1E 00 00 00 F1 FF DE FF

F1 FF 00 00 D5 FF FD FF EE FF 00 00 22 00 16 00 18 00 00 00 24 00 FF FF 22 00 00 00 0E 00 26 00

F3 FF 00 00 25 00 FB FF FC FF 00 00 0B 00 D8 FF EE FF 00 00 20 00 E8 FF 16 00 00 00 FA FF 1A 00

D8 FF 00 00 FF FF 16 00 C0 FF 00 00 19 00 FD FF D9 FF 00 00 00 00 E6 FF D6 FF 00 00 FF FF 00 00

67 FF 00 00 00 00 EC FF 7C FF 00 00 13 00 00 00 7C FF 00 00 FF FF 15 00 7C FF 00 00 15 00 00 00

C8 FF 00 00 00 00 25 00 00 00 00 00 26 00 00 00 08 00 10 00 00 00 00 00 96 5F 50 30 41 28 19 00

2D 19 14 00 20 00 28 00 18 00 00 00 7D 46 32 30 2D 19 14 00 5A 37 23 00 38 00 20 00 30 00 00 00

AA 73 55 30 7D 46 32 00 C8 96 6E 00 20 00 40 00 28 00 00 00 7D 46 32 30 37 23 19 00 2D 19 14 00

38 00 40 00 20 00 00 00 AA 73 55 30 37 23 19 00 7D 46 32 00 50 00 18 00 48 00 00 00 46 1C 14 30

5A 37 23 00 2D 19 14 00 60 00 48 00 58 00 00 00 2D 1E 19 30 2D 19 14 00 23 14 0F 00 58 00 18 00

28 00 00 00 23 14 0F 30 5A 37 23 00 2D 19 14 00 70 00 60 00 68 00 00 00 7D 46 3C 30 2D 1E 19 00

E0 98 7B 00 30 00 68 00 38 00 00 00 C8 96 6E 30 E0 98 7B 00 AA 73 55 00 80 00 88 00 78 00 00 00

2D 19 14 30 2D 19 14 00 19 0F 05 00 88 00 08 00 90 00 00 00 2D 19 14 30 96 5F 50 00 6E 3C 37 00

50 00 30 00 20 00 00 00 46 1C 14 30 C8 96 6E 00 7D 46 32 00 90 00 00 00 40 00 00 00 6E 3C 37 30

2D 19 14 00 37 23 19 00 00 00 78 00 40 00 00 00 2D 19 14 30 19 0F 05 00 37 23 19 00 88 00 58 00

78 00 00 00 2D 19 14 30 23 14 0F 00 19 0F 05 00 28 00 40 00 78 00 00 00 2D 19 14 30 37 23 19 00

19 0F 05 00 38 00 90 00 40 00 00 00 AA 73 55 30 6E 3C 37 00 37 23 19 00 68 00 88 00 90 00 00 00

E0 98 7B 30 2D 19 14 00 6E 3C 37 00 10 00 A0 00 98 00 00 00 41 28 19 30 7D 55 46 00 46 23 23 00

A0 00 A8 00 98 00 00 00 7D 55 46 30 46 23 23 00 46 23 23 00 98 00 A8 00 B0 00 00 00 46 23 23 30

46 23 23 00 46 23 23 00 98 00 B0 00 10 00 00 00 46 23 23 30 46 23 23 00 41 28 19 00 10 00 08 00

A0 00 00 00 41 28 19 30 96 5F 50 00 7D 55 46 00 30 00 50 00 70 00 00 00 C8 96 6E 30 46 1C 14 00

7D 46 3C 00 18 00 50 00 20 00 00 00 5A 37 23 30 46 1C 14 00 7D 46 32 00 88 00 B8 00 08 00 00 00

2D 19 14 30 2D 19 14 00 96 5F 50 00 88 00 80 00 B8 00 00 00 2D 19 14 30 2D 19 14 00 2D 19 14 00

78 00 00 00 80 00 00 00 19 0F 05 30 2D 19 14 00 2D 19 14 00 00 00 90 00 08 00 00 00 2D 19 14 30

6E 3C 37 00 96 5F 50 00 68 00 30 00 70 00 00 00 E0 98 7B 30 C8 96 6E 00 7D 46 3C 00 38 00 68 00

90 00 00 00 AA 73 55 30 E0 98 7B 00 6E 3C 37 00 70 00 50 00 60 00 00 00 7D 46 3C 30 46 1C 14 00

2D 1E 19 00 88 00 68 00 60 00 00 00 2D 19 14 30 E0 98 7B 00 2D 1E 19 00 58 00 28 00 78 00 00 00

23 14 0F 30 2D 19 14 00 19 0F 05 00 18 00 58 00 48 00 00 00 5A 37 23 30 23 14 0F 00 2D 19 14 00

50 00 48 00 60 00 00 00 46 1C 14 30 2D 19 14 00 2D 1E 19 00 58 00 88 00 60 00 00 00 23 14 0F 30

2D 19 14 00 2D 1E 19 00 03 00 00 00 B8 00 80 00 A8 00 B0 00 2D 19 14 38 2D 19 14 00 46 23 23 00

46 23 23 00 00 00 10 00 80 00 B0 00 2D 19 14 38 41 28 19 00 2D 19 14 00 46 23 23 00 A0 00 08 00

A8 00 B8 00 7D 55 46 38 96 5F 50 00 46 23 23 00 2D 19 14 00

  
  
  
Bone 12 \[at offset 0x00003C78\]:

  
58 00 00 00 00 00 1F 00 E8 FF 00 00 00 00 20 00 80 FF 00 00 1E 00 02 00 E5 FF 00 00 1D 00 00 00

7F FF 00 00 E0 FF FE FF 80 FF 00 00 00 00 E2 FF 7F FF 00 00 14 00 00 00 FB FF 00 00 E0 FF FF FF

E7 FF 00 00 ED FF 00 00 FC FF 00 00 00 00 E2 FF F1 FF 00 00 00 00 00 00 0C 00 00 00 00 00 25 00

00 00 00 00 0A 00 00 00 08 00 10 00 00 00 00 00 37 1E 19 30 4B 2D 28 00 2D 1E 0F 00 30 00 00 00

10 00 00 00 5F 37 32 30 2D 1E 0F 00 4B 2D 28 00 40 00 48 00 38 00 00 00 41 28 23 30 96 5A 50 00

48 28 23 00 48 00 30 00 10 00 00 00 96 5A 50 30 5F 37 32 00 4B 2D 28 00 00 00 40 00 38 00 00 00

2D 1E 0F 30 41 28 23 00 48 28 23 00 40 00 00 00 50 00 00 00 41 28 23 30 2D 1E 0F 00 55 3C 28 00

30 00 48 00 50 00 00 00 5F 37 32 30 96 5A 50 00 55 3C 28 00 48 00 40 00 50 00 00 00 96 5A 50 30

41 28 23 00 55 3C 28 00 00 00 30 00 50 00 00 00 2D 1E 0F 30 5F 37 32 00 55 3C 28 00 10 00 08 00

18 00 00 00 4B 2D 28 30 37 1E 19 00 64 3C 28 00 04 00 00 00 08 00 20 00 18 00 28 00 50 32 28 38

32 1E 14 00 31 21 1B 00 AF 87 6E 00 10 00 18 00 48 00 28 00 4B 2D 28 38 64 3C 28 00 96 5A 50 00

AF 87 6E 00 48 00 28 00 38 00 20 00 96 5A 50 38 AF 87 6E 00 48 28 23 00 32 1E 14 00 38 00 20 00

00 00 08 00 48 28 23 38 32 1E 14 00 2D 1E 0F 00 37 1E 19 00

  
  
  
Bone 13 \[at offset 0x00003E0C\]:

  
00 01 00 00 0F 00 E9 FF 9D FF 00 00 0F 00 E7 FF A8 FF 00 00 12 00 18 00 AE FF 00 00 0E 00 F3 FF

E2 FF 00 00 05 00 C9 FF D5 FF 00 00 FB FF E0 FF C9 FF 00 00 F2 FF E3 FF F5 FF 00 00 0E 00 E3 FF

ED FF 00 00 0B 00 1D 00 EE FF 00 00 0B 00 00 00 EE FF 00 00 FF FF 00 00 02 00 00 00 F4 FF E1 FF

B8 FF 00 00 FE FF FF FF D2 FF 00 00 E3 FF DF FF CF FF 00 00 E8 FF FE FF F8 FF 00 00 F7 FF 21 00

C1 FF 00 00 00 00 1F 00 D6 FF 00 00 EA FF 1D 00 F7 FF 00 00 DE FF E1 FF B4 FF 00 00 F8 FF E7 FF

AA FF 00 00 F0 FF EA FF 9B FF 00 00 E3 FF 23 00 BE FF 00 00 07 00 E2 FF C7 FF 00 00 FB FF D1 FF

CB FF 00 00 14 00 DB FF D3 FF 00 00 1C 00 DA FF BE FF 00 00 11 00 1A 00 A3 FF 00 00 FB FF 1E 00

B1 FF 00 00 F3 FF 20 00 A3 FF 00 00 16 00 D4 FF BB FF 00 00 13 00 DB FF BB FF 00 00 0D 00 D5 FF

B8 FF 00 00 00 00 25 00 00 00 00 00 28 00 00 00 90 00 98 00 A0 00 00 00 19 19 23 30 6E 69 69 00

17 17 17 00 98 00 90 00 58 00 00 00 6E 69 69 30 19 19 23 00 28 2D 32 00 A8 00 D8 00 78 00 00 00

37 2D 37 30 37 3C 4B 00 19 1E 1E 00 D8 00 A8 00 E0 00 00 00 37 3C 4B 30 37 2D 37 00 37 2D 37 00

D0 00 D8 00 E0 00 00 00 37 2D 37 30 37 3C 4B 00 37 2D 37 00 D8 00 D0 00 10 00 00 00 37 3C 4B 30

37 2D 37 00 64 69 69 00 F0 00 E8 00 C8 00 00 00 2B 2B 2B 30 87 8C 91 00 5A 5A 5A 00 E8 00 F0 00

F8 00 00 00 87 8C 91 30 2B 2B 2B 00 15 15 15 00 F8 00 B0 00 B8 00 00 00 15 15 15 30 0F 14 19 00

0F 14 19 00 B0 00 F8 00 F0 00 00 00 0F 14 19 30 15 15 15 00 2B 2B 2B 00 C0 00 B0 00 F0 00 00 00

5F 5F 64 30 0F 14 19 00 2B 2B 2B 00 C0 00 F0 00 C8 00 00 00 5F 5F 64 30 2B 2B 2B 00 5A 5A 5A 00

68 00 20 00 B8 00 00 00 08 08 08 30 1B 1B 1B 00 05 05 05 00 88 00 80 00 40 00 00 00 09 09 09 30

08 08 08 00 0F 0F 0F 00 18 00 B0 00 C0 00 00 00 07 07 07 30 08 08 08 00 19 19 19 00 38 00 18 00

C0 00 00 00 22 22 22 30 07 07 07 00 19 19 19 00 28 00 60 00 58 00 00 00 03 03 03 30 05 05 05 00

0F 0F 0F 00 68 00 28 00 90 00 00 00 08 08 08 30 03 03 03 00 06 06 06 00 78 00 60 00 80 00 00 00

0A 0A 0A 30 05 05 05 00 08 08 08 00 20 00 30 00 38 00 00 00 1B 1B 1B 30 0F 0F 0F 00 22 22 22 00

68 00 B8 00 28 00 00 00 08 08 08 30 05 05 05 00 03 03 03 00 90 00 28 00 58 00 00 00 06 06 06 30

03 03 03 00 0F 0F 0F 00 60 00 18 00 48 00 00 00 05 05 05 30 07 07 07 00 11 11 11 00 18 00 38 00

48 00 00 00 07 07 07 30 22 22 22 00 11 11 11 00 70 00 A8 00 88 00 00 00 05 05 05 30 05 05 05 00

09 09 09 00 68 00 70 00 30 00 00 00 08 08 08 30 05 05 05 00 0F 0F 0F 00 28 00 18 00 60 00 00 00

03 03 03 30 07 07 07 00 05 05 05 00 B0 00 18 00 28 00 00 00 08 08 08 30 07 07 07 00 03 03 03 00

20 00 38 00 C0 00 00 00 1B 1B 1B 30 22 22 22 00 19 19 19 00 20 00 68 00 30 00 00 00 1B 1B 1B 30

08 08 08 00 0F 0F 0F 00 28 00 B8 00 B0 00 00 00 03 03 03 30 05 05 05 00 08 08 08 00 88 00 40 00

50 00 00 00 09 09 09 30 0F 0F 0F 00 08 08 08 00 70 00 88 00 50 00 00 00 05 05 05 30 09 09 09 00

08 08 08 00 30 00 70 00 50 00 00 00 0F 0F 0F 30 05 05 05 00 08 08 08 00 38 00 30 00 50 00 00 00

22 22 22 30 0F 0F 0F 00 08 08 08 00 48 00 38 00 50 00 00 00 11 11 11 30 22 22 22 00 08 08 08 00

40 00 48 00 50 00 00 00 0F 0F 0F 30 11 11 11 00 08 08 08 00 58 00 60 00 78 00 00 00 0F 0F 0F 30

05 05 05 00 0A 0A 0A 00 90 00 70 00 68 00 00 00 06 06 06 30 05 05 05 00 08 08 08 00 A8 00 70 00

90 00 00 00 05 05 05 30 05 05 05 00 06 06 06 00 0A 00 00 00 D8 00 98 00 78 00 58 00 37 3C 4B 38

6E 69 69 00 19 1E 1E 00 28 2D 32 00 08 00 98 00 10 00 D8 00 87 82 73 38 6E 69 69 00 64 69 69 00

37 3C 4B 00 08 00 10 00 00 00 D0 00 87 82 73 38 64 69 69 00 37 2D 37 00 37 2D 37 00 A0 00 98 00

00 00 08 00 17 17 17 38 6E 69 69 00 37 2D 37 00 87 82 73 00 E0 00 A0 00 D0 00 00 00 37 2D 37 38

17 17 17 00 37 2D 37 00 37 2D 37 00 A0 00 E0 00 90 00 A8 00 17 17 17 38 37 2D 37 00 19 19 23 00

37 2D 37 00 20 00 C0 00 E8 00 C8 00 87 82 73 38 5F 5F 64 00 87 8C 91 00 5A 5A 5A 00 B8 00 20 00

F8 00 E8 00 0F 14 19 38 87 82 73 00 15 15 15 00 87 8C 91 00 60 00 48 00 80 00 40 00 05 05 05 38

11 11 11 00 08 08 08 00 0F 0F 0F 00 80 00 88 00 78 00 A8 00 08 08 08 38 09 09 09 00 0A 0A 0A 00

05 05 05 00

  
  
  
Bone 15 \[at offset 0x00004330\]:

  
70 00 00 00 00 00 F3 FF 0F 00 00 00 00 00 1C 00 02 00 00 00 27 00 F7 FF F5 FF 00 00 00 00 CE FF

02 00 00 00 C6 FF FC FF F7 FF 00 00 CF FF CF FF 21 FF 00 00 00 00 B5 FF FB FE 00 00 43 00 CD FF

23 FF 00 00 6E 00 F8 FF 15 FF 00 00 3D 00 33 00 05 FF 00 00 00 00 52 00 08 FF 00 00 AC FF 01 00

27 FF 00 00 C4 FF 2F 00 21 FF 00 00 05 00 FC FF BE FE 00 00 00 00 25 00 00 00 00 00 18 00 00 00

60 00 58 00 68 00 00 00 12 0E 13 30 12 0E 13 00 11 0E 12 00 50 00 60 00 68 00 00 00 0E 09 13 30

12 0E 13 00 11 0E 12 00 48 00 50 00 68 00 00 00 0E 09 13 30 0E 09 13 00 11 0E 12 00 40 00 48 00

68 00 00 00 1C 17 27 30 0E 09 13 00 11 0E 12 00 38 00 40 00 68 00 00 00 20 1C 2A 30 1C 17 27 00

11 0E 12 00 30 00 38 00 68 00 00 00 20 1C 2A 30 20 1C 2A 00 11 0E 12 00 28 00 30 00 68 00 00 00

0E 09 13 30 20 1C 2A 00 11 0E 12 00 58 00 28 00 68 00 00 00 12 0E 13 30 0E 09 13 00 11 0E 12 00

18 00 28 00 20 00 00 00 20 1C 2A 30 0E 09 13 00 12 0E 13 00 30 00 28 00 18 00 00 00 20 1C 2A 30

0E 09 13 00 20 1C 2A 00 20 00 28 00 58 00 00 00 12 0E 13 30 0E 09 13 00 12 0E 13 00 18 00 38 00

30 00 00 00 20 1C 2A 30 20 1C 2A 00 20 1C 2A 00 10 00 38 00 18 00 00 00 20 1C 2A 30 20 1C 2A 00

20 1C 2A 00 38 00 10 00 40 00 00 00 20 1C 2A 30 20 1C 2A 00 1C 17 27 00 10 00 48 00 40 00 00 00

20 1C 2A 30 0E 09 13 00 1C 17 27 00 08 00 48 00 10 00 00 00 0E 09 0F 30 0E 09 13 00 20 1C 2A 00

48 00 08 00 50 00 00 00 0E 09 13 30 0E 09 0F 00 0E 09 13 00 08 00 60 00 50 00 00 00 0E 09 0F 30

12 0E 13 00 0E 09 13 00 20 00 60 00 08 00 00 00 12 0E 13 30 12 0E 13 00 0E 09 0F 00 60 00 20 00

58 00 00 00 12 0E 13 30 12 0E 13 00 12 0E 13 00 00 00 08 00 10 00 00 00 20 1C 2A 30 0E 09 0F 00

20 1C 2A 00 18 00 00 00 10 00 00 00 20 1C 2A 30 20 1C 2A 00 20 1C 2A 00 00 00 18 00 20 00 00 00

20 1C 2A 30 20 1C 2A 00 12 0E 13 00 08 00 00 00 20 00 00 00 0E 09 0F 30 20 1C 2A 00 12 0E 13 00

00 00 00 00

  
  
  
Bone 16 \[at offset 0x00004594\]:

  
18 01 00 00 00 00 CF FF 2B 00 00 00 00 00 29 00 25 00 00 00 31 00 CF FF 00 00 00 00 E1 FF D9 FF

A6 FF 00 00 05 00 C8 FF AF FF 00 00 4E 00 F7 FF FD FF 00 00 33 00 1D 00 F7 FF 00 00 BF FF 00 00

F7 FF 00 00 00 00 49 00 E9 FF 00 00 D8 FF 29 00 F1 FF 00 00 00 00 E4 FF 4E FF 00 00 00 00 1C 00

4E FF 00 00 40 00 F5 FF BB FF 00 00 D3 FF D1 FF FA FF 00 00 00 00 C4 FF DC FF 00 00 00 00 B8 FF

00 00 00 00 DE FF 07 00 B0 FF 00 00 D4 FF 0D 00 9C FF 00 00 33 00 00 00 DC FF 00 00 00 00 36 00

B2 FF 00 00 00 00 31 00 CE FF 00 00 00 00 E4 FF 79 FF 00 00 19 00 00 00 4E FF 00 00 25 00 00 00

8F FF 00 00 00 00 1C 00 88 FF 00 00 E8 FF 00 00 4E FF 00 00 E3 FF 00 00 78 FF 00 00 23 00 00 00

09 FF 00 00 DD FF 00 00 09 FF 00 00 00 00 28 00 FA FE 00 00 00 00 D8 FF 09 FF 00 00 23 00 00 00

4E FF 00 00 00 00 28 00 4E FF 00 00 DD FF 00 00 4E FF 00 00 00 00 D8 FF 4E FF 00 00 00 00 25 00

00 00 00 00 32 00 00 00 D8 00 E8 00 F0 00 00 00 1D 18 0A 30 0E 0E 06 00 1D 18 0A 00 E8 00 E0 00

F0 00 00 00 0E 0E 06 30 1D 18 11 00 1D 18 0A 00 00 00 10 00 78 00 00 00 0E 09 17 30 23 1E 2D 00

0F 0C 19 00 00 00 28 00 10 00 00 00 0E 09 17 30 0E 09 17 00 23 1E 2D 00 08 00 28 00 00 00 00 00

09 04 0B 30 0E 09 17 00 0E 09 17 00 00 00 38 00 08 00 00 00 0E 09 17 30 0E 09 13 00 09 04 0B 00

38 00 00 00 68 00 00 00 0E 09 13 30 0E 09 17 00 0F 0C 19 00 68 00 00 00 78 00 00 00 0F 0C 19 30

0E 09 17 00 0F 0C 19 00 08 00 48 00 40 00 00 00 09 04 0B 30 0E 09 13 00 0E 09 17 00 08 00 38 00

48 00 00 00 09 04 0B 30 0E 09 13 00 0E 09 13 00 08 00 30 00 28 00 00 00 09 04 0B 30 0E 09 17 00

0E 09 17 00 30 00 08 00 40 00 00 00 0E 09 17 30 09 04 0B 00 0E 09 17 00 38 00 68 00 80 00 00 00

0E 09 13 30 0F 0C 19 00 0E 09 17 00 70 00 80 00 68 00 00 00 05 0A 0F 30 0E 09 17 00 0F 0C 19 00

10 00 70 00 78 00 00 00 23 1E 2D 30 05 0A 0F 00 0F 0C 19 00 90 00 70 00 10 00 00 00 0F 0F 14 30

05 0A 0F 00 23 1E 2D 00 90 00 10 00 28 00 00 00 0F 0F 14 30 23 1E 2D 00 0E 09 17 00 18 00 70 00

20 00 00 00 20 1C 23 30 05 0A 0F 00 0F 0C 19 00 60 00 20 00 70 00 00 00 20 1C 23 30 0F 0C 19 00

05 0A 0F 00 60 00 70 00 90 00 00 00 20 1C 23 30 05 0A 0F 00 0F 0F 14 00 70 00 18 00 80 00 00 00

05 0A 0F 30 20 1C 23 00 0E 09 17 00 A8 00 18 00 20 00 00 00 0F 0C 19 30 20 1C 23 00 0F 0C 19 00

80 00 18 00 88 00 00 00 0E 09 17 30 20 1C 23 00 0F 0C 19 00 88 00 18 00 D0 00 00 00 0F 0C 19 30

20 1C 23 00 0E 09 17 00 18 00 A8 00 D0 00 00 00 20 1C 23 30 0F 0C 19 00 0E 09 17 00 20 00 60 00

B8 00 00 00 0F 0C 19 30 20 1C 23 00 0F 0C 19 00 B8 00 A8 00 20 00 00 00 0F 0C 19 30 0F 0C 19 00

0F 0C 19 00 30 00 90 00 28 00 00 00 0E 09 17 30 0F 0F 14 00 0E 09 17 00 30 00 A0 00 90 00 00 00

0E 09 17 30 09 04 0B 00 0F 0F 14 00 A0 00 30 00 40 00 00 00 09 04 0B 30 0E 09 17 00 0E 09 17 00

80 00 48 00 38 00 00 00 0E 09 17 30 0E 09 13 00 0E 09 13 00 48 00 A0 00 40 00 00 00 0E 09 13 30

09 04 0B 00 0E 09 17 00 A0 00 48 00 80 00 00 00 09 04 0B 30 0E 09 13 00 0E 09 17 00 50 00 C8 00

A8 00 00 00 1B 14 1C 30 1B 14 1C 00 0F 0C 19 00 A8 00 B0 00 50 00 00 00 0F 0C 19 30 11 0E 12 00

1B 14 1C 00 C0 00 58 00 B0 00 00 00 12 0E 17 30 0F 0C 19 00 11 0E 12 00 C8 00 58 00 C0 00 00 00

1B 14 1C 30 0F 0C 19 00 12 0E 17 00 C0 00 B8 00 98 00 00 00 12 0E 17 30 0F 0C 19 00 0E 09 17 00

60 00 98 00 B8 00 00 00 20 1C 23 30 0E 09 17 00 0F 0C 19 00 98 00 60 00 90 00 00 00 0E 09 17 30

20 1C 23 00 0F 0F 14 00 98 00 80 00 88 00 00 00 0E 09 17 30 0E 09 17 00 0F 0C 19 00 98 00 D0 00

C0 00 00 00 0E 09 17 30 0E 09 17 00 12 0E 17 00 70 00 68 00 78 00 00 00 05 0A 0F 30 0F 0C 19 00

0F 0C 19 00 80 00 98 00 A0 00 00 00 0E 09 17 30 0E 09 17 00 09 04 0B 00 D0 00 98 00 88 00 00 00

0E 09 17 30 0E 09 17 00 0F 0C 19 00 98 00 90 00 A0 00 00 00 0E 09 17 30 0F 0F 14 00 09 04 0B 00

A8 00 C8 00 D0 00 00 00 0F 0C 19 30 1B 14 1C 00 0E 09 17 00 B0 00 A8 00 B8 00 00 00 11 0E 12 30

0F 0C 19 00 0F 0C 19 00 C0 00 B0 00 B8 00 00 00 12 0E 17 30 11 0E 12 00 0F 0C 19 00 C8 00 C0 00

D0 00 00 00 1B 14 1C 30 12 0E 17 00 0E 09 17 00 05 00 00 00 F8 00 D8 00 10 01 F0 00 2B 26 17 38

1D 18 0A 00 46 3F 22 00 1D 18 0A 00 00 01 E8 00 F8 00 D8 00 0B 0A 06 38 0E 0E 06 00 2B 26 17 00

1D 18 0A 00 08 01 00 01 10 01 F8 00 14 0E 0A 38 0B 0A 06 00 46 3F 22 00 2B 26 17 00 10 01 F0 00

08 01 E0 00 46 3F 22 38 1D 18 0A 00 14 0E 0A 00 1D 18 11 00 00 01 08 01 E8 00 E0 00 0B 0A 06 38

14 0E 0A 00 0E 0E 06 00 1D 18 11 00

  
  
  
Bone 17 \[at offset 0x00004B20\]:

  
88 00 00 00 13 00 EA FF FB FF 00 00 2C 00 25 00 F0 FF 00 00 FF FF 15 00 23 00 00 00 01 00 3A 00

FC FF 00 00 DB FF 25 00 F0 FF 00 00 EA FF EC FF F6 FF 00 00 DE FF 36 00 D0 FF 00 00 01 00 4B 00

DB FF 00 00 29 00 36 00 D0 FF 00 00 E3 FF 00 00 B3 FF 00 00 29 00 00 00 B3 FF 00 00 E9 FF F8 FF

C3 FF 00 00 22 00 F5 FF C8 FF 00 00 00 00 CE FF D9 FF 00 00 1C 00 FB FF 17 00 00 00 E0 FF FB FF

17 00 00 00 FE FF DC FF 0C 00 00 00 00 00 25 00 00 00 00 00 19 00 00 00 38 00 30 00 40 00 00 00

03 05 07 30 02 04 06 00 01 02 03 00 40 00 50 00 60 00 00 00 14 11 03 30 17 15 05 00 2B 23 17 00

40 00 60 00 08 00 00 00 14 11 03 30 2B 23 17 00 17 15 0A 00 60 00 00 00 08 00 00 00 2B 23 17 30

3D 31 1B 00 17 15 0A 00 60 00 68 00 00 00 00 00 2B 23 17 30 4F 42 22 00 3D 31 1B 00 00 00 68 00

80 00 00 00 3D 31 1B 30 4F 42 22 00 17 11 0A 00 70 00 00 00 80 00 00 00 17 11 0A 30 3D 31 1B 00

17 11 0A 00 08 00 00 00 70 00 00 00 17 15 0A 30 3D 31 1B 00 17 11 0A 00 10 00 08 00 70 00 00 00

0E 0A 06 30 17 15 0A 00 17 11 0A 00 08 00 10 00 18 00 00 00 17 15 0A 30 0E 0A 06 00 0B 0A 03 00

18 00 40 00 08 00 00 00 0B 0A 03 30 14 11 03 00 17 15 0A 00 40 00 18 00 38 00 00 00 14 11 03 30

0B 0A 03 00 0B 0A 03 00 10 00 20 00 18 00 00 00 0E 0A 06 30 11 11 06 00 0B 0A 03 00 78 00 20 00

10 00 00 00 11 0E 0A 30 11 11 06 00 0E 0A 06 00 10 00 70 00 78 00 00 00 0E 0A 06 30 17 11 0A 00

11 0E 0A 00 18 00 30 00 38 00 00 00 0B 0A 03 30 11 11 06 00 0B 0A 03 00 30 00 18 00 20 00 00 00

11 11 06 30 0B 0A 03 00 11 11 06 00 58 00 30 00 20 00 00 00 11 11 06 30 11 11 06 00 11 11 06 00

20 00 28 00 58 00 00 00 11 11 06 30 14 0E 06 00 11 11 06 00 28 00 20 00 78 00 00 00 14 0E 06 30

11 11 06 00 11 0E 0A 00 80 00 28 00 78 00 00 00 17 11 0A 30 14 0E 06 00 11 0E 0A 00 48 00 30 00

58 00 00 00 11 11 06 30 11 11 06 00 11 11 06 00 68 00 28 00 80 00 00 00 4F 42 22 30 14 0E 06 00

17 11 0A 00 68 00 58 00 28 00 00 00 4F 42 22 30 11 11 06 00 14 0E 06 00 78 00 70 00 80 00 00 00

11 0E 0A 30 17 11 0A 00 17 11 0A 00 01 00 00 00 40 00 30 00 50 00 48 00 01 02 03 38 02 04 06 00

01 02 02 00 02 04 05 00

  
  
  
Bone 18 \[at offset 0x00004DC8\]:

  
58 00 00 00 2A 00 DE FF B0 FF 00 00 D9 FF DF FF B0 FF 00 00 01 00 CE FF 90 FF 00 00 D0 FF 00 00

B2 FF 00 00 34 00 00 00 B2 FF 00 00 02 00 00 00 87 FF 00 00 29 00 00 00 00 00 00 00 E3 FF 00 00

00 00 00 00 22 00 E9 FF 00 00 00 00 E9 FF EE FF 00 00 00 00 00 00 C7 FF E8 FF 00 00 00 00 25 00

00 00 00 00 0D 00 00 00 20 00 18 00 28 00 00 00 03 04 06 30 02 04 04 00 05 08 0A 00 20 00 40 00

30 00 00 00 23 18 11 30 2B 23 17 00 17 11 0A 00 40 00 20 00 00 00 00 00 2B 23 17 30 23 18 11 00

43 38 22 00 28 00 00 00 20 00 00 00 2B 23 1B 30 43 38 22 00 23 18 11 00 00 00 28 00 10 00 00 00

43 38 22 30 2B 23 1B 00 5D 54 25 00 00 00 10 00 50 00 00 00 43 38 22 30 5D 54 25 00 4F 42 22 00

40 00 00 00 50 00 00 00 2B 23 17 30 43 38 22 00 4F 42 22 00 28 00 08 00 10 00 00 00 2B 23 1B 30

11 0E 06 00 5D 54 25 00 28 00 18 00 08 00 00 00 2B 23 1B 30 18 15 06 00 11 0E 06 00 18 00 48 00

08 00 00 00 18 15 06 30 17 11 0A 00 11 0E 06 00 18 00 38 00 48 00 00 00 18 15 06 30 11 11 06 00

17 11 0A 00 48 00 50 00 08 00 00 00 17 11 0A 30 4F 42 22 00 11 0E 06 00 10 00 08 00 50 00 00 00

5D 54 25 30 11 0E 06 00 4F 42 22 00 01 00 00 00 20 00 30 00 18 00 38 00 03 04 06 38 02 04 05 00

02 04 04 00 01 02 02 00

  
  
  
Bone 20 \[at offset 0x00004F50\]:

  
70 00 00 00 FB FF FC FF BE FE 00 00 3C 00 2F 00 21 FF 00 00 54 00 01 00 27 FF 00 00 00 00 52 00

08 FF 00 00 C3 FF 33 00 05 FF 00 00 92 FF F8 FF 15 FF 00 00 BD FF CD FF 23 FF 00 00 00 00 B5 FF

FB FE 00 00 31 00 CF FF 21 FF 00 00 3A 00 FC FF F7 FF 00 00 00 00 CE FF 02 00 00 00 D9 FF F7 FF

F5 FF 00 00 00 00 1C 00 02 00 00 00 00 00 F3 FF 0F 00 00 00 00 00 25 00 00 00 00 00 18 00 00 00

10 00 08 00 00 00 00 00 19 17 23 30 17 12 1F 00 12 0E 12 00 08 00 18 00 00 00 00 00 17 12 1F 30

0E 09 0F 00 12 0E 12 00 18 00 20 00 00 00 00 00 0E 09 0F 30 0E 09 0F 00 0F 0C 14 00 20 00 28 00

00 00 00 00 0E 09 0F 30 20 1C 2A 00 0F 0C 14 00 28 00 30 00 00 00 00 00 20 1C 2A 30 20 1C 2A 00

0F 0C 14 00 30 00 38 00 00 00 00 00 20 1C 2A 30 20 1C 2A 00 0F 0C 14 00 38 00 40 00 00 00 00 00

20 1C 2A 30 19 17 23 00 0F 0C 14 00 40 00 10 00 00 00 00 00 19 17 23 30 19 17 23 00 0F 0C 14 00

40 00 50 00 48 00 00 00 19 17 23 30 20 1C 2A 00 0E 09 13 00 40 00 38 00 50 00 00 00 19 17 23 30

20 1C 2A 00 20 1C 2A 00 40 00 48 00 10 00 00 00 19 17 23 30 0E 09 13 00 19 17 23 00 30 00 50 00

38 00 00 00 20 1C 2A 30 20 1C 2A 00 20 1C 2A 00 30 00 58 00 50 00 00 00 20 1C 2A 30 0E 09 0F 00

20 1C 2A 00 58 00 30 00 28 00 00 00 0E 09 0F 30 20 1C 2A 00 20 1C 2A 00 20 00 58 00 28 00 00 00

0E 09 0F 30 0E 09 0F 00 20 1C 2A 00 20 00 60 00 58 00 00 00 0E 09 0F 30 0E 09 0F 00 0E 09 0F 00

60 00 20 00 18 00 00 00 0E 09 0F 30 0E 09 0F 00 0E 09 0F 00 08 00 60 00 18 00 00 00 17 12 1F 30

0E 09 0F 00 0E 09 0F 00 08 00 48 00 60 00 00 00 17 12 1F 30 0E 09 13 00 0E 09 0F 00 48 00 08 00

10 00 00 00 0E 09 13 30 17 12 1F 00 19 17 23 00 60 00 68 00 58 00 00 00 0E 09 0F 30 17 12 1B 00

0E 09 0F 00 68 00 50 00 58 00 00 00 1C 17 27 30 20 1C 2A 00 0E 09 0F 00 50 00 68 00 48 00 00 00

20 1C 2A 30 1C 17 27 00 0E 09 13 00 68 00 60 00 48 00 00 00 17 12 1B 30 0E 09 0F 00 0E 09 13 00

00 00 00 00

  
  
  
Bone 21 \[at offset 0x000051B4\]:

  
18 01 00 00 00 00 D8 FF 4E FF 00 00 23 00 00 00 4E FF 00 00 00 00 28 00 4E FF 00 00 DD FF 00 00

4E FF 00 00 00 00 D8 FF 09 FF 00 00 00 00 28 00 FA FE 00 00 23 00 00 00 09 FF 00 00 DD FF 00 00

09 FF 00 00 1D 00 00 00 78 FF 00 00 18 00 00 00 4E FF 00 00 00 00 1C 00 88 FF 00 00 DB FF 00 00

8F FF 00 00 E7 FF 00 00 4E FF 00 00 00 00 E4 FF 79 FF 00 00 00 00 31 00 CE FF 00 00 00 00 36 00

B2 FF 00 00 CD FF 00 00 DC FF 00 00 2C 00 0D 00 9C FF 00 00 22 00 07 00 B0 FF 00 00 00 00 B8 FF

00 00 00 00 00 00 C4 FF DC FF 00 00 2D 00 D1 FF FA FF 00 00 C0 FF F5 FF BB FF 00 00 00 00 1C 00

4E FF 00 00 00 00 E4 FF 4E FF 00 00 28 00 29 00 F1 FF 00 00 00 00 49 00 E9 FF 00 00 41 00 00 00

F7 FF 00 00 CD FF 1D 00 F7 FF 00 00 B2 FF F7 FF FD FF 00 00 FB FF C8 FF AF FF 00 00 1F 00 D9 FF

A6 FF 00 00 CF FF CF FF 00 00 00 00 00 00 29 00 25 00 00 00 00 00 CF FF 2B 00 00 00 00 00 25 00

00 00 00 00 32 00 00 00 28 00 38 00 20 00 00 00 14 12 04 30 0F 0E 04 00 1D 18 0A 00 30 00 28 00

20 00 00 00 1D 18 0A 30 14 12 04 00 1D 18 0A 00 00 01 10 01 98 00 00 00 18 11 19 30 1C 14 24 00

14 14 1E 00 E8 00 10 01 00 01 00 00 14 0C 19 30 1C 14 24 00 18 11 19 00 E8 00 08 01 10 01 00 00

14 0C 19 30 14 14 1E 00 1C 14 24 00 D8 00 10 01 08 01 00 00 18 11 19 30 1C 14 24 00 14 14 1E 00

10 01 D8 00 A8 00 00 00 1C 14 24 30 18 11 19 00 18 11 19 00 10 01 A8 00 98 00 00 00 1C 14 24 30

18 11 19 00 14 14 1E 00 C8 00 08 01 D0 00 00 00 0E 08 12 30 14 14 1E 00 14 14 1E 00 D8 00 08 01

C8 00 00 00 18 11 19 30 14 14 1E 00 0E 08 12 00 E0 00 08 01 E8 00 00 00 14 0C 19 30 14 14 1E 00

14 0C 19 00 08 01 E0 00 D0 00 00 00 14 14 1E 30 14 0C 19 00 14 14 1E 00 A8 00 D8 00 90 00 00 00

18 11 19 30 18 11 19 00 1D 16 1C 00 90 00 A0 00 A8 00 00 00 1D 16 1C 30 14 0F 1E 00 18 11 19 00

A0 00 00 01 98 00 00 00 14 0F 1E 30 18 11 19 00 14 0F 1E 00 A0 00 80 00 00 01 00 00 14 0F 1E 30

14 0C 19 00 18 11 19 00 00 01 80 00 E8 00 00 00 18 11 19 30 14 0C 19 00 14 0C 19 00 A0 00 F8 00

F0 00 00 00 14 0F 1E 30 18 11 19 00 1E 19 23 00 F0 00 B0 00 A0 00 00 00 1E 19 23 30 14 10 19 00

14 10 19 00 A0 00 B0 00 80 00 00 00 14 10 19 30 14 10 19 00 14 10 19 00 F8 00 A0 00 90 00 00 00

18 11 19 30 14 0F 1E 00 1D 16 1C 00 F8 00 68 00 F0 00 00 00 18 11 19 30 14 0F 1E 00 1E 19 23 00

F8 00 90 00 88 00 00 00 18 11 19 30 1D 16 1C 00 18 11 19 00 F8 00 88 00 40 00 00 00 18 11 19 30

18 11 19 00 1D 16 19 00 68 00 F8 00 40 00 00 00 14 14 1E 30 18 11 19 00 1D 16 19 00 B0 00 F0 00

58 00 00 00 14 0F 14 30 1E 19 23 00 14 0F 14 00 68 00 58 00 F0 00 00 00 0E 08 12 30 0E 08 12 00

1E 19 23 00 80 00 E0 00 E8 00 00 00 14 0C 19 30 14 0C 19 00 14 0C 19 00 70 00 E0 00 80 00 00 00

14 0C 19 30 14 0C 19 00 14 0C 19 00 E0 00 70 00 D0 00 00 00 14 0C 19 30 14 0C 19 00 14 14 1E 00

C8 00 90 00 D8 00 00 00 0E 08 12 30 1D 16 1C 00 18 11 19 00 70 00 C8 00 D0 00 00 00 13 14 19 30

0E 08 12 00 14 14 1E 00 C8 00 70 00 90 00 00 00 0E 08 12 30 13 14 19 00 1D 16 1C 00 48 00 C0 00

68 00 00 00 12 0D 0F 30 27 1F 25 00 14 14 1E 00 60 00 68 00 C0 00 00 00 1B 13 15 30 14 14 1E 00

27 1F 25 00 B8 00 50 00 60 00 00 00 22 1A 1C 30 0E 08 12 00 1B 13 15 00 B8 00 48 00 50 00 00 00

22 1A 1C 30 12 0D 0F 00 0E 08 12 00 58 00 50 00 78 00 00 00 0E 08 12 30 13 14 19 00 0E 08 12 00

78 00 B0 00 58 00 00 00 0E 08 12 30 13 14 19 00 0E 08 12 00 B0 00 78 00 80 00 00 00 13 14 19 30

0E 08 12 00 13 14 19 00 90 00 78 00 88 00 00 00 1D 16 1C 30 0E 08 12 00 18 11 19 00 40 00 78 00

50 00 00 00 1D 16 19 30 0E 08 12 00 13 14 19 00 A8 00 A0 00 98 00 00 00 18 11 19 30 14 0F 1E 00

14 0F 1E 00 78 00 90 00 70 00 00 00 0E 08 12 30 1D 16 1C 00 13 14 19 00 78 00 40 00 88 00 00 00

0E 08 12 30 1D 16 19 00 18 11 19 00 80 00 78 00 70 00 00 00 13 14 19 30 0E 08 12 00 13 14 19 00

48 00 68 00 40 00 00 00 12 0D 0F 30 14 14 1E 00 1D 16 19 00 68 00 60 00 58 00 00 00 14 14 1E 30

1B 13 15 00 0E 08 12 00 60 00 50 00 58 00 00 00 1B 13 15 30 13 14 19 00 0E 08 12 00 50 00 48 00

40 00 00 00 13 14 19 30 12 0D 0F 00 1D 16 19 00 05 00 00 00 38 00 18 00 20 00 00 00 0F 0E 04 38

1A 15 11 00 1D 18 0A 00 46 3F 22 00 28 00 10 00 38 00 18 00 14 12 04 38 0B 0A 06 00 0F 0E 04 00

1A 15 11 00 10 00 08 00 18 00 00 00 0B 0A 06 38 2B 26 17 00 1A 15 11 00 46 3F 22 00 20 00 00 00

30 00 08 00 1D 18 0A 38 46 3F 22 00 1D 18 0A 00 2B 26 17 00 08 00 10 00 30 00 28 00 2B 26 17 38

0B 0A 06 00 1D 18 0A 00 14 12 04 00

  
  
  
Bone 22 \[at offset 0x00005740\]:

  
88 00 00 00 02 00 DC FF 0C 00 00 00 1F 00 FB FF 17 00 00 00 E4 FF FB FF 17 00 00 00 00 00 CE FF

D9 FF 00 00 DE FF F5 FF C8 FF 00 00 17 00 F8 FF C3 FF 00 00 D7 FF 00 00 B3 FF 00 00 1D 00 00 00

B3 FF 00 00 D7 FF 36 00 D0 FF 00 00 FF FF 4B 00 DB FF 00 00 22 00 36 00 D0 FF 00 00 16 00 EC FF

F6 FF 00 00 25 00 25 00 F0 FF 00 00 FF FF 3A 00 FC FF 00 00 01 00 15 00 23 00 00 00 D4 FF 25 00

F0 FF 00 00 ED FF EA FF FB FF 00 00 00 00 25 00 00 00 00 00 19 00 00 00 50 00 48 00 40 00 00 00

01 02 02 30 01 02 02 00 02 04 06 00 10 00 08 00 00 00 00 00 14 11 06 30 20 18 14 00 14 11 06 00

28 00 18 00 58 00 00 00 29 23 17 30 3A 2D 1B 00 38 2D 22 00 58 00 18 00 00 00 00 00 38 2D 22 30

3A 2D 1B 00 14 11 06 00 50 00 38 00 28 00 00 00 09 09 02 30 1C 18 0D 00 29 23 17 00 58 00 00 00

08 00 00 00 38 2D 22 30 14 11 06 00 20 18 14 00 60 00 58 00 08 00 00 00 14 11 06 30 38 2D 22 00

20 18 14 00 58 00 60 00 28 00 00 00 38 2D 22 30 14 11 06 00 29 23 17 00 50 00 28 00 60 00 00 00

09 09 02 30 29 23 17 00 14 11 06 00 68 00 50 00 60 00 00 00 08 07 03 30 09 09 02 00 14 11 06 00

50 00 68 00 48 00 00 00 09 09 02 30 08 07 03 00 0B 0A 06 00 10 00 70 00 08 00 00 00 14 11 06 30

14 11 06 00 20 18 14 00 60 00 08 00 70 00 00 00 14 11 06 30 20 18 14 00 14 11 06 00 60 00 70 00

68 00 00 00 14 11 06 30 14 11 06 00 08 07 03 00 68 00 40 00 48 00 00 00 08 07 03 30 14 11 06 00

0B 0A 06 00 40 00 68 00 78 00 00 00 14 11 06 30 08 07 03 00 14 11 06 00 70 00 78 00 68 00 00 00

14 11 06 30 14 11 06 00 08 07 03 00 78 00 70 00 10 00 00 00 14 11 06 30 14 11 06 00 14 11 06 00

80 00 78 00 10 00 00 00 14 11 06 30 14 11 06 00 14 11 06 00 80 00 10 00 00 00 00 00 14 11 06 30

14 11 06 00 14 11 06 00 18 00 80 00 00 00 00 00 3A 2D 1B 30 14 11 06 00 14 11 06 00 18 00 20 00

80 00 00 00 3A 2D 1B 30 14 0E 06 00 14 11 06 00 80 00 20 00 78 00 00 00 14 11 06 30 14 0E 06 00

14 11 06 00 20 00 40 00 78 00 00 00 14 0E 06 30 14 11 06 00 14 11 06 00 30 00 40 00 20 00 00 00

14 11 06 30 14 11 06 00 14 0E 06 00 01 00 00 00 40 00 30 00 50 00 38 00 02 04 06 38 02 04 05 00

01 02 02 00 04 06 07 00

  
  
  
Bone 23 \[at offset 0x000059E8\]:

  
58 00 00 00 00 00 C7 FF E8 FF 00 00 17 00 EE FF 00 00 00 00 DE FF E9 FF 00 00 00 00 1D 00 00 00

00 00 00 00 D7 FF 00 00 00 00 00 00 FE FF 00 00 87 FF 00 00 CC FF 00 00 B2 FF 00 00 30 00 00 00

B2 FF 00 00 FF FF CE FF 90 FF 00 00 27 00 DF FF B0 FF 00 00 D6 FF DE FF B0 FF 00 00 00 00 25 00

00 00 00 00 0D 00 00 00 38 00 30 00 28 00 00 00 01 02 02 30 01 02 02 00 05 08 0A 00 48 00 40 00

00 00 00 00 52 46 29 30 5D 54 22 00 3A 2D 1B 00 00 00 08 00 48 00 00 00 3A 2D 1B 30 29 23 17 00

52 46 29 00 18 00 38 00 08 00 00 00 11 0E 0A 30 20 18 11 00 29 23 17 00 08 00 38 00 48 00 00 00

29 23 17 30 20 18 11 00 52 46 29 00 38 00 28 00 48 00 00 00 20 18 11 30 2B 23 1B 00 52 46 29 00

48 00 28 00 40 00 00 00 52 46 29 30 2B 23 1B 00 5D 54 22 00 50 00 10 00 00 00 00 00 1D 18 0D 30

14 11 06 00 3A 2D 1B 00 40 00 50 00 00 00 00 00 5D 54 22 30 1D 18 0D 00 3A 2D 1B 00 28 00 50 00

40 00 00 00 2B 23 1B 30 1D 18 0D 00 5D 54 22 00 50 00 28 00 30 00 00 00 1D 18 0D 30 2B 23 1B 00

10 0F 04 00 30 00 10 00 50 00 00 00 10 0F 04 30 14 11 06 00 1D 18 0D 00 10 00 30 00 20 00 00 00

14 11 06 30 10 0F 04 00 14 11 06 00 01 00 00 00 30 00 38 00 20 00 18 00 01 02 02 38 01 02 02 00

04 06 07 00 02 04 06 00

  
  
  

- \*\* \*\*\* Bone Data Section runs until Model Settings Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Model Settings Section** \[at offset 0x00005B70\]:

  
Note: After the first 0x68 bytes of this data, there seem to be relative offsets to what Akari considers animation data (perhaps it's something else in playable character battle models)...this seems to end at 0X5CFF, followed by...something else.

  
  
Model Settings \[at offset 0x00005B70\]:

  
00 00 80 00 90 01 00 0A 00 0A 00 00 00 00 E0 FC 7C FC 02 00 00 00 00 00 0D 08 03 00 03 17 12 00

00 00 00 00 38 04 00 00 38 04 00 00 38 04 00 00 38 04 00 00 38 04 00 00 38 04 00 00 38 04 00 00

38 04 00 00 80 01 32 01 80 01 00 00 99 03 A8 FD FF F9 00 00 DC FD 00 00 01 FD 58 FF AB F9 00 00

30 FE 00 00 2C 01 00 00 90 01 00 00 94 01 00 00 9C 01 00 00 A0 01 00 00 B0 01 00 00 C0 01 00 00

C4 01 00 00 CC 01 00 00 D0 01 00 00 D4 01 00 00 E4 01 00 00 E8 01 00 00 EC 01 00 00 F0 01 00 00

F4 01 00 00 00 02 00 00 FC 01 00 00 10 02 00 00 04 02 00 00 98 01 00 00 6C 02 00 00 84 02 00 00

18 03 00 00 2C 03 00 00 58 03 00 00 6C 03 00 00 78 03 00 00 84 03 00 00 38 03 00 00 10 02 00 00

20 02 00 00 30 02 00 00 44 02 00 00 58 02 00 00 90 02 00 00 90 02 00 00 6C 02 00 00 84 02 00 00

EC 02 00 00 FC 02 00 00 C8 02 00 00 C8 02 00 00 B0 02 00 00 B0 02 00 00 0C 03 00 00 0C 03 00 00

90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00

90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 94 03 00 00 B8 03 00 00

D8 03 00 00 E8 03 00 00 0C 04 00 00 18 04 00 00 28 04 00 00 24 04 00 00 E4 03 00 00 94 03 00 00

90 01 00 00 90 01 00 00 90 01 00 00 90 01 00 00 00 FE C0 00 01 FE C0 00 10 FE C0 00 E5 06 F1 00

B3 F9 03 ED E3 EE B2 F9 03 B1 03 B1 E3 EE 00 00 B3 F9 04 E4 E3 EE B2 F9 04 B0 04 B0 E3 EE 00 00

0F F2 E5 EE 10 11 F2 E5 EE 00 00 00 12 F2 E5 EE 05 E5 EE 00 AB 90 01 00 00 08 F4 0F F3 FA E5 A6

EE 00 00 00 13 E5 EE 00 18 19 E5 EE B4 02 F1 00 95 07 FE C0 C4 90 01 06 07 FE C0 00 04 FA E5 EE

E7 00 F1 00 E5 C4 90 01 06 12 E7 00 F1 00 00 00 E8 FC 03 ED E6 EA 0C 0D EC 0E 04 FA E5 EE 00 00

E8 FC 03 ED A4 EA 0C 0D EC 0E 04 FA E5 EE 00 00 E8 FC 03 ED A5 EA 0C 0D EC F4 0F F3 0E 04 FA E5

EE 00 00 00 E8 FC 03 ED D8 06 15 00 09 EA EB F4 0A F3 04 FA E5 EE 00 00 E8 FC 03 ED D8 06 15 00

0A EA EB F4 0A F3 04 FA E5 EE 00 00 FC F0 D8 00 1A 00 1A D1 B0 04 00 00 04 F0 1B F7 01 1E 1C FA

F0 1D E5 EE FC 03 ED F7 10 1F 04 FA E5 EE 00 00 FC F0 D8 00 1A 00 1A D1 B0 04 00 00 04 F0 1B F7

01 D8 01 D6 02 16 F4 06 F3 26 FA F0 1D E5 EE 00 FC F0 D8 00 1A 00 1A D1 B0 04 00 00 04 F0 1B F7

10 21 28 FA F0 1D E5 EE FC F0 D8 00 1A 00 1A D1 B0 04 00 00 04 F0 1B F7 10 20 27 FA F0 1D E5 EE

FC 03 ED F7 01 20 04 FA E5 EE 00 00 FC 03 ED F7 01 14 F4 3C F3 04 FA E5 EE 00 00 00 FC 03 ED F7

01 14 F4 5A F3 04 FA E5 EE 00 00 00 FC 03 ED F7 13 15 04 FA E5 EE 00 00 FC F0 D8 00 1A 00 1A D1

B0 04 00 00 04 F0 1B F7 01 1E 9E 00 F7 01 22 23 FA F0 1D E5 EE 00 00 00 FC F0 D8 00 1A 00 1A CC

04 CB FF E8 03 FE FE 00 08 08 F0 1B 1E F7 03 F4 06 F3 1C FA F0 1D E5 EE FC F0 D8 00 1A 00 1A D1

B0 04 00 00 04 F0 1B F7 01 1E 9E 00 E5 BD B0 04 00 00 F0 F7 03 22 9E 00 E5 BD B0 04 00 00 F0 F7

03 24 9E 00 E5 BD B0 04 00 00 F0 F7 03 29 1C FA F0 1D E5 EE E8 FC 00 E0 EA F4 19 F3 EC F0 D8 00

1A 00 2C D1 B0 04 00 00 04 F0 2D D8 06 30 00 2E FA F0 2F E5 EE 00 00 00 E8 FC 00 E0 EA F4 19 F3

EC F0 D8 00 1A 00 2C D1 B0 04 00 00 04 F0 2D 2E FA F0 2F E5 EE 00 00 00 E8 FC 00 E0 EA F4 19 F3

EC 2C 9E 00 EC 2D E5 EE E8 FC 00 E0 EA F4 19 F3 EC F0 2C D8 00 1A 00 FB 40 06 00 00 F0 2D D8 19

30 00 A8 26 08 2E FA F0 E5 EE 00 00 E8 FC 00 E0 EA F4 19 F3 EC 2C E5 EE E8 FC 00 E0 EA F4 19 F3

EC 2C E5 EE EC E5 EE 00 E8 FC 00 E0 EA F4 19 F3 EC 2C 2D 2D 2E FA E5 EE

  
  
  

- \*\* \*\*\* Model Settings Section runs until Animation Data Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Animation Data Section** \[at offset 0x00005FA8\]

  
  
1st Animation Data \[at offset 0x00005FA8\]

  
14 00 56 03 00 00 00 FE 2E 00 00 00 00 00 00 0C 00 EC E0 00 F8 2F E5 E8 A0 BB 0C 82 BC EC 2F 02

AE 61 86 40 12 C1 35 41 E4 EE 6E 53 00 00 00 02 A0 61 EF 1F EF 0F 02 5F 2F 10 06 0B 52 80 AC 2E

2B F0 80 00 00 0F C4 FF 1E C4 00 0A 2E 00 02 99 DF 1A 75 11 C0 00 00 0D 81 FF 23 08 D4 9F EE 01

00 00 36 E0 00 16 6C 04 05 72 99 00 00 00 EB 9F 87 04 4D 56 00 00 00 00 05 00 00 01 45 AC 5A F7

1B 9A 40 30 AD DB B5 8B 87 9C 62 5E 81 67 53 A5 E1 4E F2 9A B0 F7 BA 01 97 29 E9 0B 91 88 00 01

40 00 00 53 6B 12 AD C6 E6 90 0C 3C 1C 0B 58 D8 99 E6 25 E9 8A 74 FA 4E 08 EF E9 BD 85 BF C6 19

92 9E 90 B9 18 60 00 10 00 00 05 16 B1 2B DD 6E E8 00 C1 C0 B7 6B 17 0F 3C C3 BD 02 9D 16 83 54

6D EC 5F C0 CC C2 19 F2 9E 31 7E 30 00 00 10 00 00 0A 2C E1 57 BF DF D0 01 81 6E DD 8C 3C 1B 86

0D F9 89 5B B5 84 67 4A 74 D5 60 56 8B 44 D6 00 03 F0 00 02 01 2A 6D CF 33 36 80 0B 56 AC D8 C0

B7 7C B5 54 09 E7 67 E5 18 D3 A6 AB 57 85 98 95 C2 95 F0 00 F4 00 00 4C 12 A6 2A A8 01 45 14 4A

9A 26 53 01 5E E3 77 DE 9C 15 56 F3 74 39 63 12 28 DE 16 E8 CC 00 0F 40 00 08 88 11 7F 36 9D 16

86 B0 0C FC FB 97 F3 33 AD 99 F6 64 2F ED 37 1D B9 C4 55 67 33 49 BE 18 D1 4E E4 C2 65 80 07 B0

00 02 41 7F 37 73 6F 89 E2 2E 80 6F B2 32 73 76 DB AD 01 BC C3 A4 55 BA DE F7 A7 03 3B 19 DA 3C

81 89 14 6F 4B 72 CD 00 0F C0 00 0A 28 90 AB 37 73 6B 8D E2 EF 80 6F 72 B2 F3 77 1B CD 09 BB C3

A4 4F 3A E6 51 8F 12 AB 02 E8 B2 96 79 4A F8 00 02 00 00 53 81 40 9D 59 D4 69 74 92 00 CF BD 7E

FE 76 7E 19 97 6A 42 8C 2C 0C 63 26 51 62 E5 B1 7D 18 05 6B 20 00 14 00 01 6B 0E C0 95 36 E3 2B

2B 10 02 D5 8A 69 B7 6A C1 12 90 B1 A6 D1 F0 67 7F 45 58 5B DD 00 CD 94 F4 45 D8 C3 00 00 C0 00

0B 58 74 8A 6D E8 2F F7 FB 1D 10 06 36 16 0E 06 87 1C 58 98 59 D6 6A 38 93 B8 B1 7F 13 79 A2 19

74 4F 4C 67 31 40 00 28 00 02 CE 15 22 C6 16 92 FF 77 DE 69 00 34 18 B8 98 5A 5D 14 16 EA 0A 75

1A 5E 0C EF AC 5D C3 DF E2 8C C9 4F 46 5D 9E 20 00 02 00 00 51 62 42 9C 0D 0D FD 9E D3 40 01 8B

89 89 81 A3 D0 4C B5 58 51 85 83 8C 65 51 5D 8B D6 85 48 B6 56 B2 00 1F 80 00 13 AE 04 A9 B7 3C

CC DB 60 16 AD 59 A7 02 D4 14 CC 22 ED EC E3 0A 28 AE C5 42 94 AF 94 2A 00 0F A0 00 0A AE 4C 45

77 28 C4 C4 B8 01 7A F5 FA AE 5D 13 90 57 BE C8 DB 1A 9A AC DC C4 CE 18 11 2C B2 CC AE 00 07 B0

00 05 FC DA 85 79 FB EB 3C 06 BB 78 01 95 97 97 73 79 BF 17 E9 0A F7 3B CE F8 E0 6B B5 9D A1 CA

18 71 46 F4 C0 96 68 00 7A 00 00 5E CC AC 55 9D BA B5 C4 F1 1B 90 0D F6 4E 5E 6E E3 78 2F 53 02

FE DF 77 DD 9C 25 76 33 74 79 03 12 28 DE 98 12 CC 00 0F 80 00 0B F9 D5 8A B3 F7 B6 78 8E 1B 74

01 BF CD CE CE DE 6F C5 EA 42 AD DE FB 60 70 13 A7 3F 45 90 30 E2 8D F1 6D 9A 00 00

  
  
2nd Animation Data \[at offset 0x00006304\]

  
14 00 FA 02 00 FF E9 FE C0 FF D7 00 00 00 00 0C 00 D7 E0 00 09 00 14 EA 80 BB 0C 82 BC FC CF 42

AA 71 80 3F 62 A8 26 72 25 F2 FE 4B 00 00 00 02 10 5C ED E0 DA 13 42 EB 2D CF F8 0A 91 BA B6 CE

AA F1 00 00 00 0F B7 FF 8E BB 00 08 DE 00 02 B8 0E BB 05 33 60 00 00 0F 7B F5 63 5C D4 00 00 00

00 00 21 F0 00 02 9D 10 02 03 20 80 08 00 DB 1F E9 01 2D 56 00 00 00 00 00 00 0A 11 01 05 77 72

2C 68 71 6E 99 B7 D1 11 97 72 ED 19 B7 45 74 67 28 2B 8A CB 10 09 25 12 91 15 52 00 1F C0 02 48

04 CA AE 6F EC 68 B1 EE 99 B7 D0 8C 9B B7 65 9B 74 55 46 62 45 51 32 C4 48 24 A2 25 40 BF 60 00

00 00 07 D6 FF A9 1C 02 22 57 EE 6F EC 68 F1 EE 99 B7 91 11 95 72 ED 19 97 45 74 66 28 2A 56 58

80 50 94 4A 82 2F D8 00 00 00 01 6A FC 20 41 55 DC 8B 1A 3D 05 D3 36 FC A0 C9 BD 7E 59 B7 45 74

E6 24 57 13 2C 4C 12 4A 6A 08 BF 60 00 00 00 85 AB F3 80 82 AB B9 14 E8 71 AF 19 D7 D1 11 97 7A

FC B3 6E 8A E8 CE 48 AE 26 58 02 84 A2 52 15 52 00 1F C0 02 CD 60 41 55 FC BA 71 F1 2F 17 2A 91

19 B5 55 46 7D F1 5D 19 EA 11 5A 65 30 09 25 12 A0 8A A9 00 00 00 01 4C E0 10 57 7F 3A 8C 4C 3A

8B B5 4A 0C FA AB 5D BE 27 45 D4 89 C4 CA 20 12 48 90 AE 90 02 00 00 12 88 40 13 9D E9 60 5A AC

BF 30 BD 38 95 FA C4 4A F8 42 0A 12 01 12 09 C8 00 00 00 04 80 04 56 A6 98 22 11 11 38 84 40 4A

61 01 28 04 92 24 12 00 00 00 01 00 02 54 AB AE 44 A4 94 A5 44 A4 94 82 28 09 04 48 10 82 02 03

F8 00 00 44 A4 90 14 51 6A 2E 5E A4 B3 40 5A A2 51 66 91 28 B2 12 48 9A 00 4A 02 88 00 00 00 01

5D 12 04 8A 6C E1 4F 33 36 C1 6E C4 48 C1 B1 4A DD 91 44 ED A0 A2 54 13 90 21 04 0A 6B 00 00 20

01 7E 90 24 58 B3 8B 5E 4E 65 A3 02 C4 12 C3 B1 62 78 36 45 33 C1 4D 2A 54 15 C8 10 89 44 C9 58

AC 00 00 3F 85 EB 34 48 24 58 B7 A0 AF 7F 95 68 C2 B2 94 A5 8B 6A CC 61 DB 14 CF 09 05 32 A0 A8

09 A2 51 02 C5 60 00 00 00 2F 59 92 42 45 8B 7A 0A B7 B9 16 CC 3B 31 23 1E D5 98 C3 B6 29 AF 11

05 32 A0 AA 80 42 28 4C 95 9A 80 00 00 00 7A 90 FD 6E C8 12 94 59 C0 D0 D5 BD C9 B6 61 DA 4A 52

C6 C0 B7 3C 4B 62 99 E2 26 58 52 55 20 4D 12 89 92 B3 50 00 01 00 08 48 14 16 30 34 35 6F B2 6D

98 76 52 4B 1E DD B8 C3 B6 2C 4F 11 05 89 50 55 28 08 4E 51 31 66 A0 00 00 00 13 4A 41 22 9B 7A

0A B7 F9 76 CC 3B 29 4A 58 B8 16 E7 87 6C 53 3C 24 CA 65 49 54 81 08 94 41 2B 15 80 00 00 00 84

92 12 2C 5B C7 AB 27 32 D1 83 65 24 B1 30 2D CF 06 D0 A6 78 48 29 95 05 72 04 D1 24 C5 8A C1 00

  
  
3rd Animation Data \[at offset 0x00006604\]

  
2D 00 A0 04 04 FE 95 FD E3 01 D8 00 00 00 C0 FC 00 F8 03 09 13 02 FF F9 F1 CD 1D 0D FF 1E FA A4

CB 00 00 00 00 FA F2 14 44 2F 00 0B 22 F2 0D F3 00 00 F8 F7 FC 00 B2 00 36 12 CF 10 00 00 E3 FD

20 D5 00 00 00 46 00 2D DA 19 10 00 00 EC FE EF D5 00 00 80 3F AE FF D9 82 C2 25 82 AF 32 99 60

57 7A FD 74 2A 0B 57 D6 C5 5A 0A B1 48 9D 85 85 56 30 AE 98 56 33 C2 C2 CE 83 1E E9 29 5E 0E 8F

C2 A1 D0 FA 01 41 5A 54 4E 71 5D 35 05 75 44 50 22 C2 80 24 5F AA F1 62 55 84 92 AA FC C9 44 00

40 27 D0 F4 0E 80 82 42 45 11 4C 0A 6C A4 08 94 04 09 57 55 64 A2 C8 11 29 48 00 10 01 D8 4B 9F

E8 22 50 9A 25 16 A1 85 5F 09 5F C0 7C 06 FF 07 8B 4A 22 22 22 20 22 20 B1 62 C1 5A 04 A1 14 52

20 00 80 0F 02 42 88 89 CA 25 16 D1 9F 2E 17 08 CC EE 79 B5 13 82 26 09 44 0B 36 6C 93 40 91 14

4A 42 52 00 00 20 02 00 05 30 9C 53 49 4D DB 72 24 20 08 91 08 10 08 24 08 00 03 F8 00 8E 83 D0

00 12 45 32 AE 45 56 2F 41 29 49 20 22 42 02 40 82 50 12 00 03 AB 98 A3 D0 3A 00 42 4A A5 28 2A

25 4C 24 00 11 34 A5 62 C0 B1 4C 0A 12 9D 8A 45 13 90 00 79 77 14 00 90 DC D8 A6 F5 8A 2D FC 07

C0 61 E3 5C 15 4E 60 09 94 58 A4 51 44 0A 09 D1 40 94 00 00 28 30 80 10 2C 8A 97 09 D5 68 48 49

20 48 8A E6 27 12 10 4A 73 11 20 00 07 09 13 04 90 4B 0E 71 2B EC FF 80 F8 09 E7 DB 12 94 A2 88

02 84 45 75 89 CC 26 8A 27 31 12 80 00 0C 0E 23 A0 F4 01 0A 11 16 E7 3B 36 67 84 5D 8B E8 51 29

4A B9 40 24 44 E6 27 39 08 25 38 11 20 00 01 04 0E 83 D0 28 AA BA EC 5B 95 75 DE B1 63 1F 5F 73

38 BD C4 FD F5 35 CE 8C 1C 0B 5B CB 17 4B 31 64 40 20 01 13 00 00 3F BE 07 A0 74 12 AE 75 4A DA

AA EE 44 68 29 EF 30 3E 03 E0 34 BA 5E BA 8A E7 3C FB 96 32 25 70 B0 AC 48 12 00 4A 80 00 00 03

30 04 44 5F 17 F7 D9 F5 ED BB 7A CA 65 7E 50 DB 6C B7 D9 78 D9 17 83 BF 12 CF CF AC 89 00 96 0E

05 64 40 00 00 35 00 4A 51 78 5E C9 BB 35 EB E5 71 66 24 DE EF 70 F2 75 51 58 6C 42 E5 C9 80 06

0E 04 C0 00 00 1E C0 10 98 9D 51 39 4E 00 27 7A D2 DA 03 40 13 98 00 28 A0 00 00 00 FA 00 01 02

00 11 3A 28 A1 04 9A 40 9C 40 00 51 44 08 90 00 00 7E 00 00 00 02 51 2B 12 04 6E 01 00 00 94 80

00 00 0F C0 00 00 00 0A 44 44 37 21 00 00 4A 50 00 00 FE 00 00 00 00 00 4A 52 24 D2 80 00 09 48

00 FE 00 00 10 00 00 00 09 48 49 A8 40 00 02 52 12 00 00 00 00 00 04 80 02 44 01 11 BA 00 00 80

80 00 00 07 F0 04 80 09 00 12 12 10 DD 80 00 09 48 00 00 00 00 00 01 20 00 10 05 0D 30 22 00 00

00 00 00 3F 80 00 91 22 40 00 04 B4 E1 00 00 4A 50 00 00 00 FE 00 00 40 00 00 23 74 00 00 24 00

00 00 00 00 00 88 08 00 24 04 DB 90 00 00 90 00 00 01 FC 01 00 00 00 80 12 69 82 49 00 00 20 00

00 20 00 00 01 00 02 44 09 4B 4C 09 00 00 00 00 00 00 00 00 40 00 40 20 43 70 00 00 00 00 00 00

08 00 00 00 01 01 0D C8 00 00 40 00 00 00 00 00 00 00 00 88 82 4D 40 4A 40 00 80 00 00 00 08 00

02 42 40 04 A2 73 48 94 B5 20 00 02 22 40 00 00 00 40 09 02 54 4A 49 48 04 A5 44 EB AE 24 22 E0

4A 40 00 88 12 00 00 00 10 00 09 48 89 00 14 4E BA C2 23 7E 12 48 00 27 39 00 00 80 04 84 80 04

92 00 22 56 2A 89 C9 29 45 19 89 14 50 00 48 BD 7A 82 25 00 04 00 60 29 10 40 94 A4 48 01 2B 55

53 09 D3 4C ED 4D 49 66 CD 00 0A 52 AE 78 05 54 C0 01 7F 1B 0A 04 22 B8 44 44 00 24 8A 2D DE B1

12 BF 62 C4 F0 21 41 66 CC 84 02 85 13 9E 09 55 8A C0 10 00 D0 58 10 8A 88 04 00 45 18 17 2D 29

B9 4D 8A F0 64 B0 8B 16 28 00 58 51 2A 2C 95 D8 98 07 7F 16 0B 62 65 50 98 00 49 3B 58 B9 36 EC

63 6F E5 62 EE 0D A5 B4 A7 30 02 DA 35 5A AC C2 89 C8 03 00 09 85 B4 A9 AA 22 71 4D 40 01 4D 35

E1 68 F6 B9 D6 38 5C 4F 7F F7 88 DD EA 56 C9 CC 44 48 2D AB C5 C5 CA 29 AE 80 02 00 06 04 A5 38

9D 29 4C 00 25 44 ED 58 C8 CA CC C4 B7 76 EE 05 DD 08 00 00 94 A6 00 FE 00 FA 00 00 00 00 00 00

00 08 8A 00 12 00 00 00

  
  
4th Animation Data \[at offset 0x00006AAC\]

  
0E 00 E0 01 04 00 00 FE 63 FF 9E 00 00 00 C0 ED 00 F8 FE E9 0C 0D 2C EC F0 AE 18 40 2B 32 24 F4

E2 00 00 03 06 F4 FF 0F 26 2F 00 0B 28 AC E2 E5 00 00 FD FF F8 00 A3 00 22 DC 8B 0C 00 00 DC 00

15 C3 80 80 00 37 00 12 BC 03 3E 80 80 D8 F8 02 D7 00 00 00 80 21 7F EA 00 00 0A E8 A2 61 48 02

E1 26 00 BB 4E 7C 16 25 BA C5 04 5F AF 7E 64 60 5D 98 01 FF 69 FF 9E 80 00 16 AF 5E B2 17 00 43

48 4D BC 16 B4 9C A6 29 C5 DD AA C7 C0 7C 00 D6 D3 9D 85 F0 1F 01 AB B3 8B BD F8 0F 80 00 40 FF

BA 80 00 00 00 12 00 00 00 65 68 74 19 9F 01 F0 18 39 75 68 FE 03 E0 00 20 08 04 C0 56 8A 2C 4A

A4 80 02 B4 C2 00 0C 4D 36 9F 50 76 16 F4 20 4F 3E 8D EF C0 7C 06 1E 0E EC 00 40 12 7F E8 83 1F

0F 34 00 27 4D 39 81 60 01 BF 2B 96 86 ED 19 6E 0F 57 04 B4 9B 7C AF 80 F8 04 B1 F7 55 5C E1 BE

03 E0 3B BB 78 00 00 1D B0 50 94 09 00 89 26 02 00 98 51 09 CA AA AA 14 54 0A 04 CA 92 00 0F 22

82 68 90 80 12 85 00 24 05 01 39 28 8B 16 2C 09 D8 04 C5 05 84 00 07 72 21 58 10 90 11 14 84 48

02 C1 25 52 8A 6C 6F F2 AA 28 96 8A F7 C0 7C 02 2B A1 29 7C 07 C0 59 AA 80 00 EE 4C 2A 24 44 24

81 22 90 89 24 12 59 24 AA 88 A5 B6 DD 5D 2B A3 1E D8 55 4C A8 BE 5A BF 40 00 71 2E 17 C9 11 11

20 4A 22 90 80 10 B0 22 FD 0B 15 EE 77 99 A4 F3 34 16 C2 FD 95 19 C6 05 56 40 03 99 28 AF 37 0E

49 21 20 22 29 08 92 41 25 82 4A A8 53 7F 33 3B 3C 96 5E 2D A0 AE CC A5 70 B7 5D 80 00 FC 0A 25

F1 7E EA 10 00 00 02 12 00 4E 20 44 A4 09 10 48 00 00 4F 62 3D D7 E2 C2 40 00 00 24 80 05 12 90

94 40 20 91 00 00 00 00

  
  
5th Animation Data \[at offset 0x00006C94\]

  
0C 00 61 01 04 00 00 FE 5C 00 1C 00 00 00 C0 6D 80 F8 FE E9 0C 0D 2C EC F0 AE 18 40 2B 2F 26 F6

E5 00 00 05 0C F5 FF 0F 26 2F 00 0B 28 AD E4 E6 00 00 FD 04 F9 00 A3 00 2E FD C1 2D 00 00 D8 FA

30 D4 00 00 00 37 00 0F C2 04 2F 00 00 EE F8 07 D5 00 00 00 2B 17 00 00 2F D3 40 59 B2 04 4A 8C

E2 76 70 C5 5A BD 46 2F C0 7C 04 54 02 ED 11 68 A2 29 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 1F FA 38 02 80 7C 07 C0 00 05 72 90 8B F0 04 A7 56 61 A1 BD 58

B5 C0 68 AF 99 78 BD 60 18 D2 B3 DE 1C 05 19 60 01 B2 03 00 04 A5 02 54 04 A0 12 AE 52 01 6C CE

9C 0B BF 4D F7 7D DF C0 7C 06 15 3C 10 19 51 7F 89 36 4B 20 02 00 8F 00 89 02 22 42 26 18 B9 F9

E2 2E DD 88 04 35 45 E9 EF 06 1F A3 73 FC 59 95 D2 F2 80 62 2C 77 A6 32 60 00 20 40 00 00 94 E6

20 01 25 04 4A 04 60 E0 59 25 95 8A 00 AC A0 00 0F 0E 00 00 04 51 40 90 02 13 25 12 12 CF B9 7C

8C 6C B0 05 24 C0 00 C6 90 00 00 00 00 48 00 8D A6 DF 38 C0 E1 36 A0 4A 71 6C B8 90 00 73 56 00

00 00 00 00 05 7B 6D CE 41 6B 0A F8 12 85 A2 F2 80 00 EC B2 00 00 00 00 00 0B B9 19 3B F2 D5 A8

02 50 B0 5E 89 00 00 00

  
  
6th Animation Data \[at offset 0x00006DFC\]

  
0A 00 6A 01 04 00 00 FE 25 00 63 00 00 00 C0 ED 00 FD FD 22 15 F9 E9 07 EE E2 22 38 26 19 38 19

E5 00 00 E6 00 00 EE 06 5E 2A D6 E5 08 C7 26 E2 00 00 00 F5 00 00 A3 00 32 F9 A1 1F 00 00 DD 0C

F0 C2 80 80 00 37 00 1F CB 01 0A 00 00 03 FD 00 D5 00 00 00 00 00 1A 6F 90 F7 2C 4B 50 31 2C DF

00 0C 4B 54 80 06 25 9D 1E EF 79 BE 00 4E 8D D6 96 CD 90 50 00 00 20 16 A0 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 83 75 EE 1F 1D 99 7A 43 32 FD 90 00 CC BD 58 00

66 5F DE E9 74 9A 20 05 13 D3 6E EF DF 04 C0 03 B2 A0 A3 1F 26 FC 6C E3 17 83 C9 AB 71 7E C5 3A

1A 2B 18 D6 B3 AC E0 6C AC E8 F4 3A DB 39 B8 05 56 73 E1 17 F2 EC 66 94 5E E0 2D FC 07 C0 14 5E

BD 46 39 99 39 00 00 F5 31 3C 9C 75 1B 4B 96 F8 0C CB 5B 4B F6 28 C3 DB 77 43 1D 77 12 5B 66 9F

4B 4E C3 A7 B6 2C E6 C9 2A B2 A5 51 55 FD 7E 18 4E 77 E9 C7 33 6B A4 00 02 80 01 4D 10 29 A6 05

C9 48 0A 68 90 BD 8B 82 2C 4C 2D FB 3F AD F1 26 67 73 A1 01 62 80 00 03 B7 FE 98 08 89 08 80 A6

20 08 80 A2 FD 62 72 0B 5D 77 69 9A 58 D1 67 00 88 00 00 02 7F E5 C0 9C 04 E7 21 64 02 71 02 C5

CB C2 72 0C BE AF B1 D9 16 F4 77 C0 57 00 02 00

  
  
7th Animation Data \[at offset 0x00006F6C\]

  
01 00 4E 00 04 00 00 FF C6 00 00 00 00 00 00 00 00 F9 00 00 07 00 CB F6 EE C5 2F 0B FF 1B 06 FE

C6 00 00 00 F0 00 F6 12 3B 2F 00 0B 04 FA 0A F4 00 00 06 FE F6 F6 C0 C0 2F 13 FE 0A 00 00 06 00

00 D5 00 00 F6 40 40 17 F5 FD 3D 00 00 0F 00 00 D5 00 00 00

  
  
8th Animation Data \[at offset 0x00006FC0\]

  
06 00 20 01 04 00 00 FD A8 00 00 00 00 00 D5 80 00 F9 00 EC 07 03 13 EE F1 B2 2F 00 F5 22 E3 9D

E3 00 00 00 00 00 FE 11 29 2F 00 0B 37 14 40 EB 00 00 00 E9 FA FB 37 EB 02 46 00 3B 00 00 FB 00

00 D5 00 00 FB C9 15 34 22 5D 1E 00 00 04 00 00 D5 00 00 00 24 00 00 D2 2B DE E0 57 A3 1A 3D 6F

07 84 6F CB 92 D1 08 DE 26 29 90 E1 EF 53 B4 2A 33 3E 03 E0 06 DB E5 3E 8F 81 36 E0 00 24 00 00

D7 4E AE FF 12 9D 58 E8 78 1E 4F 38 B2 66 DE D7 8C AD E5 74 91 97 82 34 FF 47 F4 7B 13 10 C2 07

7F 66 37 5F 01 F0 18 E0 00 FF DC 00 00 67 CA 58 B5 CE E0 D1 53 31 88 53 4E 70 B7 17 C4 B0 6A 19

B5 55 AF 05 1F 01 F0 03 05 2D 27 C0 7C 00 00 04 80 00 1B B9 53 A4 CF 8D E8 E0 BE FF EB EC 83 02

9D D8 B5 A5 C0 A8 8B 17 86 D7 DA FD 7B 80 37 00 1C 3D 9A F6 44 CC DF 80 F8 00 02 40 00 0D 95 76

35 79 B6 B6 43 73 63 3F 44 0C 4A F6 A3 0F 63 D0 58 25 83 68 77 F5 4B 77 F0 1F 01 A0 00 D3 70 DC

16 C4 C1 30 8B 00 00 00

  
  
9th Animation Data \[at offset 0x000070E8\]

  
01 00 4E 00 04 00 00 FE 68 FF 4D 00 00 00 C6 00 00 F9 00 00 13 00 00 F6 EE C5 13 08 FB 29 30 EC

C8 00 00 E1 B3 FC F6 12 3B 15 F9 05 25 CC 0A D8 00 00 E1 34 09 FE B6 FA 0F 2B EB 31 00 00 E6 0E

0C D5 00 00 FE 4A 06 0F D5 15 31 00 00 E6 F2 F4 D5 00 00 00

  
  
10th Animation Data \[at offset 0x0000713C\]

  
0E 00 31 02 04 00 00 FE 29 00 00 00 00 00 C0 ED 00 F8 FE E0 0C 0D 2C EA F3 A5 18 40 2B 1E D4 9F

E5 00 00 03 06 EF 02 0D 1E 2F 00 0B 1C C5 F4 F1 00 00 02 F3 F8 00 A3 00 29 DE A6 10 00 00 DB 01

2F D4 00 00 00 37 00 17 C0 06 28 00 00 EC F8 04 D5 00 00 00 80 44 40 28 43 B4 59 AE FE 75 CE 2E

98 BD A7 E8 3A AC 5D E6 C7 67 F0 1F 01 5D ED 0D AA AB 18 DC DF A6 6F 09 D1 80 ED 1B 8F 44 F4 7E

07 E0 3E 02 FF 29 F3 D2 1D A2 E7 01 C2 C1 A8 A7 6E 00 00 00 00 00 00 00 00 00 00 00 00 00 1B 7F

F7 41 A6 4E C7 03 81 1D 8E 0D 5C 00 C4 F8 0F 7D BD F0 1F 01 2A 73 F2 B0 35 A2 FF DF 74 B6 49 C6

33 4C B3 BD CA C5 25 7B 4E 1A 65 DD F6 E7 18 DD 67 E2 00 0F FC 2F FD 78 31 53 96 8E 55 6C ED 34

63 BE BF 9D A7 22 BC 1C E8 D0 89 EE B2 A8 24 BC C5 63 6F 36 DB EF 80 F8 0C 3D AE A2 06 2B 47 99

9B 51 93 6A 80 01 FF 90 FF AE 86 0A 27 8B B4 A3 75 66 58 A3 ED F3 35 DA 70 5F BF 8C 25 91 9B 41

29 5C 60 A9 EF 7B CD C9 8D BC B0 18 2D 6D FC BD 81 63 0A D0 00 77 73 09 0A 27 44 C9 0B D9 B8 52

04 44 82 20 10 92 2B AE 64 A6 09 28 BB 72 B1 20 00 09 0D 08 13 A2 74 10 2D 61 E7 40 25 28 09 48

12 42 54 D3 41 14 02 13 B7 81 48 80 00 00 00 00 00 00 00 00 00 00 00 00 00 14 80 29 81 6E C5 DB

F7 F0 E9 A3 3A 2A AB 4D 8D 91 90 12 C0 B3 78 55 6A C8 44 82 54 4C BF 6B 10 0C EB 16 ED 94 44 C0

01 8C 01 48 0C 19 67 54 C2 B1 19 69 C6 B2 88 DF 83 12 8B E2 AB 76 60 90 25 4C A6 67 D1 A0 03 31

4E 09 62 FD 80 00 5F 00 45 02 D5 59 B3 9E 14 AB CC 95 AB 3A CA 2C 65 84 61 4E E8 AE CD 12 22 50

25 45 10 5D BB A3 03 36 16 CA 6A A4 00 03 84 01 9F 56 6E 8E 9C 4C B9 DD AB 89 E1 74 17 23 14 95

37 6B AF 24 5B B1 7A C9 5D 8B 80 08 9D 20 40 12 00 07 B7 80 32 E9 CC D2 E3 E2 64 59 BB BD D3 E8

70 F6 FB DD 31 45 39 D7 68 C8 18 15 E4 5A 22 D6 60 00 80 24 04 07 00 00

  
  
11th Animation Data \[at offset 0x00007374\]

  
0F 00 8A 02 04 FF FE FE 32 00 36 00 00 00 C0 DE 00 FD 02 EB 08 0A 2E F1 F4 AF 22 2F 1D 33 15 EC

DB 00 00 FD 0C F2 03 13 2A 2F 00 0B 21 C2 E8 EF 00 00 01 FA EE 00 94 00 2B 01 C7 22 00 00 D3 09

1A D6 00 00 00 28 00 15 C9 0A 2A 00 00 EC FB 03 D5 00 00 7D 08 37 0E 17 AD B1 4D 15 CE 56 69 95

1B 8D D5 77 2B CF 2F 58 A2 8B 16 05 DD 2D 99 96 AA 32 97 35 7A 9D 01 2D 1E C6 06 52 78 36 24 28

07 D0 23 80 CA 58 B1 62 BA E8 B3 62 8B FB BC 8A EE CF 3C BF 4C A8 B1 60 5E D1 53 32 CD F3 2D 7B

1F 17 04 C5 BF 56 68 CB 51 85 85 51 12 07 E1 22 20 CE 51 62 89 CE 8A 69 95 DC CB B3 BC BA 5F A5

2B 16 05 FC 7B 10 59 AA 19 AB F8 56 EC 18 99 B5 DD F8 0F 80 66 A5 85 89 68 50 00 0F AF E0 53 2A

E7 5D 99 4A AA E6 A6 BA 65 F0 1F 01 3A 27 62 53 15 48 25 39 80 00 00 00 00 06 02 05 71 4D 14 DF

88 B1 4D 0A E9 AE 3E 03 E0 28 9D 15 45 02 C4 04 51 40 00 00 00 00 CD 1F F4 E0 CF E4 F7 DB AD 56

34 76 17 B6 FC 04 F7 3B ED D6 BE 9E 0C C6 E9 75 5B 5D CE 80 5A D7 7A 2D E3 3E DE 89 C5 35 5D AF

DA EF 4D 46 76 0E 00 E2 91 B5 D9 41 11 70 02 34 FF CA 03 85 70 35 70 33 C9 EC F8 BA F4 3A AD 7E

97 2B 51 85 60 B9 E8 99 7A 8D FF 12 32 A5 62 F9 9F 2A 5C 2B 7D F7 BD A7 78 69 EF B1 7E 03 E0 1C

2B 0F 65 73 0C DD 4F 10 00 00 00 81 6A C5 A9 CE F5 BB 16 28 B7 6A 74 CA 43 02 76 65 64 57 2A 20

84 85 75 4E A2 C5 73 B0 00 00 00 00 00 02 89 53 08 A6 8A 22 FD 50 90 82 89 50 2A A2 90 89 08 94

0A 2A AE 00 00 00 0F EF E0 4E 27 29 51 39 C4 5F AA 50 81 54 A2 20 24 12 40 95 0A 08 26 00 00 00

02 00 02 F5 57 68 95 9B 95 5F 53 45 13 98 95 52 BD 17 85 BA AF C8 4A 05 32 A6 82 FD BB 30 00 00

00 7F 80 3D 86 63 69 89 DA E0 61 F0 DD AE 1E D2 FF 19 C4 E8 B3 73 A6 61 67 32 35 5D 80 B7 F3 DD

0E 01 5D 8C F6 62 8C 1E 42 93 B6 C6 D5 CC 66 2E E0 D9 B8 68 26 00 00 A5 61 74 A3 22 78 3A AB B6

32 33 F1 B0 F1 B3 E2 0B 37 2E 5B A3 24 60 DD CF B2 45 37 57 54 5B 95 26 4D 58 90 2E A2 CC AB 2C

C4 C0 00 28 E8 5D 4E BC EB D6 B4 D7 E3 3B 3B 02 C6 35 76 E0 95 DC DA 6A CE 1A 1A F7 B6 49 53 79

75 66 DD CA 0C FB 98 B0 2E A2 CD 15 14 CE 04 00

  
  
12th Animation Data \[at offset 0x00007604\]

  
30 1A 00 00

  
  
13th Animation Data \[at offset 0x00007608\]

  
1E 00 8D 03 04 00 00 FD D5 00 E0 00 00 00 C0 EF 00 FA FF E9 09 09 2A EE F1 AE 2F 00 F5 20 00 A7

D9 00 00 00 00 00 00 10 27 2F 00 0B 2D 00 20 CA 00 00 00 F5 EE 00 A5 00 2F 0A E7 00 00 00 FB 05

07 D5 00 00 00 39 00 30 EE 1A 00 00 00 FB 00 EA D5 00 00 00 00 00 00 00 00 00 67 F1 3C B6 7F C0

7C 06 82 FE 00 00 00 00 00 00 00 00 00 00 00 0D D4 69 F0 8D 05 8C 10 00 00 00 00 00 00 00 00 00

00 13 50 14 50 00 00 00 00 00 00 00 00 00 00 02 84 C2 20 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 22 54 58 CF CB AC DD E7 E5 80 00 00 00 00 00 00 00 00 00 02 56 23 37

7F 39 46 DE 8B 80 00 00 00 00 00 00 00 00 00 00 95 9A AE 6F EB 94 64 E1 66 80 00 00 00 00 00 00

00 00 00 04 25 7E AC 99 E1 E6 D7 4E 58 00 00 00 00 00 00 00 00 00 00 49 3B EC DA 3D BB E4 A2 AC

D0 00 00 00 00 00 00 00 00 00 00 95 79 D5 CA E5 34 C4 E7 74 00 00 00 07 F0 17 E0 81 10 91 09 48

88 04 A2 27 99 DD 45 16 94 D9 B1 7B 05 08 48 00 84 44 00 1F C0 5F 80 04 82 52 01 01 99 67 BB 88

D0 5A F8 9F 7C C1 AF 46 09 00 01 00 00 27 E0 40 90 94 93 24 9C C9 48 49 12 95 58 F9 14 57 8D 8F

76 FD B6 85 24 93 00 24 94 A8 00 00 39 12 06 01 2C 3B 33 DF 58 9E 1D 59 19 56 AC 61 5B 18 0A A5

85 8F 9B C2 69 32 E8 DD E8 71 6D DF C3 60 29 AB 24 5D 5B 0C 05 38 18 E2 F4 40 00 7D 08 0C 14 31

29 BB BA B1 18 97 B3 33 AC E1 63 DB 18 2B D2 C2 BB AF F4 FD 3D C9 F0 3E D9 EE 78 15 DB 60 A5 9D

B8 17 AB C1 0C 13 1B 4E 2E C0 00 00 00 00 00 00 00 00 90 00 00 00 00 03 D0 00 13 28 20 14 53 6A

A2 ED 18 D0 0A 2B BF 51 72 FE 58 02 9A 22 60 02 99 CA 60 03 D0 00 13 24 4D 21 2B 36 EA 33 E7 A1

9C A0 4A FD CA 8C B9 E5 00 29 A2 26 00 29 9C A6 00 3D 00 01 32 89 27 12 14 5A C1 A8 B9 77 47 34

0A 2F 67 D4 65 5A C9 00 58 A1 58 00 B1 35 60 03 D8 00 10 50 42 41 67 02 A2 AC FD 0C 20 2F DD A8

CF D0 EE C0 14 50 98 00 A2 72 98 00 FA 02 24 4C 91 34 84 F0 B0 28 22 74 CD 02 79 D9 F4 11 66 F1

0A 28 14 22 02 49 CC 50 40 00 06 FE 20 A0 82 84 0A 33 AE 4C 95 15 D0 90 A3 0B 06 64 AF DA 24 9C

C4 D2 90 42 8A 04 C9 00 01 6F C2 D7 C0 7C 06 21 9D 0C 29 5F 19 DF 79 D1 EF 41 85 16 46 77 A2 73

9B D0 49 6A BC BC B1 7A A5 92 4B F5 E2 E2 8B D6 22 C8 00 16 FC 2C 98 86 71 86 BE 37 3B AD E6 1F

C0 7C 00 C3 59 1B 9D 36 93 0F E0 3E 00 50 B3 56 7E 70 BD 55 16 0A 17 AA C1 C2 17 AC 4E C0 00 02

FA 28 28 26 52 89 D7 3B 97 EE DB 27 55 9A 54 4E 9A 6E 59 B7 6C 9E 06 79 28 9C E0 88 48 22 28 A2

08 92 40 03 F8 18 99 32 82 B4 A8 A6 8C 0B 36 EE 94 58 BF 5A 74 57 5E 05 FB B7 4A 2E 60 91 2A 28

91 29 20 25 29 CE 44 A1 00 00 08 A0 BE 5C 30 4B D2 A7 0B 85 E0 34 9C 7F 2F 67 E0 3E 03 41 85 B1

BC AF 0B BB D8 69 3B 1E A6 CF C0 7C 06 A7 23 5F 0B F6 74 3A 1B 04 02 16 6C EF F7 F6 08 00 00 08

D0 BD F0 1F 01 9E 61 C9 9F 16 32 F8 FE 27 BD E2 F9 CE 30 C4 CD EF 33 D5 65 F6 5D BF 7B DA F4 9C

61 A2 D0 F0 13 5E 96 BF 5F 64 40 4D 6A 5B 1D 95 91 20 00 00

  
  
14th Animation Data \[at offset 0x0000799C\]

  
06 00 CF 00 04 00 00 FD C5 01 36 00 00 00 C0 00 00 F9 00 00 18 01 02 F6 EE C5 22 38 26 00 21 00

00 00 00 00 01 00 F6 12 3B 22 C9 DA 00 DF 00 00 00 00 00 F4 00 00 B6 00 32 16 D9 09 00 00 ED 01

17 D5 00 00 00 4A 00 32 EA 28 09 00 00 ED FF E9 D5 00 00 00 00 00 00 00 00 40 00 12 00 00 00 00

00 FA F6 24 41 49 00 95 A8 0C E4 02 57 A4 18 40 88 98 90 12 49 30 00 00 30 51 04 8A 09 01 66 41

9C 90 17 E0 30 81 29 50 20 08 42 80 00 01 32 31 63 E0 3E 03 00 99 6E 55 0B F2 A0 21 6D 60 5F 89

84 92 58 AE D5 8C 42 FC 48 49 5D 77 AF E2 17 E5 00 00 60 B4 58 30 8A CC 28 A8 5E 8A 42 4C 25 81

7A 8A C2 12 58 AA D5 8D 09 7E 72 12 5F AA F5 5A 12 FD 10 21

  
  
15th Animation Data \[at offset 0x00007A70\]

  
0B 00 DE 01 04 00 00 FD D6 01 81 00 00 00 C5 80 80 09 00 00 15 01 02 04 EE BE 2D 20 12 0E 2F F8

F7 00 00 00 F9 00 04 12 42 2D E0 EE 0E D1 08 F7 00 00 00 03 00 01 B6 05 2E 1D DD 18 00 00 EA FE

19 D5 00 00 01 4A FB 2E E3 23 18 00 00 EA 02 E7 D5 00 00 00 69 7B 15 93 27 09 CA 52 EE BB DD 25

DD E5 C1 8A 9A 25 C3 F0 7A 4B 7A 4B 82 F0 AE C5 DB D9 65 A8 02 9B 18 16 B2 CB 52 00 07 C7 C1 3F

80 F8 09 93 21 2C FD D6 FB 07 6D DE 5C 18 68 46 7E 97 45 83 AA E1 2E 0B E8 4E 8C FB D9 A5 A4 08

51 46 05 AC D2 D2 40 00 00 00 00 00 00 00 00 00 00 00 00 01 FC 20 0B D3 CC AE CE 1E 74 67 D9 C2

C0 BD 9F 91 74 67 93 CB C0 D9 7D B6 E2 DB BD F9 AF 86 C1 E1 3E E8 28 90 44 01 2C 0C 09 89 40 00

01 78 02 FC B3 6A A7 0B 3E 9C FB 3A 2D 05 FB F9 F7 45 C4 33 32 30 BB FD ED B6 9F 73 7B 3B B9 E4

42 70 12 90 11 72 E5 02 24 1E C1 D0 C2 B4 27 12 B3 39 4D A5 D1 D8 BF 40 45 65 71 5D 38 34 D7 9F

3D 06 1D 76 15 99 99 B4 97 A5 60 2B 65 F7 FD FE 90 AD 60 02 85 FF EE 82 A4 22 4B 02 BD 0E 82 D5

56 69 14 56 29 CF C2 D0 45 FC DE 83 D2 28 9D F5 49 E6 66 D2 5E 95 90 A9 91 9D 9F A2 27 3B 21 E0

3D 04 2A 12 4A C2 17 B1 30 AD B0 69 25 2A 90 B5 73 1B 41 9F 9B 89 DC 71 35 D8 A1 52 79 D9 F4 97

E8 B0 15 2B AE 2C 15 CE C8 08 18 FF DC 85 42 52 95 82 57 70 2D 59 C6 D3 52 28 AE 12 B7 2D 3E 0F

71 DC E8 33 2D 5D B5 25 4A EE DD A4 BF 2B 30 2A 51 39 41 15 DB 00 06 BF F9 10 A8 89 4A 8B 08 95

DB 54 C6 AF 83 A4 A2 8A 89 53 87 C0 E7 77 7D E6 36 5D DB D6 61 52 AB D7 EC 17 AB B6 15 25 5C A0

8A AD 88 00

  
  
16th Animation Data \[at offset 0x00007C54\]

  
09 00 B4 01 04 00 00 FD BF 01 AA 00 00 00 C0 FB 00 15 FA EB 0E 0F 20 08 ED A7 18 40 2B 11 14 DF

CB 00 00 02 05 EF 18 0F 35 2F 00 0B 19 B6 EA D5 00 00 00 FF 02 00 B1 00 2E 3B 0C 1C 00 00 EE F6

1B C8 00 00 00 45 00 16 C0 05 0E 00 00 FE F9 00 D7 00 00 00 80 22 40 2D 82 CA D4 A8 9C EE DA 80

CF BF 45 C2 52 58 A2 D0 8B 34 DD 29 A2 DA CB 26 D5 8B 46 1D 59 73 16 52 4A B2 82 60 04 01 0A 01

04 07 5F 87 2D 86 F7 3F B3 B5 A4 1A 9E C3 6B A4 2C 61 4B B4 C0 DC 8D 4F 2B CC 6B 4C 7B 17 06 6C

E2 D1 73 03 69 8E 0B 32 97 2B F0 1F 01 DD D5 83 96 00 09 02 81 54 97 EB 95 51 4C E5 2A 33 AA A4

95 0A A5 31 5E 26 2D 82 99 05 71 14 93 A2 60 4C A8 BD 55 8B 40 00 23 D0 16 22 11 2B 12 AA 72 95

74 51 04 A5 16 27 40 A2 22 04 A4 05 04 40 01 32 22 89 00 0C AA 40 60 55 4D 9B 13 C0 89 D8 9C E5

81 44 C9 D7 2B 75 5A 12 CD CC AC AE 70 2C 4E 28 2F 52 02 DD 14 5A 28 A6 AB A0 07 FE 1F FE 22 06

96 7A 0D 5D AC 8D 54 ED E9 FA 0E AB 43 C0 DE BE 5D C8 D0 62 4F 4E 33 BB BD A6 49 BE C8 81 AF C1

DF EF 0C DA 34 00 68 3D 9B DA FA AF 80 F8 0D 2E 2E 6D F0 00 8F FE 56 17 17 EB CF B5 63 45 9F 3B

B5 F0 9C 0D 8C 5D 16 00 A2 F4 57 9C 2A EE FB DC 02 8B 16 97 16 B3 EB C1 33 77 DC 28 5C 6F 7E 4F

E5 30 8A 2B 96 88 00 3F FF 88 86 6B 3A 59 51 83 AA CA A7 3B 79 AC D2 C6 8F 5D 86 53 63 36 B6 FC

59 B5 56 29 7A D6 D9 9A DF FD 17 D6 EF 0C 0D 0E 24 0C D5 DB 13 D2 11 7E 90 00 00 00

  
  
17th Animation Data \[at offset 0x00007E10\]

  
09 00 52 01 04 00 00 FD B0 FF F8 00 00 00 C2 74 80 F3 00 00 09 FE 05 F1 ED C7 2F 00 F5 2D E5 A2

E6 00 00 0A 00 00 F1 13 39 2F 00 0B 2A 25 63 F2 00 00 00 F5 00 00 AA 02 35 05 BF 0E 00 00 0B 07

02 CD 80 80 00 3E FE 33 D9 12 18 00 00 FD 00 00 C3 80 80 00 78 79 12 2F 98 D4 59 BF 14 8A EF DF

BC 60 17 E5 58 A2 BA ED 02 49 33 B3 E6 0A C9 22 9C 1C 1B E0 80 00 14 10 41 49 72 75 D3 29 88 89

D6 58 29 8A 04 A7 14 80 85 AB 32 05 01 29 DE BD 48 24 00 04 83 88 2C 19 6A AC 4A 62 8A 6C 5A 2E

96 14 08 A6 9B E0 84 30 B0 A9 05 24 25 5D DB D6 01 20 00 18 10 47 C0 7C 05 83 36 8A E9 40 A2 CD

AB 46 79 4C 48 4E C5 17 40 43 03 02 40 A0 25 5D 75 D2 09 00 0E CF 22 8F 80 F8 0A CC 08 A2 69 09

53 62 C1 78 9A 04 E8 A2 A0 12 66 66 4C 15 04 58 B5 66 F8 20 00 76 78 12 2F 9A 08 B3 7E 28 13 BD

72 E1 86 5F 94 C5 35 57 80 09 28 66 66 D6 0A C9 27 63 0B 0A F8 26 00 02 01 88 2B 30 28 A6 B8 A0

57 7E F5 C3 0C AE 53 14 5F AB 00 04 2C 58 90 24 12 8B F7 E8 00 00 07 06 10 59 32 A7 7E CC AB 14

D8 B3 6C CF 2C C5 22 76 29 BA 08 43 07 06 80 52 42 55 DE BD 60 14 16 00

  
  
18th Animation Data \[at offset 0x00007F68\]

  
09 00 6F 01 04 00 00 FD BB 00 00 00 00 00 C0 F4 00 F9 00 00 F7 00 00 F6 EE C5 2F 00 F5 2E EA A9

ED 00 00 00 00 00 F6 12 3B 2F 00 0B 28 29 66 EB 00 00 00 F5 00 00 AA 00 35 13 CD 11 00 00 0B 07

02 D1 80 80 00 3E 00 2E D2 0C 1D 00 00 FD 00 00 C5 80 80 00 7F 80 2A 81 A3 31 8D 0A E0 CC E5 38

A0 34 2C 01 5F DC F4 77 C0 2D EF 77 94 1B 4B F5 E4 02 22 2E 17 6B 95 8F 80 F8 00 00 D8 02 48 1A

03 0C C6 9D C1 91 A1 D0 81 8D 46 00 DE 6D F7 15 00 47 D8 7D 7C 1B 7B B6 74 9F 01 F0 02 21 78 BD

39 62 00 00 00 00 00 00 00 00 00 00 00 00 00 02 6C 41 35 EA AF CA 9C 0B B3 86 93 45 66 A8 81 2A

EB AA E0 B5 7E BA 48 A2 A4 D1 AC E0 24 4F 37 53 21 35 DA A7 6C 88 48 00 17 5D 08 5D 9D E5 38 79

E9 D5 A4 D1 5B AA 53 14 55 55 77 05 AB B7 29 27 45 48 55 89 A0 A0 B1 5E 8E 42 19 F7 E7 80 42 52

00 05 57 42 6B 91 52 C6 15 C9 45 EC 4C 2B 75 4A 64 A5 55 F9 DC 16 2E 66 52 45 15 26 AA C5 B1 44

B1 42 6B D5 C5 B2 20 00 04 98 82 17 28 AA BA 30 33 E8 8B D6 EC E0 55 4C 12 95 77 E5 78 58 BF 9B

48 A2 A4 2F CA C4 C5 BA E0 41 35 04 24 00 04 59 02 17 69 AA 72 B7 72 99 DD B3 4E 04 B0 26 4A 55

DF A6 E8 A6 FE 5D 22 8A 90 AA 54 D6 30 B3 E6 21 29 A4 21 33

  
  
19th Animation Data \[at offset 0x000080DC\]

  
0E 00 4A 02 04 00 00 FD 5F 00 00 00 00 00 CD 80 80 E8 00 00 EC 00 00 E7 EA CE 2F 00 F5 2C F6 A2

F7 00 00 00 EB 00 E7 16 32 2F 00 0B 2F F3 31 D2 00 00 00 F5 00 03 B6 0C 34 FC B1 0F 00 00 0C 00

00 D5 00 00 03 4A F4 2B D1 18 21 00 00 04 00 00 D5 00 00 00 FF 84 80 0C 6A 15 C5 15 53 54 45 33

BB 7B 23 2F 34 4A 72 AD 21 7B 8A E2 22 BA 25 3B 14 D8 C7 A3 1F 1B 14 A6 AA A4 52 C9 CA CE CB C5

28 90 00 7F DA 40 06 9E 6B 72 9D 9A EC 59 A6 ED 18 36 F3 F3 2F 5C 22 88 B7 3A 06 76 9B 45 2A 67

14 55 4D 1A 69 E8 F4 7A 02 BB 36 60 A6 F6 EB 7B 55 CC 62 70 00 10 08 50 01 C8 1A B3 00 D3 D1 98

4A CD 34 6F 84 9A 8A F1 05 DB B7 AF 70 3D FD 9C 2D EC F1 39 2C CD 56 9F 18 02 79 BD 75 E8 9D 00

00 10 0E E0 01 A0 F8 0F 80 D5 18 E6 9E AC C2 30 6D 53 BF 10 D3 D9 C4 15 67 5F B3 AE D9 62 C6 DF

3A 5C 5E 5E 16 0C BE 03 E0 00 CE 9F 6B 04 C0 00 20 1D C0 02 65 84 70 09 58 9D 62 44 C1 4C A9 17

77 F8 B6 33 31 B3 F2 3B 98 4A AA 68 AC 02 11 52 00 00 10 0D 10 00 2A 4B 53 62 9A A8 A4 41 40 2B

8A C5 AB 76 2D EE B5 39 12 C9 25 62 B9 D2 00 45 84 80 00 0E 40 03 A1 33 CE EA AA AE D1 64 5C 00

B9 5D F1 77 67 F0 1A ED 9E A3 87 B5 EC 57 F2 FD 03 4B DD 77 B9 DF 01 F0 00 5F C5 E8 38 7C 5D 30

00 02 01 AA 00 24 67 9D 91 72 8B 02 EC A0 0B 91 50 C1 95 3B 62 69 A5 19 DF 7F D2 6F 40 09 5F F5

3F 58 00 00 7F EE 00 04 02 FD 76 02 15 D1 5C 80 02 FD B8 33 B0 64 85 51 58 00 5E 9D 81 00 00 FF

D7 80 09 02 CD 35 04 94 CE 98 00 15 57 6A C9 72 D4 D2 58 95 20 01 6A 8A 84 80 00 36 00 2C 17 8C

2C 0C 9B CA 54 53 A1 CE D0 C0 A1 79 31 5C AC D9 2B 57 12 BF 87 77 02 F9 30 44 59 D0 D3 BE 14 80

00 F4 00 59 2E 18 8D F5 D5 2B 14 E2 6A B9 5A C4 97 55 8B F4 D8 B2 45 73 4A FE 0F 09 CC 5C 27 10

13 B3 77 A0 FA 61 60 00 07 A0 02 D1 70 C0 B9 BC BA B0 A6 9D E6 3F 07 31 42 EA A1 7E 85 A2 75 CD

2B D9 BA BE 2E E9 30 22 D6 E3 41 7A 45 80 30 00

  
  
20th Animation Data \[at offset 0x0000832C\]

  
0C 00 4D 02 04 00 00 FE 28 00 82 00 00 00 C0 ED 00 F8 FE D8 07 0A 36 E8 F7 9B 2F 10 03 39 15 E5

E5 00 00 F9 0B EF 05 0B 16 2F 00 0B 14 AC EE E6 00 00 FD F5 0C 00 A3 00 33 F7 CE 25 00 00 D3 FC

19 D4 00 00 00 37 00 1A C5 03 1C 00 00 F6 FD 01 D5 00 00 00 01 80 3A 00 64 57 56 0C F0 37 D9 1D

6F 6B 4E EF 76 2E 53 16 2F 64 8C AB F8 79 E6 03 54 2E 6A B8 5D 11 9F AC EC 80 95 89 DD 2D 51 00

00 18 88 2A 17 61 44 A9 B9 7A AA E5 7A A9 13 A2 25 3B C9 CE A9 D3 04 96 55 21 6A 82 8B 19 50 2A

5F A2 8D 01 9B 2A E4 00 3D 2F 05 81 6E 49 C5 78 16 AC 53 16 AC 41 44 E5 14 5A 51 45 8A 2B 91 0B

EB 09 2F 4C 9D 58 D2 16 16 67 3C 83 0E 29 80 01 6F FE E8 1A 72 35 D2 8B B6 72 78 2C 1C 4C 1B 96

6A A8 A2 FD AC FC 0D 65 78 B8 9A 0B 77 6E 11 17 DA 74 62 D1 33 03 33 18 34 EC 0C B8 BC 51 25 40

02 B7 FD 78 35 0A 63 82 94 EE E8 2F 70 36 F4 FA 4B 98 51 51 66 FD AC C7 03 7F 0F 07 51 8D 87 9C

42 FB 50 9E 3D 13 30 6F 59 90 D4 30 B2 57 C1 78 00 59 FF B5 86 AD 4C B5 F2 9D DC 7B 3A A8 D6 EA

EE E0 AF 96 2B B1 7B 3F 80 BF 6E D5 1C CF 3F 70 89 5E 6A D3 C5 A2 66 15 74 06 AD 83 96 AC 82 A0

01 9F FF 3A 1A E5 14 68 51 7E D6 06 86 F6 8B 1E AB 32 BE 58 8A 17 B4 75 D3 46 6E 16 82 BF 80 F8

09 AF 35 C8 B6 A8 B5 58 35 CB 35 85 65 60 03 F3 80 70 48 8B D2 A2 27 5D EB F8 16 A8 8A 2F 12 94

E2 8B B4 CE 76 6E 65 5A F8 0F 80 9C AE 38 22 BA AF 14 57 01 C1 25 8F 55 82 E1 48 00 22 68 1C 3A

B9 EE 28 A6 9C EB 9B AA A9 A6 DD FB 37 84 AF D1 83 B6 B3 76 FB BA EB F1 89 D3 9E E1 CC EB D7 09

CE 61 C3 AA D7 CB 04 CD 2D 80 03 F0 04 D0 E2 15 CB 6F 2B 14 65 C6 EE BA 68 B7 18 30 4A 8B F6 ED

6D EC E6 E7 E5 64 EF B1 C8 A7 3D C4 29 DF E6 5D 27 2B 50 38 85 DD 3D 8C 12 E4 4A D0 01 00 61 80

5F 87 0E 89 6E 25 62 9C DB 3B 8A A9 95 8C 2D 26 BC 95 17 F0 5B 9A 72 B2 F1 37 3B 7C 62 54 E7 38

74 BE EF A3 B8 64 D3 C7 07 0E DB 77 D6 70 CC 5B B4 C8 00 00

  
  
21st Animation Data \[at offset 0x00008580\]

  
10 00 18 02 04 FF DF FD EF 00 BF 00 00 00 C0 F8 00 F9 00 EE 0E 08 1E EF F0 B4 16 41 2C 2A 25 F8

E7 00 00 FF 08 FD FE 11 2C 2F F5 02 24 B2 E5 E0 00 00 03 FC 02 00 AE 00 3C 49 03 22 00 00 D1 EC

20 D4 00 00 00 42 00 1F C1 09 33 00 00 EC F8 04 CE 00 00 63 51 80 47 86 01 2B 54 57 97 44 AC D1

11 7A CD 13 27 5E 15 74 59 5D BA 89 64 94 DB C5 60 2F 5E A3 34 D0 69 3B F0 C0 60 D9 B1 98 0B 63

2B 6A 90 17 63 12 D5 FD FC 55 8F A7 E8 3A AD 4F 5F F3 BB 42 9E FA 59 AB 6D 15 3A 7D 27 A8 E5 18

DC 16 D4 5A F9 0F 98 DC 98 16 22 40 D2 7B 3F AB 77 25 76 66 00 00 03 00 00 00 00 00 01 2A 29 02

40 95 73 09 40 00 00 02 02 40 00 00 00 00 25 20 00 20 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 FC 04 00 00 00 00 00 88 00 02 40 00 00 07 40 00 00 00 00 00 44 EB 02 01 14 D0 11 20 6C 45 FF

4B 02 C0 29 94 D6 ED EC FD 5B DA 35 C4 63 D5 4A 89 EE B2 F6 39 3D 97 00 5C CA B2 33 72 B2 ED 03

20 1B 3F 91 F9 FE 44 90 08 E0 0B 5F F8 40 29 05 28 5B B5 B9 BB 4E A4 B7 8D 14 C4 A7 BE CE DA 61

E7 EB 49 E5 D8 19 F1 5D A0 58 F8 0F 80 17 32 E3 3C A1 00 1C C5 38 24 24 89 C8 57 5D F4 58 25 2A

09 45 75 DF 92 C1 25 09 2F 44 0B B4 C5 62 4B D3 68 8C C4 80 08 43 B8 00 82 48 81 21 21 24 22 49

00 40 22 50 04 16 09 A4 1F DE 02 40 04 88 4A 42 04 08 49 28 40 04 81 28 90 12 2A 28 40 79 4F 32

08 10 95 10 29 A6 CA 55 11 13 22 54 D3 66 15 10 9A 16 A5 21 6E B9 52 21 6A 86 F8 C4 40 00 7F 09

0C F2 33 6B C0 D2 DF 67 5D E0 75 BA 5C C6 59 5D 19 F6 23 3E C6 87 1F 4B 55 57 4B F7 B3 D9 E9 61

E3 D0 6F AF 71 D8 7F 01 F0 0C F2 DD 01 39 00 00 10 80 CE 44 66 5D B3 A7 BF 46 5E 46 87 13 4F B4

DF 65 0B 19 B6 67 98 D3 E9 74 7B FD B5 C3 3E FD C6 71 8F 85 41 4C AC 86 71 81 48 57 40 00 00 00

  
  
22nd Animation Data \[at offset 0x000087A0\]

  
1E 00 D2 03 04 FF DD FE 0D 00 23 00 00 00 C0 F2 00 F8 FF EB 0E 0C 25 ED F0 B1 1C 3C 28 37 1F ED

E7 00 00 05 08 E9 FE 10 28 2F FB FD 37 D5 17 FA 06 F6 F3 F8 E7 00 A8 00 2E DF AC 11 00 00 D9 FF

27 D4 00 00 00 3C 00 17 C0 06 37 00 00 E5 FC FB D5 00 00 5D 65 35 0B 48 95 12 9D C2 8B 17 AF D1

5D 52 28 95 F8 94 A7 56 56 FB 59 C5 E0 59 AB 3A FD 4B 4A 6C E0 48 51 9B 21 69 62 89 60 15 DA CD

0B CC D0 06 30 B4 28 A2 77 0A 2C 5E BF 45 FB B4 14 AF CE 54 4E 79 9B AC BC 2C 2A 6B CE AA 16 94

E0 E2 4C B3 6B 24 2D 31 70 6D 67 96 29 CF 0C 2D 10 07 70 C1 44 A9 95 79 92 95 8A 72 B3 25 BC DC

D2 42 53 95 15 32 77 F9 D6 2E 6A 34 55 4A A6 0A 8C 5D 0D 45 BA 33 43 05 8D AB D4 EF 8B 4B C1 DD

EE 00 F8 1A 95 74 60 B3 FB D3 0A FF 75 B0 AB AB E8 ED 99 F9 FC 05 EA 6D E7 68 F6 94 70 D9 1D BF

AE FB FF 07 2B AD 4A 31 31 45 0B A1 A9 4F 86 E4 3B C2 52 BC 00 00 00 00 00 00 00 00 00 00 00 00

1F C0 02 82 94 92 45 FA 22 51 5C E2 27 21 14 94 2C 57 39 45 54 66 A7 35 29 57 13 25 14 85 2A 37

D9 36 CA E5 20 FC 00 02 19 E9 4A FC 51 A0 8A 2F 12 92 40 8A 57 EF E4 E3 62 E2 2F E0 E9 34 7A AB

4C F4 63 59 A0 26 19 E8 D2 E2 D6 4A 55 87 E0 17 F0 CC 50 BA A3 45 3A 2E CA 44 81 28 B2 BE DC E3

68 74 17 EA F8 6F 80 BB C0 70 6C C4 68 2C 50 44 AB 0C C5 7A 6C 5B E5 12 A8 00 02 BF 06 52 52 BD

14 E2 A8 BA 94 84 02 C4 5F B3 BF B5 89 99 D8 67 76 3A EB BB 98 65 27 A0 94 84 50 19 46 35 80 A2

A0 02 0A FA 19 29 45 D9 D3 83 14 5C 04 81 14 C5 FA 2E D1 5E D3 67 A0 E0 36 93 CA 93 25 1A 19 50

22 80 C9 46 3D 89 0A 2A 00 00 4F A1 70 55 39 60 4E 8B E9 00 14 45 FA 2E B2 A7 A3 D2 5F CD 8B 37

97 11 82 90 50 17 0B 74 04 A6 00 00 5F C0 85 62 15 80 02 75 8D FE E3 7B 9C 37 98 00 02 00 00 00

17 F0 00 A1 11 31 34 C0 02 22 63 6D 9B 81 9C 05 05 60 02 82 70 10 00 0F E0 01 4A 69 89 CA 00 02

13 19 3A 1D 25 A0 29 4A A4 04 05 25 50 0A 00 03 F0 00 59 4D 31 5A 60 01 38 98 BB AD 9D A0 2C 97

C1 28 0B 29 55 01 12 00 0F E0 01 65 34 09 CA 00 02 13 15 68 72 71 40 B2 95 E4 00 2C 97 E6 21 40

00 7E 00 0B 09 A6 27 29 80 04 E2 61 44 48 0B 05 F0 20 2C 17 E0 22 40 01 FC 00 2C 27 28 13 40 00

42 61 39 40 16 0B E0 94 05 82 A9 82 40 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 0B 75 DB 9D

2B 77 ED 80 05 86 05 3A 27 2F BC C7 CA 00 00 00 00 00 00 00 00 59 8B 42 DC EC 80 05 32 B6 30 A8

97 02 69 F0 AC 80 00 00 00 FA FC 12 04 81 28 27 04 48 12 48 4A 80 A6 54 09 44 EB 28 8A 00 A2 BA

E9 20 0F E0 00 20 00 48 00 00 02 52 90 42 00 00 10 00 00 00 00 00 00 00 00 00 00 00 00 00 10 07

F0 00 20 00 00 02 22 02 49 00 00 24 00 30 27 70 20 11 22 89 12 80 42 04 4C 2B 89 88 95 14 93 94

C0 9D 34 D6 48 05 63 FF F8 00 BC 29 4A C2 76 2D 69 B4 56 34 7A 8C C1 45 F8 53 6A D6 16 0E F6 BA

8B 95 5C 5E 51 5C B1 8C AA F4 21 79 2F A2 FA BC 42 75 63 03 52 4F FB 40 5E 44 53 29 53 29 D8 AB

5B A9 8E 57 9A CD 25 45 E8 53 67 1B 45 83 B4 CB BC 67 4A E2 F2 9D DE 4E 09 77 6F C3 05 E6 E7 73

97 8C 45 ED 08 33 25 FF B4 85 D2 2C 4A 8B 12 9D 39 9A 1C 6B D8 5A 0C 02 8A 2F 4D 4B 47 A6 A7 BD

DD 5F 33 E9 CF 5D 65 74 FD 66 E4 C0 D1 20 5D 5F B1 67 18 A7 3F 46 2D 00

  
  
23rd Animation Data \[at offset 0x00008B78\]

  
06 00 29 01 04 00 00 FE 25 FC 9F 07 00 00 C0 EE 00 04 05 2D 04 F9 E6 11 F8 EA 1A 29 11 FA 1C DB

C9 80 80 02 05 F7 F2 09 6B 1F 22 28 15 08 3C C6 00 00 F5 F4 F4 00 A4 00 23 50 F5 36 00 00 CE 11

F8 D3 00 00 00 38 00 21 D2 0E 33 80 80 E2 03 F0 D1 00 00 00 3A FF 57 84 2D 5A CE 95 8C 6A 68 CC

D2 64 D5 9B 8F AC E3 7E 03 E0 25 2D E6 06 16 7E FB 12 D6 87 02 9C 23 0E 5A 84 25 F2 DF 31 D5 13

A5 21 0D F5 DC FB 05 C5 9A C2 E5 E8 06 E5 F1 BF 46 7E DF 0A 35 D9 B9 DB 9D AF DD F4 DA 7C 9E DF

67 F0 1F 01 5D 5A 4B 51 B9 AA 89 5C CD 97 04 17 1B F4 73 FE B9 CB 96 AF 4E 43 7E A7 4F 2C AF 80

F8 0D 25 58 18 00 A3 AC 01 7A 62 EA 73 CE B1 63 1A F4 EE 61 5B B1 A6 DA 65 6E 84 F0 69 8C E8 92

BB EC 60 A9 75 5C B1 AC 13 56 17 5A 0C 4A 3B 73 57 2A 60 04 0A 14 08 22 EA 54 57 2B D2 28 BB 54

82 54 AF 08 84 80 84 29 A4 9D 15 84 12 8A CA 49 00 21 E0 C0 17 88 9C AF 4E 21 38 B2 0A 25 7C 08

00 84 A5 F0 1F 01 14 5F 90 26 52 44 24 25 00 00

  
  
24th Animation Data \[at offset 0x00008CA8\]

  
30 1A 00 00

  
  
25th Animation Data \[at offset 0x00008CAC\]

  
06 00 0D 01 04 00 00 FE 4F 01 20 00 00 00 C4 49 C0 FB FC FA 15 FD FF F5 EB BE 1D 3C 29 23 32 FC

D9 00 00 FF F9 07 FA 0E 37 2E E7 F4 02 CA 17 EA 00 00 20 E6 D2 FC BF 01 20 45 0C 3B 80 80 DC DF

40 D5 00 00 04 53 01 2A DB 17 23 80 80 E2 F9 02 D5 00 00 00 34 80 6E 8B 1A D5 89 68 72 F2 BB 4C

36 35 8A AB CE C0 A7 2C C3 D9 53 5C 68 6F EF 77 F9 53 D3 5D 2B BB 87 56 B6 59 1B 6A E9 F8 0F 80

C4 C5 DD 0B 1A D9 6D E5 44 8C EA 26 00 0A 20 15 C2 9D 42 9A 31 32 6C 6C F0 29 C2 C2 C9 CC BD 6A

59 E4 B2 F5 93 8C 5B F9 D7 6F 67 EA EF 14 5E C2 AF 51 2C 5D 96 FF AD 38 7D 46 CC 53 A8 96 44 B2

70 4C FB 57 80 00 B8 B0 95 22 89 CA A9 28 94 E7 04 CA A8 9A 28 84 22 C0 5B B4 A5 2B F7 EE 96 65

30 A5 39 D7 7C AE 89 80 00 40 40 02 50 10 00 80 82 10 25 21 28 88 24 80 92 08 22 50 00 1F 1F 00

08 90 48 01 20 91 24 84 40 89 4A 44 24 10 91 22 51 20 00 00

  
  
26th Animation Data \[at offset 0x00008DC0\]

  
06 00 59 01 04 00 00 FE AB 02 AB 00 00 00 CB 7E C0 02 FF 17 F9 F3 B6 08 EE D6 2B 29 1A 13 40 00

C3 00 00 0B CE 26 F5 0C 55 24 CA DC EE BF 48 DD 00 00 1F D9 E7 F5 F4 03 1D 0D F8 0B 00 00 0F 04

0D D5 00 00 0B 88 03 01 DD 0A 2D 80 80 CF 01 FA D5 00 00 00 72 FF DE 08 CE 44 55 66 BC 2A E7 54

51 45 13 52 57 A3 B9 25 FA 29 A2 56 33 A8 22 8A A5 9D 19 78 D8 FC 29 B8 DF 62 08 CF 8B 11 81 7C

B1 5D 20 01 9B FF 2C 27 94 9C 5C C2 8D 1D F8 BD 5D AB 36 2A 8B 44 B4 37 A5 2B 94 DB B3 66 CE FE

C1 16 2F 51 94 68 28 C6 32 6F 68 44 F2 58 8B 75 16 6B A4 00 26 7F C8 C5 5B 35 51 BF C5 C6 E3 33

59 59 D8 78 16 6E 4F 14 A2 8C AA 65 BF B3 A3 D0 E3 51 BA B6 53 6F 36 C6 CE 34 1A AA 6B F8 0F 80

CC CB D3 0A B6 71 A9 89 C1 85 3A 00 03 47 FD 80 4F 21 39 67 57 87 AB BF 46 7D 74 D1 A1 CF BD 6C

BF 81 97 4C B3 A5 8F 8D A9 CF CF B0 66 69 31 68 C8 8D 67 6F DC E7 7C 07 C0 66 5C C5 82 79 11 DF

EC F7 D8 7F 01 F0 16 92 00 0E 5F F8 01 3F B4 F4 08 95 DB D6 74 55 53 76 72 5A CF BB 64 AF 0B 2A

85 D6 16 0E 2E EB B4 A4 DC 59 C5 A3 31 BD E8 BA 1E FC C2 E2 36 82 79 8C 6A 25 78 B1 12 13 00 00

  
  
27th Animation Data \[at offset 0x00008F20\]

  
02 00 7D 00 04 00 19 FE 4A 00 70 00 00 00 C0 ED 00 FF FB 0A 0F 05 0A 00 E9 CB 15 42 2D 20 1C D3

CF 00 00 02 06 00 F7 0C 47 2F 00 0B 36 08 47 D3 80 80 FA F8 EC 00 A3 00 2C EA B1 20 00 00 C9 1B

FF D4 00 00 00 37 00 11 C6 07 2F 00 00 EB F8 04 D5 00 00 1A 26 80 38 01 6F 03 80 B9 97 DE 68 F1

75 94 CE 7B 3D 0C EC 92 68 67 5F 04 36 17 B6 9A D3 82 E1 77 62 8C 7C 6D 01 85 C9 FD 88 17 ED 2D

00 00 00 00

  
  
28th Animation Data \[at offset 0x00008FA4\]

  
05 00 B5 00 04 00 00 FE 1D FD 82 00 00 00 C0 ED 00 06 03 2A 07 F8 E6 13 F6 E7 1F 3B 28 F7 14 D5

C7 00 00 FB 02 11 F5 09 69 2F 00 0B F9 DB 23 C0 80 80 EE 04 D4 00 A3 00 04 5F FC 21 80 80 09 07

04 D4 00 00 00 37 00 1C 47 8B 02 00 00 08 F5 F0 D5 00 00 00 00 79 02 48 04 00 20 92 00 00 44 95

14 00 4C A8 94 40 00 00 79 80 24 04 20 00 48 00 00 95 45 09 01 32 F9 40 00 00 03 A4 08 89 02 84

80 48 88 90 00 09 44 60 15 20 0B 06 09 5C A4 00 01 60 0F D6 C1 7F 3F 10 4E AC 6B B6 69 03 02 C2

F6 56 20 00 0C 7B 95 E4 FC 07 C0 6C AA 90 1A 6F AF FA 6E 4B E0 3E 03 6F 87 31 00 00

  
  
29th Animation Data \[at offset 0x00009060\]

  
03 00 C3 00 04 00 00 FE 7E FB 52 00 E5 00 C0 05 00 1C 0B C0 07 03 3D 0B 0E 83 2F 0F 03 22 20 C9

D2 00 00 0F 0A 0A 2D 13 06 0F BB D2 21 FA 4D E1 00 00 0B 19 87 00 BB 00 1A FE D1 2B 00 00 E5 16

1F D1 00 00 00 4F 00 0F D9 17 3B 00 00 E4 DF 18 D5 00 00 00 FF 81 C0 5D AE 62 D2 C8 6F E3 43 3B

75 6F AE E3 32 72 B4 FC 17 1A 2F 66 EC 37 96 31 F4 DA 2C 3D 07 4D F7 D8 46 EB 2F 8D 64 34 78 F3

DD 1A 2B D9 34 0C 84 EB B9 67 E0 3E 03 13 49 BD 00 05 90 18 9C FC 6A D9 2C DC EC 75 AA AE 6F F4

42 AD 6F 12 33 E5 B4 C9 B9 89 85 C9 F1 DB DD A6 C3 08 AB 3B 8E 64 B4 7C EF 23 BB 30 F2 32 28 19

2A EB BD 7C D1 62 DF 00

  
  
30th Animation Data \[at offset 0x00009128\]

  
04 00 CD 00 04 00 00 FD C5 FF FA EF 00 00 C0 E6 00 00 00 E0 05 10 35 F1 F6 A3 2F 00 F5 35 5F 1F

D2 00 00 00 00 CE 0A 0F 21 2F 00 0B 1E A4 EB F5 00 00 F1 02 E2 00 9C 00 40 4A 00 00 00 00 FA 00

00 D5 00 00 00 30 00 0A D3 09 3B 80 80 02 00 00 D5 00 00 00 80 35 03 68 45 B5 89 E0 CF 33 36 DD

FC 0D CF A0 72 DB FE AF BB D1 94 DA E0 4C 31 7F 4D 45 46 1D 78 4B 6D EF 45 D7 F1 47 71 C8 77 B0

2D B1 77 B5 EF 7E 03 E0 37 57 2C 00 06 F7 29 09 2F A5 62 95 F8 A2 BA 25 6A FD 54 11 2A 6F A6 2D

55 7C 49 24 95 77 1B 4D B9 83 B2 E6 42 49 13 00 00 0B 0E 81 0B A8 B3 6A 8B A9 53 38 C3 BF 7A 64

A2 BB CA 86 0E 75 E1 08 41 7B 2E 08 DE EA C2 10 50 01 00 00

  
  
31st Animation Data \[at offset 0x000091FC\]

  
06 00 30 01 04 00 00 FE 25 FC 9F 08 00 00 C0 ED 00 06 03 2A 07 F8 E6 13 F6 E7 27 31 21 07 44 D3

CE 00 00 15 00 E9 F5 09 69 2F 00 F7 40 57 75 EC 80 80 2D CC 9D 00 A3 00 23 51 F5 35 00 00 CD 17

F1 D4 00 00 00 37 00 0F D5 18 2B 80 80 EF 00 EE DA 00 00 00 3A FF 57 C0 2F 55 B0 8C 1E 1B 7B 73

69 6F 73 BC AA 5C 27 10 6F AD 5E A6 DF 7C 69 3E FB D9 7E AF 49 F0 1F 01 D3 F2 3A 91 2F 95 F9 8E

AC 8A ED 81 9B 95 9B 82 0B E0 00 F8 25 DD A9 A8 6B 31 3E DA 54 72 38 7C 07 DC 4B 37 3B 5F DD F6

5D E1 89 63 87 E5 69 FB FD 87 DD F4 FC 1F 3D C6 EC 4D 3E B3 B1 6A 19 DA 8F 44 E2 CD 4D 1C 3D 63

50 C3 D1 61 5B F8 0F 80 CD EF F8 A0 62 34 DC AC A5 6F 2F 7F 0C 1C 0B F9 8B F7 F3 B4 18 7A 21 2D

CD BE FB BC AA E4 F2 25 67 00 C4 CC CF 52 AE EC E0 95 8A 02 95 76 E8 91 62 BB 20 20 15 F5 12 12

AE A2 8A 22 62 28 A2 91 2A 97 2E 44 27 12 A0 A2 B9 84 40 4A 40 24 04 83 C3 D8 1A 50 22 9B 04 E7

2A 04 A7 3A C4 58 60 60 4A 4A 25 13 27 4D 01 29 04 40 08 02 02 00 00 00

  
  
32nd Animation Data \[at offset 0x00009334\]

  
1F 00 E7 04 04 FF A5 FD EF 01 0D 00 00 00 C0 B7 40 FD 00 E4 0A 09 27 EF F4 A7 2B 29 1A 2A 3A F4

EB 00 00 00 03 F9 06 10 23 2F 00 0B 1E AB E2 F0 00 00 00 05 F8 00 AD 00 31 49 FA 2A 00 00 D4 F2

21 D5 00 00 00 41 00 1D BA 03 35 00 00 E7 FC 02 D5 00 00 1F 53 80 6C 07 A4 F4 16 13 9D 77 2C 4A

BB 1D BF 77 73 45 2B 02 BB 76 01 7A 25 32 8B 38 2C 14 E5 6B 62 6B 71 BB F0 C1 58 AA BC 22 C5 89

80 D0 B8 02 18 97 A3 F4 09 DA 94 64 4A AB 71 5D 68 BD 59 42 FD 71 68 4A 52 BC 52 AA 2D AB 9A B2

DC E8 91 2B 69 D9 B5 57 C0 7C 04 E4 00 E3 04 62 56 D1 18 34 46 45 35 E0 4A DD B5 DC FA 89 45 EA

98 02 C4 A5 74 A6 BB 91 6D 5D 53 91 44 AC 89 5B 55 81 6A 65 48 00 23 25 A8 4B 06 71 2C 09 55 91

44 60 B0 B0 22 E6 7D 45 05 52 B6 29 92 E1 13 B9 16 E5 17 67 32 C4 58 12 B7 29 E1 53 41 50 1F 86

CB 90 96 14 E2 58 31 7F 26 86 04 61 E1 D7 9F 9F 7C 92 57 D6 C5 32 5D 2B 5D 8C 04 EE CE B2 D2 91

2C 05 78 76 28 2F C8 1F C6 8A 10 A2 D4 A6 C1 AA 79 74 B0 63 0B 06 FD EB B5 14 28 BF 18 02 C5 34

DC 26 B9 16 E5 17 67 05 89 50 28 B6 9E 1D 34 7C 07 C0 56 00 11 41 B5 24 A9 86 15 71 9B 4C B0 A7

66 C5 EA EA BC 53 14 5F 9E 10 B1 6B 0A F1 14 67 45 84 EE D7 22 54 53 02 C4 A7 81 2A 89 C0 04 BD

BB 31 0D FE 39 8D 34 EC D3 8B 2A AB CE A6 33 CB 49 5F AB 18 57 A4 E0 2B 29 A3 21 3A EB BF 7F 04

CF B1 40 89 CA 72 5D 2D DF A0 06 BE 30 34 46 C7 4F 12 D0 22 8A 6D 68 28 CE CE CE A2 8C E2 DA 55

DD D1 0D FD 8D 08 B7 2D E4 AE 57 55 77 F1 8C 9B 30 2B B9 4C EA 8C E3 0A F8 07 93 B2 34 4A 36 FA

08 8D 04 94 CA D6 82 59 59 97 2F 53 6F E0 3E 02 DC A8 67 E9 06 FD 87 23 0A 37 B2 B9 5D F8 AF 1C

C9 C2 CE 13 B9 44 57 3C F3 0E ED 60 30 A9 A1 A0 53 91 83 0C 62 C2 CE 33 33 36 F5 CA 70 4B 52 A2

8B D8 E3 22 AB 43 06 F6 FA 57 2B BE 9E 29 73 43 BD 13 B9 4C 55 17 0B 77 6F 87 C0 00 94 84 22 44

42 51 04 80 22 88 94 88 91 10 12 89 C0 50 10 4E 04 50 90 00 00 00 00 00 00 00 00 00 00 00 00 B8

D9 FF 49 7D 03 3F D9 BA 2B 57 3E D7 4B 3D 06 66 CB ED AF 72 1C 5E 33 77 99 F0 1F 01 BD A6 9C 6D

2F D6 CF B9 EF 79 9D 56 7D 1F 01 F0 1B 8D 17 0F 2E 1F 0A BD 2E B6 C7 C0 7C 05 7D F5 98 2C 71 19

BA 1D 56 AF 80 36 19 D2 CF 00 04 19 57 91 C0 EC 71 A8 FB AC FD 27 33 5E 9F EE 6D 6F B2 30 F7 D6

9F 01 F0 15 D8 B1 C2 E7 74 19 1B 9D EF 79 2D 1E 17 C0 7C 06 13 7D 2A 24 94 5F 2F D7 28 22 88 A3

06 DD 45 57 E9 B0 3D 80 32 B0 91 F3 BE BF 85 99 D6 DC BD C3 69 EC F6 D2 D9 ED 75 38 17 EC FC 07

C0 29 A5 DD FD F6 5D CA B5 14 51 A2 2A B3 7E 55 45 11 5C 15 D8 81 15 4A 74 CB 3C A2 BA 2C 00 00

0F A9 1B 2D 6A BB C5 8A 6B BF 15 D7 4C A2 80 57 55 E9 C2 99 4A 82 25 08 08 00 40 04 24 3F BF BF

80 88 24 40 00 22 00 90 00 00 01 00 00 20 20 41 44 28 A0 9C 4A 84 A5 09 01 2A 28 91 04 08 90 00

00 24 00 00 00 02 83 02 E2 8A 49 C4 A9 4A 51 08 04 A8 B0 92 22 20 09 04 80 12 00 90 00 00 00 86

93 78 50 44 4A 52 94 A0 80 4A 52 91 04 12 00 00 00 04 00 00 00 00 00 00 00 00 00 00 00 00 01 8A

8A 88 36 EC 8D 7F A1 CA 37 1B 4B 7C D4 44 44 82 46 7F 3D EA 71 08 48 49 0D BA DE 9A 56 C9 20 36

EC 0D 46 9E E1 3D 15 13 02 93 92 52 36 CB F7 79 B4 F6 F8 BB BE 6A 52 94 A0 20 DA 4F 96 94 92 40

84 9B 66 0E 96 87 C0 7C 02 24 1B 64 B8 1D 66 71 77 40 AC 76 5A 41 59 33 D4 4E CD 12 95 88 B0 D1

E8 B0 EF D8 B2 4E 77 95 D9 C1 B3 46 04 AE D2 66 DF C2 67 B0 73 AF 67 14 DE C5 0C F6 2D BC 1B 85

8C 4C F9 81 62 1F F3 66 29 79 7A FE EA 9B 5A 1C AB FB FC EE 07 5B 6E 5A 5C 42 F5 79 96 27 BA D1

E9 F4 58 3D 9F 49 80 67 EF B8 65 E6 07 D0 7D AE F0 AD AC 90 BC DC FC 3F C6 58 38 CC FD 35 80 54

41 49 64 AD 5B 36 29 C0 BB 46 75 CC 0B 32 B7 A0 B4 57 2B F4 33 6C 69 F4 B7 72 B7 94 94 D7 A4 56

BB BE CF B8 58 60 05 6B B7 EC E8 0B F5 55 40 00 04 EE A0 22 55 A5 4C E5 5C E8 92 8B 32 09 95 30

6D CE 75 C8 92 D0 8A E2 B2 89 48 05 72 A4 BF 13 90 F8 00 FC 91 02 69 4A 69 C4 A4 A2 99 10 89 26

B1 66 69 82 C2 10 94 14 24 10 94 E4 2A 89 87 D0 07 E4 82 13 4A 88 94 E7 24 4A 99 04 13 59 B1 08

91 25 22 21 05 12 01 29 D1 05 49 81

  
  
33rd Animation Data \[at offset 0x00009820\]

  
19 00 8E 03 04 00 00 FD F2 FC 51 00 00 00 C0 F1 00 F5 FD 0F 17 00 00 F8 EB D4 0E 08 FB DE 1B 1F

D9 00 00 00 00 00 EC 0D 48 0E F8 05 DF E6 E0 CF 00 00 00 F5 00 00 A7 00 2A 33 EF 2C 00 00 EC 07

FD C3 80 80 00 3B 00 22 D0 04 1A 00 00 F0 00 00 D5 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

80 3D 7F C7 86 A7 1D 85 4E 4C CA 69 DF 6B B5 DA DF 48 E1 76 3C 38 31 EC E7 6A 3B 6E EB D0 3B AE

03 91 2B D2 64 5E D0 ED E3 21 32 9D 26 7E 39 7B 17 53 B9 66 F0 3F 01 F0 1B 2E C3 9B 00 03 6D 62

9A 04 C4 4A 25 83 83 2A AB 11 4D 12 4E D5 10 88 15 CE DA 8A D3 09 51 14 0A 29 AE 85 E2 9C CC 40

00 08 FA 24 08 08 4A 84 40 48 24 80 11 42 44 00 00 04 E8 00 0F 80 62 01 20 92 26 94 82 02 12 01

29 A0 90 00 00 51 30 00 CA 2A 2B 98 A0 4A 25 19 F9 F1 62 91 2A E7 0A 2F 4E 49 48 53 45 D4 E9 50

11 39 4C 4E BA 66 B4 57 89 98 00 00 9C 45 14 2B 8A 13 BF 0B 13 C1 C0 C0 C0 C3 CB 2A DB E7 D7 12

AA FD FB 38 58 12 37 7B EC A5 11 44 4E 65 12 8A 45 12 89 20 55 60 00 3F 07 89 CD 54 A6 A2 CD F4

51 9F 72 D5 9A 37 C6 76 66 75 72 AA FD FA E7 85 81 06 EA 79 A9 CA 72 A2 82 71 2A C4 E2 50 90 B1

50 00 4C 80 64 8D BE E1 46 1E D3 3B 07 99 CF D0 EC FB DF BA EC F6 16 BB AD 81 C8 6B 77 98 D8 3B

7B F5 4F BE 8C 8B A7 0D BE DE 5A DB 6A 72 2A C5 D1 FC 07 C0 6F F6 9A 6B DF 01 F0 16 B7 5B 7C 6B

FA 5B 9F 01 F0 18 7C 07 64 00 1E 86 85 3E FB F0 12 95 50 B6 A6 AB D7 A8 BF 62 2C 7C 07 C0 5B BB

76 85 70 8A A8 98 A2 BB D2 AE 9A 65 45 1F 01 F0 0B F6 60 95 75 D3 4D 8A CB 16 2A 00 0F E0 82 50

4A 09 08 89 24 91 44 4C 01 02 21 12 92 41 12 08 82 50 10 00 00 5F 04 48 89 10 25 28 42 09 CA 80

04 84 A4 94 42 02 50 12 91 12 09 00 00 66 61 5F C1 FC 04 45 89 2E AB B1 6A D4 EC D5 2A BE 03 E0

2E DB B7 35 32 4A C4 E8 13 A6 D4 53 5D 71 39 FC 07 C0 2C DF 91 14 D3 5D 75 52 55 55 80 00 0C FA

10 A2 20 A2 88 9E 05 17 A2 CE 16 29 BC D3 F0 94 4C 44 EA 81 A0 9F 0C 84 E1 00 90 84 42 92 2B A0

00 02 80 81 4C E7 0A 68 4F 01 7A F5 9C 1C 73 77 9B C2 53 10 2B BE 1A 1D 17 22 80 99 09 04 20 A0

88 90 00 75 02 09 11 4C 97 E5 5D 38 51 55 F9 58 C5 30 37 FC 1C 45 24 A2 A0 CF D5 71 8A 14 49 49

24 40 A1 44 97 CA 2C 56 00 3F F3 80 C1 A0 5E BD AE B3 9F D9 DA CC D7 E0 E8 F1 F0 6E D1 49 18 15

6F EA D4 D8 A6 58 34 51 49 99 87 75 A0 68 A7 7B 79 F0 1F 01 8B 63 36 E8 D0 34 6C CE D8 D5 68 32

C0 01 78 50 70 2D 04 F9 AC CB BF 51 C1 E0 F2 95 73 5C AE 6E 4C AC 94 63 DC 96 E7 9E B7 6E CE 5D

8A AC 16 B4 95 B8 15 9B F9 76 49 59 AE CF C0 7C 03 81 66 77 F1 A0 2A 00 03 BB 8D 03 05 45 16 E7

2C FA 6D 60 4E C5 33 80 95 0A 56 E4 4E 51 21 44 98 29 66 D5 51 5C A2 B1 82 67 C5 64 00 00 00 00

08 89 C9 4C 4E 72 9C E2 49 10 A2 13 9C 42 41 5C A4 00 00 00 00 00 00 00 00 00 01 20 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 10 00 00 00 00 00 00 00 00 00 25 2A 21

5C A8 A2 28 A2 50 82 49 C9 45 12 92 02 98 80 00 00 00 0A 00

  
  
34th Animation Data \[at offset 0x00009BB4\]

  
14 00 D4 02 04 00 00 FE 3A FD 2A 00 00 00 C0 ED 00 16 08 39 07 F8 DB 26 FD F3 18 40 2B DE 39 C5

DB 00 00 0E 1D 00 04 07 78 1A F9 06 20 C5 E9 E5 80 80 F5 0A DC 00 A3 00 16 54 01 32 00 00 E7 00

00 CF 00 00 00 37 00 2F CF 0A 3A 80 80 E9 01 01 C1 80 80 00 80 2F 7F EF 40 89 C0 89 C0 8B 15 89

67 E7 22 05 CC 9D FD 25 57 30 C6 75 35 CB E0 3E 03 74 5A 06 27 33 CC 53 F0 1F 01 BE 8A 74 80 00

63 A8 12 A2 42 54 48 00 12 90 00 01 59 00 11 87 85 22 60 00 00 00 00 00 00 00 00 00 00 00 00 00

6D 00 00 00 06 21 BF D4 6D 84 F6 5B EB 56 AC 0D BD AC 51 41 60 90 04 A7 3A CB 12 48 00 FF 8A FF

CE 86 1E 8D D8 5C E9 F4 18 1C 2F DF EF 3B CC EE A3 B0 97 7D EB B9 45 1D A7 09 B1 D0 7D CE 76 B7

43 D0 F1 56 36 FF 01 F0 1C 46 F7 12 BD 1E 6F 19 B6 A7 AC F8 0F 80 E3 68 AB 7B F0 1F 01 5E 8F 0E

3A CE E3 2C D1 45 51 F0 1F 00 01 FC 43 FF C2 8B A4 C1 09 00 04 20 00 28 5B 97 7B DA 70 66 82 D6

06 8F E0 3E 02 85 DD 8F 7F B7 C4 F8 0F 80 E1 40 01 FF 96 74 10 09 10 04 48 08 04 4A 00 25 17 EF

D8 28 94 A9 08 AE 13 2C 00 01 2D F8 08 04 44 A2 11 5D 30 08 94 45 12 4A 26 20 25 3A 84 8A 01 28

81 4C 40 00 79 03 10 40 11 28 22 74 C0 42 51 12 45 13 82 22 44 93 98 94 01 12 84 89 00 00 78 18

08 04 08 22 40 40 90 80 80 13 21 10 0A 25 29 10 00 03 B0 51 22 40 94 92 92 52 80 25 04 11 29 09

08 53 62 64 10 12 94 92 2B 00 04 01 34 00 48 A0 82 89 4E 52 4A D5 DA 02 54 45 14 57 14 57 62 82

54 41 0B 56 C4 CA C2 53 92 0A A5 20 01 02 50 6A 18 66 AC BC 6A 2C E5 68 34 DA 0E 0F 55 B1 D2 06

06 A2 FE 36 17 71 B5 D3 6F B5 5A 93 07 49 3A E5 9B 9F 83 A6 B0 6F B0 2F EF 0A E3 0F 75 85 7F 2C

EE 63 0C 00 40 92 86 C5 ED 8B 4B AF D7 5B C2 C4 D7 EB 74 5A C9 DA C5 D2 E4 E8 C9 2F E0 E9 F8 2D

37 39 C6 61 6C 2B D5 96 2A A6 8D 85 BC CD C7 57 9A 76 9C C7 59 A4 28 D9 5D D2 E9 EB B6 77 78 7B

20 01 00 45 04 11 7C 00 16 27 00 01 62 02 30 A8 5F 95 78 54 E8 0B 1A 5D C0 5F 8A AD D3 98 58 F9

5F 6D 00 0E 80 01 24 E7 02 B8 0A 22 00 9C E0 51 10 09 24 4E 2B 22 74 84 A5 28 8A 09 CA 60 01 B9

F8 24 9C E0 4E 72 14 C2 61 62 71 02 80 2B 84 A2 53 8A 88 BF 68 24 94 D4 93 B5 78 00 36 3F 84 93

98 4E 02 92 61 66 73 81 44 04 AB 85 09 56 BE 45 EB 61 24 A7 16 0A F9 2E B4 00 36 BF 89 50 9C 40

9C 48 53 0A C2 CC 44 0A 12 0A A1 24 AB 8A 88 B9 80 14 25 38 A4 A7 92 EB 80 00 00 00

  
  
35th Animation Data \[at offset 0x00009E90\]

  
0A 00 8E 01 04 00 00 FE 7E FB 52 00 E5 00 C0 05 00 1C 0B C0 07 03 3D 0B 0E 83 2F 00 F5 2C 15 BF

D2 00 00 0F 0A 0A 2D 13 06 0F BB D2 14 F5 37 E1 00 00 08 CF C3 00 BB 00 1A FE D1 2B 00 00 E5 16

1F D1 00 00 00 4F 00 0F D9 17 3B 00 00 E4 DF 18 D5 00 00 00 00 00 00 00 2D 51 20 00 B3 4E 94 5B

E6 7D 54 00 00 00 00 10 30 94 25 F0 1F 01 67 3F 36 16 EC D7 70 32 32 6A 2C 57 7E D6 F3 77 54 E2

C6 8B 0A 65 72 A0 94 4A 52 12 00 90 4A 24 1F DF 5D D2 47 C0 7C 05 FC 1C 39 2E DF A7 00 34 18 F6

0A A9 B3 7B 49 A5 B1 44 AA DF 67 50 53 13 22 51 10 20 02 02 25 01 AD 63 FF 36 C5 5A AD B1 CD F6

3A 73 FE AA BD A7 B0 2C D8 EC BD 13 9F E3 8D 9E EB 9A E8 73 BD 6B 80 F4 5E 67 69 F6 5F 6D AF 33

2D F0 D1 3B D8 57 B2 B7 A5 9C DB F5 91 5D AB 17 2E C8 CE A6 A0 B6 DC 8A C2 58 85 AB 9A B9 C6 DF

12 5A AC DE 47 8B B1 91 92 2C D1 81 4E F3 5A 23 1A F0 B3 2C E8 9D 56 33 72 F3 09 5D AE 64 45 8A

2F 54 2E D9 BC 1C 5E DB 94 A8 85 96 0A 33 EC D8 C3 B9 6E D4 5E BA 28 95 36 AA C1 17 EC D6 2B A6

CC 22 55 5E A8 57 10 44 49 39 89 D3 58 78 7E 79 48 28 58 85 54 D3 66 BA 64 AE B0 4A 98 B0 2C 4A

E0 AA 9B 48 89 57 39 88 02 48 81 12 98 7E 00 7E 00 91 04 A1 20 24 49 21 29 40 84 81 00 00 02 40

04 00 04 01 04 88 92 00 82 10 22 24 24 80 48 00 00 40 30 00

  
  
36th Animation Data \[at offset 0x0000A024\]

  
03 00 C3 00 04 FF DB FD D1 FB A7 FC F5 01 C6 FB 00 08 FF 3C 0E F9 D7 19 F9 FB 1D 3C 29 07 47 ED

04 00 00 FA F4 58 F6 FD 7C 2F 00 0B 00 BB F9 01 00 00 01 17 3E FF B2 FB 2B FA C0 10 00 00 F0 0A

13 CF 00 00 FF 45 05 11 D0 0E 3E 00 00 E0 ED 08 D5 00 00 25 FF D6 C0 48 6A BB 4D EB C9 4B 73 6B

03 5D 7E E6 D6 DD EB F6 29 A6 A2 BA 33 29 C3 DC 09 55 4C 16 EE E7 4A ED 9A 34 78 F6 4B 76 AB B0

4A F5 FA AD 4A 8F 80 F8 0D 05 AA C0 01 7C 06 27 3F 45 53 25 9E FB BC 9C 7F 40 EF 6C F4 78 7D 57

63 C5 69 78 FE C8 C1 C2 F8 2D 0D BF BD 1A DD EE FF 34 DC E5 7D 73 25 A3 E7 79 1D D9 87 91 91 40

C9 57 5D EB E6 8B 16 F8

  
  
37th Animation Data \[at offset 0x0000A0EC\]

  
0A 00 77 01 04 FF B0 FE 34 FA BA 00 00 00 CA 00 FF FD F9 3B 0C F7 CC 0E F3 FB 1B 3C 28 1E 33 E5

E4 00 00 05 06 04 EB F7 7B 36 09 14 15 BE E5 EB 00 00 0E ED FA FE B5 F7 2C EF B5 0D 00 00 DE 08

11 D1 00 00 FE 49 09 16 C8 0A 39 00 00 D4 ED 0B D5 00 00 01 78 1D 13 4A ED BC AB 14 60 E7 51 97

29 D7 A3 B1 AB DC 93 DE 7D F5 EC 7D F5 9D 76 B7 55 A1 D7 EF CD B5 AE B1 2A 25 81 6A C9 9B 87 9D

60 4A 72 9C 56 58 A6 90 F8 08 08 0C 20 00 00 00 05 99 45 18 51 46 5E 68 AF 23 4A 27 84 9D EA 85

34 60 01 C6 D7 91 7F 7D 45 38 5D 9D 8C 0E 4F 2A 9E DF 02 ED 5B AD CF 54 34 5B DB FA 1D 37 67 77

ED FE E6 E6 7D 76 4A 6E E7 B2 2C CF 02 F4 CA 2D 6F C5 19 15 61 61 E1 5F 27 6B 78 05 5A 20 12 42

79 54 61 CB 69 7E 9E 0D 81 B0 B5 72 FE 46 7D 9D 47 C0 7C 06 3E F6 BD 34 6E B3 73 EF 77 17 62 C1

66 F6 A9 97 4C B9 4E 4B 44 59 B3 98 28 CB AF 0B 41 C0 6C 0C 76 58 06 78 3C 11 EF BE FD 4C F3 E2

78 52 96 78 00 5A AE E8 00 2A 5E C6 C7 B6 53 2A C2 A3 03 1F 2C B3 5D 60 05 F8 28 4A 12 41 44 90

00 12 88 00 02 51 29 48 20 08 95 13 24 00 00 00 00 00 00 00 00 00 00 00 00 00 00 17 E0 90 11 00

00 00 00 00 00 00 01 FC 05 E0 41 09 10 48 00 22 52 00 02 25 11 01 20 25 13 A0 80 6E

  
  
38th Animation Data \[at offset 0x0000A268\]

  
03 00 BE 00 04 FF ED FE 19 FA EE 01 00 00 C3 9D 48 07 0C F2 0C 0D 25 FD FD B2 3A 01 F6 25 2F DF

DE 00 00 05 03 D6 09 1E 35 2E DE EC 22 B8 FB EC 00 00 02 10 BF 03 9A 00 28 13 C9 1E 00 00 D7 1B

FF D4 00 00 FD 2E FF 13 DB 0F 3C 80 80 DC E7 0E D5 00 00 0E FF DB 40 67 AE 11 99 89 3B D9 95 4B

06 F5 79 B7 F4 9A 3C 4B 18 59 C5 3B FC DA 6E E5 CB 0F 0A 59 F7 68 33 E3 0A 25 2B 7C 77 15 94 6B

B6 98 72 25 28 AA AA C6 8B 1B 30 02 AF 40 71 73 89 FA AF D6 5F BD 7A BA 2D DE AA AB DB BD E5 8E

33 96 99 73 1A 99 DC BA D3 E9 6F E6 E7 DB 2E 65 EA 67 28 D0 E0 E2 E4 18 B2 CE 14 4A 8B F5 57 06

93 0E 63 00

  
  
39th Animation Data \[at offset 0x0000A32C\]

  
04 00 E2 00 04 00 3C FE 2D FC E2 FD 00 00 C0 D7 00 06 FF F1 12 04 25 FC F0 B1 20 DE D8 24 F9 BD

C5 80 80 00 00 FA 08 11 33 0E 2D 2E 18 E4 27 F2 00 00 FD F5 FC 00 8D 00 21 2E 00 3A 00 00 CF F4

08 D6 00 00 00 21 00 1C EB 09 0A 00 00 09 00 00 D6 00 00 73 5E 80 29 56 29 42 A9 D3 62 B9 57 62

CD 8C 0B 14 DF F8 0F 80 33 A4 AB 06 A9 D5 BB DE E7 95 D1 7D 4A C6 0D AC E3 06 E5 A8 14 AA BF 2C

52 00 D4 9D 00 87 BE 2C AB 5E BF 66 D5 54 5F B5 85 81 89 A6 D2 E0 86 42 2E E2 E6 5C C0 DF 65 58

2F D8 CE 59 62 62 D1 BA 34 58 79 A1 65 77 3D A6 2B 03 3A A4 02 5A F0 B6 9C AE DE B1 6A AA 6F 59

D1 E8 6B F4 CF 4A C1 0D F4 A2 EE 1E CF 6F 46 DF 6B 80 55 6F 35 6D 8F 6A E6 D8 D4 60 D6 16 D7 73

A3 1B E0 3E 02 B2 01 00

  
  
40th Animation Data \[at offset 0x0000A414\]

  
03 00 C7 00 04 00 00 FD F2 FC B3 02 00 00 C4 93 7E 05 FB 2E 09 F8 C6 13 F0 EC 2C 26 18 11 49 04

EC 00 00 01 04 30 F4 FF 6D 27 D0 E0 FD C5 00 FE 00 00 14 1C 2F 01 C7 04 2B 24 F2 33 00 00 EF 06

FE C2 80 80 01 5B FC 1C B1 05 21 00 00 F6 00 00 D5 00 00 00 69 80 48 CC A7 7A BA DB E0 58 E0 F2

6F 6E A9 DF E4 E3 D1 4D C2 BB FB E8 C2 DA D9 C2 C0 C4 CF 8A C8 DB ED 65 BE A2 BD 15 91 6E B9 53

F0 1F 00 DF 4E EE 3D 38 A5 80 00 29 40 43 77 E5 DF 66 F8 2A 2C F5 79 9A 4F 4C DE E2 75 AD DE F3

4B A4 D4 6F 8A 25 F6 1A 7B 5D 7D 3C 37 07 A5 DC 6F 2F 1D F4 75 D3 DB DE D4 69 30 7A D3 12 B9 68

08 DB DA CD D1 CB 17 E0 3E 03 00 00

  
  
41st Animation Data \[at offset 0x0000A4E0\]

  
03 00 C9 00 04 00 0C FE 04 FC 2A 01 00 00 C3 9B 4A 09 0B F1 0C 0D 26 FF FC B0 3A 00 F6 1F 38 E6

ED 00 00 05 03 D3 0B 1D 35 2E DE EB 23 B8 FB EC 00 00 02 11 BF 03 9A 00 2B 0A C3 1A 00 00 D7 15

05 D4 00 00 FD 2F FE 14 DB 0C 3B 80 80 DB EF 07 D5 00 00 74 FF BE C0 27 A0 B5 B5 D6 D1 1B 0B B5

E8 EF 61 EC 6B CD CD C3 B3 6B 30 B1 55 DC 6B DB 0C FD FE 56 26 93 57 90 6B 35 19 F6 2C 5A B1 67

1A F9 C0 5F C3 81 4D EB B7 E9 B2 69 6C 4C 00 16 40 62 77 E6 7F B3 7C CE 6E 76 3A D5 57 37 FA 2B

98 78 58 7C 17 27 92 67 CA 8C 9B 98 98 5C 9F 1D BF EE 3B 5D 49 D9 F7 3C 65 D9 DE D0 F3 7C 7E EC

C3 C8 C8 A0 A6 78 15 D7 7A F9 A2 C5 BE 3B 00 00

  
  
42nd Animation Data \[at offset 0x0000A5B0\]

  
0A 00 BB 01 04 FF D3 FE 06 FB 7C 00 00 00 C0 65 8C FE 0A E6 10 04 23 F1 FE AA 2B 1B 0C 13 31 DE

CE 00 00 FF FF D5 05 1B 26 29 E4 F3 0A C7 0D E3 00 00 0C F4 D8 00 A7 00 2B 26 E1 26 00 00 D7 10

FF D5 00 00 00 3B 00 29 D3 26 12 00 00 EA F7 F9 D5 00 00 6E 09 59 0C 06 75 DC 6B 0D ED FC BD 14

F2 B2 B6 7C 07 0F 8A 5D BB A9 C9 BD 81 5E 36 2E D7 17 40 30 B4 18 2C 05 19 19 75 95 CA C0 60 2E

E6 EF 34 05 52 B6 1C C0 5A 03 E4 FD D2 FD 78 96 2A C8 95 FC 6A B3 EF E7 5C CD B4 60 5F D1 67 C6

05 58 36 F7 9B DB 52 30 31 E8 5B 4B 2B 32 B2 2B B4 16 D7 EB B9 68 2C 80 65 A3 20 2E 02 EC EC 18

E3 04 17 68 A8 B9 3A 6B 05 22 9A 69 B8 60 66 E0 01 A0 B7 85 DC 1A 5A 33 80 13 D8 48 13 04 44 8A

44 81 12 82 12 80 48 08 24 01 11 02 94 07 82 B4 50 30 81 81 4D F3 7C 33 81 81 5D 93 06 8A AC 02

A1 5D 75 E0 99 F8 77 00 C9 BD 9F C4 1B 89 E1 87 A8 04 37 FD 80 60 EC 5C 2E BF 5C C2 C4 E3 B5 F8

5A 5D 46 A3 82 96 7E BC 96 2D 3A 8D 2F 15 89 A1 C7 E1 32 FB 4D 79 BF CA D7 4F 63 73 2B 4F 7E D9

7F 95 EC 24 4F 63 81 56 AA 58 9F 01 F0 1B 6E 93 96 0F E1 8E 61 5A 8B 56 52 A2 9B 56 29 DC 6E 62

54 D2 25 12 B1 66 54 D3 39 D9 A4 45 0A E2 72 81 29 20 57 2A 28 41 2C EC 10 02 E8 1A 14 A7 7A FA

27 5D EA AB D4 69 E5 15 D6 22 51 55 F8 AE BA 28 BF 58 94 D4 CA 88 90 88 48 53 13 9A 44 61 67 80

06 F0 50 33 33 6B 19 77 29 18 F7 E7 74 31 B3 73 EF 0C 4A C0 0A 22 2B 17 B0 20 12 88 A4 8C 1C F0

  
  
43rd Animation Data \[at offset 0x0000A770\]

  
30 1A 00 00

  
  
44th Animation Data \[at offset 0x0000A774\]

  
30 1A 00 00

  
  
45th Animation Data \[at offset 0x0000A778\]

  
30 1A 00 00

  
  
46th Animation Data \[at offset 0x0000A77C\]

  
30 1A 00 00

  
  
47th Animation Data \[at offset 0x0000A780\]

  
30 1A 00 00

  
  
48th Animation Data \[at offset 0x0000A784\]

  
30 1A 00 00

  
  
49th Animation Data \[at offset 0x0000A788\]

  
30 1A 00 00

  
  
50th Animation Data \[at offset 0x0000A78C\]

  
30 1A 00 00

  
  
51st Animation Data \[at offset 0x0000A790\]

  
30 1A 00 00

  
  
52nd Animation Data \[at offset 0x0000A794\]

  
30 1A 00 00

  
  
53rd Animation Data \[at offset 0x0000A798\]

  
14 00 6A 00 00 00 79 FE 68 FF 67 E7 9F EC 05 70 00 60 0B 72 98 00 2B FE 04 A6 00 0A 01 6D 30 00

10 0B 72 98 03 F3 FD 84 00 3D 80 4A 40 07 A0 1B D1 20 07 A0 0C A8 A4 01 F4 07 2A 74 80 01 00 DD

8B 0F E0 C0 14 A9 7F 09 00 C0 58 7E 08 01 C2 95 2F E0 80 18 12 A4 01 FC 02 C2 40 0F 80 15 20 09

E1 FF 3E 2A 01 77 00 CE 8B E0 4F 20 19 CA 80 00

  
  
54th Animation Data \[at offset 0x0000A808\]

  
14 00 54 00 00 00 C8 FF 0B FF 78 EE DF 31 00 67 F7 F0 00 FE FE 00 91 FD FC 00 3F 80 00 24 7F 7F

00 84 9F C0 00 09 00 3F 80 25 27 F0 00 00 00 00 01 09 00 00 00 49 00 20 00 00 00 04 01 10 02 00

00 40 08 08 01 00 20 00 12 80 08 08 00 01 01 00 40 04 04 00 00 00 80 4A 24 00 00 00

  
  
55th Animation Data \[at offset 0x0000A864\]

  
2D 00 1B 01 04 FD F5 FD FC 00 B5 D3 2C 0B 6F 2F 80 98 E1 6B 6A 12 02 80 20 51 68 F0 00 E9 13 3A

02 B4 10 E8 0A C8 88 00 7F 7C 4A 01 80 00 54 40 50 63 9D 23 5B 63 F4 D2 07 02 11 50 0C 07 12 53

0F 0F ED 91 54 03 BE 7F DE 65 B3 B6 30 8F FF 81 BD B8 AD 0B FD FD FF A0 B9 E9 1F 23 00 9B FF A0

A2 61 61 FD B8 03 A0 07 03 E8 3D C0 03 A0 07 11 CB 6A C0 1E 80 36 BE 8D C7 00 07 80 76 BC 8E F4

00 3C 03 49 E9 7D 60 03 80 07 1B C6 E2 80 38 00 65 FA 77 2E 00 20 01 D9 F1 77 80 04 00 2C FA 87

4C 00 DA 01 C7 71 72 00 6E 00 A3 D4 39 A0 01 20 0E CF 8B B2 00 26 01 9B E9 DD 38 03 90 07 1B C6

E6 80 38 00 68 BD 33 95 00 10 00 ED 79 0D 10 00 70 06 DF D1 FB 00 06 C0 0E 23 95 DB 80 36 00 70

1E 85 C5 00 07 80 77 5C D7 00 00 32 01 DE 73 9D F3 0A FC 01 67 17 06 D3 63 64 01 F7 43 87 82 10

11 00 7A D0 62 62 40 10 CA 20 0D 7A 1D 1E 8E 00 FC 6A 09 89 A5 BA 5C 52 0D 83 AE D1 BE 00 3E 92

  
  
56th Animation Data \[at offset 0x0000A984\]

  
0E 00 48 00 04 00 89 FE 6F FE EA E0 FB 04 04 23 FF CD D5 3A 1B 3F F6 DF F6 5C 3B 40 04 0F FB B0

07 30 22 AE 26 1D 00 4E FF 92 61 56 7F 08 68 90 02 F0 31 03 F3 D1 64 C7 B7 92 F8 91 E5 D0 E2 72

93 CB B1 5C E8 93 FB F0 30 01 02 7A 0D 00 00 00

  
  
57th Animation Data \[at offset 0x0000A9D4\]

  
0C 00 3C 00 04 00 84 FE 69 FF 61 DF FB 09 00 7A 01 B9 2A 40 00 00 00 00 00 00 02 FF C9 40 15 22

2A 05 7D 80 C1 AC 5E 6E 80 52 C0 2E B4 2B 0F 61 E2 B2 01 5C 5A E0 00 63 48 00 0E 6A C0 01 D9 68

5F 00 00 00

  
  
58th Animation Data \[at offset 0x0000AA18\]

  
0A 00 3B 00 04 FF FB FD 8B FF 6C E6 AE 45 6E 5B 2D A2 AC 10 00 08 05 A8 00 00 00 02 44 AA F3 B1

9E 2D 00 A5 61 C8 E2 3B C8 03 41 A1 26 87 89 DA 87 B8 A8 2C 54 F8 FB FF BA 4E 4E A2 3F FB 44 E9

  
  
59th Animation Data \[at offset 0x0000AA58\]

  
01 00 09 00 04 FE 4E FF E7 FF 50 00 FE 41 00 00

  
  
60th Animation Data \[at offset 0x0000AA68\]

  
06 00 21 00 04 00 9D FE 47 00 2C 02 80 FF 7A 12 4E 98 38 D9 FF A4 85 0E 0B 05 24 9F 4E CE 09 AA

C0 13 20 09 49 5A 00 00

  
  
61st Animation Data \[at offset 0x0000AA90\]

  
01 00 09 00 04 FF 41 FD AE FE 84 00 C1 80 00 00

  
  
62nd Animation Data \[at offset 0x0000AAA0\]

  
0E 00 60 00 04 00 B9 FE 0F FF 22 D5 EC 09 3D 80 6D C0 48 F5 3F 35 A6 00 00 00 1F FB CF FD 17 FD

E3 67 89 A8 FF D6 7F DE BF E9 99 7E 99 D5 2B 7F E6 3F ED D8 FC D7 6A FC EE E9 2A 20 08 24 32 27

20 00 00 00 24 33 00 45 67 D0 39 00 41 80 23 D1 97 6C 72 00 95 00 44 A3 33 05 F4 6C 56 DB 1D F8

18 33 07 07 1D 00 00 00

  
  
63rd Animation Data \[at offset 0x0000AB08\]

  
0F 00 65 00 04 00 B1 FE 52 FF 63 E9 02 F6 25 04 00 33 C5 42 C3 AB AE B1 01 60 EA EE C8 85 E0 3E

2A 2F 84 38 CA C3 FB 0B FF 8B 31 B7 7F D1 E0 31 1F EC D8 05 A6 AB 9C E0 89 55 D5 2D E0 D8 1A 6C

65 B1 6E 80 10 80 D9 CE 68 06 C7 59 F9 55 32 40 27 BF C9 9D 36 1F B9 C0 28 A0 0C 70 06 6D 0F 67

AF 6B 80 49 40 14 B1 32 B8 06 00 00

  
  
64th Animation Data \[at offset 0x0000AB74\]

  
30 1A 00 00

  
  
65th Animation Data \[at offset 0x0000AB78\]

  
1E 00 B6 00 04 FF B7 FD 83 FF A9 C1 86 73 55 80 2E C0 15 B8 FF 51 FA 84 10 38 02 6F 15 93 5B F3

F0 1D 15 C0 10 13 E4 E9 A0 00 00 00 1B 3A AB EE AB A8 D9 21 77 6F 72 C0 EF FE CD BB 6F D3 72 28

01 29 1E 8D F6 5C 4C 01 25 84 1F 33 E5 3E A9 AF FE D7 00 44 EA FE 7F D2 19 55 44 F4 D6 AC 38 B3

C0 1B 78 8D 0D A7 48 02 44 01 BB 5D AF E0 04 9B 60 08 13 B5 BF 16 79 1C AB 13 2D FC 01 F5 38 00

7C 07 51 43 FB E8 54 A8 A5 FD F4 25 4D 20 0F C0 C9 50 FC 02 10 A6 CB E8 13 E2 21 F8 05 7A 79 B9

AF C0 EB 95 DC B8 FA 06 F3 10 7E 00 0C 95 34 BF 01 90 D1 62 D3 F0 31 4C AD 60 35 00

  
  
66th Animation Data \[at offset 0x0000AC34\]

  
06 00 20 00 04 FF A7 FC 9D 01 74 2C B1 7C 00 00 00 00 0F CF C9 48 00 08 09 10 00 1C 17 3B B7 00

05 83 6B BB 72 00 00 00

  
  
67th Animation Data \[at offset 0x0000AC5C\]

  
0B 00 4C 00 04 FF A7 FC A7 01 80 26 A2 6B 00 69 74 20 01 F1 DA 22 00 00 00 00 63 D1 96 05 8C 27

50 A1 AB 18 7A 25 8F FD 97 FE B3 BD CA D2 88 2C 7F C5 F6 9B 5B D0 06 C8 03 8F FC 8B 69 9D 7E 00

D7 01 00 FF D3 64 FB D7 BF 09 40 36 09 F8 0C 0B BE 00 00 00

  
  
68th Animation Data \[at offset 0x0000ACB0\]

  
09 00 43 00 04 00 28 FD EC 00 86 D4 13 F2 FF D4 40 13 60 15 57 F3 B1 BF EE 27 B0 0E 4D 26 46 AD

60 64 7E D5 36 42 04 40 2C 40 51 A9 32 27 38 02 07 FD 9F FD D9 B7 BF 93 00 D3 1C FF A4 D9 B1 90

63 00 56 FF 9A 63 DB B6

  
  
69th Animation Data \[at offset 0x0000ACF8\]

  
09 00 2E 00 04 FF 2B FE 4B FF FA 09 F5 0E 05 04 69 9C A1 E8 04 6A D4 8F 4F 82 B4 44 9F DE 42 D3

04 BE 31 5D 80 18 3B 4C 50 7F 0B 06 A6 50 F6 F6 27 28 97 00

  
  
70th Animation Data \[at offset 0x0000AD2C\]

  
09 00 36 00 04 FF 27 FE 42 00 16 0D F3 0E 80 20 34 FF E1 F7 FB DB 50 07 E7 66 7D ED 55 80 00 00

02 D0 D7 8A AC D6 62 1E 01 3C 0B E4 C1 80 4C 0A 82 03 5D 65 6C 10 1A EB 4D B9 1C 00

  
  
71st Animation Data \[at offset 0x0000AD68\]

  
0E 00 5B 00 04 FF 4C FC F3 FF 6D D6 9E 6C 5E FF AD 1B CF 0A F0 7F FE D5 E2 EE CB 80 FF D6 C0 1A

8B 38 2C 9E 05 5E 01 E4 47 C2 66 52 45 00 BC 7E C8 DD E5 00 C0 33 90 A8 DC 5F FF C7 8F 96 D8 DA

7D 6B AC 02 D9 2A EE F6 1F 57 1B A8 CD 90 02 A3 9C AF 43 D8 FB 92 B9 BC 19 37 C0 F4 5A DB 5C 00

  
  
72nd Animation Data \[at offset 0x0000ADC8\]

  
0C 00 62 00 04 01 01 FD BE 00 66 C4 46 84 4C FF C8 C0 45 B8 5B 3D CF FE E9 E2 00 C7 6B 2E 70 04

60 8F FC ED EC 5A 3F F1 40 DF E0 6B DE 87 2F F5 89 8C 01 3A BF 52 CA 80 97 8D 40 11 6D FA 46 FA

01 5C EF FE B7 B1 CA 67 B4 3B 7F D6 F3 38 2C 10 76 40 0D CD EE 19 E5 B8 E6 CF D6 7B 27 FE B2 02

09 01 08 D5 77 7C F0 00

  
  
73rd Animation Data \[at offset 0x0000AE30\]

  
10 00 5B 00 04 00 2C FD DC FF D5 D5 03 F8 FF C8 7F E4 A0 0F B9 99 BA 17 57 E8 02 65 58 B9 40 00

41 72 89 00 00 81 00 00 00 00 00 FE FC 00 1F 9D 62 50 5C CD FE D8 B2 91 2C 01 1F FE AB 8D 7A CB

E1 12 5C A4 00 05 78 90 00 F6 11 00 22 F1 AC 42 00 A5 00 78 33 B5 5C 88 E0 0A 50 06 AC 1A 6C 3B

  
  
74th Animation Data \[at offset 0x0000AE90\]

  
1E 00 CF 00 04 FF DB FE 58 FF 3B DF 03 06 FF B4 FF D5 D4 36 D3 A7 FF 51 FE EA 80 4C EB 3E 2F DC

45 FF EB D0 1A BE 4F 5B 10 08 F8 04 EC 04 07 41 C0 52 00 00 00 06 41 88 15 4F FE BB FF AD 5C CD

CB D6 FF CE 60 0B 7F F2 8E BB 07 06 00 8D 00 52 FF A9 66 76 B1 00 F7 80 29 FF E1 77 FD A5 30 0C

81 13 CA FA AD 41 B7 FD 86 01 59 A8 9F 79 FF 5E FF B1 C0 14 B8 08 DF 21 34 9D E2 EA F7 EE 2D 4E

B6 F8 0B 2A AC 4D 97 B0 B0 1E DF 45 65 48 1C 04 5E 9A 60 00 00 00 3E C0 1E BF D8 5D C4 A4 87 01

2F FF D9 68 FE 0F DF DC 02 C4 30 24 7E 02 03 90 00 00 00 00 9F 9F 60 10 75 70 B9 08 04 44 01 27

FF 31 99 7E 98 03 FC 01 73 FF 75 72 10 04 E8 02 32 AC 59 B1

  
  
75th Animation Data \[at offset 0x0000AF64\]

  
06 00 29 00 04 FE FE FD 9B FD 50 F0 09 42 80 20 40 10 7F DE 9A 1C 7A BF F3 C4 90 05 FA 33 73 1E

1B 80 25 7E 40 61 8A 72 BC 0B 14 4D 95 D1 00 00

  
  
76th Animation Data \[at offset 0x0000AF94\]

  
30 1A 00 00

  
  
77th Animation Data \[at offset 0x0000AF98\]

  
06 00 26 00 04 FF A4 FD B8 00 0A DA 09 10 FF B5 81 C0 60 6C 6E 78 90 48 02 0C 04 FB 5F 8B 48 18

A1 0D 2B 00 20 60 A4 9F DF 5E C8 00

  
  
78th Animation Data \[at offset 0x0000AFC4\]

  
06 00 2E 00 04 FF 13 FD FC 02 C9 FD FF 3C 78 5D FF C2 66 5C A0 11 8B FE 7D BD BF 7E 01 2A FB FE

7F AB 4F DB C0 27 20 10 3F F8 6C 2D F6 71 C9 52 C5 38 0E 00

  
  
79th Animation Data \[at offset 0x0000AFF8\]

  
02 00 13 00 04 FF CB FD D8 FF D2 CE 63 91 FF DB FF EC E0 21 5A 5E 1B 7E

  
80th Animation Data \[at offset 0x0000B010\]

  
05 00 1E 00 04 FF 82 FD 16 FC F7 E3 89 81 01 01 76 44 80 40 9D A2 0F CF A2 92 A2 02 9A 60 15 56

71 EE E8 00

  
  
81st Animation Data \[at offset 0x0000B034\]

  
03 00 19 00 04 00 9B FE 6C FC 0C 15 B8 BE 71 FF AF 40 43 F2 B5 DC 29 BB D4 04 AF B9 D3 43 00 00

  
  
82nd Animation Data \[at offset 0x0000B054\]

  
04 00 1D 00 04 00 C3 FD DC FF F0 E0 EC E2 5B 80 3A 7F CC 6D EB B5 6D 4F C0 F2 AE DB 88 AC 01 02

2E 50 00 00

  
  
83rd Animation Data \[at offset 0x0000B078\]

  
06 00 2B 00 04 FF 2E FD 91 FC 7B F0 63 B1 80 6C C0 1C BF B0 F3 E8 F5 D0 09 48 03 4C 08 2B 87 F9

2D F8 E8 11 8C A7 6C 05 EC 1E 50 7F 05 79 89 18

  
  
84th Animation Data \[at offset 0x0000B0A8\]

  
1F 00 C2 00 04 00 36 FE 15 00 6E E7 FB 03 16 FF DD C0 2D 67 62 7F FB 90 31 59 68 AF FF E6 03 87

E5 A7 CF FF CA 82 40 16 A9 D6 65 FF EB C1 A0 11 D6 75 79 8D 01 F0 0A 8B 5A 8C F2 E0 F8 04 A5 9D

25 E8 03 03 3C 01 02 8C 4B D0 07 44 87 C9 62 5F 80 3F 3B 24 CF 49 23 F7 3F FD 24 F4 93 04 7D 01

51 00 00 00 03 FD 4B 00 78 FF 21 58 F8 5B 70 1A E3 30 8A 7E 76 7F F6 B7 88 07 AD 8E AE 4B EF E0

F1 7A 4F 80 00 00 30 01 F9 40 44 05 F6 54 C0 40 03 F2 40 00 00 01 00 76 12 FF 9D CF 85 C5 4D 0C

FF 91 DA E1 30 BF F5 C1 3F FB 18 C0 E0 5D 85 BF E8 B9 97 F0 4D 1E D2 F3 6F C8 35 E1 C6 A8 01 BC

BD 4E 00 8F 2F 55 9C 00

  
  
85th Animation Data \[at offset 0x0000B170\]

  
19 00 8F 00 04 FF FE FC 46 FC E7 26 80 7F 00 00 00 02 70 2D 9F F0 D7 69 F0 1F 02 0C 3E E5 24 C0

41 5F 83 FB D8 10 7A 61 0E 85 0F 0F 4E B4 E8 BB 61 35 04 AA F0 BB 88 06 BF F9 6E 03 25 9B F5 BA

05 D5 38 02 3C B2 AC 3C 3C 85 AB 90 40 3B AA 98 23 2D FF DC C6 35 4F 24 64 FB 8D 9F 14 06 2A 3B

A3 ED 39 E1 B6 95 8D 36 2E B7 FE E6 B3 FE CD 73 D4 7F 9F 86 20 37 2F 77 9C 01 61 9E 00 84 D1 D2

E4 F2 EB 11 43 F3 FB F0 00 00 00 00 40 20 40 38 1C 2E 52 98

  
  
86th Animation Data \[at offset 0x0000B204\]

  
14 00 77 00 04 FF A6 FD 08 FC EE FC 8F 75 0E 80 2F AA 62 DA A1 EC 3D CA 25 20 00 00 00 F0 52 E9

83 52 00 C3 FE 6B 1A D4 6F AE 00 7F 1B 14 30 1A 00 3F FD 30 3D 33 02 B4 8B 5A B9 70 14 54 56 9E

C7 B0 03 29 0C 8D A6 CD F0 95 DE 5C 9F 24 E8 1C 97 99 C1 70 61 70 33 BF EB A7 CD FC 17 C0 31 C0

E3 60 1A 3C A5 70 19 00 4B 26 94 A4 00 D4 01 20 09 98 0A 80 05 98 0A 91 FD 98 0E 80

  
  
87th Animation Data \[at offset 0x0000B280\]

  
0A 00 43 00 04 00 94 FE 4B FB F9 F5 85 F6 1E 12 1B C2 EE FD 41 2E 00 80 37 46 5D D3 54 06 59 E2

DB FF 5B FF E0 BF BB 76 7E 22 3F E8 3F FA 48 05 AD FE 56 42 DF FA 53 FB BA 1C 31 10 42 86 1C 81

5F 01 62 47 B0 47 B9 40

  
  
88th Animation Data \[at offset 0x0000B2C8\]

  
03 00 1B 00 04 FE A9 FD 42 FB 79 07 1E 4A 80 6A A5 40 12 6F 75 F9 10 14 58 05 C4 0A 13 BF 8F A8

  
  
89th Animation Data \[at offset 0x0000B2E8\]

  
0A 00 42 00 04 FE 99 FD E7 FA E7 E4 56 E4 3E 80 39 B6 F1 3A 7C A0 10 33 66 15 30 0F 9F FD 9F FB

73 1F ED F6 70 0D BF F7 1C 04 AB A3 FB 8D C8 D3 DC 02 0A 7B 0D 20 10 00 AA FD 20 00 0F E0 00 01

F1 23 F0 03 82 C5 7B 00

  
  
90th Animation Data \[at offset 0x0000B330\]

  
03 00 19 00 04 00 AC FE 57 FA 95 0F 0B EF 14 FF CF 40 71 B7 59 99 C0 69 F0 1E BD BE F6 B0 00 00

  
  
91st Animation Data \[at offset 0x0000B350\]

  
04 00 24 00 04 FF 80 FD EF FB 93 EA D5 33 80 70 FF E9 20 08 9B 9E D3 43 00 73 08 80 87 65 7A 07

D5 B7 94 C0 58 75 74 E5 BC 00 00 00

  
  
92nd Animation Data \[at offset 0x0000B37C\]

  
03 00 1C 00 04 FE D7 FD 69 FC B7 FA 1F 35 80 64 86 7F E8 37 7D 56 FA 02 47 00 4F 80 F7 DF A7 EF

C1 00 00 00

  
  
93rd Animation Data \[at offset 0x0000B3A0\]

  
03 00 19 00 04 00 C9 FE 4C FB DA 0F 0B F1 6B FF B8 C0 41 F2 B2 70 C3 C1 E0 2C BD FE 46 D8 00 00

  
  
94th Animation Data \[at offset 0x0000B3C0\]

  
0A 00 40 00 04 00 A1 FD 50 FA C5 DF E8 D3 FF 87 7F CE 11 6E 7C CF D1 81 A7 C0 2E 38 18 C0 01 68

80 66 68 92 01 03 21 A4 7E 15 FF 89 EE D0 E3 02 F9 FF 49 E0 7B FF C0 83 8E 89 25 27 96 36 E4 40

72 18 D5 32 92 00 00 00

  
  

- \*\* \*\*\* Animation Data Section runs until Texture Data Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Texture Data Section** - \[at offset 0x0000B408\]

  
Note: This section (in this case, consisting of one 'file'...maybe in all playable character battle models?) is modified TIM data.

  
Texture Data (modified TIM format) - \[at offset 0x0000B408\]

  
10 00 00 00 08 00 00 00 4C 00 00 00 00 00 E0 01 10 00 02 00 00 00 8D 31 20 04 01 00 48 04 5B 67

74 4A D4 2D CB 10 8C 0C 0F 25 35 29 B7 35 20 32 00 25 20 04 00 00 23 04 68 04 3B 1E 81 28 93 8D

BF 8E E5 38 27 59 CB 75 AB 90 40 90 8F 25 13 36 75 3A 81 28 0C 1E 00 00 40 01 00 00 3C 00 40 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 30 53 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 36 53 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 60 36 55 22 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 33 36 55 22 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 30 63 33 55 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 33 66

33 55 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 30 33 66 33 55 22 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 33 63 66 33 55 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 30 33 66 36 33 55 22 02 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 33 66 66 36 53 55 22 02

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 90 44 44

44 94 89 98 49 44 44 44 09 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 30 63 66 66 33 53 55 22 22 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 90 44 44 44 44 44 44 44 44 44 44 44

44 09 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 33 66 66 66 33 53 55 22 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 80 49 89 88 88 99 99 44 44 99 99 88 88 98 94 08 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 63 66 66 66

33 55 55 22 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 63 66 66 66 33 55 55 22 22 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 50 63 66 66 66 33 55 55 A2 1A 11 11 2A 22 02 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 35 66 66 66 33 55 55 22 11 11 A1 22 22 22 22 22 02 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 63 66 66 33 55 55 12

11 11 22 22 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 63 66 66 33 55 55 12 11 21 22 22 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 35 66 66 36 53 55 12 21 22 22 22 22 22 22 22 22 22 22 22 22 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 65

66 33 53 55 12 A1 11 11 11 11 11 11 11 11 11 11 11 02 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 63 36 33 55 15 11 11 22 22

22 22 22 22 12 11 11 2A 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 66 33 55 15 A1 11 22 BB 4B 44 BF BB BB FF 22 11 01

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 35 36 55 15 11 1A 21 BB F4 FF FF FF 44 BB FB CC 12 01 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 33 53

55 11 2A 11 4B FB FF FF FF FF FF B4 FB CC 2C 11 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 33 55 A2 2A 12 41 88 F7 FF FF

FF FF FF 4F FB CC CC 12 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 35 53 15 2A 22 11 CC 9D F8 FF FF 4F 44 7F 47 F4 EE CD 2C

11 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 35 55 00 22 10 C1 CC 9D 78 FF FF F4 F4 77 77 7F EE DE CC 12 01 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 25 0A 20

02 10 CC 4C 88 77 F7 4F 4B 44 77 77 7F EE EE DD 20 11 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 50 AA 00 22 00 21 CC 4D 44 74 47 BF

BB 74 87 77 7F EE DD CD 00 20 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 20 02 10 22 DC 4E 74 77 47 B4 BB 74 88 78 7F DD DD CC

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 02 DC 4E 74 77 77 44 4B 74 88 78 7F DD CD 0C 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 DC 4E 74 77 77 47 44 77 88 78 CF DD CD 0C 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 DC 8E 74 87 88 77

77 87 88 78 CF DD CC 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 DC DD 74 88 88 88 88 88 88 77 C7 CD 1C 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 C0 DD 78 88 88 88 88 88 88 47 CC CC 12 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 C0 DD 8D 84 88 88 88 88 78 74 CC 2C 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 DC DD 47 88 88

88 88 47 C7 CC 22 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 C0 DD 7D 77 77 77 77 77 CC 2C 12 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 CC CC 7C F7 7F 77 CC CC 22 01 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 AA 22 22 22 22 22 22 22 22 11 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 2A 22 11

11 11 11 11 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

  
  
  

- \*\* \*\*\* Texture Data Section runs until Weapon Bone Data Section\*\*\*

  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Weapon Bone Data Section**

  
Note: The first 0x0C bytes of each of these is the same type of data in normal Individual Bone Structure data (far above).

  
  
1st Weapon Bone Data \[at offset 0x0000D268\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 40 02 00 00 0D 00 E7 FF CD FF 00 00 13 00 06 00 CD FF 00 00

F6 FF 0B 00 CD FF 00 00 F0 FF EE FF CD FF 00 00 F0 FF EE FF C7 FF 00 00 0D 00 E7 FF C7 FF 00 00

13 00 06 00 C7 FF 00 00 F6 FF 0B 00 C7 FF 00 00 21 00 3A 00 C7 FF 00 00 21 00 3A 00 A9 FF 00 00

07 00 B1 FF A9 FF 00 00 07 00 B1 FF C7 FF 00 00 FC FF 41 00 A9 FF 00 00 E2 FF B8 FF A9 FF 00 00

FC FF 41 00 C7 FF 00 00 E2 FF B8 FF C7 FF 00 00 0D 00 02 00 CD FF 00 00 09 00 ED FF CD FF 00 00

09 00 ED FF A7 00 00 00 0D 00 02 00 A7 00 00 00 F6 FF F2 FF CD FF 00 00 FA FF 05 00 CD FF 00 00

F6 FF F2 FF A7 00 00 00 FA FF 05 00 A7 00 00 00 10 00 00 00 8D FF 00 00 12 00 08 00 A9 FF 00 00

12 00 08 00 5A FF 00 00 10 00 00 00 6D FF 00 00 01 00 B2 FF 2F FD 00 00 12 00 08 00 4E FD 00 00

F5 FF B5 FF AA FC 00 00 01 00 B2 FF A9 FF 00 00 01 00 B2 FF 5A FF 00 00 10 00 00 00 9A FF 00 00

0E 00 F5 FF 87 FF 00 00 0C 00 EA FF 8D FF 00 00 0C 00 EA FF 9A FF 00 00 0E 00 F5 FF A1 FF 00 00

0C 00 EA FF 6D FF 00 00 0E 00 F5 FF 74 FF 00 00 10 00 00 00 60 FF 00 00 0E 00 F5 FF 59 FF 00 00

0C 00 EA FF 60 FF 00 00 0E 00 3E 00 45 FD 00 00 0E 00 3E 00 5A FF 00 00 0E 00 3E 00 A9 FF 00 00

F2 FF EF FF 60 FF 00 00 F4 FF FA FF 5A FF 00 00 F6 FF 04 00 60 FF 00 00 F4 FF FA FF 74 FF 00 00

F2 FF EF FF 6D FF 00 00 F4 FF FA FF A1 FF 00 00 F2 FF EF FF 9A FF 00 00 F2 FF EF FF 8D FF 00 00

F4 FF FA FF 87 FF 00 00 F6 FF 04 00 9A FF 00 00 E7 FF B7 FF 5A FF 00 00 E7 FF B7 FF A9 FF 00 00

F8 FF 0D 00 4F FD 00 00 E7 FF B7 FF 2F FD 00 00 F6 FF 04 00 6D FF 00 00 F8 FF 0D 00 5A FF 00 00

F8 FF 0D 00 A9 FF 00 00 F6 FF 04 00 8D FF 00 00 09 00 ED FF DA FF 00 00 FA FF 05 00 DA FF 00 00

F6 FF F2 FF DA FF 00 00 0D 00 02 00 DA FF 00 00 09 00 ED FF 99 00 00 00 FA FF 05 00 99 00 00 00

F6 FF F2 FF 99 00 00 00 0D 00 02 00 99 00 00 00 00 00 20 00 00 00 00 00 1D 00 00 00 F0 00 E8 00

58 01 00 00 2F 3C 3F 30 CC C9 D1 00 CC C9 D1 00 D0 01 F0 00 58 01 00 00 66 6A 74 30 28 32 37 00

94 93 A0 00 E8 00 F0 00 E0 00 00 00 64 6A 6F 30 3C 48 4B 00 2F 3C 3F 00 E8 00 48 01 D0 00 00 00

64 6A 6F 30 4E 57 5A 00 64 6A 6F 00 00 01 50 01 48 01 00 00 09 1B 1C 30 4E 57 5A 00 4E 57 5A 00

40 01 D0 00 48 01 00 00 4E 57 5A 30 64 6A 6F 00 4E 57 5A 00 C8 00 08 01 28 01 00 00 3C 48 4B 30

3C 48 4B 00 3C 48 4B 00 F8 00 20 01 18 01 00 00 09 1B 1C 30 3C 48 4B 00 3C 48 4B 00 C8 00 28 01

F8 00 00 00 3C 48 4B 30 3C 48 4B 00 09 1B 1C 00 F8 00 28 01 20 01 00 00 09 1B 1C 30 3C 48 4B 00

3C 48 4B 00 00 01 30 01 50 01 00 00 09 1B 1C 30 46 4F 53 00 4E 57 5A 00 D8 00 D0 00 40 01 00 00

46 4F 53 30 64 6A 6F 00 4E 57 5A 00 C8 00 C0 00 08 01 00 00 3C 48 4B 30 3C 48 4B 00 3C 48 4B 00

48 01 E0 00 00 01 00 00 4E 57 5A 30 2F 3C 3F 00 09 1B 1C 00 E0 00 48 01 E8 00 00 00 2F 3C 3F 30

4E 57 5A 00 64 6A 6F 00 D8 01 E0 00 F0 00 00 00 2D 2D 2D 30 2D 2D 2D 00 3C 48 4B 00 F0 00 D0 01

D8 01 00 00 32 3C 42 30 32 3C 42 00 28 32 37 00 78 01 D0 01 E8 01 00 00 32 3C 42 30 32 3C 42 00

32 3C 42 00 70 01 C0 01 78 01 00 00 32 3C 42 30 06 15 18 00 32 3C 42 00 E8 01 80 01 78 01 00 00

32 3C 42 30 32 3C 42 00 32 3C 42 00 B8 01 F0 01 98 01 00 00 32 3C 42 30 32 3C 42 00 32 3C 42 00

A0 01 C8 01 A8 01 00 00 32 3C 42 30 06 15 18 00 32 3C 42 00 98 01 F0 01 C8 01 00 00 32 3C 42 30

32 3C 42 00 06 15 18 00 98 01 C8 01 A0 01 00 00 32 3C 42 30 06 15 18 00 32 3C 42 00 90 01 C0 01

70 01 00 00 32 3C 42 30 06 15 18 00 32 3C 42 00 E8 01 E0 01 80 01 00 00 32 3C 42 30 32 3C 42 00

32 3C 42 00 F8 01 F0 01 B8 01 00 00 32 3C 42 30 32 3C 42 00 32 3C 42 00 D8 01 78 01 C0 01 00 00

28 32 37 30 32 3C 42 00 06 15 18 00 78 01 D8 01 D0 01 00 00 32 3C 42 30 28 32 37 00 32 3C 42 00

32 00 00 00 50 00 68 00 58 00 78 00 BD C2 9A 38 90 94 76 00 BD C2 9A 00 58 5A 48 00 48 00 50 00

40 00 58 00 96 A0 8C 38 69 69 5A 00 96 A0 8C 00 69 69 5A 00 60 00 48 00 70 00 40 00 25 26 1E 38

25 26 1E 00 25 26 1E 00 25 26 1E 00 68 00 60 00 78 00 70 00 2D 32 28 38 41 41 32 00 2D 32 28 00

41 41 32 00 58 00 78 00 40 00 70 00 6E 71 5A 38 2F 30 26 00 1E 1E 18 00 23 23 1C 00 48 00 60 00

50 00 68 00 56 58 46 38 2B 2C 23 00 A7 AC 88 00 47 49 3A 00 30 02 20 02 10 02 00 02 17 05 20 38

46 10 30 00 17 05 20 00 47 10 30 00 20 02 38 02 00 02 18 02 46 10 30 38 0A 02 1A 00 47 10 30 00

0A 02 1A 00 38 02 28 02 18 02 08 02 0A 02 1A 38 00 00 17 00 0A 02 1A 00 00 00 17 00 28 02 30 02

08 02 10 02 00 00 17 38 17 05 20 00 00 00 17 00 17 05 20 00 60 01 58 01 D0 00 E8 00 79 7D 82 38

CC C9 D1 00 32 41 41 00 CC C9 D1 00 68 01 60 01 C8 00 D0 00 79 7D 82 38 79 7D 82 00 32 41 41 00

32 41 41 00 58 01 60 01 D0 01 E8 01 94 93 A0 38 66 6A 74 00 66 6A 74 00 28 32 32 00 60 01 68 01

E8 01 F0 01 66 6A 74 38 66 6A 74 00 28 32 32 00 28 32 32 00 C8 00 D0 00 C0 00 D8 00 3C 48 4B 38

64 6A 6F 00 3C 48 4B 00 46 4F 53 00 C0 00 D8 00 10 01 38 01 3C 48 4B 38 46 4F 53 00 3C 48 4B 00

3C 48 4B 00 10 01 38 01 18 01 30 01 3C 48 4B 38 3C 48 4B 00 3C 48 4B 00 46 4F 53 00 F8 00 18 01

00 01 30 01 09 1B 1C 38 3C 48 4B 00 09 1B 1C 00 46 4F 53 00 C0 01 00 01 D8 01 E0 00 3C 48 4B 38

3C 48 4B 00 2D 2D 2D 00 2D 2D 2D 00 C8 01 F8 00 C0 01 00 01 6E 6E 6E 38 6E 6E 6E 00 3C 48 4B 00

3C 48 4B 00 E8 01 F0 01 E0 01 F8 01 32 3C 42 38 32 3C 42 00 32 3C 42 00 32 3C 42 00 E0 01 F8 01

88 01 B0 01 32 3C 42 38 32 3C 42 00 32 3C 42 00 32 3C 42 00 88 01 B0 01 90 01 A8 01 32 3C 42 38

32 3C 42 00 32 3C 42 00 32 3C 42 00 A8 01 C8 01 90 01 C0 01 32 3C 42 38 06 15 18 00 32 3C 42 00

06 15 18 00 A0 01 20 01 98 01 28 01 2E 38 3A 38 2E 38 3A 00 4E 57 5A 00 4E 57 5A 00 98 01 28 01

B8 01 08 01 4E 57 5A 38 4E 57 5A 00 80 8D 93 00 80 8D 93 00 B8 01 08 01 F8 01 C0 00 80 8D 93 38

80 8D 93 00 2E 38 3A 00 2E 38 3A 00 F8 01 C0 00 B0 01 10 01 2E 38 3A 38 2E 38 3A 00 1A 29 2A 00

1A 29 2A 00 B0 01 10 01 A8 01 18 01 1A 29 2A 38 1A 29 2A 00 10 16 17 00 10 16 17 00 A8 01 18 01

A0 01 20 01 10 16 17 38 10 16 17 00 2E 38 3A 00 2E 38 3A 00 70 01 50 01 90 01 30 01 17 1D 1D 38

17 1D 1D 00 2C 36 36 00 2C 36 36 00 90 01 30 01 88 01 38 01 2C 36 36 38 2C 36 36 00 3F 49 49 00

3F 49 49 00 78 01 48 01 70 01 50 01 1C 2D 2D 38 1C 2D 2D 00 17 1D 1D 00 17 1D 1D 00 80 01 40 01

78 01 48 01 2C 36 36 38 2C 36 36 00 1C 2D 2D 00 1C 2D 2D 00 88 01 38 01 E0 01 D8 00 3F 49 49 38

3F 49 49 00 85 99 99 00 85 99 99 00 E0 01 D8 00 80 01 40 01 85 99 99 38 85 99 99 00 2C 36 36 00

2C 36 36 00 90 00 B0 00 98 00 B8 00 93 9A 7D 38 40 43 37 00 28 2A 22 00 37 37 37 00 98 00 38 02

90 00 20 02 28 2A 22 38 1F 21 1B 00 93 9A 7D 00 BD C2 9A 00 90 00 20 02 B0 00 30 02 93 9A 7D 38

BD C2 9A 00 40 43 37 00 4A 4D 3F 00 B0 00 30 02 B8 00 28 02 40 43 37 38 4A 4D 3F 00 37 37 37 00

19 19 00 00 B8 00 28 02 98 00 38 02 37 37 37 38 19 19 00 00 28 2A 22 00 1F 21 1B 00 88 00 00 02

80 00 18 02 81 7D 5A 38 81 7D 5A 00 31 30 23 00 15 15 0F 00 00 00 08 00 28 00 30 00 67 65 4B 38

1B 1B 14 00 81 7D 5A 00 31 30 23 00 08 00 00 00 10 00 18 00 1B 1B 14 38 67 65 4B 00 20 20 18 00

2C 2B 20 00 80 00 18 02 A8 00 08 02 31 30 23 38 15 15 0F 00 00 00 00 00 00 00 00 00 08 00 10 00

30 00 38 00 1B 1B 14 38 00 00 00 00 31 30 23 00 00 00 00 00 10 00 18 00 38 00 20 00 00 00 00 38

2F 29 2E 00 00 00 00 00 40 36 3D 00 18 00 00 00 20 00 28 00 2F 29 2E 38 67 65 4B 00 40 36 3D 00

81 7D 5A 00 A0 00 10 02 88 00 00 02 29 23 29 38 2F 29 2E 00 81 7D 5A 00 81 7D 5A 00 A8 00 08 02

A0 00 10 02 00 00 00 38 00 00 00 00 29 23 29 00 2F 29 2E 00

  
  
2nd Weapon Bone Data \[at offset 0x0000DBBC\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 40 02 00 00 04 00 FA FF 5D 00 00 00 06 00 FA FF B3 FF 00 00

F7 FF F1 FF 5D 00 00 00 F5 FF ED FF B3 FF 00 00 FB FF 0B 00 B3 FF 00 00 FB FF 07 00 5D 00 00 00

F4 FF EC FF 80 00 00 00 FA FF 0C 00 80 00 00 00 07 00 F9 FF 80 00 00 00 F8 FF 93 FF 95 FF 00 00

E1 FF 97 FF 95 FF 00 00 07 00 62 00 95 FF 00 00 1E 00 5E 00 95 FF 00 00 1E 00 5E 00 AA FF 00 00

F8 FF 93 FF AA FF 00 00 E1 FF 97 FF AA FF 00 00 07 00 62 00 AA FF 00 00 F1 FF EC FF B3 FF 00 00

F8 FF 0D 00 B3 FF 00 00 0E 00 09 00 B3 FF 00 00 07 00 E8 FF B3 FF 00 00 E8 FF BC FF A2 FF 00 00

FF FF B8 FF A2 FF 00 00 17 00 39 00 A2 FF 00 00 00 00 3D 00 A2 FF 00 00 F7 FF 8B FF A0 FF 00 00

E0 FF 8F FF A0 FF 00 00 20 00 66 00 A0 FF 00 00 09 00 6A 00 A0 FF 00 00 0F 00 24 00 72 FF 00 00

06 00 20 00 ED FD 00 00 F9 FF D5 FF ED FD 00 00 00 00 CE FF 72 FF 00 00 F0 FF D1 FF 72 FF 00 00

00 00 27 00 72 FF 00 00 00 00 FB FF 68 FD 00 00 03 00 E7 FF 8C FF 00 00 0A 00 0B 00 8C FF 00 00

FC FF 0E 00 8C FF 00 00 F5 FF EA FF 8C FF 00 00 F9 FF FC FF D9 FE 00 00 07 00 FA FF D9 FE 00 00

04 00 EB FF 13 FF 00 00 0A 00 07 00 13 FF 00 00 F6 FF EE FF 13 FF 00 00 FB FF 0A 00 13 FF 00 00

03 00 E7 FF 95 FF 00 00 F5 FF EA FF 95 FF 00 00 FC FF 0E 00 95 FF 00 00 0A 00 0B 00 95 FF 00 00

07 00 FA FF ED FD 00 00 F9 FF FC FF ED FD 00 00 08 00 16 00 ED FD 00 00 FE FF DD FF ED FD 00 00

03 00 FA FF 89 FD 00 00 FC FF FC FF 89 FD 00 00 F7 FF DF FF ED FD 00 00 01 00 17 00 ED FD 00 00

01 00 DB FF 7F FF 00 00 F3 FF DE FF 7F FF 00 00 0D 00 17 00 7F FF 00 00 FE FF 1A 00 7F FF 00 00

0D 00 06 00 95 FF 00 00 08 00 EA FF 95 FF 00 00 F2 FF EE FF 95 FF 00 00 F7 FF 0B 00 95 FF 00 00

09 00 F9 FF 13 FF 00 00 09 00 F9 FF 8C FF 00 00 F6 FF FD FF 13 FF 00 00 F6 FF FD FF 8C FF 00 00

09 00 F9 FF 95 FF 00 00 F6 FF FD FF 95 FF 00 00 00 00 20 00 00 00 00 00 33 00 00 00 B0 01 A8 01

90 01 00 00 36 49 74 30 3C 53 76 00 34 47 70 00 A0 01 B0 01 90 01 00 00 2B 3A 5A 30 36 49 74 00

34 47 70 00 48 01 A0 01 90 01 00 00 34 46 6F 30 2B 3A 5A 00 34 47 70 00 A8 01 48 01 90 01 00 00

3C 53 76 30 34 46 6F 00 34 47 70 00 48 01 A8 01 50 01 00 00 34 46 6F 30 3C 53 76 00 36 4B 76 00

D0 01 50 01 A8 01 00 00 35 49 71 30 36 4B 76 00 3C 53 76 00 A0 01 48 01 58 01 00 00 2B 3A 5A 30

34 46 6F 00 31 42 67 00 58 01 E0 01 A0 01 00 00 31 42 67 30 21 39 59 00 2B 3A 5A 00 E0 01 58 01

28 01 00 00 21 39 59 30 31 42 67 00 1E 36 59 00 50 01 D0 01 20 01 00 00 36 4B 76 30 35 49 71 00

35 49 71 00 60 01 D8 01 C0 01 00 00 26 32 4B 30 28 35 50 00 27 33 4D 00 C0 01 40 01 60 01 00 00

27 33 4D 30 25 30 49 00 26 32 4B 00 C8 01 40 01 98 01 00 00 24 2E 44 30 25 30 49 00 25 30 49 00

40 01 C0 01 98 01 00 00 25 30 49 30 27 33 4D 00 25 30 49 00 C0 01 B8 01 98 01 00 00 27 33 4D 30

25 30 48 00 25 30 49 00 B8 01 C8 01 98 01 00 00 25 30 48 30 24 2E 44 00 25 30 49 00 40 01 C8 01

68 01 00 00 25 30 49 30 24 2E 44 00 25 30 47 00 E8 01 68 01 C8 01 00 00 23 2C 41 30 25 30 47 00

24 2E 44 00 68 01 E8 01 30 01 00 00 25 30 47 30 23 2C 41 00 21 28 3C 00 D8 01 60 01 38 01 00 00

28 35 50 30 26 32 4B 00 29 35 50 00 E8 00 F0 00 A0 01 00 00 C8 E1 DC 30 C8 D7 D2 00 46 55 55 00

E8 00 A0 01 E0 01 00 00 C8 E1 DC 30 46 55 55 00 46 55 55 00 A8 01 00 01 D0 01 00 00 46 55 55 30

C8 E1 DC 00 46 55 55 00 00 01 F8 00 08 01 00 00 A4 9F A9 30 A4 9F A9 00 48 46 4B 00 10 01 F0 00

E8 00 00 00 30 2E 35 30 1E 19 23 00 1E 19 23 00 C8 01 10 01 E8 01 00 00 48 56 56 30 7A 85 82 00

48 56 56 00 10 01 C8 01 F0 00 00 00 7A 85 82 30 48 56 56 00 7A 85 82 00 C0 01 08 01 F8 00 00 00

48 56 56 30 7A 85 82 00 7A 85 82 00 08 01 C0 01 D8 01 00 00 7A 85 82 30 48 56 56 00 48 56 56 00

00 01 A8 01 F8 00 00 00 C8 E1 DC 30 46 55 55 00 C8 D7 D2 00 48 01 50 01 10 02 00 00 1F 2D 4C 30

21 30 52 00 1F 2D 4C 00 58 01 48 01 10 02 00 00 1D 29 46 30 1F 2D 4C 00 1F 2D 4C 00 40 01 68 01

20 02 00 00 14 23 34 30 14 22 33 00 14 23 34 00 60 01 40 01 20 02 00 00 14 24 35 30 14 23 34 00

14 23 34 00 F8 01 B0 00 A0 00 00 00 8C 8C 96 30 5F 5F 78 00 2D 2D 3C 00 B0 00 F8 01 48 00 00 00

5F 5F 78 30 8C 8C 96 00 AA AA B4 00 48 00 70 00 B0 00 00 00 AA AA B4 30 54 54 54 00 5F 5F 78 00

F0 01 98 00 B8 00 00 00 8C 8C 96 30 2D 2D 3C 00 5F 5F 78 00 F0 01 B8 00 60 00 00 00 8C 8C 96 30

5F 5F 78 00 8C 8C 96 00 68 00 60 00 B8 00 00 00 64 64 6E 30 8C 8C 96 00 5F 5F 78 00 78 00 50 00

A8 00 00 00 33 33 33 30 51 51 51 00 31 31 31 00 00 02 A8 00 50 00 00 00 33 33 33 30 31 31 31 00

51 51 51 00 00 02 88 00 A8 00 00 00 33 33 33 30 32 32 32 00 31 31 31 00 08 02 C0 00 90 00 00 00

33 33 33 30 2F 2F 2F 00 30 30 30 00 58 00 80 00 C0 00 00 00 2D 2D 2D 30 2F 2F 2F 00 2F 2F 2F 00

C0 00 08 02 58 00 00 00 2F 2F 2F 30 33 33 33 00 2D 2D 2D 00 70 00 48 00 C8 00 00 00 53 03 03 30

BD 08 08 00 B7 08 08 00 60 00 68 00 D8 00 00 00 66 04 04 30 28 02 02 00 1B 01 01 00 50 00 78 00

D0 00 00 00 50 03 03 30 33 02 02 00 55 04 04 00 80 00 58 00 E0 00 00 00 2E 02 02 30 2D 02 02 00

90 01 01 00 38 00 40 00 30 00 00 00 23 23 23 30 51 51 51 00 4A 4A 4A 00 26 00 00 00 D0 01 D8 01

20 01 38 01 4C 66 78 38 2E 39 40 00 58 77 7D 00 2F 39 40 00 E8 01 E0 01 30 01 28 01 25 2B 36 38

22 27 31 00 22 27 32 00 21 25 2D 00 A8 01 B0 01 F8 00 18 01 46 55 55 38 82 8C 87 00 C8 D7 D2 00

C8 E1 DC 00 A0 01 F0 00 B0 01 18 01 46 55 55 38 C8 D7 D2 00 82 8C 87 00 C8 E1 DC 00 D8 01 D0 01

08 01 00 01 38 37 3A 38 83 7F 87 00 39 38 3C 00 83 7F 87 00 10 01 E8 00 E8 01 E0 01 23 1E 28 38

14 0F 14 00 3A 39 40 00 23 1E 28 00 F8 00 18 01 C0 01 B8 01 7A 85 82 38 89 90 8C 00 48 56 56 00

48 56 56 00 18 01 F0 00 B8 01 C8 01 89 90 8C 38 7A 85 82 00 48 56 56 00 48 56 56 00 10 02 18 02

58 01 28 01 1F 2D 4C 38 1F 2C 4B 00 1D 29 46 00 1C 2C 47 00 50 01 20 01 10 02 18 02 21 30 52 38

25 36 5D 00 1F 2D 4C 00 1F 2C 4B 00 20 02 28 02 60 01 38 01 14 23 34 38 14 23 34 00 14 24 35 00

15 25 39 00 68 01 30 01 20 02 28 02 14 22 33 38 12 1F 2D 00 14 23 34 00 14 23 34 00 18 02 30 02

28 01 88 01 7D 6E 2D 38 7D 6E 32 00 19 0F 00 00 1E 14 00 00 30 02 18 02 70 01 20 01 7D 6E 32 38

7D 6E 2D 00 5B 4C 2B 00 6B 5D 39 00 20 01 38 01 70 01 78 01 6B 5D 39 38 40 2E 12 00 5B 4C 2B 00

3F 2D 11 00 28 02 38 02 38 01 78 01 3D 2A 0F 38 3D 2A 0F 00 40 2E 12 00 3F 2D 11 00 38 02 28 02

80 01 30 01 3D 2A 0F 38 3D 2A 0F 00 1E 0F 00 00 23 14 0A 00 30 01 28 01 80 01 88 01 23 14 0A 38

19 0F 00 00 1E 0F 00 00 1E 14 00 00 F0 01 F8 01 98 00 A0 00 23 23 41 38 23 23 41 00 0F 0F 0F 00

19 19 19 00 00 02 F8 01 08 02 F0 01 11 11 11 38 35 35 35 00 11 11 11 00 35 35 35 00 A0 00 88 00

98 00 90 00 19 19 19 38 11 11 11 00 0F 0F 0F 00 10 10 10 00 00 02 08 02 88 00 90 00 14 14 28 38

14 14 28 00 14 14 28 00 19 19 3C 00 F8 01 00 02 48 00 50 00 3F 3F 3F 38 15 15 15 00 4E 4E 4E 00

21 21 21 00 D0 00 C8 00 50 00 48 00 23 23 23 38 4C 4C 4C 00 21 21 21 00 4E 4E 4E 00 C8 00 D0 00

70 00 78 00 4C 4C 4C 38 23 23 23 00 22 22 22 00 15 15 15 00 08 02 F0 01 58 00 60 00 15 15 15 38

3F 3F 3F 00 13 13 13 00 2A 2A 2A 00 58 00 60 00 E0 00 D8 00 13 13 13 38 2A 2A 2A 00 0B 0B 0B 00

0B 0B 0B 00 E0 00 D8 00 80 00 68 00 0B 0B 0B 38 0B 0B 0B 00 13 13 13 00 11 11 11 00 B8 00 C0 00

68 00 80 00 1C 1C 1C 38 13 13 13 00 11 11 11 00 13 13 13 00 98 00 90 00 B8 00 C0 00 12 12 12 38

14 14 14 00 1C 1C 1C 00 13 13 13 00 B0 00 A8 00 A0 00 88 00 20 20 20 38 14 14 14 00 1E 1E 1E 00

14 14 14 00 A8 00 B0 00 78 00 70 00 14 14 14 38 20 20 20 00 15 15 15 00 22 22 22 00 28 00 00 00

38 00 40 00 1B 1B 1B 38 AA BE B9 00 23 23 23 00 8C 96 91 00 00 00 10 00 40 00 30 00 AA BE B9 38

7C 7C 7C 00 8C 96 91 00 4A 4A 4A 00 10 00 28 00 30 00 38 00 7C 7C 7C 38 1B 1B 1B 00 4A 4A 4A 00

23 23 23 00 00 00 08 00 10 00 18 00 19 2C 23 38 1D 32 27 00 17 29 21 00 1C 30 26 00 28 00 20 00

00 00 08 00 04 0E 0F 38 05 10 10 00 19 2C 23 00 1D 32 27 00 10 00 18 00 28 00 20 00 17 29 21 38

1C 30 26 00 04 0E 0F 00 05 10 10 00

  
  
3rd Weapon Bone Data \[at offset 0x0000E5A8\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 78 02 00 00 F4 FF F9 FF C7 FF 00 00 03 00 03 00 C7 FF 00 00

0F 00 F4 FF C7 FF 00 00 FF FF E8 FF C7 FF 00 00 12 00 E9 FF 8F 00 00 00 FD FF DA FF 8F 00 00 00

ED FF F0 FF 8F 00 00 00 03 00 FF FF 8F 00 00 00 12 00 F2 FF 72 00 00 00 0F 00 F5 FF DD FF 00 00

04 00 06 00 72 00 00 00 04 00 05 00 DD FF 00 00 FF FF E4 FF 72 00 00 00 00 00 EA FF DD FF 00 00

F0 FF F9 FF 72 00 00 00 F4 FF FA FF DD FF 00 00 12 00 F3 FF C7 FF 00 00 12 00 F3 FF BE FF 00 00

FF FF E5 FF BE FF 00 00 FF FF E5 FF C7 FF 00 00 F0 FF F9 FF C7 FF 00 00 F0 FF F9 FF BE FF 00 00

04 00 07 00 BE FF 00 00 04 00 07 00 C7 FF 00 00 16 00 F2 FF BE FF 00 00 16 00 F2 FF B2 FF 00 00

FE FF E1 FF B2 FF 00 00 FE FF E1 FF BE FF 00 00 ED FF FA FF BE FF 00 00 ED FF FA FF B2 FF 00 00

05 00 0A 00 B2 FF 00 00 05 00 0A 00 BE FF 00 00 23 00 1F 00 B2 FF 00 00 23 00 1F 00 70 FF 00 00

12 00 C3 FF 70 FF 00 00 12 00 C3 FF B2 FF 00 00 E0 FF CC FF B2 FF 00 00 E0 FF CC FF 70 FF 00 00

F1 FF 28 00 70 FF 00 00 F1 FF 28 00 B2 FF 00 00 15 00 0E 00 70 FF 00 00 18 00 21 00 E2 FD 00 00

00 00 9E FF E2 FD 00 00 08 00 CC FF 70 FF 00 00 EC FF D1 FF 70 FF 00 00 E4 FF A4 FF E2 FD 00 00

FC FF 26 00 E2 FD 00 00 F8 FF 13 00 70 FF 00 00 FC FF 25 00 C1 FE 00 00 18 00 20 00 C1 FE 00 00

05 00 B8 FF 9E FE 00 00 E8 FF BE FF 9E FE 00 00 0D 00 35 00 E2 FD 00 00 09 00 1F 00 70 FF 00 00

0C 00 30 00 C2 FE 00 00 0E 00 EB FF E2 FD 00 00 F2 FF F0 FF E2 FD 00 00 00 00 EA FF 42 00 00 00

12 00 F8 FF 42 00 00 00 05 00 0A 00 42 00 00 00 F3 FF FE FF 42 00 00 00 12 00 C7 FF AD FF 00 00

22 00 1B 00 AD FF 00 00 22 00 1B 00 74 FF 00 00 12 00 C7 FF 74 FF 00 00 F1 FF 24 00 AD FF 00 00

E1 FF D1 FF AD FF 00 00 E1 FF D1 FF 74 FF 00 00 F1 FF 24 00 74 FF 00 00 0E 00 E9 FF 70 FF 00 00

11 00 FD FF 70 FF 00 00 F5 FF 01 00 70 FF 00 00 F1 FF EE FF 70 FF 00 00 0F 00 F3 FF F1 FE 00 00

F3 FF F8 FF F1 FE 00 00 F1 FF EE FF 07 FF 00 00 F5 FF 01 00 07 FF 00 00 0E 00 E9 FF 07 FF 00 00

11 00 FD FF 07 FF 00 00 00 00 20 00 00 00 00 00 1B 00 00 00 88 01 B0 01 48 01 00 00 46 4B 4B 30

9B A0 A0 00 4B 50 50 00 70 01 48 01 A0 01 00 00 37 3F 3F 30 2F 3C 3C 00 21 2A 2A 00 B0 01 80 01

70 01 00 00 4B 50 50 30 1D 22 2B 00 23 29 34 00 48 01 B0 01 A0 01 00 00 4B 50 50 30 9B A0 A0 00

9B A0 A0 00 B0 01 70 01 A0 01 00 00 4B 50 50 30 23 29 34 00 41 46 46 00 B8 01 88 01 48 01 00 00

2D 37 37 30 82 8C 8C 00 78 82 82 00 90 01 B8 01 50 01 00 00 18 19 19 30 2D 37 37 00 18 19 19 00

68 02 58 01 28 02 00 00 64 69 69 30 55 5A 5A 00 91 9B 9B 00 C0 01 98 01 68 01 00 00 2D 32 32 30

14 19 19 00 14 19 19 00 80 01 C0 01 70 01 00 00 55 5A 5A 30 2D 32 32 00 55 5E 5E 00 60 02 78 01

38 02 00 00 50 55 55 30 54 5D 5D 00 50 55 55 00 68 02 48 02 90 01 00 00 64 69 69 30 64 69 69 00

18 19 19 00 40 01 70 02 30 02 00 00 82 8C 8C 30 64 69 69 00 91 9B 9B 00 90 01 88 01 B8 01 00 00

18 19 19 30 82 8C 8C 00 2D 37 37 00 70 02 40 01 88 01 00 00 64 69 69 30 82 8C 8C 00 82 8C 8C 00

58 01 68 02 90 01 00 00 55 5A 5A 30 64 69 69 00 18 19 19 00 88 01 48 02 70 02 00 00 82 8C 8C 30

64 69 69 00 64 69 69 00 90 01 48 02 88 01 00 00 18 19 19 30 64 69 69 00 82 8C 8C 00 98 01 50 02

58 02 00 00 14 19 19 30 50 55 55 00 50 55 55 00 60 01 58 02 40 02 00 00 4B 50 50 30 50 55 55 00

50 55 55 00 80 01 60 02 50 02 00 00 55 5A 5A 30 50 55 55 00 50 55 55 00 80 01 50 02 C0 01 00 00

55 5A 5A 30 50 55 55 00 2D 32 32 00 58 02 60 01 98 01 00 00 50 55 55 30 4B 50 50 00 14 19 19 00

50 02 98 01 C0 01 00 00 50 55 55 30 14 19 19 00 2D 32 32 00 78 01 60 02 80 01 00 00 54 5D 5D 30

50 55 55 00 55 5A 5A 00 68 02 70 02 48 02 00 00 38 05 05 30 38 05 05 00 38 05 05 00 60 02 58 02

50 02 00 00 27 02 02 30 27 02 02 00 27 02 02 00 31 00 00 00 60 00 70 00 28 00 30 00 5F 36 1A 38

19 0E 06 00 3F 23 11 00 1B 0F 07 00 70 00 50 00 30 00 38 00 19 0E 06 38 0E 07 03 00 1B 0F 07 00

14 0B 05 00 40 00 60 00 20 00 28 00 24 1A 0C 38 33 25 11 00 1B 13 08 00 22 18 0B 00 50 00 40 00

38 00 20 00 0E 07 03 38 43 26 12 00 14 0B 05 00 32 1C 0D 00 28 00 30 00 20 00 38 00 4A 24 12 38

20 10 08 00 3B 1D 0E 00 18 0C 06 00 68 00 48 00 18 00 10 00 2F 22 10 38 25 1B 0D 00 36 27 13 00

2E 21 0F 00 48 00 58 00 10 00 08 00 46 27 13 38 0E 07 03 00 55 30 17 00 0F 08 03 00 78 00 68 00

00 00 18 00 19 0E 06 38 56 31 18 00 1B 0F 07 00 64 39 1C 00 58 00 78 00 08 00 00 00 0E 07 03 38

19 0E 06 00 0F 08 03 00 1B 0F 07 00 E0 01 C8 01 78 00 68 00 32 28 2F 38 81 74 64 00 32 28 2F 00

7C 70 61 00 70 00 60 00 E0 01 C8 01 32 27 2E 38 87 7A 68 00 32 28 2F 00 81 74 64 00 50 00 70 00

D8 01 E0 01 24 1A 25 38 32 27 2E 00 24 1A 25 00 32 28 2F 00 D8 01 E0 01 58 00 78 00 24 1A 25 38

32 28 2F 00 24 1A 25 00 32 28 2F 00 40 00 50 00 D0 01 D8 01 64 59 51 38 24 1A 25 00 67 5B 52 00

24 1A 25 00 D0 01 D8 01 48 00 58 00 67 5B 52 38 24 1A 25 00 69 5C 54 00 24 1A 25 00 60 00 40 00

C8 01 D0 01 87 7A 68 38 64 59 51 00 81 74 64 00 67 5B 52 00 C8 01 D0 01 68 00 48 00 81 74 64 38

67 5B 52 00 7C 70 61 00 69 5C 54 00 F8 00 C0 00 E0 00 D8 00 0F 0C 00 38 21 1C 00 00 15 11 00 00

2B 23 00 00 E0 00 E8 00 F8 00 F0 00 15 11 00 38 15 11 00 00 46 37 00 00 0B 09 00 00 F8 00 F0 00

C0 00 C8 00 46 37 00 38 0B 09 00 00 96 87 3C 00 43 36 00 00 C0 00 C8 00 D8 00 D0 00 96 87 3C 38

43 36 00 00 5F 5A 37 00 19 14 00 00 D8 00 D0 00 E0 00 E8 00 5F 5A 37 38 19 14 00 00 15 11 00 00

15 11 00 00 A0 00 B8 00 98 00 80 00 15 11 00 38 0F 0C 00 00 2B 23 00 00 21 1C 00 00 98 00 90 00

A0 00 A8 00 5F 5A 37 38 19 14 00 00 15 11 00 00 15 11 00 00 A0 00 A8 00 B8 00 B0 00 15 11 00 38

15 11 00 00 4B 41 00 00 0B 09 00 00 B8 00 B0 00 80 00 88 00 4B 41 00 38 0B 09 00 00 96 87 3C 00

43 36 00 00 80 00 88 00 98 00 90 00 96 87 3C 38 43 36 00 00 5F 5A 37 00 19 14 00 00 F0 01 F8 01

E8 01 00 02 21 21 21 38 21 21 21 00 21 21 21 00 21 21 21 00 18 01 10 01 20 01 28 01 3C 46 46 38

28 2D 2D 00 3C 46 46 00 28 2D 2D 00 38 01 30 01 00 01 08 01 32 37 37 38 1E 28 28 00 32 37 37 00

1E 28 28 00 10 02 18 02 08 02 20 02 0C 0C 0C 38 0C 0C 0C 00 0C 0C 0C 00 0C 0C 0C 00 38 01 00 01

20 01 18 01 0A 0A 0A 38 09 09 09 00 0E 0E 0E 00 20 20 20 00 10 01 08 01 28 01 30 01 33 33 33 38

3C 46 46 00 1A 1A 1A 00 3C 46 46 00 08 01 10 01 F8 01 00 02 64 73 6E 38 64 73 6E 00 32 41 3C 00

32 41 3C 00 10 01 18 01 00 02 E8 01 64 73 6E 38 64 73 6E 00 32 41 3C 00 32 41 3C 00 00 01 08 01

F0 01 F8 01 64 73 6E 38 64 73 6E 00 32 41 3C 00 32 41 3C 00 18 01 00 01 E8 01 F0 01 64 73 6E 38

64 73 6E 00 32 41 3C 00 32 41 3C 00 30 01 38 01 20 02 08 02 50 64 64 38 50 64 64 00 14 23 23 00

14 23 23 00 30 01 20 02 28 01 18 02 50 64 64 38 14 23 23 00 50 64 64 00 14 23 23 00 20 01 28 01

10 02 18 02 50 64 64 38 50 64 64 00 14 23 23 00 14 23 23 00 38 01 20 01 08 02 10 02 50 64 64 38

50 64 64 00 14 23 23 00 14 23 23 00 A8 01 B0 01 40 01 88 01 1B 20 29 38 9B A0 A0 00 1D 22 2B 00

46 4B 4B 00 78 01 80 01 A8 01 B0 01 22 28 33 38 1D 22 2B 00 1B 20 29 00 4B 50 50 00 58 01 90 01

60 01 98 01 35 38 37 38 4F 53 51 00 17 19 18 00 19 1A 19 00 98 01 90 01 68 01 50 01 19 1A 19 38

4F 53 51 00 2C 2F 2D 00 58 5E 5B 00 68 01 50 01 C0 01 B8 01 44 4C 4C 38 86 8B 8B 00 23 2C 2C 00

63 69 69 00 48 01 70 01 B8 01 C0 01 4B 52 52 38 20 29 29 00 63 69 69 00 23 2C 2C 00 70 02 68 02

30 02 28 02 38 05 05 38 38 05 05 00 50 02 02 00 50 02 02 00 38 02 40 02 60 02 58 02 27 02 02 38

27 02 02 00 27 02 02 00 27 02 02 00

  
  
4th Weapon Bone Data \[at offset 0x0000EEF4\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 80 02 00 00 07 00 1E 00 59 FF 00 00 07 00 1E 00 12 FE 00 00

FA FF D3 FF 12 FE 00 00 03 00 D1 FF 59 FF 00 00 F1 FF D5 FF 59 FF 00 00 FE FF E5 FF 62 FD 00 00

FD FF E0 FF CC FD 00 00 04 00 0E 00 D5 FD 00 00 06 00 E2 FF 9F FF 00 00 0E 00 0C 00 9F FF 00 00

FC FF 0F 00 9F FF 00 00 F4 FF E5 FF 9F FF 00 00 F3 FF E0 FF 71 FF 00 00 05 00 DD FF 71 FF 00 00

FD FF 14 00 71 FF 00 00 0F 00 11 00 71 FF 00 00 0E 00 0C 00 12 FE 00 00 FC FF 0F 00 12 FE 00 00

F6 FF F7 FF C7 FD 00 00 08 00 F3 FF C7 FD 00 00 03 00 D1 FF 2F FE 00 00 F1 FF D5 FF 2F FE 00 00

08 00 EF FF EF FD 00 00 F6 FF F2 FF EF FD 00 00 06 00 E3 FF 10 FE 00 00 F4 FF E7 FF 10 FE 00 00

0B 00 01 00 E6 FD 00 00 FA FF 05 00 E6 FD 00 00 03 00 D1 FF BB FE 00 00 F1 FF D5 FF BB FE 00 00

F2 FF DB FF D5 FE 00 00 F1 FF D5 FF EF FE 00 00 F2 FF DB FF 0A FF 00 00 F1 FF D5 FF 24 FF 00 00

F2 FF DB FF 3E FF 00 00 04 00 D8 FF 3E FF 00 00 03 00 D1 FF 24 FF 00 00 04 00 D8 FF 0A FF 00 00

03 00 D1 FF EF FE 00 00 04 00 D8 FF D5 FE 00 00 0E 00 0C 00 A7 FF 00 00 06 00 E2 FF A7 FF 00 00

F4 FF E5 FF A7 FF 00 00 FC FF 0F 00 A7 FF 00 00 04 00 E9 FF BE FF 00 00 F8 FF EB FF BE FF 00 00

FD FF 08 00 BE FF 00 00 0A 00 06 00 BE FF 00 00 0A 00 06 00 B0 00 00 00 04 00 E9 FF B0 00 00 00

F8 FF EB FF B0 00 00 00 FD FF 08 00 B0 00 00 00 09 00 00 00 BE FF 00 00 05 00 EE FF BE FF 00 00

09 00 00 00 B0 00 00 00 05 00 EE FF B0 00 00 00 F9 FF F1 FF B0 00 00 00 FC FF 03 00 B0 00 00 00

F9 FF F1 FF BE FF 00 00 FC FF 03 00 BE FF 00 00 05 00 DF FF B7 FF 00 00 F3 FF E2 FF B7 FF 00 00

FD FF 12 00 B7 FF 00 00 0E 00 0F 00 B7 FF 00 00 0E 00 0F 00 BE FF 00 00 05 00 DF FF BE FF 00 00

F3 FF E2 FF BE FF 00 00 FD FF 12 00 BE FF 00 00 0E 00 CA FF A7 FF 00 00 E4 FF D3 FF A7 FF 00 00

F9 FF 43 00 A7 FF 00 00 23 00 3B 00 A7 FF 00 00 22 00 36 00 B7 FF 00 00 0E 00 CA FF B7 FF 00 00

E4 FF D3 FF B7 FF 00 00 F8 FF 3E 00 B7 FF 00 00 FB FF 4F 00 CF FF 00 00 FD FF 58 00 C4 FF 00 00

27 00 50 00 C4 FF 00 00 26 00 47 00 CF FF 00 00 00 00 20 00 00 00 00 00 32 00 00 00 08 00 78 00

00 00 00 00 E0 F4 EF 30 39 3E 3C 00 A8 B7 B4 00 80 00 48 00 78 00 00 00 15 17 17 30 23 29 28 00

39 3E 3C 00 D8 00 08 00 88 00 00 00 16 18 17 30 79 84 82 00 16 18 17 00 38 00 08 00 D8 00 00 00

79 84 82 30 79 84 82 00 16 18 17 00 38 00 D8 00 90 00 00 00 79 84 82 30 16 18 17 00 16 18 17 00

38 00 98 00 D0 00 00 00 E0 F4 EF 30 15 17 17 00 15 17 17 00 D0 00 08 00 38 00 00 00 15 17 17 30

E0 F4 EF 00 E0 F4 EF 00 08 00 D0 00 80 00 00 00 E0 F4 EF 30 15 17 17 00 15 17 17 00 B8 00 30 00

90 00 00 00 2F 39 37 30 A1 B0 AC 00 2C 34 34 00 10 00 30 00 B8 00 00 00 A1 B0 AC 30 A1 B0 AC 00

2F 39 37 00 B0 00 30 00 10 00 00 00 BD CE CA 30 72 7C 79 00 D5 E8 E3 00 98 00 30 00 B0 00 00 00

BD CE CA 30 72 7C 79 00 BD CE CA 00 30 00 98 00 28 00 00 00 72 7C 79 30 BD CE CA 00 BF D0 CC 00

98 00 38 00 28 00 00 00 15 17 17 30 E0 F4 EF 00 A7 C6 C2 00 38 00 90 00 28 00 00 00 79 84 82 30

16 18 17 00 78 8F 8C 00 90 00 30 00 28 00 00 00 2C 34 34 30 A1 B0 AC 00 78 8F 8C 00 88 00 70 00

50 00 00 00 16 18 17 30 1C 21 21 00 16 18 17 00 08 00 70 00 88 00 00 00 79 84 82 30 1C 21 21 00

16 18 17 00 78 00 08 00 80 00 00 00 39 3E 3C 30 E0 F4 EF 00 15 17 17 00 78 00 70 00 00 00 00 00

23 29 28 30 28 2F 2E 00 23 29 28 00 70 00 08 00 00 00 00 00 1C 21 21 30 79 84 82 00 79 84 82 00

C8 00 10 00 B8 00 00 00 2F 38 37 30 A1 B0 AC 00 2F 39 37 00 C8 00 A8 00 10 00 00 00 2F 38 37 30

3E 49 48 00 A1 B0 AC 00 A0 00 C0 00 10 00 00 00 E0 F4 EF 30 BD CE CA 00 D5 E8 E3 00 10 00 C0 00

B0 00 00 00 D5 E8 E3 30 BD CE CA 00 BD CE CA 00 A0 00 10 00 A8 00 00 00 61 70 70 30 63 72 72 00

92 A8 A8 00 38 01 80 00 A0 00 00 00 A8 B7 B4 30 72 7C 79 00 72 7C 79 00 80 00 C0 00 A0 00 00 00

72 7C 79 30 72 7C 79 00 72 7C 79 00 B0 00 D0 00 98 00 00 00 72 7C 79 30 72 7C 79 00 72 7C 79 00

80 00 38 01 48 00 00 00 72 7C 79 30 A8 B7 B4 00 69 72 70 00 28 01 38 01 30 01 00 00 A8 B7 B4 30

A8 B7 B4 00 A8 B7 B4 00 18 01 28 01 20 01 00 00 A8 B7 B4 30 A8 B7 B4 00 A8 B7 B4 00 10 01 60 00

20 00 00 00 46 53 50 30 34 3E 3B 00 46 53 50 00 00 01 10 01 08 01 00 00 46 53 50 30 46 53 50 00

46 53 50 00 F0 00 00 01 F8 00 00 00 46 53 50 30 46 53 50 00 46 53 50 00 28 01 18 01 48 00 00 00

A8 B7 B4 30 A8 B7 B4 00 69 72 70 00 68 00 48 00 18 01 00 00 A8 B7 B4 30 69 72 70 00 A8 B7 B4 00

38 01 28 01 48 00 00 00 A8 B7 B4 30 A8 B7 B4 00 69 72 70 00 48 00 68 00 40 00 00 00 69 72 70 30

A8 B7 B4 00 69 72 70 00 68 00 18 01 18 00 00 00 A8 B7 B4 30 A8 B7 B4 00 A8 B7 B4 00 38 01 A0 00

E0 00 00 00 A8 B7 B4 30 A8 B7 B4 00 A8 B7 B4 00 A8 00 F0 00 E8 00 00 00 46 53 50 30 46 53 50 00

22 2C 2A 00 F0 00 88 00 50 00 00 00 46 53 50 30 46 53 50 00 34 3E 3B 00 10 01 00 01 50 00 00 00

46 53 50 30 46 53 50 00 34 3E 3B 00 60 00 50 00 58 00 00 00 34 3E 3B 30 34 3E 3B 00 34 3E 3B 00

50 00 60 00 10 01 00 00 34 3E 3B 30 34 3E 3B 00 46 53 50 00 00 01 F0 00 50 00 00 00 46 53 50 30

46 53 50 00 34 3E 3B 00 F0 00 A8 00 88 00 00 00 46 53 50 30 46 53 50 00 46 53 50 00 A8 00 C8 00

88 00 00 00 46 53 50 30 46 53 50 00 46 53 50 00 D8 00 B8 00 90 00 00 00 46 53 50 30 46 53 50 00

46 53 50 00 2A 00 00 00 B0 01 A0 01 B8 01 A8 01 41 0A 0A 38 2D 05 05 00 41 0A 0A 00 2D 05 05 00

C8 01 B0 01 C0 01 B8 01 17 01 01 38 1C 01 01 00 17 01 01 00 1C 01 01 00 D8 01 C8 01 D0 01 C0 01

32 05 05 38 46 05 05 00 32 05 05 00 46 05 05 00 60 01 68 01 88 01 90 01 16 16 16 38 0B 0B 0B 00

0D 0D 0D 00 06 06 06 00 B8 01 A8 01 88 01 60 01 06 06 06 38 10 10 10 00 4E 4E 4E 00 16 16 16 00

A0 01 B0 01 78 01 80 01 10 10 10 38 06 06 06 00 34 34 34 00 6F 6F 6F 00 D0 01 C0 01 68 01 90 01

05 05 05 38 05 05 05 00 0B 0B 0B 00 59 59 59 00 C8 01 D8 01 98 01 70 01 05 05 05 38 05 05 05 00

55 55 55 00 04 04 04 00 70 01 78 01 98 01 80 01 04 04 04 38 07 07 07 00 04 04 04 00 04 04 04 00

C0 01 B8 01 90 01 88 01 05 05 05 38 06 06 06 00 06 06 06 00 0D 0D 0D 00 B0 01 C8 01 80 01 98 01

06 06 06 38 05 05 05 00 04 04 04 00 04 04 04 00 F8 01 E0 01 00 02 08 02 38 38 38 38 38 38 38 00

8A 8A 8A 00 8A 8A 8A 00 E0 01 E8 01 08 02 10 02 53 53 53 38 2A 2A 2A 00 33 33 33 00 16 16 16 00

48 00 40 00 40 01 48 01 0B 0B 0B 38 49 49 49 00 0E 0E 0E 00 33 33 33 00 58 00 50 00 50 01 58 01

18 18 18 38 0C 0C 0C 00 16 16 16 00 10 10 10 00 50 00 48 00 58 01 40 01 0C 0C 0C 38 0B 0B 0B 00

10 10 10 00 0E 0E 0E 00 40 00 58 00 48 01 50 01 49 49 49 38 18 18 18 00 33 33 33 00 16 16 16 00

E8 01 F0 01 10 02 18 02 2E 2E 2E 38 2E 2E 2E 00 2A 2A 2A 00 59 59 59 00 F0 01 F8 01 18 02 00 02

10 10 10 38 19 19 19 00 5C 5C 5C 00 6D 6D 6D 00 08 02 10 02 00 02 18 02 33 33 33 38 16 16 16 00

0E 0E 0E 00 10 10 10 00 38 02 40 02 70 02 78 02 12 1F 1B 38 1D 32 2B 00 11 1C 18 00 24 40 37 00

30 02 38 02 68 02 70 02 0A 0F 0D 38 0E 17 14 00 1A 2D 27 00 1A 2D 27 00 38 02 20 02 40 02 48 02

12 1F 1B 38 23 3D 34 00 1E 34 2C 00 1E 34 2C 00 28 02 20 02 30 02 38 02 13 20 1C 38 2F 52 46 00

0A 0F 0D 00 21 3A 32 00 40 02 58 02 78 02 60 02 15 23 1E 38 0B 11 0F 00 0A 0F 0D 00 0B 11 0F 00

48 02 50 02 40 02 58 02 16 26 21 38 0B 12 10 00 15 23 1E 00 0B 11 0F 00 68 02 70 02 60 02 78 02

06 09 08 38 06 09 08 00 1E 34 2C 00 1F 36 2E 00 28 02 30 02 50 02 58 02 19 2B 25 38 10 1B 17 00

18 29 23 00 22 3C 33 00 58 02 30 02 60 02 68 02 22 3C 33 38 10 1B 17 00 22 3C 33 00 0D 15 12 00

20 02 28 02 48 02 50 02 12 1F 1B 38 13 20 1C 00 16 26 21 00 0B 12 10 00 70 00 78 00 50 00 48 00

28 2F 2E 38 23 29 28 00 25 2C 2C 00 23 29 28 00 D0 00 B0 00 80 00 C0 00 72 7C 79 38 72 7C 79 00

72 7C 79 00 72 7C 79 00 38 01 F0 00 30 01 F8 00 81 9A 98 38 32 3B 3A 00 82 9C 9A 00 3E 49 49 00

F0 00 38 01 E8 00 E0 00 26 2C 2C 38 62 75 73 00 29 31 2F 00 60 74 72 00 00 01 28 01 F8 00 30 01

26 2C 2C 38 62 75 73 00 2F 37 37 00 63 76 75 00 28 01 00 01 20 01 08 01 81 9A 98 38 32 3B 3A 00

82 9C 9A 00 3E 49 49 00 10 01 18 01 08 01 20 01 26 2C 2C 38 62 75 73 00 2F 37 37 00 63 76 75 00

18 01 10 01 18 00 20 00 81 9A 97 38 32 3B 3A 00 7F 99 96 00 3C 47 47 00 60 00 68 00 20 00 18 00

26 2D 2C 38 5C 6E 6C 00 2D 36 36 00 60 74 72 00 E8 00 E0 00 A8 00 A0 00 2E 35 35 38 6D 7E 7E 00

92 A8 A8 00 61 70 70 00 58 00 40 00 60 00 68 00 26 2E 2D 38 61 74 72 00 26 2D 2C 00 5C 6E 6C 00

C8 00 B8 00 88 00 D8 00 46 53 50 38 46 53 50 00 46 53 50 00 46 53 50 00

  
  
5th Weapon Bone Data \[at offset 0x0000F96C\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 E0 02 00 00 1A 00 1E 00 CA FF 00 00 F8 FF 24 00 CA FF 00 00

01 00 59 00 A5 FF 00 00 23 00 52 00 A5 FF 00 00 1C 00 3C 00 92 FF 00 00 15 00 15 00 AE FF 00 00

F9 FF 1A 00 AE FF 00 00 E7 FF B5 FF 92 FF 00 00 EE FF DC FF AE FF 00 00 09 00 D7 FF AE FF 00 00

02 00 B0 FF 92 FF 00 00 01 00 98 FF A5 FF 00 00 DF FF 9F FF A5 FF 00 00 E9 FF D3 FF CA FF 00 00

0B 00 CD FF CA FF 00 00 0F 00 F6 FF B9 FF 00 00 0C 00 E7 FF B0 FF 00 00 0C 00 E7 FF 9E FF 00 00

0F 00 F6 FF 95 FF 00 00 12 00 05 00 9E FF 00 00 12 00 05 00 B0 FF 00 00 15 00 F5 FF A7 FF 00 00

04 00 05 00 B9 FF 00 00 0B 00 F7 FF B9 FF 00 00 FF FF EB FF B9 FF 00 00 F8 FF FA FF B9 FF 00 00

F8 FF FA FF A4 00 00 00 04 00 05 00 A4 00 00 00 0B 00 F7 FF A4 00 00 00 FF FF EB FF A4 00 00 00

F8 FF FA FF AD 00 00 00 04 00 05 00 AD 00 00 00 0B 00 F7 FF AD 00 00 00 FF FF EB FF AD 00 00 00

F1 FF EC FF 95 FF 00 00 0C 00 E7 FF 95 FF 00 00 05 00 C1 FF 76 FF 00 00 EA FF C6 FF 76 FF 00 00

05 00 C1 FF 7F FF 00 00 EA FF C6 FF 7F FF 00 00 F1 FF EC FF 9E FF 00 00 0C 00 E7 FF 9E FF 00 00

00 00 A6 FF 7F FF 00 00 E5 FF AB FF 7F FF 00 00 F1 FF EC FF B9 FF 00 00 0C 00 E7 FF B9 FF 00 00

02 00 B0 FF 92 FF 00 00 E7 FF B5 FF 92 FF 00 00 FE FF 96 FF 7F FF 00 00 FE FF 96 FF 76 FF 00 00

E2 FF 9B FF 76 FF 00 00 E2 FF 9B FF 7F FF 00 00 05 00 5B 00 7F FF 00 00 05 00 5B 00 76 FF 00 00

21 00 56 00 76 FF 00 00 21 00 56 00 7F FF 00 00 00 00 41 00 92 FF 00 00 1C 00 3C 00 92 FF 00 00

12 00 05 00 B9 FF 00 00 F7 FF 0A 00 B9 FF 00 00 02 00 4B 00 7F FF 00 00 1E 00 46 00 7F FF 00 00

12 00 05 00 9E FF 00 00 F7 FF 0A 00 9E FF 00 00 FE FF 30 00 7F FF 00 00 19 00 2B 00 7F FF 00 00

FE FF 30 00 76 FF 00 00 19 00 2B 00 76 FF 00 00 12 00 05 00 95 FF 00 00 F7 FF 0A 00 95 FF 00 00

07 00 1A 00 51 FF 00 00 07 00 1A 00 7A FD 00 00 01 00 F9 FF 30 FD 00 00 0D 00 06 00 51 FF 00 00

FB FF 09 00 51 FF 00 00 08 00 F8 FF 85 FD 00 00 FB FF FA FF 85 FD 00 00 0D 00 05 00 BD FD 00 00

FB FF 08 00 BD FD 00 00 FB FF 09 00 95 FF 00 00 0A 00 2A 00 78 FF 00 00 0D 00 06 00 95 FF 00 00

07 00 E8 FF 95 FF 00 00 F9 FF C7 FF 78 FF 00 00 F6 FF EB FF 95 FF 00 00 F6 FF EC FF BD FD 00 00

07 00 E9 FF BD FD 00 00 F6 FF EB FF 51 FF 00 00 07 00 E8 FF 51 FF 00 00 FC FF D7 FF 7A FD 00 00

FC FF D7 FF 51 FF 00 00 00 00 41 00 92 FF 00 00 00 00 20 00 00 00 00 00 30 00 00 00 78 00 A8 00

80 00 00 00 0A 23 1E 30 50 9B 8C 00 3C 69 5C 00 80 00 A8 00 88 00 00 00 3C 69 5C 30 50 9B 8C 00

A0 D2 C8 00 88 00 A8 00 90 00 00 00 A0 D2 C8 30 50 9B 8C 00 40 70 62 00 90 00 A8 00 98 00 00 00

40 70 62 30 50 9B 8C 00 0F 1E 18 00 98 00 A8 00 A0 00 00 00 0F 1E 18 30 50 9B 8C 00 0F 32 23 00

A0 00 A8 00 78 00 00 00 0F 32 23 30 50 9B 8C 00 0A 23 1E 00 B0 02 68 02 58 02 00 00 54 54 64 30

4A 4A 5B 00 50 50 60 00 70 02 A8 02 60 02 00 00 69 69 78 30 69 69 78 00 48 48 5A 00 C8 02 58 02

40 02 00 00 D7 C3 91 30 50 3C 19 00 D7 C3 91 00 38 02 58 02 68 02 00 00 96 82 46 30 41 2D 14 00

41 2D 14 00 58 02 38 02 40 02 00 00 41 2D 14 30 96 82 46 00 96 82 46 00 D0 02 B0 02 C8 02 00 00

91 78 32 30 50 3C 19 00 D7 C3 91 00 58 02 C8 02 B0 02 00 00 50 3C 19 30 D7 C3 91 00 50 3C 19 00

68 02 30 02 38 02 00 00 41 2D 14 30 7D 6E 3C 00 96 82 46 00 30 02 68 02 48 02 00 00 7D 6E 3C 30

41 2D 14 00 41 2D 14 00 30 02 88 02 80 02 00 00 7D 6E 3C 30 29 1B 06 00 41 2D 14 00 88 02 30 02

48 02 00 00 29 1B 06 30 7D 6E 3C 00 41 2D 14 00 90 02 D0 02 98 02 00 00 3C 28 0A 30 91 78 32 00

50 3C 19 00 D0 02 90 02 C0 02 00 00 91 78 32 30 3C 28 0A 00 50 3C 19 00 B0 02 D0 02 C0 02 00 00

50 3C 19 30 91 78 32 00 50 3C 19 00 D0 02 A8 02 B8 02 00 00 99 94 64 30 47 3A 1E 00 48 3B 1E 00

D0 02 B8 02 A0 02 00 00 99 94 64 30 48 3B 1E 00 48 3B 1E 00 D0 02 A0 02 98 02 00 00 99 94 64 30

48 3B 1E 00 96 91 60 00 50 02 30 02 78 02 00 00 41 33 18 30 5E 4D 20 00 43 36 1B 00 78 02 30 02

80 02 00 00 43 36 1B 30 5E 4D 20 00 5E 4D 20 00 70 02 30 02 50 02 00 00 42 34 19 30 5E 4D 20 00

41 33 18 00 30 02 70 02 38 02 00 00 5E 4D 20 30 42 34 19 00 5E 4D 20 00 38 02 70 02 60 02 00 00

5E 4D 20 30 42 34 19 00 44 37 1B 00 A8 02 C8 02 60 02 00 00 47 3A 1E 30 A3 9F 6C 00 44 37 1B 00

A8 02 D0 02 C8 02 00 00 47 3A 1E 30 99 94 64 00 A3 9F 6C 00 60 02 C8 02 40 02 00 00 44 37 1B 30

A3 9F 6C 00 70 67 40 00 38 02 60 02 40 02 00 00 5E 4D 20 30 44 37 1B 00 70 67 40 00 50 01 20 01

88 01 00 00 58 54 35 30 55 51 33 00 8D 87 54 00 50 01 88 01 80 01 00 00 58 54 35 30 8D 87 54 00

5B 58 37 00 20 01 50 01 30 01 00 00 55 51 33 30 58 54 35 00 5E 5A 39 00 18 02 E8 01 B0 01 00 00

5A 41 1E 30 4B 3C 23 00 2F 2E 1D 00 E8 01 18 02 08 02 00 00 4B 3C 23 30 5A 41 1E 00 5C 59 38 00

B0 01 E8 01 B8 01 00 00 2F 2E 1D 30 4B 3C 23 00 41 37 19 00 28 01 58 01 90 01 00 00 2D 2B 1F 30

32 30 21 00 51 4E 34 00 28 01 38 01 58 01 00 00 2D 2B 1F 30 2E 2C 1F 00 32 30 21 00 90 01 58 01

98 01 00 00 51 4E 34 30 32 30 21 00 33 31 21 00 E0 01 10 02 A8 01 00 00 2A 29 1D 30 3C 3A 28 00

28 27 1C 00 10 02 E0 01 00 02 00 00 3C 3A 28 30 2A 29 1D 00 2E 2C 1F 00 E0 01 A8 01 A0 01 00 00

2A 29 1D 30 28 27 1C 00 29 28 1D 00 30 01 50 01 70 01 00 00 3F 2A 15 30 3C 28 15 00 46 37 19 00

E8 01 08 02 C8 01 00 00 1E 11 0A 30 3E 29 15 00 46 37 19 00 00 02 E0 01 C0 01 00 00 1C 10 09 30

1A 0E 08 00 37 2D 14 00 58 01 38 01 78 01 00 00 1F 11 0A 30 1C 10 09 00 37 2D 14 00 31 00 00 00

48 02 68 02 C0 02 B0 02 87 87 87 38 4A 4A 5B 00 87 87 87 00 54 54 64 00 90 02 88 02 C0 02 48 02

47 47 59 38 3E 3E 50 00 87 87 87 00 87 87 87 00 78 02 A0 02 50 02 B8 02 48 48 5A 38 4A 4A 5B 00

73 73 73 00 73 73 73 00 A8 02 70 02 B8 02 50 02 69 69 78 38 69 69 78 00 73 73 73 00 73 73 73 00

B8 00 C0 00 E0 00 E8 00 1E 23 2D 38 23 28 31 00 3C 41 55 00 1F 24 2C 00 B0 00 B8 00 D8 00 E0 00

0A 0B 0D 38 1E 23 2D 00 0A 0B 0D 00 3C 41 55 00 C0 00 C8 00 E8 00 D0 00 23 28 31 38 0E 0F 12 00

1F 24 2C 00 0D 0F 12 00 C8 00 B0 00 D0 00 D8 00 0E 0F 12 38 0A 0B 0D 00 0D 0F 12 00 0A 0B 0D 00

E0 00 E8 00 00 01 08 01 81 81 81 38 A2 A2 A2 00 49 49 49 00 63 63 63 00 F8 00 00 01 F0 00 08 01

23 23 23 38 49 49 49 00 30 30 30 00 63 63 63 00 E8 00 D0 00 08 01 F0 00 A2 A2 A2 38 30 30 30 00

63 63 63 00 30 30 30 00 D8 00 E0 00 F8 00 00 01 1B 1B 1B 38 81 81 81 00 23 23 23 00 49 49 49 00

D0 00 D8 00 F0 00 F8 00 30 30 30 38 1B 1B 1B 00 30 30 30 00 23 23 23 00 08 00 10 00 00 00 18 00

32 28 19 38 28 1E 0A 00 2D 23 19 00 28 1E 0A 00 10 00 08 00 D8 02 30 00 5A 46 28 38 4B 3C 14 00

14 0F 00 00 14 0F 00 00 28 00 30 00 00 00 08 00 23 19 00 38 23 19 00 00 3C 2A 15 00 2B 1C 0E 00

20 00 18 00 D8 02 10 00 0F 0A 00 38 37 28 0F 00 14 0F 05 00 37 28 0F 00 20 00 28 00 18 00 00 00

1E 0F 00 38 1E 0F 00 00 5A 46 28 00 5A 46 28 00 60 00 68 00 58 00 70 00 30 22 11 38 37 28 0A 00

3A 2C 18 00 37 28 0A 00 50 00 38 00 58 00 60 00 1E 19 00 38 2F 1F 10 00 6E 5A 32 00 40 2D 17 00

38 00 40 00 60 00 68 00 14 0F 00 38 14 0F 00 00 5A 46 28 00 4B 3C 14 00 40 00 48 00 68 00 70 00

1E 11 0A 38 1C 0F 08 00 29 1A 0E 00 24 16 0C 00 48 00 50 00 70 00 58 00 1E 0F 00 38 1E 0F 00 00

5A 46 28 00 5A 46 28 00 88 01 90 01 80 01 98 01 8D 87 53 38 4A 47 2C 00 5A 57 35 00 2A 28 18 00

20 01 28 01 88 01 90 01 54 50 31 38 24 22 15 00 8D 87 53 00 4A 47 2C 00 18 01 20 01 48 01 30 01

5B 58 37 38 55 51 33 00 5D 5A 38 00 5E 5A 39 00 18 02 20 02 08 02 F0 01 5A 41 1E 38 7B 76 49 00

5C 59 38 00 5C 59 38 00 20 02 18 01 F0 01 48 01 7B 76 49 38 5B 58 37 00 5C 59 38 00 5D 5A 38 00

18 02 B0 01 10 02 A8 01 7F 7A 4B 38 6E 64 41 00 34 32 1F 00 1F 1E 12 00 28 02 20 02 10 02 18 02

1C 1B 11 38 55 54 38 00 24 24 18 00 59 58 3A 00 18 01 10 01 20 01 28 01 3F 3E 29 38 1A 19 11 00

3B 39 26 00 19 18 10 00 28 02 10 01 20 02 18 01 1C 1B 11 38 1A 19 11 00 55 54 38 00 3F 3E 29 00

28 01 10 01 38 01 40 01 2D 2B 1F 38 2E 2C 1F 00 2E 2C 1F 00 2E 2C 1F 00 F8 01 40 01 28 02 10 01

2E 2C 1F 38 2E 2C 1F 00 31 2F 20 00 2E 2C 1F 00 28 02 10 02 F8 01 00 02 31 2F 20 38 3C 3A 28 00

2E 2C 1F 00 2E 2C 1F 00 E8 01 E0 01 B8 01 A0 01 28 26 17 38 21 20 13 00 1B 1A 10 00 20 1F 13 00

58 01 50 01 98 01 80 01 29 27 18 38 57 53 33 00 2A 28 18 00 5A 57 35 00 A8 01 B0 01 A0 01 B8 01

1F 1E 12 38 2D 2C 1B 00 20 1F 13 00 1B 1A 10 00 70 01 50 01 78 01 58 01 41 2C 17 38 3C 28 15 00

20 12 0A 00 1F 11 0A 00 48 01 30 01 68 01 70 01 3E 29 15 38 3F 2A 15 00 46 37 19 00 46 37 19 00

78 01 60 01 70 01 68 01 20 12 0A 38 1E 11 0A 00 41 2C 17 00 2B 1B 0E 00 D0 01 68 01 D8 01 60 01

19 0E 07 38 2B 1B 0E 00 1C 0F 08 00 1E 11 0A 00 08 02 F0 01 C8 01 D0 01 3E 29 15 38 3E 29 15 00

46 37 19 00 19 0E 07 00 E8 01 C8 01 E0 01 C0 01 1E 11 0A 38 17 0B 07 00 1A 0E 08 00 18 0D 07 00

D0 01 D8 01 C8 01 C0 01 19 0E 07 38 1C 0F 08 00 17 0B 07 00 18 0D 07 00 F8 01 00 02 D8 01 C0 01

1C 10 09 38 1C 10 09 00 37 2D 14 00 37 2D 14 00 D8 01 60 01 F8 01 40 01 37 2D 14 38 37 2D 14 00

1C 10 09 00 1C 10 09 00 38 01 40 01 78 01 60 01 1C 10 09 38 1C 10 09 00 37 2D 14 00 37 2D 14 00

F0 01 48 01 D0 01 68 01 3E 29 15 38 3E 29 15 00 19 0E 07 00 46 37 19 00

  
  
6th Weapon Bone Data \[at offset 0x000104C4\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 40 02 00 00 13 00 F7 FF C4 FF 00 00 13 00 F7 FF B9 FF 00 00

FF FF E8 FF B9 FF 00 00 FF FF E8 FF C4 FF 00 00 F0 FF FE FF C4 FF 00 00 F0 FF FE FF B9 FF 00 00

04 00 0C 00 B9 FF 00 00 04 00 0C 00 C4 FF 00 00 E6 FF FF FF A5 00 00 00 05 00 15 00 A5 00 00 00

1C 00 F6 FF A5 00 00 00 FD FF DF FF A5 00 00 00 1C 00 F6 FF AC 00 00 00 FD FF DF FF AC 00 00 00

E6 FF FF FF AC 00 00 00 05 00 15 00 AC 00 00 00 0D 00 44 00 B3 FF 00 00 08 00 23 00 25 FF 00 00

FA FF D0 FF 25 FF 00 00 F5 FF B0 FF B3 FF 00 00 FB FF D5 FF DF FE 00 00 06 00 1A 00 A7 FE 00 00

01 00 C8 FF E0 FD 00 00 0C 00 3A 00 0D FF 00 00 F1 FF CB FF E0 FD 00 00 FE FF E3 FF D2 FC 00 00

F9 FF FD FF 6F FD 00 00 09 00 FA FF 6F FD 00 00 12 00 5E 00 00 FE 00 00 0B 00 35 00 7F FD 00 00

15 00 69 00 36 FF 00 00 13 00 65 00 98 FE 00 00 0D 00 1F 00 CA FD 00 00 0F 00 39 00 4D FE 00 00

02 00 21 00 CA FD 00 00 09 00 3A 00 4D FE 00 00 ED FF B6 FF 35 FE 00 00 F3 FF D8 FF 49 FE 00 00

FE FF B3 FF 35 FE 00 00 04 00 D5 FF 49 FE 00 00 E8 FF 68 FF 7D FE 00 00 F6 FF B4 FF 78 FE 00 00

FD FF 03 00 D6 FD 00 00 FB FF 03 00 54 FE 00 00 F4 FF E0 FF 20 FE 00 00 09 00 01 00 D6 FD 00 00

05 00 DD FF 20 FE 00 00 0B 00 00 00 54 FE 00 00 08 00 ED FF 79 FE 00 00 F7 FF F0 FF 79 FE 00 00

0C 00 F9 FF 9F FE 00 00 17 00 F6 FF 25 FF 00 00 1E 00 F5 FF 82 FF 00 00 E5 FF FF FF 82 FF 00 00

EB FF FE FF 25 FF 00 00 F6 FF FD FF 9F FE 00 00 02 00 E9 FF B2 FE 00 00 FA FF EB FF B2 FE 00 00

25 00 19 00 B3 FF 00 00 18 00 D0 FF B3 FF 00 00 EA FF 24 00 B3 FF 00 00 DD FF DA FF B3 FF 00 00

24 00 14 00 98 FF 00 00 EA FF 1E 00 98 FF 00 00 DF FF E0 FF 98 FF 00 00 19 00 D6 FF 98 FF 00 00

F5 FF B0 FF B9 FF 00 00 DD FF DA FF B9 FF 00 00 EA FF 24 00 B9 FF 00 00 0D 00 44 00 B9 FF 00 00

25 00 19 00 B9 FF 00 00 18 00 D0 FF B9 FF 00 00 00 00 20 00 00 00 00 00 4A 00 00 00 00 01 E8 00

D8 00 00 00 15 16 19 30 AA B4 C3 00 38 3B 43 00 E0 00 00 01 08 01 00 00 9B A0 AF 30 15 16 19 00

15 16 19 00 E8 00 00 01 E0 00 00 00 AA B4 C3 30 15 16 19 00 9B A0 AF 00 08 01 F8 00 E0 00 00 00

15 16 19 30 9B A0 AF 00 9B A0 AF 00 B8 00 F8 00 08 01 00 00 0E 0E 10 30 9B A0 AF 00 15 16 19 00

F8 00 B8 00 F0 00 00 00 9B A0 AF 30 0E 0E 10 00 9B A0 AF 00 B8 00 F8 00 F0 00 00 00 0E 0E 10 30

5B 60 6D 00 5B 60 6D 00 F8 00 B8 00 18 01 00 00 5B 60 6D 30 0E 0E 10 00 0E 0E 10 00 E0 00 10 01

E8 00 00 00 9B A0 AF 30 0E 0E 10 00 9B A0 AF 00 10 01 E0 00 18 01 00 00 0E 0E 10 30 9B A0 AF 00

0E 0E 10 00 F8 00 18 01 E0 00 00 00 5B 60 6D 30 0E 0E 10 00 9B A0 AF 00 E8 00 10 01 D0 00 00 00

9B A0 AF 30 0E 0E 10 00 2A 2C 32 00 E8 00 D0 00 C8 00 00 00 9B A0 AF 30 2A 2C 32 00 9B A0 AF 00

D8 00 E8 00 C8 00 00 00 38 3B 43 30 AA B4 C3 00 5A 5F 6E 00 08 02 F0 01 A0 01 00 00 72 66 2F 30

3C 23 19 00 6E 5F 28 00 F8 01 00 02 A8 01 00 00 39 29 0C 30 66 50 1C 00 4C 48 24 00 30 02 20 02

28 02 00 00 04 04 04 30 05 05 05 00 04 04 04 00 18 02 38 02 10 02 00 00 06 06 06 30 0A 0A 0A 00

0B 0B 0B 00 C0 01 C8 01 A0 00 00 00 1E 33 1E 30 10 1B 10 00 1A 2D 1B 00 30 01 20 01 40 01 00 00

1D 32 1E 30 08 0E 08 00 11 1E 12 00 28 01 38 01 48 01 00 00 08 0D 08 30 11 1E 12 00 08 0D 08 00

B0 00 D0 00 C0 00 00 00 00 37 2D 30 08 0E 08 00 0C 14 0C 00 D0 00 D8 00 C8 00 00 00 08 0E 08 30

00 37 2D 00 15 24 15 00 F0 01 98 01 A0 01 00 00 17 27 1E 30 0F 28 23 00 14 23 23 00 F8 01 80 00

E0 01 00 00 11 1F 15 30 0E 1B 11 00 11 1F 15 00 00 02 B0 01 A8 01 00 00 15 23 1A 30 14 22 18 00

14 22 18 00 98 01 88 00 A8 00 00 00 0F 28 23 30 0C 36 2F 00 0C 31 2F 00 A8 00 88 00 B0 01 00 00

0E 1B 11 30 0E 1B 11 00 0F 19 14 00 90 00 A0 00 B0 01 00 00 36 48 44 30 36 48 44 00 14 22 18 00

70 01 30 01 38 01 00 00 0C 31 2F 30 11 3B 34 00 1D 2F 27 00 B8 00 A8 00 18 01 00 00 15 23 1A 30

0E 1B 11 00 14 22 18 00 30 01 48 01 38 01 00 00 11 3B 34 30 0C 31 2F 00 1D 2F 27 00 20 01 28 01

48 01 00 00 16 23 1B 30 15 23 1A 00 15 23 19 00 50 01 C0 00 D0 00 00 00 15 23 19 30 1B 2B 22 00

16 23 1B 00 78 01 08 01 68 01 00 00 0C 31 2F 30 11 3B 34 00 1E 2F 28 00 78 01 90 01 A8 00 00 00

0C 31 2F 30 0F 28 23 00 0C 31 2F 00 58 01 18 01 A8 00 00 00 14 23 19 30 14 22 18 00 0E 1B 11 00

D8 00 70 01 68 01 00 00 11 3B 34 30 0C 31 2F 00 1E 2F 28 00 08 01 78 01 A8 00 00 00 11 3B 34 30

0C 31 2F 00 0C 31 2F 00 B8 01 58 01 A8 00 00 00 0F 19 14 30 14 23 19 00 0E 1B 11 00 08 01 A8 00

B8 00 00 00 11 3B 34 30 0C 31 2F 00 11 3B 34 00 C0 00 50 01 20 01 00 00 1B 2B 22 30 15 23 19 00

16 23 1B 00 50 01 D0 00 10 01 00 00 15 23 19 30 16 23 1B 00 14 22 18 00 20 01 48 01 40 01 00 00

16 23 1B 30 15 23 19 00 25 36 2F 00 48 01 30 01 40 01 00 00 0C 31 2F 30 11 3B 34 00 11 3B 34 00

30 01 70 01 B0 00 00 00 11 3B 34 30 0C 31 2F 00 11 3B 34 00 B0 00 70 01 D8 00 00 00 11 3B 34 30

0C 31 2F 00 11 3B 34 00 D0 00 B0 00 D8 00 00 00 0F 1F 13 30 00 37 2D 00 00 37 2D 00 90 01 80 01

C0 01 00 00 22 34 2C 30 2F 43 3D 00 34 49 44 00 98 01 A0 00 90 00 00 00 11 3F 39 30 2F 42 3C 00

2F 42 3C 00 08 02 98 00 D8 01 00 00 2C 3F 39 30 11 3F 39 00 2C 3F 39 00 C8 01 B8 01 B0 01 00 00

23 32 2B 30 14 22 18 00 14 22 18 00 B8 01 88 01 58 01 00 00 14 22 18 30 17 24 1C 00 14 23 19 00

C0 01 98 01 90 01 00 00 34 49 44 30 11 3F 39 00 22 34 2C 00 80 01 90 01 78 01 00 00 2F 43 3D 30

22 34 2C 00 0C 31 2F 00 B0 01 A0 00 C8 01 00 00 14 22 18 30 36 48 44 00 23 32 2B 00 D8 00 68 01

00 01 00 00 11 3B 34 30 1E 2F 28 00 11 3B 34 00 B8 01 C8 01 88 01 00 00 14 22 18 30 23 32 2B 00

17 24 1C 00 98 01 C0 01 A0 00 00 00 11 3F 39 30 34 49 44 00 2F 42 3C 00 08 02 98 01 90 00 00 00

2C 3F 39 30 11 3F 39 00 2F 42 3C 00 08 02 90 00 98 00 00 00 2C 3F 39 30 2F 42 3C 00 11 3F 39 00

98 01 08 02 A0 01 00 00 11 3F 39 30 2C 3F 39 00 23 35 2D 00 80 00 F0 01 D0 01 00 00 11 3F 39 30

17 27 1E 00 15 25 1C 00 88 00 F0 01 80 00 00 00 0C 36 2F 30 17 27 1E 00 11 3F 39 00 98 01 F0 01

88 00 00 00 0F 28 23 30 17 27 1E 00 0C 36 2F 00 98 00 00 02 E8 01 00 00 34 46 42 30 15 23 1A 00

16 23 1B 00 90 00 00 02 98 00 00 00 36 48 44 30 15 23 1A 00 34 46 42 00 B0 01 00 02 90 00 00 00

14 22 18 30 15 23 1A 00 36 48 44 00 F8 01 B0 01 88 00 00 00 11 1F 15 30 0F 19 14 00 0E 1B 11 00

F8 01 88 00 80 00 00 00 11 1F 15 30 0E 1B 11 00 0E 1B 11 00 B0 01 F8 01 A8 01 00 00 0F 19 14 30

11 1F 15 00 0F 19 14 00 A8 00 B0 01 B8 01 00 00 0E 1B 11 30 0F 19 14 00 0F 19 14 00 98 01 A8 00

90 01 00 00 0F 28 23 30 0C 31 2F 00 0F 28 23 00 68 01 08 01 00 01 00 00 1E 2F 28 30 11 3B 34 00

11 3B 34 00 20 00 00 00 08 02 D8 01 F0 01 D0 01 72 66 2F 38 72 66 2F 00 3C 23 19 00 34 29 15 00

D0 01 D8 01 30 02 38 02 82 78 55 38 E4 E4 E4 00 34 21 0E 00 65 51 26 00 F8 01 E0 01 00 02 E8 01

39 29 0C 38 39 29 0C 00 66 50 1C 00 34 25 10 00 E8 01 E0 01 18 02 20 02 7D 7D 7D 38 7D 7D 7D 00

41 2E 13 00 3B 27 11 00 80 00 D0 01 28 02 30 02 03 03 03 38 09 09 09 00 04 04 04 00 04 04 04 00

D8 01 98 00 38 02 10 02 12 12 12 38 12 12 12 00 0A 0A 0A 00 0B 0B 0B 00 20 02 30 02 18 02 38 02

05 05 05 38 04 04 04 00 06 06 06 00 0A 0A 0A 00 98 00 E8 01 10 02 18 02 12 12 12 38 06 06 06 00

0B 0B 0B 00 06 06 06 00 E0 01 80 00 20 02 28 02 04 04 04 38 03 03 03 00 05 05 05 00 04 04 04 00

40 00 48 00 70 00 78 00 42 46 48 38 25 27 29 00 42 47 49 00 30 34 35 00 68 00 70 00 60 00 78 00

86 8F 93 38 42 47 49 00 65 6C 6F 00 30 34 35 00 48 00 50 00 78 00 60 00 25 27 29 38 B1 BC C2 00

30 34 35 00 65 6C 6F 00 58 00 40 00 68 00 70 00 E1 F0 F7 38 42 46 48 00 86 8F 93 00 42 47 49 00

50 00 58 00 60 00 68 00 B1 BC C2 38 E1 F0 F7 00 65 6C 6F 00 86 8F 93 00 38 00 00 00 48 00 50 00

08 09 0A 38 27 2B 33 00 08 09 0A 00 27 2B 33 00 00 00 18 00 50 00 58 00 27 2B 33 38 33 37 42 00

27 2B 33 00 32 36 41 00 18 00 20 00 58 00 40 00 33 37 42 38 0E 0F 12 00 32 36 41 00 0E 0F 12 00

20 00 38 00 40 00 48 00 0E 0F 12 38 08 09 0A 00 0E 0F 12 00 08 09 0A 00 00 00 08 00 18 00 10 00

A0 6E 00 38 64 46 00 00 A0 78 00 00 7A 55 00 00 38 00 30 00 00 00 08 00 12 0C 00 38 12 0D 00 00

A0 6E 00 00 64 46 00 00 18 00 10 00 20 00 28 00 A0 78 00 38 7A 55 00 00 20 16 00 00 21 17 00 00

20 00 28 00 38 00 30 00 20 16 00 38 21 17 00 00 12 0C 00 00 12 0D 00 00 38 01 28 01 80 01 88 01

17 23 1A 38 0F 14 10 00 20 30 22 00 10 16 11 00 88 01 C8 01 80 01 C0 01 09 0F 09 38 10 1B 10 00

1B 2E 1B 00 1E 33 1E 00 50 01 68 01 60 01 70 01 08 0D 08 38 12 1E 12 00 05 09 05 00 08 0E 08 00

58 01 78 01 50 01 68 01 07 0C 07 38 15 23 15 00 08 0D 08 00 12 1E 12 00 60 01 70 01 58 01 78 01

05 09 05 38 08 0E 08 00 07 0C 07 00 15 23 15 00 20 01 30 01 C0 00 B0 00 08 0E 08 38 1D 32 1E 00

0C 14 0C 00 00 37 2D 00 58 01 88 01 60 01 28 01 14 23 19 38 17 24 1C 00 10 1D 13 00 15 23 1A 00

18 01 58 01 10 01 50 01 14 22 18 38 14 23 19 00 14 22 18 00 15 23 19 00 20 01 50 01 28 01 60 01

16 23 1B 38 15 23 19 00 15 23 1A 00 10 1D 13 00 80 01 78 01 38 01 70 01 2F 43 3D 38 0C 31 2F 00

1D 2F 27 00 0C 31 2F 00

  
  
7th Weapon Bone Data \[at offset 0x00010FEC\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 A0 02 00 00 07 00 2E 00 A7 FF 00 00 0D 00 55 00 A7 FF 00 00

0A 00 41 00 89 FF 00 00 0F 00 5E 00 BD FF 00 00 11 00 6E 00 A5 FF 00 00 07 00 30 00 74 FF 00 00

06 00 28 00 65 FF 00 00 06 00 2C 00 A7 FF 00 00 05 00 20 00 BD FF 00 00 06 00 28 00 38 FF 00 00

04 00 1F 00 90 FF 00 00 F9 FF D4 FF 90 FF 00 00 F8 FF CB FF 38 FF 00 00 F9 FF D3 FF BD FF 00 00

F7 FF C7 FF A7 FF 00 00 F8 FF CB FF 65 FF 00 00 F6 FF C3 FF 74 FF 00 00 EC FF 85 FF A5 FF 00 00

EF FF 95 FF BD FF 00 00 F3 FF B1 FF 89 FF 00 00 F0 FF 9E FF A7 FF 00 00 F7 FF C5 FF A7 FF 00 00

04 00 1F 00 90 FF 00 00 0F 00 0C 00 90 FF 00 00 16 00 F6 FF 90 FF 00 00 08 00 E2 FF 90 FF 00 00

F9 FF D4 FF 90 FF 00 00 EF FF E7 FF 90 FF 00 00 E7 FF FE FF 90 FF 00 00 F6 FF 11 00 90 FF 00 00

F5 FF 10 00 BD FF 00 00 05 00 20 00 BD FF 00 00 0F 00 0C 00 BD FF 00 00 17 00 F6 FF BD FF 00 00

08 00 E2 FF BD FF 00 00 F9 FF D3 FF BD FF 00 00 EE FF E7 FF BD FF 00 00 E7 FF FE FF BD FF 00 00

06 00 2C 00 A7 FF 00 00 14 00 12 00 A7 FF 00 00 1E 00 F5 FF A7 FF 00 00 0B 00 DB FF A7 FF 00 00

F7 FF C7 FF A7 FF 00 00 E9 FF E1 FF A7 FF 00 00 DF FF FF FF A7 FF 00 00 F2 FF 18 00 A7 FF 00 00

0B 00 F8 FF D0 FF 00 00 09 00 F8 FF BD FF 00 00 FE FF EF FF BD FF 00 00 FD FF EE FF D0 FF 00 00

F3 FF FC FF D0 FF 00 00 F5 FF FC FF BD FF 00 00 00 00 03 00 BD FF 00 00 00 00 05 00 D0 FF 00 00

F3 FF FC FF A8 00 00 00 00 00 05 00 A8 00 00 00 0B 00 F8 FF A8 00 00 00 FD FF EE FF A8 00 00 00

FF FF FA FF BC 00 00 00 16 00 F6 FF B1 FD 00 00 16 00 F6 FF 90 FF 00 00 08 00 E2 FF B1 FD 00 00

08 00 E2 FF 90 FF 00 00 F9 FF D4 FF B1 FD 00 00 F9 FF D4 FF 90 FF 00 00 EF FF E7 FF B1 FD 00 00

EF FF E7 FF 90 FF 00 00 E7 FF FE FF B1 FD 00 00 E7 FF FE FF 90 FF 00 00 F6 FF 11 00 B1 FD 00 00

F6 FF 11 00 90 FF 00 00 04 00 1F 00 B1 FD 00 00 04 00 1F 00 90 FF 00 00 0F 00 0C 00 B1 FD 00 00

0F 00 0C 00 90 FF 00 00 05 00 E9 FF 43 FD 00 00 10 00 F7 FF 43 FD 00 00 0A 00 07 00 43 FD 00 00

03 00 15 00 43 FD 00 00 F8 FF 0A 00 43 FD 00 00 EE FF FD FF 43 FD 00 00 F3 FF EC FF 43 FD 00 00

FB FF DE FF 43 FD 00 00 FF FF FA FF 1A FD 00 00 00 00 20 00 00 00 00 00 36 00 00 00 90 02 58 02

98 02 00 00 78 7D B5 30 B9 BB D9 00 78 7D B5 00 88 02 90 02 98 02 00 00 6B 6E AA 30 6B 6E AA 00

6B 6E AA 00 80 02 88 02 98 02 00 00 69 6B A9 30 69 6B A9 00 69 6B A9 00 78 02 80 02 98 02 00 00

61 61 A9 30 61 61 A9 00 61 61 A9 00 70 02 78 02 98 02 00 00 70 73 A3 30 70 73 A3 00 70 73 A3 00

68 02 70 02 98 02 00 00 42 3C 96 30 42 3C 96 00 42 3C 96 00 60 02 68 02 98 02 00 00 6C 66 B2 30

6C 66 B2 00 6C 66 B2 00 58 02 60 02 98 02 00 00 96 8F E7 30 96 8F E7 00 96 8F E7 00 88 00 98 00

A0 00 00 00 73 9F 9F 30 22 22 4B 00 22 22 4B 00 90 00 88 00 A0 00 00 00 32 3E 76 30 73 9F 9F 00

22 22 4B 00 A8 00 90 00 A0 00 00 00 00 00 00 30 32 3E 76 00 22 22 4B 00 90 00 A8 00 A0 00 00 00

50 64 BE 30 00 00 00 00 37 37 78 00 88 00 90 00 A0 00 00 00 B9 FF FF 30 50 64 BE 00 37 37 78 00

98 00 88 00 A0 00 00 00 37 37 78 30 B9 FF FF 00 37 37 78 00 58 00 80 00 98 00 00 00 1E 3C 5A 30

1E 3C 5A 00 37 37 78 00 A8 00 70 00 98 00 00 00 00 00 00 30 00 00 00 00 22 22 4B 00 80 00 58 00

98 00 00 00 12 25 38 30 12 25 38 00 22 22 4B 00 98 00 60 00 80 00 00 00 22 22 4B 30 4B 5D 76 00

12 25 38 00 60 00 98 00 88 00 00 00 4B 5D 76 30 22 22 4B 00 73 9F 9F 00 88 00 98 00 60 00 00 00

B9 FF FF 30 37 37 78 00 78 96 BE 00 60 00 98 00 80 00 00 00 78 96 BE 30 37 37 78 00 1E 3C 5A 00

80 00 60 00 78 00 00 00 12 25 38 30 4B 5D 76 00 12 25 38 00 80 00 78 00 60 00 00 00 1E 3C 5A 30

1E 3C 5A 00 78 96 BE 00 10 00 48 00 20 00 00 00 22 22 4B 30 4B 5D 76 00 73 9F 9F 00 10 00 20 00

48 00 00 00 37 37 78 30 B9 FF FF 00 78 96 BE 00 10 00 48 00 28 00 00 00 37 37 78 30 78 96 BE 00

1E 3C 5A 00 30 00 28 00 48 00 00 00 1E 3C 5A 30 1E 3C 5A 00 78 96 BE 00 48 00 28 00 30 00 00 00

4B 5D 76 30 12 25 38 00 12 25 38 00 48 00 10 00 28 00 00 00 4B 5D 76 30 22 22 4B 00 12 25 38 00

28 00 50 00 10 00 00 00 1E 3C 5A 30 1E 3C 5A 00 37 37 78 00 50 00 28 00 10 00 00 00 12 25 38 30

12 25 38 00 22 22 4B 00 10 00 20 00 08 00 00 00 22 22 4B 30 73 9F 9F 00 22 22 4B 00 20 00 18 00

08 00 00 00 73 9F 9F 30 32 3E 76 00 22 22 4B 00 18 00 20 00 08 00 00 00 50 64 BE 30 B9 FF FF 00

37 37 78 00 20 00 10 00 08 00 00 00 B9 FF FF 30 37 37 78 00 37 37 78 00 00 00 18 00 08 00 00 00

00 00 00 30 50 64 BE 00 37 37 78 00 18 00 00 00 08 00 00 00 32 3E 76 30 00 00 00 00 22 22 4B 00

98 00 70 00 58 00 00 00 37 37 78 30 00 00 00 00 1E 3C 5A 00 A8 00 90 00 68 00 00 00 14 1E 32 30

14 14 68 00 14 1E 32 00 18 00 00 00 40 00 00 00 14 19 55 30 0F 14 23 00 0F 14 23 00 90 00 A8 00

68 00 00 00 14 28 50 30 14 1E 3C 00 14 1E 3C 00 00 00 18 00 40 00 00 00 14 1E 3C 30 1E 32 5A 00

14 1E 3C 00 38 00 40 00 00 00 00 00 00 00 00 30 0D 16 25 00 00 00 00 00 68 00 70 00 A8 00 00 00

19 2B 49 30 00 00 00 00 00 00 00 00 40 00 38 00 00 00 00 00 0D 16 25 30 00 00 00 00 00 00 00 00

70 00 68 00 A8 00 00 00 00 00 00 30 19 2B 49 00 00 00 00 00 20 01 10 01 18 01 00 00 2F 38 3D 30

47 54 5B 00 43 50 57 00 F8 00 00 01 F0 00 00 00 25 2C 30 30 26 2D 31 00 2B 33 37 00 C8 00 D8 00

D0 00 00 00 A9 C8 D9 30 59 6A 73 00 A5 C4 D4 00 E8 00 B8 00 B0 00 00 00 29 31 35 30 5B 6C 75 00

1D 23 26 00 C8 01 B0 01 D0 01 00 00 86 86 86 30 2F 2F 2F 00 31 31 31 00 C0 01 C8 01 D0 01 00 00

63 63 63 30 86 86 86 00 31 31 31 00 B8 01 C0 01 D0 01 00 00 1A 1A 1A 30 63 63 63 00 31 31 31 00

B0 01 B8 01 D0 01 00 00 2F 2F 2F 30 1A 1A 1A 00 31 31 31 00 2F 00 00 00 08 02 F8 01 88 02 90 02

BF C0 D7 38 6C 6F AB 00 6C 6F AB 00 6C 6F AB 00 F8 01 E8 01 90 02 58 02 7C 82 B9 38 FF FF FF 00

7C 82 B9 00 B9 BB D9 00 18 02 08 02 80 02 88 02 65 67 A5 38 65 67 A5 00 65 67 A5 00 65 67 A5 00

28 02 18 02 78 02 80 02 50 4E A4 38 50 4E A4 00 50 4E A4 00 50 4E A4 00 38 02 28 02 70 02 78 02

5D 5A A3 38 5D 5A A3 00 5D 5A A3 00 5D 5A A3 00 48 02 38 02 68 02 70 02 45 40 99 38 96 8F E7 00

45 40 99 00 45 40 99 00 D8 01 48 02 60 02 68 02 5E 56 A8 38 96 8F E7 00 5E 56 A8 00 5E 56 A8 00

E8 01 D8 01 58 02 60 02 C9 CB E0 38 78 7D B5 00 8E 8A D3 00 8E 8A D3 00 50 02 48 02 E0 01 D8 01

96 8F E7 38 6C 66 B2 00 6C 66 B2 00 6C 66 B2 00 40 02 38 02 50 02 48 02 52 52 A4 38 52 52 A4 00

52 52 A4 00 52 52 A4 00 30 02 28 02 40 02 38 02 54 51 9E 38 6C 66 B2 00 54 51 9E 00 54 51 9E 00

20 02 18 02 30 02 28 02 49 45 9F 38 49 45 9F 00 82 84 AE 00 49 45 9F 00 10 02 08 02 20 02 18 02

5C 5B 9D 38 5C 5B 9D 00 AA AB C8 00 5C 5B 9D 00 00 02 F8 01 10 02 08 02 70 74 AF 38 70 74 AF 00

70 74 AF 00 D2 D0 E8 00 F0 01 E8 01 00 02 F8 01 FF FF FF 38 B9 BA D7 00 7B 7F B7 00 7B 7F B7 00

E0 01 D8 01 F0 01 E8 01 FF FF FF 38 73 7D C8 00 73 7D C8 00 FF FF FF 00 58 00 70 00 98 00 A8 00

12 25 38 38 00 00 00 00 22 22 4B 00 00 00 00 00 38 00 50 00 00 00 10 00 00 00 00 38 12 25 38 00

00 00 00 00 22 22 4B 00 38 00 00 00 50 00 10 00 00 00 00 38 00 00 00 00 1E 3C 5A 00 37 37 78 00

38 01 30 01 B8 00 B0 00 7D 64 AC 38 28 20 4E 00 4F 3F 7A 00 2E 24 55 00 30 01 38 01 F8 00 00 01

34 29 5B 38 40 33 68 00 34 29 5B 00 43 36 6D 00 38 01 40 01 00 01 08 01 3C 30 65 38 AC 8C EC 00

36 2B 5E 00 2B 23 52 00 40 01 38 01 C0 00 B8 00 A9 87 DE 38 5B 49 87 00 79 60 A8 00 4F 3F 7A 00

48 01 40 01 C8 00 C0 00 8D 71 BE 38 E0 C4 FE 00 95 77 C7 00 79 60 A8 00 40 01 48 01 08 01 10 01

66 51 93 38 A7 85 DB 00 2B 23 52 00 3D 31 66 00 48 01 50 01 10 01 18 01 4F 3F 7A 38 84 69 B4 00

3D 31 66 00 3A 2E 62 00 50 01 48 01 D0 00 C8 00 84 69 B4 38 C6 9E FE 00 92 74 C4 00 95 77 C7 00

58 01 50 01 D8 00 D0 00 2A 22 51 38 84 69 B4 00 4E 3E 78 00 92 74 C4 00 50 01 58 01 18 01 20 01

84 69 B4 38 4B 3C 75 00 3A 2E 62 00 28 20 4E 00 60 01 58 01 E0 00 D8 00 46 38 6F 38 4B 3C 75 00

61 4E 8E 00 6E 58 9D 00 58 01 60 01 20 01 28 01 2A 22 51 38 4F 3F 7A 00 28 20 4E 00 27 1F 4D 00

60 01 68 01 28 01 F0 00 28 20 4E 38 2C 23 53 00 27 1F 4D 00 25 1E 4B 00 68 01 60 01 E8 00 E0 00

1A 15 3F 38 6E 58 9C 00 23 1C 49 00 53 42 7E 00 30 01 68 01 B0 00 E8 00 14 10 38 38 28 20 4E 00

19 14 3D 00 23 1C 49 00 68 01 30 01 F0 00 F8 00 1A 15 3F 38 14 10 38 00 25 1E 4B 00 32 28 5A 00

28 01 08 01 20 01 10 01 2D 35 39 38 32 3C 41 00 2F 38 3D 00 47 54 5B 00 F0 00 00 01 28 01 08 01

2B 33 37 38 26 2D 31 00 2D 35 39 00 32 3C 41 00 C0 00 E0 00 C8 00 D8 00 89 A3 B1 38 2E 37 3C 00

A9 C8 D9 00 59 6A 73 00 B8 00 E8 00 C0 00 E0 00 5B 6C 75 38 29 31 35 00 89 A3 B1 00 2E 37 3C 00

A8 01 70 01 B8 01 C0 01 06 06 2C 38 23 23 45 00 06 06 2C 00 1C 1C 3F 00 70 01 88 01 C0 01 C8 01

23 23 45 38 2E 2E 4E 00 1C 1C 3F 00 26 26 47 00 88 01 90 01 C8 01 B0 01 2E 2E 4E 38 0C 0C 31 00

26 26 47 00 0C 0C 31 00 90 01 A8 01 B0 01 B8 01 0C 0C 31 38 06 06 2C 00 0C 0C 31 00 06 06 2C 00

70 01 78 01 88 01 80 01 23 2E 3A 38 28 36 43 00 90 98 A4 00 31 42 53 00 A8 01 A0 01 70 01 78 01

07 0A 0C 38 08 0A 0D 00 23 2E 3A 00 28 36 43 00 88 01 80 01 90 01 98 01 90 98 A4 38 31 42 53 00

0D 11 15 00 0D 12 16 00 90 01 98 01 A8 01 A0 01 0D 11 15 38 0D 12 16 00 07 0A 0C 00 08 0A 0D 00

  
  
8th Weapon Bone Data \[at offset 0x00011B4C\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 80 02 00 00 11 00 D2 FF AE FF 00 00 F4 FF B1 FF 85 FF 00 00

F0 FF 9A FF 94 FF 00 00 09 00 9F FF C9 FF 00 00 DA FF A7 FF C9 FF 00 00 E2 FF DA FF AE FF 00 00

DA FF 67 FF A9 FF 00 00 F5 FF 62 FF A9 FF 00 00 EB FF 7C FF 94 FF 00 00 E6 FF 5A FF 57 FF 00 00

F8 FF CC FF AE FE 00 00 F4 FF B1 FF 85 FF 00 00 08 00 F8 FF D6 FE 00 00 F6 FF FB FF D6 FE 00 00

08 00 F8 FF 62 FF 00 00 F6 FF FB FF 62 FF 00 00 F6 FF C1 FF 9D FE 00 00 F7 FF C7 FF 47 FE 00 00

F3 FF AA FF 68 FE 00 00 F7 FF C4 FF FC FD 00 00 00 00 FA FF 95 FD 00 00 F8 FF CD FF 8A FE 00 00

F7 FF C4 FF 12 FF 00 00 08 00 F8 FF 4E FE 00 00 F8 FF E7 FF 9D FE 00 00 F6 FF FB FF 4E FE 00 00

00 00 E6 FF 9D FE 00 00 F9 FF D2 FF 5E FE 00 00 00 00 E8 FF D9 FD 00 00 02 00 EA FF 28 FE 00 00

F7 FF EC FF 28 FE 00 00 FA FF E9 FF D9 FD 00 00 08 00 F8 FF 2C FF 00 00 F6 FF FB FF 2C FF 00 00

05 00 E5 FF D3 FE 00 00 F3 FF E8 FF D3 FE 00 00 F3 FF D2 FF 6F FF 00 00 FF FF D0 FF 6F FF 00 00

FA FF D6 FF AE FF 00 00 F6 FF FB FF 83 FF 00 00 08 00 F8 FF 8E FF 00 00 FD FF E8 FF D5 FF 00 00

FD FF E8 FF BA 00 00 00 F6 FF FB FF BA 00 00 00 08 00 F8 FF BA 00 00 00 08 00 F8 FF C8 FF 00 00

05 00 E4 FF AB FF 00 00 0B 00 0C 00 AB FF 00 00 02 00 0A 00 BA 00 00 00 02 00 0A 00 D5 FF 00 00

04 00 1C 00 AE FF 00 00 0B 00 21 00 6F FF 00 00 00 00 23 00 6F FF 00 00 FA FF 0E 00 D3 FE 00 00

0B 00 0B 00 D3 FE 00 00 FF FF 0B 00 D9 FD 00 00 FC FF 09 00 28 FE 00 00 07 00 07 00 28 FE 00 00

05 00 0A 00 D9 FD 00 00 05 00 21 00 5E FE 00 00 06 00 0B 00 9D FE 00 00 FE FF 0D 00 9D FE 00 00

07 00 2E 00 12 FF 00 00 06 00 26 00 8A FE 00 00 08 00 2F 00 FC FD 00 00 0C 00 49 00 68 FE 00 00

07 00 2C 00 47 FE 00 00 08 00 32 00 9D FE 00 00 0B 00 42 00 85 FF 00 00 06 00 27 00 AE FE 00 00

19 00 98 00 57 FF 00 00 13 00 77 00 94 FF 00 00 25 00 8C 00 A9 FF 00 00 09 00 91 00 A9 FF 00 00

EE FF 20 00 AE FF 00 00 F6 FF 54 00 C9 FF 00 00 25 00 4C 00 C9 FF 00 00 0E 00 59 00 94 FF 00 00

0B 00 42 00 85 FF 00 00 1C 00 19 00 AE FF 00 00 00 00 20 00 00 00 00 00 8E 00 00 00 D0 01 C8 01

10 02 00 00 2B 08 1B 30 32 0A 23 00 2D 07 1D 00 E8 00 E0 00 88 00 00 00 2F 09 20 30 28 07 19 00

2D 07 1D 00 D0 00 60 00 B8 00 00 00 23 06 14 30 3C 0F 28 00 44 0F 34 00 60 00 E0 01 B8 00 00 00

3C 0F 28 30 33 0A 23 00 38 0C 28 00 B0 01 00 01 98 01 00 00 2B 08 1B 30 2F 09 20 00 24 06 15 00

00 01 10 01 28 01 00 00 3E 0D 2D 30 28 07 19 00 27 07 18 00 18 01 08 01 20 01 00 00 29 07 1A 30

33 08 20 00 29 07 1A 00 08 01 A8 01 A0 01 00 00 28 07 19 30 28 07 19 00 28 07 19 00 C8 00 68 00

C0 00 00 00 28 07 19 30 28 07 19 00 29 07 1A 00 68 00 C8 00 E8 01 00 00 28 07 19 30 28 07 19 00

28 07 19 00 10 02 C0 01 B8 01 00 00 2D 07 1D 30 27 07 18 00 27 07 18 00 F0 00 88 00 F8 00 00 00

27 07 18 30 2D 07 1D 00 27 07 18 00 A8 01 28 02 F0 01 00 00 00 00 00 30 14 09 2A 00 55 32 8C 00

28 02 B0 01 F0 01 00 00 0E 06 1E 30 14 0A 2D 00 55 32 8C 00 28 02 E0 01 B0 01 00 00 0E 06 1E 30

09 04 12 00 14 0A 2D 00 E0 01 28 02 18 02 00 00 09 04 12 30 0E 06 1E 00 55 32 8C 00 28 02 E8 01

18 02 00 00 14 09 2A 30 00 00 00 00 55 32 8C 00 28 02 A8 01 E8 01 00 00 14 09 2A 30 00 00 00 00

00 00 00 00 98 01 70 00 20 02 00 00 0C 05 1A 30 16 0A 2F 00 00 00 00 00 98 01 20 02 F0 01 00 00

0C 05 1A 30 00 00 00 00 55 32 8C 00 A0 01 F0 01 20 02 00 00 00 00 00 30 55 32 8C 00 00 00 00 00

A0 01 20 02 78 00 00 00 00 00 00 30 00 00 00 00 00 00 00 00 F8 01 E0 01 18 02 00 00 0E 06 1E 30

09 04 12 00 55 32 8C 00 E8 01 F8 01 18 02 00 00 00 00 00 30 14 09 2A 00 55 32 8C 00 D0 01 10 02

00 02 00 00 12 08 27 30 0B 05 17 00 5A 4B 96 00 00 02 10 02 08 02 00 00 5A 4B 96 30 0B 05 17 00

15 09 2D 00 10 02 00 02 08 02 00 00 0B 05 17 30 5A 4B 96 00 15 09 2D 00 10 02 B8 01 00 02 00 00

0B 05 17 30 00 00 00 00 5A 4B 96 00 D8 01 C0 01 10 02 00 00 55 32 8C 30 00 00 00 00 0B 05 17 00

C8 01 D8 01 10 02 00 00 18 0A 32 30 55 32 8C 00 0B 05 17 00 00 02 A0 00 D0 01 00 00 5A 4B 96 30

5A 4B 96 00 12 08 27 00 A0 00 00 02 B8 01 00 00 5A 4B 96 30 5A 4B 96 00 00 00 00 00 C8 00 F8 01

E8 01 00 00 00 00 00 30 14 09 2A 00 00 00 00 00 F8 01 B8 00 E0 01 00 00 0E 06 1E 30 15 09 2C 00

09 04 12 00 D8 01 B8 00 F8 01 00 00 55 32 8C 30 15 09 2C 00 0E 06 1E 00 F8 01 C8 00 D8 01 00 00

14 09 2A 30 00 00 00 00 55 32 8C 00 98 01 F0 01 B0 01 00 00 0C 05 1A 30 55 32 8C 00 14 0A 2D 00

F0 01 A0 01 A8 01 00 00 55 32 8C 30 00 00 00 00 00 00 00 00 A8 01 68 00 E8 01 00 00 00 00 00 30

00 00 00 00 00 00 00 00 60 00 B0 01 E0 01 00 00 0B 0F 28 30 14 0A 2D 00 09 04 12 00 C0 01 D8 01

C8 00 00 00 00 00 00 30 55 32 8C 00 00 00 00 00 D8 01 C8 01 B8 00 00 00 55 32 8C 30 18 0A 32 00

15 09 2C 00 A0 00 E0 00 D0 01 00 00 5A 4B 96 30 12 08 27 00 12 08 27 00 C8 01 E8 00 B8 00 00 00

18 0A 32 30 18 0A 32 00 15 09 2C 00 C8 00 F0 00 C0 01 00 00 00 00 00 30 00 00 00 00 00 00 00 00

B8 01 F8 00 A0 00 00 00 00 00 00 30 00 00 00 00 5A 4B 96 00 60 00 00 01 B0 01 00 00 0B 0F 28 30

11 07 23 00 14 0A 2D 00 08 01 68 00 A8 01 00 00 00 00 00 30 00 00 00 00 00 00 00 00 A0 01 78 00

08 01 00 00 00 00 00 30 00 00 00 00 00 00 00 00 98 01 00 01 70 00 00 00 0C 05 1A 30 11 07 23 00

17 0A 30 00 00 01 28 01 70 00 00 00 1F 0E 42 30 10 07 22 00 27 12 53 00 70 00 28 01 58 00 00 00

2A 13 58 30 10 07 22 00 02 00 04 00 58 00 28 01 B0 00 00 00 02 00 04 30 10 07 22 00 55 32 8C 00

B0 00 28 01 10 01 00 00 55 32 8C 30 10 07 22 00 15 09 2C 00 20 01 B0 00 18 01 00 00 00 00 00 30

55 32 8C 00 00 00 00 00 B0 00 20 01 58 00 00 00 55 32 8C 30 00 00 00 00 02 00 04 00 58 00 20 01

78 00 00 00 02 00 04 30 00 00 00 00 00 00 00 00 78 00 20 01 08 01 00 00 00 00 00 30 00 00 00 00

0A 05 14 00 68 00 18 01 C0 00 00 00 00 00 00 30 00 00 00 00 00 00 00 00 18 01 50 00 C0 00 00 00

00 00 00 30 14 09 2A 00 00 00 00 00 50 00 18 01 B0 00 00 00 14 09 2A 30 00 00 00 00 55 32 8C 00

08 01 18 01 68 00 00 00 0A 05 14 30 00 00 00 00 00 00 00 00 10 01 50 00 B0 00 00 00 15 09 2C 30

14 09 2A 00 55 32 8C 00 D0 00 50 00 10 01 00 00 10 07 23 30 14 09 2A 00 15 09 2C 00 10 01 60 00

D0 00 00 00 14 0A 2D 30 14 0A 2D 00 10 07 23 00 60 00 10 01 00 01 00 00 14 0A 2D 30 14 0A 2D 00

1F 0E 42 00 98 00 A0 00 F8 00 00 00 5A 4B 96 30 5A 4B 96 00 00 00 00 00 F8 00 88 00 98 00 00 00

00 00 00 30 0B 05 17 00 5A 4B 96 00 F0 00 D8 00 88 00 00 00 00 00 00 30 55 32 8C 00 0B 05 17 00

D8 00 F0 00 C8 00 00 00 55 32 8C 30 00 00 00 00 00 00 00 00 E8 00 D8 00 B8 00 00 00 18 0A 32 30

55 32 8C 00 15 09 2C 00 D8 00 E8 00 88 00 00 00 55 32 8C 30 18 0A 32 00 0B 05 17 00 88 00 E0 00

98 00 00 00 0B 05 17 30 12 08 27 00 5A 4B 96 00 A0 00 98 00 E0 00 00 00 5A 4B 96 30 5A 4B 96 00

12 08 27 00 B8 00 D8 00 A8 00 00 00 15 09 2C 30 55 32 8C 00 14 09 2A 00 C8 00 A8 00 D8 00 00 00

00 00 00 30 14 09 2A 00 55 32 8C 00 50 00 D0 00 80 00 00 00 14 09 2A 30 10 07 23 00 55 32 8C 00

D0 00 A8 00 80 00 00 00 10 07 23 30 14 09 2A 00 55 32 8C 00 B8 00 A8 00 D0 00 00 00 15 09 2C 30

14 09 2A 00 10 07 23 00 A8 00 C8 00 C0 00 00 00 14 09 2A 30 00 00 00 00 00 00 00 00 A8 00 C0 00

80 00 00 00 14 09 2A 30 00 00 00 00 55 32 8C 00 C0 00 50 00 80 00 00 00 00 00 00 30 14 09 2A 00

55 32 8C 00 98 00 88 00 90 00 00 00 5A 4B 96 30 0B 05 17 00 15 09 2D 00 88 00 98 00 90 00 00 00

0B 05 17 30 5A 4B 96 00 15 09 2D 00 40 01 78 01 90 01 00 00 1F 29 17 30 13 1B 0F 00 05 0A 04 00

90 01 70 00 40 01 00 00 05 0A 04 30 1E 28 17 00 14 1C 0F 00 30 01 70 00 58 00 00 00 0E 15 0B 30

46 55 32 00 20 2B 19 00 30 01 40 01 70 00 00 00 0E 15 0B 30 1F 29 17 00 46 55 32 00 70 00 90 01

20 02 00 00 1E 28 17 30 05 0A 04 00 21 2C 19 00 78 01 88 01 90 01 00 00 13 1B 0F 30 04 09 03 00

05 0A 04 00 48 01 70 01 30 01 00 00 25 31 1C 30 28 34 1E 00 1F 29 17 00 70 01 48 01 68 01 00 00

28 34 1E 30 25 31 1C 00 1B 25 15 00 88 01 78 01 68 01 00 00 04 09 03 30 13 1B 0F 00 1B 25 15 00

40 01 30 01 70 01 00 00 1F 29 17 30 1F 29 17 00 28 34 1E 00 38 01 48 01 30 01 00 00 0A 10 08 30

25 31 1C 00 1F 29 17 00 58 00 38 01 30 01 00 00 20 2B 19 30 0A 10 08 00 1F 29 17 00 38 01 58 00

78 00 00 00 0A 10 08 30 20 2B 19 00 0A 10 08 00 20 02 38 01 78 00 00 00 05 0A 04 30 0A 10 08 00

0A 10 08 00 38 01 20 02 90 01 00 00 0A 10 08 30 05 0A 04 00 05 0A 04 00 88 01 38 01 90 01 00 00

04 09 03 30 0A 10 08 00 05 0A 04 00 48 02 38 02 30 02 00 00 14 1C 0F 30 24 2F 1B 00 5A 64 3C 00

60 02 48 02 40 02 00 00 17 20 12 30 14 1C 0F 00 13 1B 0F 00 40 02 48 02 30 02 00 00 13 1B 0F 30

14 1C 0F 00 5A 64 3C 00 48 02 68 02 38 02 00 00 14 1C 0F 30 5A 64 3C 00 24 2F 1B 00 68 02 48 02

58 02 00 00 5A 64 3C 30 14 1C 0F 00 16 1E 10 00 48 02 60 02 58 02 00 00 14 1C 0F 30 17 20 12 00

16 1E 10 00 38 02 40 02 30 02 00 00 24 2F 1B 30 13 1B 0F 00 5A 64 3C 00 68 02 40 02 38 02 00 00

5A 64 3C 30 13 1B 0F 00 24 2F 1B 00 40 02 68 02 60 02 00 00 13 1B 0F 30 5A 64 3C 00 17 20 12 00

40 00 30 00 48 00 00 00 18 21 12 30 17 20 12 00 5A 64 3C 00 38 00 10 00 40 00 00 00 24 2F 1B 30

5A 64 3C 00 18 21 12 00 38 00 40 00 48 00 00 00 24 2F 1B 30 18 21 12 00 5A 64 3C 00 10 00 30 00

40 00 00 00 5A 64 3C 30 17 20 12 00 18 21 12 00 30 00 10 00 20 00 00 00 17 20 12 30 5A 64 3C 00

16 1F 11 00 30 00 38 00 48 00 00 00 17 20 12 30 24 2F 1B 00 5A 64 3C 00 30 00 18 00 38 00 00 00

17 20 12 30 19 22 13 00 24 2F 1B 00 18 00 30 00 20 00 00 00 19 22 13 30 17 20 12 00 16 1F 11 00

10 00 38 00 18 00 00 00 5A 64 3C 30 24 2F 1B 00 19 22 13 00 28 00 10 00 08 00 00 00 01 05 01 30

13 1B 0F 00 11 18 0D 00 10 00 28 00 20 00 00 00 13 1B 0F 30 01 05 01 00 05 0A 04 00 00 00 20 00

28 00 00 00 01 05 01 30 05 0A 04 00 01 05 01 00 28 00 08 00 00 00 00 00 01 05 01 30 11 18 0D 00

01 05 01 00 20 00 00 00 18 00 00 00 05 0A 04 30 01 05 01 00 08 0D 06 00 00 00 10 00 18 00 00 00

01 05 01 30 13 1B 0F 00 08 0D 06 00 00 00 08 00 10 00 00 00 01 05 01 30 11 18 0D 00 13 1B 0F 00

68 02 78 02 60 02 00 00 0B 11 08 30 19 22 13 00 07 0C 05 00 78 02 58 02 60 02 00 00 19 22 13 30

05 0A 04 00 07 0C 05 00 58 02 78 02 50 02 00 00 05 0A 04 30 19 22 13 00 08 0D 06 00 70 02 50 02

78 02 00 00 0D 14 0A 30 08 0D 06 00 19 22 13 00 70 02 78 02 68 02 00 00 0D 14 0A 30 19 22 13 00

0B 11 08 00 68 02 50 02 70 02 00 00 0B 11 08 30 08 0D 06 00 0D 14 0A 00 50 02 68 02 58 02 00 00

08 0D 06 30 0B 11 08 00 05 0A 04 00 88 01 60 01 80 01 00 00 1C 15 33 30 22 1A 39 00 1E 16 34 00

58 01 88 01 80 01 00 00 1F 17 36 30 1C 15 33 00 1E 16 34 00 60 01 58 01 80 01 00 00 22 1A 39 30

1F 17 36 00 1E 16 34 00 88 01 68 01 60 01 00 00 1C 15 33 30 2A 1F 40 00 22 1A 39 00 58 01 60 01

50 01 00 00 1F 17 36 30 22 1A 39 00 6A 50 7F 00 60 01 48 01 50 01 00 00 22 1A 39 30 66 4C 7A 00

6A 50 7F 00 68 01 48 01 60 01 00 00 2A 1F 40 30 66 4C 7A 00 22 1A 39 00 48 01 58 01 50 01 00 00

66 4C 7A 30 1F 17 36 00 6A 50 7F 00 38 01 88 01 58 01 00 00 1F 17 36 30 1C 15 33 00 1F 17 36 00

48 01 38 01 58 01 00 00 66 4C 7A 30 1F 17 36 00 1F 17 36 00 03 00 00 00 E0 00 E8 00 D0 01 C8 01

12 08 27 38 18 0A 32 00 12 08 27 00 18 0A 32 00 C0 01 F0 00 B8 01 F8 00 00 00 00 38 00 00 00 00

00 00 00 00 00 00 00 00 40 01 70 01 78 01 68 01 FF 2A 9B 38 90 1C 68 00 3A 04 0F 00 51 0A 27 00

  
  
9th Weapon Bone Data \[at offset 0x0001294C\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 D8 02 00 00 0E 00 F8 FF CA FF 00 00 0F 00 F8 FF B8 FF 00 00

F4 FF F0 FF CA FF 00 00 F1 FF EE FF B8 FF 00 00 F6 FF 0A 00 B8 FF 00 00 F8 FF 07 00 CA FF 00 00

0E 00 F8 FF A3 00 00 00 F4 FF F0 FF A3 00 00 00 F8 FF 07 00 A3 00 00 00 F8 FF 31 00 92 FF 00 00

F8 FF 31 00 71 FF 00 00 02 00 43 00 79 FF 00 00 02 00 43 00 8B FF 00 00 14 00 40 00 8B FF 00 00

14 00 40 00 79 FF 00 00 18 00 2C 00 71 FF 00 00 18 00 2C 00 92 FF 00 00 22 00 83 00 8D FF 00 00

09 00 87 00 8D FF 00 00 16 00 85 00 74 FF 00 00 03 00 42 00 8A FF 00 00 0B 00 41 00 7B FF 00 00

12 00 40 00 8A FF 00 00 FC FF B1 FF 8A FF 00 00 F4 FF B3 FF 7B FF 00 00 ED FF B4 FF 8A FF 00 00

E9 FF 6F FF 74 FF 00 00 DD FF 71 FF 8D FF 00 00 F6 FF 6D FF 8D FF 00 00 07 00 C3 FF 92 FF 00 00

07 00 C3 FF 71 FF 00 00 FD FF B1 FF 79 FF 00 00 FD FF B1 FF 8B FF 00 00 EB FF B4 FF 8B FF 00 00

EB FF B4 FF 79 FF 00 00 E7 FF C8 FF 71 FF 00 00 E7 FF C8 FF 92 FF 00 00 13 00 F7 FF C0 FF 00 00

EE FF FD FF C0 FF 00 00 0C 00 CC FF AD FF 00 00 E7 FF D2 FF AD FF 00 00 09 00 BA FF 81 FF 00 00

E4 FF C0 FF 81 FF 00 00 0C 00 CC FF 55 FF 00 00 E7 FF D2 FF 55 FF 00 00 13 00 F7 FF 43 FF 00 00

EE FF FD FF 43 FF 00 00 1A 00 22 00 55 FF 00 00 F5 FF 28 00 55 FF 00 00 1D 00 34 00 81 FF 00 00

F8 FF 3A 00 81 FF 00 00 1A 00 22 00 AD FF 00 00 F5 FF 28 00 AD FF 00 00 0E 00 F8 FF 8D FF 00 00

10 00 02 00 81 FF 00 00 0E 00 F8 FF 76 FF 00 00 0D 00 ED FF 81 FF 00 00 F5 FF B7 FF C9 FD 00 00

FA FF CF FF 55 FF 00 00 F3 FF AA FF 9F FD 00 00 EF FF 95 FF 81 FD 00 00 EC FF 83 FF 79 FD 00 00

F5 FF B7 FF 45 FD 00 00 F0 FF 98 FF 5F FD 00 00 F6 FF BE FF 59 FD 00 00 FB FF D0 FF 6C FD 00 00

FC FF D6 FF 6C FD 00 00 07 00 E3 FF 4C FF 00 00 0B 00 E9 FF 4A FF 00 00 10 00 06 00 4A FF 00 00

0E 00 0D 00 4C FF 00 00 07 00 1D 00 6C FD 00 00 08 00 23 00 6C FD 00 00 09 00 36 00 59 FD 00 00

0F 00 5C 00 5F FD 00 00 0A 00 3D 00 46 FD 00 00 12 00 71 00 79 FD 00 00 0F 00 5F 00 81 FD 00 00

0C 00 4A 00 9F FD 00 00 07 00 25 00 55 FF 00 00 0A 00 3D 00 C9 FD 00 00 00 00 FA FF 34 FD 00 00

00 00 FA FF 47 FD 00 00 00 00 FA FF 47 FD 00 00 09 00 36 00 59 FD 00 00 01 00 FA FF 6C FD 00 00

F6 FF BE FF 59 FD 00 00 08 00 22 00 2B FF 00 00 FC FF D1 FF 2B FF 00 00 0D 00 F8 FF 43 FF 00 00

F4 FF FC FF 43 FF 00 00 00 00 20 00 00 00 00 00 49 00 00 00 08 02 20 02 10 02 00 00 0F 0F 0F 30

06 06 06 00 0E 0E 0E 00 20 02 08 02 18 02 00 00 06 06 06 30 0F 0F 0F 00 07 07 07 00 40 02 28 02

30 02 00 00 0E 0E 0E 30 09 09 09 00 06 06 06 00 28 02 40 02 38 02 00 00 09 09 09 30 0E 0E 0E 00

0E 0E 0E 00 F0 01 98 02 B0 02 00 00 A9 B2 B2 30 5A 5A 66 00 5A 5A 66 00 B0 02 F8 01 F0 01 00 00

5A 5A 66 30 7F 86 86 00 A9 B2 B2 00 E0 01 F8 01 B0 02 00 00 5A 52 8B 30 7F 86 86 00 5A 5A 66 00

50 02 68 02 A0 02 00 00 7F 86 86 30 5A 52 8B 00 5A 5A 66 00 50 02 A0 02 58 02 00 00 7F 86 86 30

5A 5A 66 00 A9 B2 B2 00 98 02 58 02 A0 02 00 00 5A 5A 66 30 A9 B2 B2 00 5A 5A 66 00 58 02 98 02

88 02 00 00 A9 B2 B2 30 5A 5A 66 00 A9 B2 B2 00 98 02 F0 01 88 02 00 00 5A 5A 66 30 A9 B2 B2 00

A9 B2 B2 00 F0 01 00 02 90 02 00 00 CF DA DA 30 8C 91 9B 00 8C 91 9B 00 F0 01 90 02 88 02 00 00

CF DA DA 30 8C 91 9B 00 CF DA DA 00 90 02 58 02 88 02 00 00 8C 91 9B 30 CF DA DA 00 CF DA DA 00

58 02 90 02 48 02 00 00 CF DA DA 30 8C 91 9B 00 8C 91 9B 00 68 02 50 02 48 02 00 00 6E 64 AA 30

9C A4 A4 00 8C 91 9B 00 50 02 68 02 60 02 00 00 9C A4 A4 30 6E 64 AA 00 67 6D 6D 00 68 02 50 02

60 02 00 00 5A 52 8B 30 7F 86 86 00 54 59 59 00 48 02 50 02 58 02 00 00 8C 91 9B 30 9C A4 A4 00

CF DA DA 00 F8 01 E0 01 00 02 00 00 9C A4 A4 30 6E 64 AA 00 8C 91 9B 00 F8 01 00 02 F0 01 00 00

9C A4 A4 30 8C 91 9B 00 CF DA DA 00 E0 01 F8 01 E8 01 00 00 6E 64 AA 30 9C A4 A4 00 9C A4 A4 00

F8 01 E0 01 E8 01 00 00 7F 86 86 30 5A 52 8B 00 7F 86 86 00 C8 01 18 02 08 02 00 00 74 76 C7 30

1C 13 39 00 96 9B FE 00 08 02 D8 01 C8 01 00 00 96 9B FE 30 74 76 C7 00 74 76 C7 00 D8 01 08 02

E0 01 00 00 74 76 C7 30 96 9B FE 00 6E 64 AA 00 38 02 90 02 10 02 00 00 96 9B FE 30 96 9A FF 00

96 9B FE 00 10 02 C8 02 38 02 00 00 96 9B FE 30 1D 15 3B 00 96 9B FE 00 90 02 38 02 48 02 00 00

96 9A FF 30 96 9B FE 00 96 9A FF 00 48 02 40 02 68 02 00 00 96 9A FF 30 96 9B FE 00 6E 64 AA 00

40 02 70 02 68 02 00 00 96 9B FE 30 74 76 C7 00 6E 64 AA 00 70 02 40 02 80 02 00 00 74 76 C7 30

96 9B FE 00 74 76 C7 00 30 02 80 02 40 02 00 00 1C 13 38 30 74 76 C7 00 96 9B FE 00 30 02 B8 02

80 02 00 00 1C 13 38 30 17 0D 30 00 74 76 C7 00 B8 02 30 02 78 02 00 00 17 0D 30 30 1C 13 38 00

19 10 34 00 38 02 C8 02 28 02 00 00 96 9B FE 30 1D 15 3B 00 1E 15 3B 00 20 02 C8 02 10 02 00 00

1B 12 36 30 1D 15 3B 00 96 9B FE 00 18 02 C0 02 D0 01 00 00 1C 13 39 30 27 20 4A 00 1D 14 3A 00

18 02 C8 01 C0 02 00 00 1C 13 39 30 74 76 C7 00 27 20 4A 00 D0 02 C0 02 C8 01 00 00 15 0D 2B 30

1F 1A 3C 00 5F 60 A3 00 C0 02 D0 02 D0 01 00 00 1F 1A 3C 30 15 0D 2B 00 17 10 2F 00 D0 02 C8 01

A8 02 00 00 15 0D 2B 30 5F 60 A3 00 43 41 76 00 80 02 D0 02 A8 02 00 00 5F 60 A3 30 15 0D 2B 00

43 41 76 00 D8 01 A8 02 C8 01 00 00 5F 60 A3 30 43 41 76 00 5F 60 A3 00 B0 02 A8 02 E0 01 00 00

52 4D 8B 30 43 41 76 00 5A 52 8B 00 A8 02 D8 01 E0 01 00 00 43 41 76 30 5F 60 A3 00 5A 52 8B 00

A8 02 A0 02 68 02 00 00 43 41 76 30 52 4D 8B 00 5A 52 8B 00 A8 02 70 02 80 02 00 00 43 41 76 30

5F 60 A3 00 5F 60 A3 00 70 02 A8 02 68 02 00 00 5F 60 A3 30 43 41 76 00 5A 52 8B 00 D0 02 80 02

B8 02 00 00 15 0D 2B 30 5F 60 A3 00 12 0A 27 00 D0 02 B8 02 78 02 00 00 15 0D 2B 30 12 0A 27 00

14 0D 2A 00 00 02 08 02 10 02 00 00 96 9A FF 30 96 9B FE 00 96 9B FE 00 08 02 00 02 E0 01 00 00

96 9B FE 30 96 9A FF 00 6E 64 AA 00 10 02 90 02 00 02 00 00 96 9B FE 30 96 9A FF 00 96 9A FF 00

40 02 48 02 38 02 00 00 96 9B FE 30 96 9A FF 00 96 9B FE 00 A8 01 38 01 28 01 00 00 20 1C 29 30

20 1C 29 00 16 12 1F 00 38 01 A8 01 C0 01 00 00 20 1C 29 30 20 1C 29 00 1F 1B 28 00 A8 01 98 01

B0 01 00 00 20 1C 29 30 13 0F 1D 00 21 1D 2A 00 98 01 A8 01 28 01 00 00 13 0F 1D 30 53 4F 5A 00

16 12 1F 00 B0 01 98 01 88 01 00 00 21 1D 2A 30 13 0F 1D 00 12 0E 1C 00 B0 01 78 01 B8 01 00 00

21 1D 2A 30 18 14 21 00 1F 1B 28 00 78 01 B0 01 88 01 00 00 18 14 21 30 53 4F 5A 00 12 0E 1C 00

B8 01 78 01 68 01 00 00 1F 1B 28 30 18 14 21 00 23 1F 2C 00 B8 01 58 01 C0 01 00 00 1F 1B 28 30

2A 26 32 00 1F 1B 28 00 58 01 B8 01 68 01 00 00 2A 26 32 30 53 4F 5A 00 23 1F 2C 00 C0 01 58 01

48 01 00 00 1F 1B 28 30 2A 26 32 00 28 24 30 00 38 01 C0 01 48 01 00 00 20 1C 29 30 53 4F 5A 00

28 24 30 00 80 01 60 01 70 01 00 00 12 15 1C 30 1C 22 23 00 14 17 1E 00 30 01 40 01 A0 01 00 00

19 1C 21 30 1A 1E 22 00 16 1A 1F 00 38 00 40 00 30 00 00 00 00 09 15 30 00 07 0F 00 00 0D 1E 00

D8 00 E0 00 D0 00 00 00 28 28 28 30 62 62 62 00 96 96 96 00 88 00 90 00 98 00 00 00 10 10 10 30

14 14 14 00 46 46 46 00 22 00 00 00 A0 02 A8 02 98 02 B0 02 52 4D 8B 38 43 41 76 00 52 4D 8B 00

52 4D 8B 00 A8 01 B0 01 C0 01 B8 01 6E 46 AA 38 6E 46 AA 00 6E 46 AA 00 6E 46 AA 00 70 01 68 01

80 01 78 01 19 1D 16 38 30 3B 29 00 32 2D 37 00 32 2D 37 00 90 01 50 01 80 01 60 01 13 16 1D 38

20 26 27 00 17 1A 1F 00 14 17 1E 00 80 01 78 01 90 01 88 01 32 2D 37 38 32 2D 37 00 13 16 11 00

13 15 11 00 50 01 48 01 60 01 58 01 20 26 1C 38 38 45 2F 00 50 64 64 00 73 82 82 00 60 01 58 01

70 01 68 01 50 64 64 38 73 82 82 00 19 1D 16 00 30 3B 29 00 A0 01 40 01 90 01 50 01 16 1A 1F 38

1A 1E 22 00 13 16 1D 00 20 26 27 00 90 01 88 01 A0 01 98 01 14 14 14 38 14 14 14 00 18 18 18 00

15 15 15 00 40 01 38 01 50 01 48 01 1C 1C 1C 38 30 30 30 00 23 23 23 00 3E 3E 3E 00 A0 01 98 01

30 01 28 01 18 18 18 38 15 15 15 00 1A 1A 1A 00 1B 1B 1B 00 30 01 28 01 40 01 38 01 1A 1A 1A 38

1B 1B 1B 00 1C 1C 1C 00 30 30 30 00 10 00 28 00 38 00 40 00 00 11 28 38 00 05 0B 00 00 09 15 00

00 07 0F 00 00 00 10 00 30 00 38 00 00 16 32 38 00 11 28 00 00 0D 1E 00 00 09 15 00 28 00 00 00

40 00 30 00 00 05 0B 38 00 16 32 00 00 07 0F 00 00 0D 1E 00 00 00 08 00 10 00 18 00 83 72 1C 38

9E 8A 22 00 68 5A 17 00 84 72 1C 00 28 00 20 00 00 00 08 00 1C 18 06 38 25 20 08 00 83 72 1C 00

9E 8A 22 00 10 00 18 00 28 00 20 00 68 5A 17 38 84 72 1C 00 1C 18 06 00 25 20 08 00 C0 00 C8 00

D0 00 D8 00 12 12 12 38 14 14 14 00 96 96 96 00 1E 1E 1E 00 C8 00 B8 00 D8 00 E0 00 14 14 14 38

10 10 10 00 1E 1E 1E 00 4B 4B 4B 00 B8 00 C0 00 E0 00 D0 00 10 10 10 38 12 12 12 00 4B 4B 4B 00

96 96 96 00 B0 00 A0 00 88 00 90 00 1D 1D 1D 38 1E 1E 1E 00 10 10 10 00 14 14 14 00 A8 00 B0 00

98 00 88 00 23 23 23 38 1D 1D 1D 00 96 96 96 00 10 10 10 00 A0 00 A8 00 90 00 98 00 1E 1E 1E 38

23 23 23 00 14 14 14 00 96 96 96 00 00 01 F8 00 08 01 10 01 D7 BA 2E 38 FF FF 43 00 60 54 15 00

C1 A7 2A 00 E8 00 F0 00 00 01 F8 00 38 30 0C 38 8D 7B 1F 00 D7 BA 2E 00 FF FF 43 00 20 01 E8 00

08 01 00 01 42 39 0E 38 38 30 0C 00 60 54 15 00 D7 BA 2E 00 F0 00 18 01 F8 00 10 01 8D 7B 1F 38

43 3A 0E 00 FF FF 43 00 C1 A7 2A 00 08 01 10 01 20 01 18 01 60 54 15 38 C1 A7 2A 00 42 39 0E 00

43 3A 0E 00 70 00 68 00 58 00 60 00 28 23 09 38 2D 27 0A 00 31 2B 0B 00 34 2D 0B 00 78 00 80 00

70 00 68 00 FF F8 3E 38 9E 8A 22 00 28 23 09 00 2D 27 0A 00 50 00 78 00 58 00 70 00 7A 6A 1A 38

FF F8 3E 00 31 2B 0B 00 28 23 09 00 80 00 48 00 68 00 60 00 9E 8A 22 38 50 45 11 00 2D 27 0A 00

34 2D 0B 00 58 00 60 00 50 00 48 00 31 2B 0B 38 34 2D 0B 00 7A 6A 1A 00 50 45 11 00

  
  
10th Weapon Bone Data \[at offset 0x00013528\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 28 02 00 00 FC FF 10 00 B9 FF 00 00 0A 00 0E 00 B9 FF 00 00

05 00 F1 FF B9 FF 00 00 F7 FF F3 FF B9 FF 00 00 F7 FF F3 FF 90 00 00 00 FC FF 10 00 90 00 00 00

0A 00 0E 00 90 00 00 00 05 00 F1 FF 90 00 00 00 FA FF F7 FF 9B 00 00 00 FD FF 0C 00 9B 00 00 00

07 00 0A 00 9B 00 00 00 03 00 F5 FF 9B 00 00 00 0C 00 11 00 B3 FF 00 00 06 00 EC FF B3 FF 00 00

F4 FF EF FF B3 FF 00 00 FB FF 14 00 B3 FF 00 00 F4 FF EF FF B9 FF 00 00 FB FF 14 00 B9 FF 00 00

0C 00 11 00 B9 FF 00 00 06 00 EC FF B9 FF 00 00 04 00 F0 FF 9E FF 00 00 F7 FF F2 FF 9E FF 00 00

04 00 F0 FF A9 FF 00 00 F7 FF F2 FF A9 FF 00 00 FC FF 10 00 A9 FF 00 00 09 00 0E 00 A9 FF 00 00

FC FF 10 00 9E FF 00 00 09 00 0E 00 9E FF 00 00 2C 00 F9 FF A9 FF 00 00 2C 00 F9 FF B3 FF 00 00

1A 00 DC FF A9 FF 00 00 1A 00 DC FF B3 FF 00 00 F9 FF D4 FF A9 FF 00 00 F9 FF D4 FF B3 FF 00 00

DC FF E6 FF A9 FF 00 00 DC FF E6 FF B3 FF 00 00 D4 FF 07 00 A9 FF 00 00 D4 FF 07 00 B3 FF 00 00

E6 FF 24 00 A9 FF 00 00 E6 FF 24 00 B3 FF 00 00 07 00 2C 00 A9 FF 00 00 07 00 2C 00 B3 FF 00 00

24 00 1A 00 A9 FF 00 00 24 00 1A 00 B3 FF 00 00 02 00 0E 00 9E FF 00 00 03 00 12 00 BB FE 00 00

03 00 F6 FF BB FE 00 00 02 00 F2 FF 9E FF 00 00 FA FF F3 FF 9E FF 00 00 FA FF F7 FF BB FE 00 00

05 00 03 00 BB FE 00 00 04 00 00 00 9E FF 00 00 FD FF 04 00 BB FE 00 00 FC FF 00 00 9E FF 00 00

FC FF FF FF 1A FE 00 00 F9 FF F1 FF 1B FE 00 00 02 00 F0 FF 1B FE 00 00 04 00 FE FF 1A FE 00 00

02 00 0C 00 1A FE 00 00 F9 FF EC FF 82 FD 00 00 F8 FF CE FF 3B FD 00 00 01 00 EA FF 82 FD 00 00

FF FF F6 FF 6B FD 00 00 FF FF EA FF D4 FD 00 00 FB FF EA FF D4 FD 00 00 FC FF 10 00 A9 FF 00 00

F7 FF F2 FF A9 FF 00 00 04 00 F0 FF A9 FF 00 00 09 00 0E 00 A9 FF 00 00 00 00 20 00 00 00 00 00

0D 00 00 00 E0 01 E8 01 F0 01 00 00 1E 23 23 30 05 0A 0F 00 B4 BE BE 00 E0 01 F0 01 D8 01 00 00

16 19 19 30 96 A0 A0 00 00 05 0A 00 F8 01 E8 01 E0 01 00 00 29 3A 56 30 1C 28 3B 00 22 32 49 00

E8 01 F8 01 C8 01 00 00 1C 28 3B 30 29 3A 56 00 18 23 34 00 C8 01 F8 01 C0 01 00 00 18 23 34 30

29 3A 56 00 29 3B 56 00 00 02 D8 01 B0 01 00 00 10 18 23 30 0A 0F 16 00 09 0E 15 00 B0 01 B8 01

00 02 00 00 09 0E 15 30 0E 15 1E 00 10 18 23 00 D8 01 00 02 E0 01 00 00 0A 0F 16 30 10 18 23 00

22 32 49 00 00 02 F8 01 E0 01 00 00 10 18 23 30 29 3A 56 00 22 32 49 00 00 01 10 02 10 01 00 00

A9 A9 A9 30 4B 50 50 00 5F 64 64 00 10 01 10 02 20 01 00 00 5F 64 64 30 4B 50 50 00 23 28 28 00

50 01 20 02 E0 00 00 00 5F 64 64 30 4B 50 50 00 A5 AF AF 00 08 02 40 01 30 01 00 00 1E 23 23 30

50 55 55 00 28 2D 2D 00 30 00 00 00 C8 01 D0 01 E8 01 F0 01 14 18 28 38 DC F0 EB 00 14 18 28 00

DC F0 EB 00 90 01 68 01 C8 01 D0 01 14 18 28 38 DC F0 EB 00 14 18 28 00 DC F0 EB 00 60 01 68 01

98 01 90 01 DC F0 EB 38 DC F0 EB 00 14 18 28 00 14 18 28 00 F0 01 D0 01 D8 01 B0 01 A3 B2 AE 38

A3 B2 AE 00 0E 11 1D 00 0E 11 1D 00 D0 01 68 01 B0 01 A0 01 A3 B2 AE 38 A3 B2 AE 00 0E 11 1D 00

0E 11 1D 00 68 01 60 01 A0 01 A8 01 A3 B2 AE 38 A3 B2 AE 00 0E 11 1D 00 0E 11 1D 00 70 01 90 01

C0 01 C8 01 29 3B 57 38 18 23 32 00 29 3B 56 00 18 23 34 00 98 01 90 01 78 01 70 01 0A 0F 17 38

18 23 32 00 1C 29 3C 00 29 3B 57 00 80 01 88 01 A8 01 A0 01 0C 11 19 38 0E 15 1F 00 0A 0E 16 00

09 0E 15 00 78 01 70 01 80 01 88 01 1C 29 3C 38 29 3B 57 00 0C 11 19 00 0E 15 1F 00 A0 01 88 01

B0 01 B8 01 09 0E 15 38 0E 15 1F 00 09 0E 15 00 0E 15 1E 00 88 01 70 01 B8 01 C0 01 0E 15 1F 38

29 3B 57 00 0E 15 1E 00 29 3B 56 00 F8 01 00 02 C0 01 B8 01 29 3A 56 38 10 18 23 00 29 3B 56 00

0E 15 1E 00 30 00 38 00 50 00 58 00 1C 18 06 38 B2 9B 27 00 28 23 09 00 66 58 16 00 48 00 50 00

40 00 58 00 2E 28 0A 38 28 23 09 00 36 2F 0C 00 66 58 16 00 38 00 20 00 58 00 40 00 B2 9B 27 38

3D 35 0D 00 66 58 16 00 36 2F 0C 00 28 00 30 00 48 00 50 00 1F 1B 07 38 1C 18 06 00 2E 28 0A 00

28 23 09 00 20 00 28 00 40 00 48 00 3D 35 0D 38 1F 1B 07 00 36 2F 0C 00 2E 28 0A 00 08 00 10 00

30 00 38 00 0F 06 17 38 36 14 51 00 07 03 0B 00 2D 11 44 00 10 00 18 00 38 00 20 00 36 14 51 38

1C 0B 2A 00 2D 11 44 00 0F 06 17 00 00 00 08 00 28 00 30 00 0A 04 10 38 0F 06 17 00 08 03 0C 00

07 03 0B 00 18 00 00 00 20 00 28 00 1C 0B 2A 38 0A 04 10 00 0F 06 17 00 08 03 0C 00 88 00 90 00

80 00 98 00 2A 25 09 38 24 1F 08 00 39 32 0C 00 84 73 1D 00 70 00 78 00 80 00 88 00 70 61 18 38

2A 24 09 00 39 32 0C 00 2A 25 09 00 78 00 60 00 88 00 90 00 2A 24 09 38 3E 35 0D 00 2A 25 09 00

24 1F 08 00 60 00 68 00 90 00 98 00 3E 35 0D 38 D5 B9 2E 00 24 1F 08 00 84 73 1D 00 68 00 70 00

98 00 80 00 D5 B9 2E 38 70 61 18 00 84 73 1D 00 39 32 0C 00 F8 00 F0 00 08 01 00 01 27 29 33 38

43 47 58 00 1F 21 29 00 3D 41 51 00 E8 00 E0 00 F8 00 F0 00 17 18 1E 38 32 35 42 00 27 29 33 00

43 47 58 00 58 01 50 01 E8 00 E0 00 0C 0D 10 38 15 16 1B 00 17 18 1E 00 32 35 42 00 48 01 40 01

58 01 50 01 0C 0D 10 38 0A 0A 0D 00 0C 0D 10 00 15 16 1B 00 18 01 10 01 28 01 20 01 12 13 17 38

24 26 30 00 10 11 15 00 11 12 16 00 08 01 00 01 18 01 10 01 1F 21 29 38 3D 41 51 00 12 13 17 00

24 26 30 00 28 01 20 01 38 01 30 01 10 11 15 38 11 12 16 00 0E 0F 12 00 0D 0E 12 00 38 01 30 01

48 01 40 01 0E 0F 12 38 0D 0E 12 00 0C 0D 10 00 0A 0A 0D 00 10 02 18 02 08 02 20 02 6C 6C 6C 38

6C 6C 6C 00 6C 6C 6C 00 6C 6C 6C 00 00 01 F0 00 10 02 18 02 A9 A9 A9 38 B8 B8 B8 00 4B 50 50 00

4B 50 50 00 40 01 08 02 50 01 20 02 50 55 55 38 1E 23 23 00 5F 64 64 00 4B 50 50 00 E8 00 38 01

58 01 48 01 39 37 3C 38 22 21 24 00 1E 1D 1F 00 1F 1D 20 00 E8 00 F8 00 38 01 28 01 39 37 3C 38

61 5D 65 00 22 21 24 00 28 26 2A 00 28 01 F8 00 18 01 08 01 28 26 2A 38 61 5D 65 00 2C 2B 2E 00

4E 4A 51 00 30 01 20 01 08 02 10 02 28 2D 2D 38 1E 23 23 00 1E 23 23 00 4B 50 50 00 F0 00 E0 00

18 02 20 02 B8 B8 B8 38 A5 AF AF 00 4B 50 50 00 4B 50 50 00 D0 00 A8 00 D8 00 A0 00 27 20 08 38

69 57 17 00 39 2F 0C 00 C7 A6 2D 00 A8 00 D0 00 B8 00 C0 00 69 57 17 38 27 20 08 00 35 2C 0B 00

27 21 08 00 D0 00 D8 00 C0 00 C8 00 27 20 08 38 39 2F 0C 00 27 21 08 00 21 1B 07 00 A0 00 A8 00

B0 00 B8 00 C7 A6 2D 38 69 57 17 00 7B 67 1C 00 35 2C 0B 00 D8 00 A0 00 C8 00 B0 00 39 2F 0C 38

C7 A6 2D 00 21 1B 07 00 7B 67 1C 00

  
  
11th Weapon Bone Data \[at offset 0x00013CF4\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 A0 02 00 00 03 00 18 00 E8 FE 00 00 03 00 18 00 EE FE 00 00

FC FF 33 00 05 FF 00 00 FC FF 32 00 0B FF 00 00 F9 FF 3C 00 00 FF 00 00 FA FF 37 00 14 FF 00 00

FB FF 35 00 FE FE 00 00 FD FF 30 00 12 FF 00 00 FA FF D9 FF 9B FE 00 00 FA FF D9 FF A1 FE 00 00

FA FF B2 FF 8C FE 00 00 FA FF B0 FF 91 FE 00 00 FA FF AE FF 82 FE 00 00 FA FF A6 FF 95 FE 00 00

FA FF B5 FF 84 FE 00 00 FA FF AD FF 98 FE 00 00 DB FF 00 00 CE FE 00 00 DB FF 00 00 D3 FE 00 00

BC FF 01 00 D1 FE 00 00 BE FF 01 00 D6 FE 00 00 B1 FF 01 00 CE FE 00 00 BB FF 01 00 E0 FE 00 00

B7 FF 01 00 CA FE 00 00 C2 FF 00 00 DD FE 00 00 D7 FF 00 00 60 FE 00 00 D7 FF 00 00 65 FE 00 00

B7 FF 0C 00 40 FE 00 00 B5 FF 0D 00 45 FE 00 00 B3 FF 0D 00 36 FE 00 00 AB FF 10 00 4A FE 00 00

B9 FF 0B 00 39 FE 00 00 B2 FF 0E 00 4D FE 00 00 24 00 F4 FF 99 FE 00 00 24 00 F4 FF 9E FE 00 00

4A 00 FF FF 84 FE 00 00 4C 00 00 00 89 FE 00 00 4E 00 00 00 7A FE 00 00 56 00 02 00 8E FE 00 00

48 00 FF FF 7D FE 00 00 4F 00 00 00 91 FE 00 00 1F 00 F4 FF 24 FF 00 00 1F 00 F4 FF 29 FF 00 00

43 00 E5 FF 32 FF 00 00 42 00 E5 FF 38 FF 00 00 4C 00 E1 FF 2C FF 00 00 48 00 E3 FF 41 FF 00 00

45 00 E4 FF 2A FF 00 00 41 00 E6 FF 40 FF 00 00 03 00 16 00 39 FF 00 00 01 00 0D 00 99 FF 00 00

1F 00 F4 FF 39 FF 00 00 15 00 F6 FF 99 FF 00 00 FA FF DD FF 39 FF 00 00 FC FF E6 FF 99 FF 00 00

DE FF FF FF 39 FF 00 00 E8 FF FE FF 99 FF 00 00 28 00 F3 FF 30 FE 00 00 04 00 1D 00 30 FE 00 00

D6 FF 00 00 30 FE 00 00 F9 FF D6 FF 30 FE 00 00 24 00 F4 FF 10 FE 00 00 04 00 1A 00 10 FE 00 00

D9 FF 00 00 10 FE 00 00 FA FF D9 FF 10 FE 00 00 10 00 F7 FF 01 FE 00 00 01 00 08 00 01 FE 00 00

ED FF FD FF 01 FE 00 00 FD FF EB FF 01 FE 00 00 EE FF FD FF FD FF 00 00 01 00 08 00 FD FF 00 00

10 00 F7 FF FD FF 00 00 FD FF EB FF FD FF 00 00 EE FF FD FF 87 00 00 00 01 00 08 00 87 00 00 00

10 00 F7 FF 87 00 00 00 FD FF EB FF 87 00 00 00 E4 FF FE FF 8F 00 00 00 02 00 11 00 8F 00 00 00

19 00 F5 FF 8F 00 00 00 FB FF E2 FF 8F 00 00 00 E4 FF FE FF 9F 00 00 00 02 00 11 00 9F 00 00 00

19 00 F5 FF 9F 00 00 00 FB FF E2 FF 9F 00 00 00 00 00 20 00 00 00 00 00 1C 00 00 00 18 01 28 01

38 01 00 00 39 3B 43 30 1E 1F 23 00 3B 3D 45 00 28 01 18 01 38 01 00 00 1E 1F 23 30 39 3B 43 00

3B 3D 45 00 10 01 20 01 30 01 00 00 39 3B 43 30 7D 82 94 00 3A 3C 44 00 20 01 10 01 30 01 00 00

7D 82 94 30 39 3B 43 00 3A 3C 44 00 58 01 68 01 78 01 00 00 1E 1F 23 30 1E 1F 23 00 32 33 3B 00

68 01 58 01 78 01 00 00 1E 1F 23 30 1E 1F 23 00 32 33 3B 00 50 01 60 01 70 01 00 00 96 9B B1 30

75 79 8A 00 36 38 3F 00 60 01 50 01 70 01 00 00 75 79 8A 30 96 9B B1 00 36 38 3F 00 18 00 28 00

38 00 00 00 2A 2C 32 30 97 9D B3 00 97 9C B2 00 28 00 18 00 38 00 00 00 97 9D B3 30 2A 2C 32 00

97 9C B2 00 10 00 20 00 30 00 00 00 38 3A 43 30 1E 1F 23 00 C6 CD E9 00 20 00 10 00 30 00 00 00

1E 1F 23 30 38 3A 43 00 C6 CD E9 00 58 00 68 00 78 00 00 00 39 3B 43 30 C2 C8 E4 00 36 38 3F 00

68 00 58 00 78 00 00 00 C2 C8 E4 30 39 3B 43 00 36 38 3F 00 50 00 60 00 70 00 00 00 1E 1F 23 30

3A 3C 44 00 1E 1F 23 00 60 00 50 00 70 00 00 00 3A 3C 44 30 1E 1F 23 00 1E 1F 23 00 D8 00 E8 00

F8 00 00 00 CC D3 F0 30 3A 3C 44 00 37 39 41 00 E8 00 D8 00 F8 00 00 00 3A 3C 44 30 CC D3 F0 00

37 39 41 00 D0 00 E0 00 F0 00 00 00 1E 1F 23 30 3A 3C 44 00 BA C1 DC 00 E0 00 D0 00 F0 00 00 00

3A 3C 44 30 1E 1F 23 00 BA C1 DC 00 98 00 A8 00 B8 00 00 00 C2 C9 E5 30 1E 1F 23 00 67 6A 79 00

A8 00 98 00 B8 00 00 00 1E 1F 23 30 C2 C9 E5 00 67 6A 79 00 90 00 A0 00 B0 00 00 00 1E 1F 23 30

C6 CD E9 00 90 95 AA 00 A0 00 90 00 B0 00 00 00 C6 CD E9 30 1E 1F 23 00 90 95 AA 00 98 02 88 02

90 02 00 00 3B 2A 1C 30 23 10 09 00 33 21 16 00 08 02 18 02 00 02 00 00 25 12 0B 30 54 45 31 00

4B 3C 2A 00 88 02 98 02 80 02 00 00 23 10 09 30 3B 2A 1C 00 29 16 0E 00 08 02 10 02 18 02 00 00

25 12 0B 30 2F 1D 13 00 54 45 31 00 38 00 00 00 C8 01 80 01 D0 01 B0 01 1F 21 22 38 1F 21 22 00

38 3B 3F 00 39 3C 3F 00 90 01 80 01 C0 01 C8 01 64 6E 78 38 1F 21 22 00 64 6E 78 00 1F 21 22 00

D8 01 A0 01 C0 01 90 01 A8 B2 BC 38 A8 B2 BC 00 64 6E 78 00 64 6E 78 00 B0 01 A0 01 D0 01 D8 01

39 3C 3F 38 A8 B2 BC 00 38 3B 3F 00 A8 B2 BC 00 18 01 10 01 08 01 00 01 39 3B 43 38 39 3B 43 00

3A 3C 44 00 40 42 4B 00 18 01 28 01 10 01 20 01 39 3B 43 38 1E 1F 23 00 39 3B 43 00 7D 82 94 00

10 01 20 01 18 01 28 01 39 3B 43 38 7D 82 94 00 39 3B 43 00 1E 1F 23 00 10 01 18 01 00 01 08 01

39 3B 43 38 39 3B 43 00 40 42 4B 00 3A 3C 44 00 58 01 50 01 48 01 40 01 1E 1F 23 38 96 9B B1 00

32 33 3A 00 36 38 3F 00 58 01 68 01 50 01 60 01 1E 1F 23 38 1E 1F 23 00 96 9B B1 00 75 79 8A 00

50 01 60 01 58 01 68 01 96 9B B1 38 75 79 8A 00 1E 1F 23 00 1E 1F 23 00 50 01 58 01 40 01 48 01

96 9B B1 38 1E 1F 23 00 36 38 3F 00 32 33 3A 00 18 00 10 00 08 00 00 00 2A 2C 32 38 38 3A 43 00

AC B1 CA 00 B9 BF DA 00 18 00 28 00 10 00 20 00 2A 2C 32 38 97 9D B3 00 38 3A 43 00 1E 1F 23 00

10 00 20 00 18 00 28 00 38 3A 43 38 1E 1F 23 00 2A 2C 32 00 97 9D B3 00 10 00 18 00 00 00 08 00

38 3A 43 38 2A 2C 32 00 B9 BF DA 00 AC B1 CA 00 58 00 50 00 48 00 40 00 39 3B 43 38 1E 1F 23 00

31 33 3A 00 20 21 26 00 58 00 68 00 50 00 60 00 39 3B 43 38 C2 C8 E4 00 1E 1F 23 00 3A 3C 44 00

50 00 60 00 58 00 68 00 1E 1F 23 38 3A 3C 44 00 39 3B 43 00 C2 C8 E4 00 50 00 58 00 40 00 48 00

1E 1F 23 38 39 3B 43 00 20 21 26 00 31 33 3A 00 D8 00 D0 00 C8 00 C0 00 CC D3 F0 38 1E 1F 23 00

36 38 3F 00 BA C1 DC 00 D8 00 E8 00 D0 00 E0 00 CC D3 F0 38 3A 3C 44 00 1E 1F 23 00 3A 3C 44 00

D0 00 E0 00 D8 00 E8 00 1E 1F 23 38 3A 3C 44 00 CC D3 F0 00 3A 3C 44 00 D0 00 D8 00 C0 00 C8 00

1E 1F 23 38 CC D3 F0 00 BA C1 DC 00 36 38 3F 00 98 00 90 00 88 00 80 00 C2 C9 E5 38 1E 1F 23 00

40 43 4C 00 9B A0 B7 00 98 00 A8 00 90 00 A0 00 C2 C9 E5 38 1E 1F 23 00 1E 1F 23 00 C6 CD E9 00

90 00 A0 00 98 00 A8 00 1E 1F 23 38 C6 CD E9 00 C2 C9 E5 00 1E 1F 23 00 90 00 98 00 80 00 88 00

1E 1F 23 38 C2 C9 E5 00 9B A0 B7 00 40 43 4C 00 98 02 78 02 80 02 60 02 3B 2A 1C 38 6E 5F 3C 00

29 16 0E 00 29 16 0E 00 70 02 78 02 90 02 98 02 4E 3F 2C 38 6E 5F 3C 00 33 21 16 00 3B 2A 1C 00

88 02 68 02 90 02 70 02 23 10 09 38 20 0D 07 00 33 21 16 00 4E 3F 2C 00 60 02 68 02 80 02 88 02

29 16 0E 38 20 0D 07 00 29 16 0E 00 23 10 09 00 78 02 58 02 60 02 40 02 6E 5F 3C 38 32 23 0F 00

29 16 0E 00 2A 17 0E 00 50 02 58 02 70 02 78 02 41 32 1E 38 32 23 0F 00 4E 3F 2C 00 6E 5F 3C 00

68 02 48 02 70 02 50 02 20 0D 07 38 20 0D 07 00 4E 3F 2C 00 41 32 1E 00 40 02 48 02 60 02 68 02

2A 17 0E 38 20 0D 07 00 29 16 0E 00 20 0D 07 00 58 02 38 02 40 02 20 02 32 23 0F 38 73 5F 37 00

2A 17 0E 00 29 16 0E 00 30 02 38 02 50 02 58 02 45 35 25 38 73 5F 37 00 41 32 1E 00 32 23 0F 00

48 02 28 02 50 02 30 02 20 0D 07 38 20 0D 07 00 41 32 1E 00 45 35 25 00 20 02 28 02 40 02 48 02

29 16 0E 38 20 0D 07 00 2A 17 0E 00 20 0D 07 00 38 02 A8 01 20 02 B8 01 73 5F 37 38 91 82 55 00

29 16 0E 00 29 16 0E 00 98 01 A8 01 30 02 38 02 44 34 24 38 91 82 55 00 45 35 25 00 73 5F 37 00

28 02 88 01 30 02 98 01 20 0D 07 38 20 0D 07 00 45 35 25 00 44 34 24 00 B8 01 88 01 20 02 28 02

29 16 0E 38 20 0D 07 00 29 16 0E 00 20 0D 07 00 18 02 F8 01 00 02 E0 01 54 45 31 38 6E 5F 3C 00

4B 3C 2A 00 4E 3F 2C 00 F0 01 F8 01 10 02 18 02 29 16 0E 38 6E 5F 3C 00 2F 1D 13 00 54 45 31 00

08 02 E8 01 10 02 F0 01 25 12 0B 38 20 0D 07 00 2F 1D 13 00 29 16 0E 00 E0 01 E8 01 00 02 08 02

4E 3F 2C 38 20 0D 07 00 4B 3C 2A 00 25 12 0B 00 F8 01 D8 01 E0 01 C0 01 6E 5F 3C 38 87 73 3C 00

4E 3F 2C 00 48 39 28 00 D0 01 D8 01 F0 01 F8 01 29 16 0E 38 87 73 3C 00 29 16 0E 00 6E 5F 3C 00

E8 01 C8 01 F0 01 D0 01 20 0D 07 38 20 0D 07 00 29 16 0E 00 29 16 0E 00 C0 01 C8 01 E0 01 E8 01

48 39 28 38 20 0D 07 00 4E 3F 2C 00 20 0D 07 00 B8 01 B0 01 88 01 80 01 29 16 0E 38 29 16 0E 00

20 0D 07 00 20 0D 07 00 A8 01 A0 01 B8 01 B0 01 91 82 55 38 73 5F 37 00 29 16 0E 00 29 16 0E 00

98 01 90 01 A8 01 A0 01 44 34 24 38 45 35 25 00 91 82 55 00 73 5F 37 00 88 01 80 01 98 01 90 01

20 0D 07 38 20 0D 07 00 44 34 24 00 45 35 25 00

  
  
12th Weapon Bone Data \[at offset 0x00014724\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 50 02 00 00 FB FF E0 FF 2A FD 00 00 F3 FF DE FF 4A FD 00 00

F3 FF AA FF CC FC 00 00 02 00 DB FF 4A FD 00 00 FB FF EE FF 8D FF 00 00 F9 FF 01 00 8D FF 00 00

08 00 FF FF 8D FF 00 00 00 00 ED FF 8D FF 00 00 02 00 0E 00 8D FF 00 00 F7 FF F2 FF BB FF 00 00

05 00 EF FF BB FF 00 00 0A 00 0D 00 BB FF 00 00 FC FF 0E 00 BB FF 00 00 FB FF C4 FF 32 FD 00 00

F3 FF C5 FF 32 FD 00 00 09 00 C9 FF A4 FF 00 00 1A 00 2F 00 A4 FF 00 00 F7 FF 35 00 A4 FF 00 00

E6 FF CF FF A4 FF 00 00 1A 00 2F 00 B3 FF 00 00 09 00 C9 FF B3 FF 00 00 E6 FF CF FF B3 FF 00 00

F7 FF 35 00 B3 FF 00 00 05 00 F2 FF 91 00 00 00 09 00 0A 00 91 00 00 00 FB FF 0C 00 91 00 00 00

F7 FF F5 FF 91 00 00 00 F7 FF F2 FF 82 00 00 00 FC FF 0E 00 82 00 00 00 0A 00 0D 00 82 00 00 00

05 00 EF FF 82 00 00 00 08 00 FE FF 9A FE 00 00 02 00 0E 00 93 FE 00 00 F8 FF 00 00 9A FE 00 00

FA FF EE FF A0 FE 00 00 00 00 EC FF A0 FE 00 00 FE FF F0 FF 5C FD 00 00 F8 FF CA FF FA FC 00 00

0A 00 00 00 8D FF 00 00 05 00 E9 FF 8D FF 00 00 F2 FF EC FF 8D FF 00 00 F4 FF 03 00 8D FF 00 00

02 00 11 00 8D FF 00 00 02 00 11 00 A4 FF 00 00 0A 00 00 00 A4 FF 00 00 05 00 E9 FF A4 FF 00 00

F2 FF EC FF A4 FF 00 00 F4 FF 03 00 A4 FF 00 00 08 00 EB FF BB FF 00 00 0E 00 10 00 BB FF 00 00

F9 FF 12 00 BB FF 00 00 F3 FF F0 FF BB FF 00 00 F3 FF F0 FF B3 FF 00 00 08 00 EB FF B3 FF 00 00

0E 00 10 00 B3 FF 00 00 F9 FF 12 00 B3 FF 00 00 FA FF 08 00 86 00 00 00 F8 FF F9 FF 86 00 00 00

06 00 F6 FF 86 00 00 00 08 00 06 00 86 00 00 00 06 00 F6 FF 82 00 00 00 08 00 06 00 82 00 00 00

F8 FF F9 FF 82 00 00 00 FA FF 08 00 82 00 00 00 00 00 E2 FF D6 FD 00 00 F8 FF E3 FF D6 FD 00 00

00 00 03 00 C5 FD 00 00 06 00 F4 FF CF FD 00 00 F7 FF F6 FF CF FD 00 00 05 00 E9 FF A4 FF 00 00

0A 00 00 00 A4 FF 00 00 F4 FF 03 00 A4 FF 00 00 F2 FF EC FF A4 FF 00 00 02 00 11 00 A4 FF 00 00

00 00 20 00 00 00 00 00 12 00 00 00 48 00 F0 01 D8 00 00 00 1D 09 16 30 0D 04 11 00 11 05 12 00

F8 01 60 00 E0 00 00 00 0D 04 11 30 0A 03 10 00 07 02 0F 00 E0 01 50 00 F0 00 00 00 23 0B 18 30

3A 12 1E 00 32 10 1D 00 58 00 E8 01 E8 00 00 00 0F 04 11 30 23 0B 18 00 06 02 0F 00 30 02 48 02

38 02 00 00 31 2E 27 30 31 2E 27 00 31 2E 27 00 80 00 88 00 48 02 00 00 41 46 46 30 28 2D 2D 00

32 2D 28 00 48 02 88 00 38 02 00 00 32 2D 28 30 28 2D 2D 00 32 2D 28 00 80 00 48 02 30 02 00 00

41 46 46 30 32 2D 28 00 32 2D 28 00 48 01 30 01 50 01 00 00 35 29 15 30 78 6E 39 00 23 16 0B 00

28 01 18 00 00 00 00 00 DC D2 CD 30 19 1E 19 00 80 7C 70 00 18 00 28 01 10 00 00 00 19 1E 19 30

DC D2 CD 00 50 5A 55 00 08 00 10 00 28 01 00 00 11 15 11 30 38 3F 3B 00 9A 93 90 00 08 00 28 01

00 00 00 00 11 15 11 30 9A 93 90 00 4E 4A 48 00 20 01 08 00 00 00 00 00 93 8C 89 30 11 15 11 00

93 8C 89 00 18 00 20 01 00 00 00 00 19 1E 19 30 D2 C8 C3 00 D2 C8 C3 00 10 00 70 00 68 00 00 00

2B 2F 2A 30 14 15 13 00 33 38 32 00 10 00 08 00 70 00 00 00 2B 2F 2A 30 0C 0E 0C 00 14 15 13 00

18 00 10 00 68 00 00 00 20 23 1F 30 2B 2F 2A 00 33 38 32 00 32 00 00 00 E0 01 F0 00 D0 01 B8 00

6D 6B 11 38 80 99 13 00 6D 6B 11 00 64 62 10 00 F0 00 D8 00 B8 00 D0 00 80 99 13 38 37 36 0E 00

64 62 10 00 2E 2D 0E 00 D0 00 C8 00 B8 00 C0 00 2E 2D 0E 38 24 23 0E 00 64 62 10 00 1E 1E 0D 00

E0 00 E8 00 C8 00 C0 00 18 18 0D 38 16 16 0D 00 24 23 0E 00 1E 1E 0D 00 C8 00 C0 01 E0 00 F8 01

24 23 0E 38 29 28 0E 00 18 18 0D 00 29 28 0E 00 D8 01 C0 00 E8 01 E8 00 6D 6B 11 38 1E 1E 0D 00

6D 6B 11 00 16 16 0D 00 C0 00 D8 01 B8 00 D0 01 1E 1E 0D 38 6D 6B 11 00 64 62 10 00 6D 6B 11 00

C8 01 D0 00 F0 01 D8 00 29 28 0E 38 2E 2D 0E 00 29 28 0E 00 37 36 0E 00 D0 00 C8 01 C8 00 C0 01

2E 2D 0E 38 29 28 0E 00 24 23 0E 00 29 28 0E 00 D0 01 D8 01 E0 01 E8 01 23 0B 18 38 23 0B 18 00

23 0B 18 00 23 0B 18 00 D8 00 F0 00 48 00 50 00 11 05 12 38 32 10 1D 00 1D 09 16 00 3A 12 1E 00

F8 01 F0 01 60 00 48 00 0D 04 11 38 0D 04 11 00 0A 03 10 00 1D 09 16 00 E8 00 E0 00 58 00 60 00

06 02 0F 38 07 02 0F 00 0F 04 11 00 0A 03 10 00 F0 01 F8 01 C8 01 C0 01 0D 04 11 38 0D 04 11 00

0D 04 11 00 0D 04 11 00 E0 01 E8 01 50 00 58 00 23 0B 18 38 23 0B 18 00 3A 12 1E 00 0F 04 11 00

80 01 88 01 A8 01 B0 01 51 50 67 38 15 15 25 00 83 81 9F 00 23 23 35 00 88 01 90 01 B0 01 B8 01

15 15 25 38 19 19 2A 00 23 23 35 00 19 18 29 00 88 01 80 01 90 01 98 01 15 15 25 38 51 50 67 00

19 19 2A 00 22 21 33 00 98 01 80 01 A0 01 A8 01 22 21 33 38 51 50 67 00 42 41 57 00 83 81 9F 00

90 01 98 01 B8 01 A0 01 19 19 2A 38 22 21 33 00 19 18 29 00 42 41 57 00 80 00 78 00 98 00 A0 00

18 16 13 38 2F 2B 25 00 0E 0D 0B 00 2D 2A 23 00 A0 00 A8 00 98 00 B0 00 1E 19 23 38 16 15 12 00

0E 0D 0B 00 11 0F 0D 00 88 00 80 00 B0 00 98 00 10 0F 0D 38 18 16 13 00 11 0F 0D 00 0E 0D 0B 00

78 00 90 00 A0 00 A8 00 54 4E 43 38 2C 29 23 00 34 30 29 00 16 15 12 00 90 00 88 00 A8 00 B0 00

2C 29 23 38 10 0F 0D 00 16 15 12 00 11 0F 0D 00 78 00 80 00 28 02 30 02 50 55 55 38 41 46 46 00

32 2D 28 00 32 2D 28 00 88 00 90 00 38 02 40 02 28 2D 2D 38 2D 32 32 00 32 2D 28 00 32 2D 28 00

90 00 78 00 40 02 28 02 2D 32 32 38 50 55 55 00 31 2E 27 00 31 2E 27 00 30 02 38 02 28 02 40 02

31 2E 27 38 31 2E 27 00 31 2E 27 00 31 2E 27 00 30 01 38 01 60 01 68 01 78 6E 39 38 BB B3 5D 00

78 78 3C 00 78 6E 39 00 50 01 30 01 58 01 60 01 23 16 0B 38 78 6E 39 00 2A 1D 0F 00 78 78 3C 00

38 01 40 01 68 01 70 01 BB B3 5D 38 6B 60 32 00 78 6E 39 00 3B 2E 18 00 40 01 48 01 70 01 78 01

21 1E 0F 38 35 29 15 00 14 0F 00 00 4B 41 14 00 48 01 50 01 78 01 58 01 35 29 15 38 23 16 0B 00

4B 41 14 00 2A 1D 0F 00 30 01 48 01 38 01 40 01 78 6E 39 38 35 29 15 00 BB B3 5D 00 6B 60 32 00

10 02 20 02 20 01 08 00 9A 93 90 38 11 15 11 00 93 8C 89 00 11 15 11 00 08 01 00 01 28 00 40 00

11 15 11 38 9A 93 90 00 11 15 11 00 9A 93 90 00 40 00 00 01 30 00 F8 00 DC D2 CD 38 DC D2 CD 00

19 1E 19 00 19 1E 19 00 18 02 10 02 18 00 20 01 19 1E 19 38 DC D2 CD 00 19 1E 19 00 D2 C8 C3 00

10 02 18 02 00 01 F8 00 DC D2 CD 38 19 1E 19 00 DC D2 CD 00 19 1E 19 00 20 02 10 02 08 01 00 01

11 15 11 38 9A 93 90 00 11 15 11 00 9A 93 90 00 20 02 08 02 08 00 70 00 0D 0E 0C 38 16 17 15 00

0C 0E 0C 00 14 15 13 00 20 00 10 01 28 00 08 01 0F 10 0F 38 17 19 17 00 0D 0E 0C 00 0D 0E 0C 00

18 01 10 01 38 00 20 00 34 3A 33 38 17 19 17 00 24 27 23 00 0F 10 0F 00 08 02 00 02 70 00 68 00

16 17 15 38 34 38 33 00 14 15 13 00 33 38 32 00 00 02 18 02 68 00 18 00 34 38 33 38 1F 22 1E 00

33 38 32 00 20 23 1F 00 18 01 38 00 F8 00 30 00 34 3A 33 38 24 27 23 00 20 23 1F 00 10 11 0F 00

18 02 00 02 F8 00 18 01 1F 22 1E 38 34 38 33 00 20 23 1F 00 34 3A 33 00 08 02 20 02 10 01 08 01

16 17 15 38 0D 0E 0C 00 17 19 17 00 0D 0E 0C 00 00 02 08 02 18 01 10 01 34 38 33 38 16 17 15 00

34 3A 33 00 17 19 17 00

  
  
13th Weapon Bone Data \[at offset 0x00014FAC\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 A0 02 00 00 F4 FF B5 FF 71 FF 00 00 F2 FF A7 FF 9B FF 00 00

EA FF 77 FF C5 FF 00 00 EC FF 82 FF 9F FF 00 00 EC FF 80 FF 84 FF 00 00 EF FF 94 FF 20 FF 00 00

F3 FF AE FF 11 FF 00 00 F4 FF B7 FF 2F FF 00 00 F9 FF D6 FF FF FE 00 00 F8 FF CC FF D0 FE 00 00

F1 FF A2 FF F8 FE 00 00 F2 FF A7 FF 7B FE 00 00 F5 FF BA FF 18 FE 00 00 F6 FF C0 FF 8A FD 00 00

FA FF D6 FF 1D FD 00 00 FD FF ED FF 5B FD 00 00 FD FF EB FF E7 FD 00 00 00 00 00 00 D1 FD 00 00

F9 FF D1 FF 55 FE 00 00 FE FF F4 FF 3B FE 00 00 EE FF 03 00 76 FE 00 00 00 00 00 00 9F FE 00 00

F8 FF D0 FF 92 FE 00 00 FE FF F0 FF BF FE 00 00 E7 FF 04 00 35 FF 00 00 E7 FF 04 00 35 FF 00 00

02 00 11 00 BF FE 00 00 07 00 31 00 92 FE 00 00 00 00 00 00 9F FE 00 00 EE FF 03 00 76 FE 00 00

02 00 0D 00 3B FE 00 00 07 00 2F 00 55 FE 00 00 F2 FF 02 00 11 FE 00 00 00 00 00 00 D1 FD 00 00

03 00 16 00 E7 FD 00 00 03 00 14 00 5B FD 00 00 06 00 2A 00 1D FD 00 00 0A 00 40 00 8A FD 00 00

0B 00 47 00 18 FE 00 00 0E 00 5A 00 7B FE 00 00 0F 00 5F 00 F8 FE 00 00 08 00 35 00 D0 FE 00 00

06 00 2B 00 FF FE 00 00 0B 00 49 00 2F FF 00 00 0D 00 53 00 11 FF 00 00 11 00 6D 00 20 FF 00 00

14 00 80 00 84 FF 00 00 14 00 7E 00 9F FF 00 00 16 00 8A 00 C5 FF 00 00 0E 00 5A 00 9B FF 00 00

0C 00 4B 00 71 FF 00 00 EF FF 03 00 71 00 00 00 EE FF 03 00 B0 FF 00 00 02 00 0E 00 AD FF 00 00

02 00 0D 00 71 00 00 00 11 00 FE FF 71 00 00 00 12 00 FE FF B0 FF 00 00 FE FF F3 FF AD FF 00 00

FE FF F3 FF 71 00 00 00 00 00 00 00 74 FF 00 00 00 00 00 00 74 FF 00 00 09 00 3E 00 8C FF 00 00

F6 FF C3 FF 8C FF 00 00 EE FF 03 00 B0 FF 00 00 EE FF 03 00 B0 FF 00 00 00 00 00 00 74 FF 00 00

00 00 00 00 74 FF 00 00 08 00 33 00 FD FD 00 00 08 00 32 00 A4 FD 00 00 F8 FF CD FF A4 FD 00 00

F8 FF CB FF FD FD 00 00 F2 FF 02 00 11 FE 00 00 0F 00 FE FF 11 FE 00 00 0F 00 FE FF 11 FE 00 00

18 00 FD FF 35 FF 00 00 18 00 FD FF 35 FF 00 00 12 00 FE FF B0 FF 00 00 12 00 FE FF B0 FF 00 00

13 00 FE FF 76 FE 00 00 13 00 FE FF 76 FE 00 00 F1 FF E1 FF F0 FD 00 00 FC FF 23 00 F0 FD 00 00

04 00 DD FF F0 FD 00 00 0F 00 20 00 F0 FD 00 00 00 00 20 00 00 00 00 00 84 00 00 00 E8 01 F8 01

10 02 00 00 90 84 46 30 21 21 03 00 24 24 06 00 08 00 F0 01 00 02 00 00 24 24 06 30 90 84 46 00

21 21 03 00 08 00 00 00 F0 01 00 00 24 24 06 30 22 22 04 00 90 84 46 00 F8 01 E8 01 88 01 00 00

21 21 03 30 90 84 46 00 21 21 03 00 90 01 88 01 E8 01 00 00 21 21 03 30 21 21 03 00 90 84 46 00

00 02 F0 01 08 02 00 00 21 21 03 30 90 84 46 00 21 21 03 00 88 01 68 02 F8 01 00 00 21 21 03 30

23 23 05 00 21 21 03 00 88 01 90 01 E8 01 00 00 21 21 03 30 21 21 03 00 90 84 46 00 60 02 08 02

F0 01 00 00 21 21 03 30 21 21 03 00 90 84 46 00 10 02 68 02 E8 01 00 00 24 24 06 30 23 23 05 00

90 84 46 00 00 02 60 02 08 00 00 00 21 21 03 30 21 21 03 00 24 24 06 00 08 00 F0 01 00 00 00 00

24 24 06 30 90 84 46 00 22 22 04 00 08 02 60 02 00 02 00 00 21 21 03 30 21 21 03 00 21 21 03 00

08 00 60 02 F0 01 00 00 24 24 06 30 21 21 03 00 90 84 46 00 68 02 10 02 F8 01 00 00 23 23 05 30

24 24 06 00 21 21 03 00 68 02 88 01 E8 01 00 00 23 23 05 30 21 21 03 00 90 84 46 00 68 00 28 02

70 00 00 00 69 78 78 30 1D 22 27 00 1D 22 27 00 60 00 28 02 68 00 00 00 69 78 78 30 1D 22 27 00

69 78 78 00 60 00 30 02 28 02 00 00 69 78 78 30 1D 22 27 00 1D 22 27 00 30 02 60 00 58 00 00 00

1D 22 27 30 69 78 78 00 69 78 78 00 30 02 58 00 50 00 00 00 1D 22 27 30 69 78 78 00 1D 22 27 00

20 02 28 01 20 01 00 00 1D 22 27 30 69 78 78 00 1D 22 27 00 20 02 30 01 28 01 00 00 1D 22 27 30

69 78 78 00 69 78 78 00 30 01 20 02 18 02 00 00 69 78 78 30 1D 22 27 00 1D 22 27 00 30 01 18 02

38 01 00 00 69 78 78 30 1D 22 27 00 69 78 78 00 38 01 18 02 40 01 00 00 69 78 78 30 1D 22 27 00

1D 22 27 00 A0 01 C8 01 C0 01 00 00 10 1E 15 30 3C 4A 4F 00 31 3F 41 00 A0 01 C0 01 A8 01 00 00

10 1E 15 30 31 3F 41 00 09 17 0C 00 50 00 58 00 48 00 00 00 2D 00 0F 30 46 4A 51 00 2D 00 0F 00

70 02 98 00 90 00 00 00 55 00 2D 30 3C 00 19 00 3C 00 19 00 58 02 40 00 38 00 00 00 55 00 2D 30

3C 00 19 00 3C 00 19 00 58 02 48 00 40 00 00 00 55 00 2D 30 3C 00 19 00 3C 00 19 00 B0 00 58 02

B8 00 00 00 3C 00 19 30 55 00 2D 00 3C 00 19 00 28 00 38 00 30 00 00 00 55 00 2D 30 3C 00 19 00

55 00 2D 00 08 00 20 00 18 00 00 00 3C 00 19 30 3C 00 19 00 3C 00 19 00 40 02 90 00 38 02 00 00

2D 00 0F 30 2D 00 0F 00 2D 00 0F 00 40 02 88 00 80 00 00 00 55 00 2D 30 55 00 2D 00 3C 00 19 00

58 02 B0 00 48 00 00 00 55 00 2D 30 3C 00 19 00 3C 00 19 00 C0 00 E0 01 00 00 00 00 55 00 28 30

2D 00 0F 00 2D 00 0F 00 08 00 18 00 10 00 00 00 3C 00 19 30 3C 00 19 00 55 00 2D 00 60 00 90 00

58 00 00 00 46 4A 51 30 2D 00 0F 00 46 4A 51 00 B0 00 C0 00 48 00 00 00 2D 00 0F 30 55 00 28 00

2D 00 0F 00 48 00 C0 00 40 00 00 00 2D 00 0F 30 55 00 28 00 2D 00 0F 00 38 00 28 00 30 00 00 00

2D 00 0F 30 55 00 2D 00 55 00 2D 00 C0 00 38 00 40 00 00 00 55 00 28 30 2D 00 0F 00 2D 00 0F 00

A0 00 B0 00 90 00 00 00 55 00 28 30 2D 00 0F 00 2D 00 0F 00 A0 00 90 00 98 00 00 00 55 00 28 30

2D 00 0F 00 2D 00 0F 00 58 00 90 00 B0 00 00 00 46 4A 51 30 2D 00 0F 00 2D 00 0F 00 B0 00 A0 00

A8 00 00 00 2D 00 0F 30 55 00 28 00 2D 00 0F 00 18 00 08 00 10 00 00 00 2D 00 0F 30 2D 00 0F 00

55 00 2D 00 C0 00 B0 00 B8 00 00 00 55 00 28 30 2D 00 0F 00 2D 00 0F 00 48 01 40 01 D8 00 00 00

41 00 1E 30 23 00 0A 00 23 00 0A 00 10 01 00 01 08 01 00 00 41 00 1E 30 1E 00 0F 00 1E 00 0F 00

D8 00 48 01 C8 00 00 00 1E 00 0F 30 41 00 1E 00 1E 00 0F 00 88 01 78 01 80 01 00 00 1E 00 0F 30

1E 00 0F 00 1E 00 0F 00 D8 01 90 01 50 02 00 00 23 00 0A 30 23 00 0A 00 23 00 0A 00 E8 00 D8 00

E0 00 00 00 1E 00 0F 30 1E 00 0F 00 1E 00 0F 00 38 01 D8 00 F8 00 00 00 46 4A 51 30 1E 00 0F 00

41 00 1E 00 48 01 38 01 40 01 00 00 41 00 1E 30 46 4A 51 00 1E 00 0F 00 F8 00 E8 00 F0 00 00 00

41 00 1E 30 1E 00 0F 00 41 00 1E 00 D8 00 E8 00 F8 00 00 00 1E 00 0F 30 1E 00 0F 00 41 00 1E 00

D8 00 C8 00 D0 00 00 00 1E 00 0F 30 1E 00 0F 00 41 00 1E 00 90 01 D8 01 C8 00 00 00 1E 00 0F 30

1E 00 0F 00 1E 00 0F 00 70 01 78 01 88 01 00 00 41 00 1E 30 1E 00 0F 00 1E 00 0F 00 68 01 58 01

60 01 00 00 41 00 1E 30 41 00 1E 00 41 00 1E 00 C8 00 50 01 58 01 00 00 1E 00 0F 30 41 00 1E 00

41 00 1E 00 C8 00 48 01 50 01 00 00 1E 00 0F 30 41 00 1E 00 41 00 1E 00 F8 00 30 01 38 01 00 00

41 00 1E 30 46 4A 51 00 46 4A 51 00 78 01 88 01 80 01 00 00 23 00 0A 30 23 00 0A 00 23 00 0A 00

78 02 D8 00 F8 00 00 00 23 00 0A 30 23 00 0A 00 41 00 1E 00 50 02 D8 00 D0 00 00 00 23 00 0A 30

23 00 0A 00 41 00 1E 00 48 02 10 01 08 01 00 00 23 00 0A 30 41 00 1E 00 23 00 0A 00 70 01 88 01

78 01 00 00 41 00 1E 30 23 00 0A 00 23 00 0A 00 58 01 68 01 60 01 00 00 41 00 1E 30 41 00 1E 00

41 00 1E 00 D8 00 50 02 48 01 00 00 23 00 0A 30 23 00 0A 00 41 00 1E 00 50 01 50 02 58 01 00 00

41 00 1E 30 23 00 0A 00 41 00 1E 00 F0 00 78 02 F8 00 00 00 41 00 1E 30 23 00 0A 00 41 00 1E 00

20 00 08 00 18 00 00 00 2D 00 0F 30 2D 00 0F 00 2D 00 0F 00 08 00 20 00 00 00 00 00 2D 00 0F 30

2D 00 0F 00 2D 00 0F 00 70 01 88 01 90 01 00 00 41 00 1E 30 1E 00 0F 00 1E 00 0F 00 90 01 88 01

70 01 00 00 23 00 0A 30 23 00 0A 00 41 00 1E 00 08 00 00 00 20 00 00 00 3C 00 19 30 3C 00 19 00

3C 00 19 00 B0 00 50 00 48 00 00 00 3C 00 19 30 3C 00 19 00 3C 00 19 00 F8 00 40 01 18 02 00 00

41 00 1E 30 23 00 0A 00 23 00 0A 00 D8 00 40 01 F8 00 00 00 23 00 0A 30 23 00 0A 00 41 00 1E 00

50 00 90 00 30 02 00 00 3C 00 19 30 3C 00 19 00 3C 00 19 00 50 00 B0 00 90 00 00 00 3C 00 19 30

3C 00 19 00 3C 00 19 00 48 00 58 00 B0 00 00 00 2D 00 0F 30 46 4A 51 00 2D 00 0F 00 38 01 48 01

D8 00 00 00 46 4A 51 30 41 00 1E 00 1E 00 0F 00 48 02 00 01 F8 00 00 00 3B 00 13 30 3B 00 13 00

41 00 1E 00 50 02 50 01 48 01 00 00 23 00 0A 30 41 00 1E 00 41 00 1E 00 B8 00 58 02 C0 00 00 00

3B 00 13 30 3B 00 13 00 3B 00 13 00 58 02 00 00 E0 01 00 00 55 00 2D 30 3C 00 19 00 3C 00 19 00

B0 00 70 02 90 00 00 00 3C 00 19 30 55 00 2D 00 3C 00 19 00 A8 00 70 02 B0 00 00 00 3C 00 19 30

55 00 2D 00 3C 00 19 00 98 00 70 02 A0 00 00 00 2D 00 0F 30 2D 00 0F 00 2D 00 0F 00 78 02 F0 00

E8 00 00 00 3B 00 13 30 41 00 1E 00 3B 00 13 00 78 02 E0 00 D8 00 00 00 23 00 0A 30 23 00 0A 00

23 00 0A 00 80 00 88 00 38 02 00 00 2D 00 0F 30 55 00 2D 00 55 00 28 00 50 02 D0 00 C8 00 00 00

3B 00 13 30 41 00 1E 00 3B 00 13 00 00 00 58 02 38 00 00 00 3C 00 19 30 55 00 2D 00 3C 00 19 00

90 01 C8 00 58 01 00 00 1E 00 0F 30 1E 00 0F 00 41 00 1E 00 50 02 90 01 58 01 00 00 23 00 0A 30

23 00 0A 00 41 00 1E 00 C0 00 00 00 38 00 00 00 55 00 28 30 2D 00 0F 00 2D 00 0F 00 90 00 40 02

90 02 00 00 3C 00 19 30 55 00 2D 00 3C 00 19 00 40 02 80 00 90 02 00 00 55 00 2D 30 3C 00 19 00

3C 00 19 00 30 02 90 00 90 02 00 00 3C 00 19 30 3C 00 19 00 3C 00 19 00 28 02 30 02 90 02 00 00

3C 00 19 30 3C 00 19 00 3C 00 19 00 80 00 78 00 90 02 00 00 3C 00 19 30 55 00 2D 00 3C 00 19 00

78 00 70 00 90 02 00 00 55 00 2D 30 55 00 2D 00 3C 00 19 00 70 00 28 02 90 02 00 00 55 00 2D 30

3C 00 19 00 3C 00 19 00 20 01 18 01 98 02 00 00 41 00 1E 30 41 00 1E 00 23 00 0A 00 20 02 20 01

98 02 00 00 23 00 0A 30 41 00 1E 00 23 00 0A 00 18 02 20 02 98 02 00 00 23 00 0A 30 23 00 0A 00

23 00 0A 00 18 01 10 01 98 02 00 00 41 00 1E 30 41 00 1E 00 23 00 0A 00 10 01 48 02 98 02 00 00

41 00 1E 30 23 00 0A 00 23 00 0A 00 48 02 F8 00 98 02 00 00 23 00 0A 30 41 00 1E 00 23 00 0A 00

F8 00 18 02 98 02 00 00 41 00 1E 30 23 00 0A 00 23 00 0A 00 38 02 90 00 80 02 00 00 55 00 28 30

2D 00 0F 00 2D 00 0F 00 80 00 38 02 80 02 00 00 2D 00 0F 30 55 00 28 00 2D 00 0F 00 90 00 60 00

80 02 00 00 2D 00 0F 30 46 4A 51 00 2D 00 0F 00 60 00 68 00 80 02 00 00 46 4A 51 30 46 4A 51 00

2D 00 0F 00 70 00 78 00 80 02 00 00 55 00 2D 30 55 00 2D 00 2D 00 0F 00 68 00 70 00 80 02 00 00

46 4A 51 30 55 00 2D 00 2D 00 0F 00 78 00 80 00 80 02 00 00 55 00 2D 30 2D 00 0F 00 2D 00 0F 00

20 01 28 01 88 02 00 00 1E 00 0F 30 46 4A 51 00 1E 00 0F 00 10 01 18 01 88 02 00 00 41 00 1E 30

41 00 1E 00 1E 00 0F 00 18 01 20 01 88 02 00 00 41 00 1E 30 41 00 1E 00 1E 00 0F 00 28 01 30 01

88 02 00 00 46 4A 51 30 46 4A 51 00 1E 00 0F 00 30 01 F8 00 88 02 00 00 46 4A 51 30 41 00 1E 00

1E 00 0F 00 F8 00 00 01 88 02 00 00 41 00 1E 30 1E 00 0F 00 1E 00 0F 00 00 01 10 01 88 02 00 00

1E 00 0F 30 41 00 1E 00 1E 00 0F 00 09 00 00 00 B8 01 C0 01 D0 01 C8 01 18 25 20 38 31 3F 41 00

1F 2D 29 00 3C 4A 4F 00 D0 01 C8 01 98 01 A0 01 1F 2D 29 38 3C 4A 4F 00 0F 1D 14 00 10 1E 15 00

B0 01 A8 01 B8 01 C0 01 0B 19 0F 38 09 17 0C 00 18 25 20 00 31 3F 41 00 D0 01 98 01 B8 01 B0 01

1F 2D 29 38 0F 1D 14 00 18 25 20 00 0B 19 0F 00 98 01 A0 01 B0 01 A8 01 0F 1D 14 38 10 1E 15 00

0B 19 0F 00 09 17 0C 00 00 00 38 00 20 00 28 00 3C 00 19 38 3C 00 19 00 3C 00 19 00 55 00 2D 00

38 00 00 00 28 00 20 00 2D 00 0F 38 2D 00 0F 00 55 00 2D 00 2D 00 0F 00 58 01 68 01 90 01 70 01

41 00 1E 38 41 00 1E 00 1E 00 0F 00 41 00 1E 00 70 01 68 01 90 01 58 01 41 00 1E 38 41 00 1E 00

23 00 0A 00 41 00 1E 00

  
  
14th Weapon Bone Data \[at offset 0x00015D94\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 70 02 00 00 FC FF E4 FF B4 FF 00 00 EE FF FD FF B4 FF 00 00

02 00 0F 00 B4 FF 00 00 11 00 F7 FF B4 FF 00 00 09 00 F8 FF D1 FF 00 00 FE FF ED FF D1 FF 00 00

F5 FF FC FF D1 FF 00 00 01 00 06 00 D1 FF 00 00 09 00 F8 FF 83 00 00 00 FE FF ED FF 83 00 00 00

F5 FF FC FF 83 00 00 00 01 00 06 00 83 00 00 00 00 00 FA FF 9A 00 00 00 F0 FF FD FF 3C FD 00 00

00 00 FA FF C0 FC 00 00 05 00 22 00 22 FD 00 00 0F 00 F8 FF 3C FD 00 00 F9 FF D2 FF 22 FD 00 00

0F 00 F8 FF 79 FF 00 00 07 00 2C 00 63 FF 00 00 F0 FF FD FF 79 FF 00 00 F7 FF C8 FF 63 FF 00 00

E6 FF FE FF AC FF 00 00 0C 00 48 00 AC FF 00 00 19 00 F6 FF AC FF 00 00 F3 FF AB FF AC FF 00 00

15 00 F7 FF B4 FF 00 00 F4 FF B5 FF B4 FF 00 00 EA FF FE FF B4 FF 00 00 0A 00 3E 00 B4 FF 00 00

F4 FF B0 FF AC FF 00 00 F4 FF B5 FF AC FF 00 00 F1 FF A0 FF C2 FF 00 00 F1 FF A0 FF BD FF 00 00

EE FF 8F FF AC FF 00 00 ED FF 8A FF AC FF 00 00 F1 FF 9F FF 9C FF 00 00 F1 FF 9F FF 96 FF 00 00

F1 FF 9F FF DC FF 00 00 F1 FF 9F FF E1 FF 00 00 DC FF A3 FF CB FF 00 00 E1 FF A2 FF CB FF 00 00

F1 FF A0 FF BB FF 00 00 F1 FF A0 FF B6 FF 00 00 00 00 9D FF CB FF 00 00 05 00 9C FF CB FF 00 00

F4 FF B0 FF F1 FF 00 00 F5 FF B5 FF F1 FF 00 00 F1 FF A0 FF 05 00 00 00 F1 FF A0 FF 00 00 00 00

EE FF 90 FF F1 FF 00 00 EE FF 8B FF F1 FF 00 00 F1 FF A0 FF E0 FF 00 00 F1 FF A0 FF DB FF 00 00

0B 00 45 00 F1 FF 00 00 0A 00 40 00 F1 FF 00 00 0E 00 55 00 05 00 00 00 0E 00 55 00 00 00 00 00

10 00 65 00 F1 FF 00 00 11 00 6A 00 F1 FF 00 00 0E 00 55 00 E0 FF 00 00 0E 00 55 00 DB FF 00 00

0E 00 55 00 DC FF 00 00 0E 00 55 00 E1 FF 00 00 F9 FF 58 00 CB FF 00 00 FE FF 57 00 CB FF 00 00

0E 00 55 00 BB FF 00 00 0E 00 55 00 B6 FF 00 00 1E 00 52 00 CB FF 00 00 23 00 51 00 CB FF 00 00

10 00 65 00 AC FF 00 00 11 00 6A 00 AC FF 00 00 0E 00 55 00 C2 FF 00 00 0E 00 55 00 BD FF 00 00

0B 00 44 00 AC FF 00 00 0A 00 3F 00 AC FF 00 00 0E 00 54 00 9C FF 00 00 0E 00 54 00 97 FF 00 00

00 00 20 00 00 00 00 00 10 00 00 00 98 00 90 00 C0 00 00 00 BB B7 AF 30 74 72 6D 00 74 72 6D 00

90 00 A8 00 C0 00 00 00 BB B7 AF 30 AC A8 A1 00 BB B7 AF 00 80 00 78 00 70 00 00 00 BB B7 AF 30

BB B7 AF 00 AC A8 A1 00 88 00 80 00 70 00 00 00 B0 AC A4 30 BB B7 AF 00 AC A8 A1 00 70 00 78 00

68 00 00 00 7C 79 77 30 87 84 81 00 58 57 55 00 68 00 88 00 70 00 00 00 58 57 55 30 7C 79 77 00

7C 79 77 00 A8 00 A0 00 B0 00 00 00 67 65 63 30 7C 79 77 00 7C 79 77 00 A0 00 98 00 B0 00 00 00

50 55 55 30 87 84 81 00 50 55 55 00 A8 00 B0 00 C8 00 00 00 67 65 63 30 7C 79 77 00 67 65 63 00

C0 00 A8 00 C8 00 00 00 BB B7 AF 30 AC A8 A1 00 AC A8 A1 00 98 00 C0 00 B8 00 00 00 BB B7 AF 30

74 72 6D 00 BB B7 AF 00 B0 00 98 00 B8 00 00 00 50 55 55 30 87 84 81 00 87 84 81 00 58 00 40 00

60 00 00 00 1C 18 06 30 72 63 19 00 37 2F 0C 00 50 00 58 00 60 00 00 00 34 2D 0B 30 1C 18 06 00

37 2F 0C 00 48 00 50 00 60 00 00 00 97 83 21 30 34 2D 0B 00 37 2F 0C 00 40 00 48 00 60 00 00 00

72 63 19 30 97 83 21 00 37 2F 0C 00 41 00 00 00 A8 01 78 01 A0 01 70 01 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 78 01 A8 01 70 01 A0 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

A8 01 98 01 A0 01 90 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 98 01 A8 01 90 01 A0 01

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 78 01 80 01 70 01 88 01 39 27 01 38 FF FA 06 00

39 27 01 00 39 27 01 00 80 01 78 01 88 01 70 01 FF FA 06 38 39 27 01 00 39 27 01 00 39 27 01 00

98 01 80 01 90 01 88 01 39 27 01 38 FF FA 06 00 39 27 01 00 39 27 01 00 80 01 98 01 88 01 90 01

FF FA 06 38 39 27 01 00 39 27 01 00 39 27 01 00 68 01 38 01 60 01 30 01 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 38 01 68 01 30 01 60 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

68 01 58 01 60 01 50 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 58 01 68 01 50 01 60 01

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 38 01 40 01 30 01 48 01 39 27 01 38 FF FA 06 00

39 27 01 00 39 27 01 00 40 01 38 01 48 01 30 01 FF FA 06 38 39 27 01 00 39 27 01 00 39 27 01 00

58 01 40 01 50 01 48 01 39 27 01 38 FF FA 06 00 39 27 01 00 39 27 01 00 40 01 58 01 48 01 50 01

FF FA 06 38 39 27 01 00 39 27 01 00 39 27 01 00 28 01 F8 00 20 01 F0 00 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 F8 00 28 01 F0 00 20 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

28 01 18 01 20 01 10 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 18 01 28 01 10 01 20 01

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 F8 00 00 01 F0 00 08 01 39 27 01 38 E3 9B 04 00

39 27 01 00 39 27 01 00 00 01 F8 00 08 01 F0 00 E3 9B 04 38 39 27 01 00 39 27 01 00 39 27 01 00

18 01 00 01 10 01 08 01 39 27 01 38 E3 9B 04 00 39 27 01 00 39 27 01 00 00 01 18 01 08 01 10 01

E3 9B 04 38 39 27 01 00 39 27 01 00 39 27 01 00 68 02 38 02 60 02 30 02 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 38 02 68 02 30 02 60 02 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

68 02 58 02 60 02 50 02 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 58 02 68 02 50 02 60 02

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 38 02 40 02 30 02 48 02 39 27 01 38 FF FE 06 00

39 27 01 00 39 27 01 00 40 02 38 02 48 02 30 02 FF FE 06 38 39 27 01 00 39 27 01 00 39 27 01 00

58 02 40 02 50 02 48 02 39 27 01 38 FF FE 06 00 39 27 01 00 39 27 01 00 40 02 58 02 48 02 50 02

FF FE 06 38 39 27 01 00 39 27 01 00 39 27 01 00 28 02 F8 01 20 02 F0 01 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 F8 01 28 02 F0 01 20 02 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

28 02 18 02 20 02 10 02 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 18 02 28 02 10 02 20 02

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 F8 01 00 02 F0 01 08 02 39 27 01 38 FF F3 06 00

39 27 01 00 39 27 01 00 00 02 F8 01 08 02 F0 01 FF F3 06 38 39 27 01 00 39 27 01 00 39 27 01 00

18 02 00 02 10 02 08 02 39 27 01 38 FF F3 06 00 39 27 01 00 39 27 01 00 00 02 18 02 08 02 10 02

FF F3 06 38 39 27 01 00 39 27 01 00 39 27 01 00 E8 01 B8 01 E0 01 B0 01 39 27 01 38 39 27 01 00

39 27 01 00 39 27 01 00 B8 01 E8 01 B0 01 E0 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00

E8 01 D8 01 E0 01 D0 01 39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 D8 01 E8 01 D0 01 E0 01

39 27 01 38 39 27 01 00 39 27 01 00 39 27 01 00 B8 01 C0 01 B0 01 C8 01 39 27 01 38 DF 98 04 00

39 27 01 00 39 27 01 00 C0 01 B8 01 C8 01 B0 01 DF 98 04 38 39 27 01 00 39 27 01 00 39 27 01 00

D8 01 C0 01 D0 01 C8 01 39 27 01 38 DF 98 04 00 39 27 01 00 39 27 01 00 C0 01 D8 01 C8 01 D0 01

DF 98 04 38 39 27 01 00 39 27 01 00 39 27 01 00 90 00 80 00 A8 00 88 00 BB B7 AF 38 AC A8 A1 00

AC A8 A1 00 AC A8 A1 00 98 00 78 00 90 00 80 00 BB B7 AF 38 AC A8 A1 00 74 72 6D 00 74 72 6D 00

A8 00 88 00 A0 00 68 00 67 65 63 38 67 65 63 00 7C 79 77 00 7C 79 77 00 A0 00 68 00 98 00 78 00

50 55 55 38 3C 41 41 00 87 84 81 00 87 84 81 00 D8 00 E0 00 D0 00 E8 00 1C 1C 1C 38 1B 1B 1B 00

18 18 18 00 18 18 18 00 C0 00 C8 00 D0 00 D8 00 3D 3D 3D 38 4E 4E 4E 00 18 18 18 00 1C 1C 1C 00

C8 00 B0 00 D8 00 E0 00 4E 4E 4E 38 1A 1A 1A 00 1C 1C 1C 00 1B 1B 1B 00 B0 00 B8 00 E0 00 E8 00

1A 1A 1A 38 0E 0E 0E 00 1B 1B 1B 00 18 18 18 00 B8 00 C0 00 E8 00 D0 00 0E 0E 0E 38 3D 3D 3D 00

18 18 18 00 18 18 18 00 10 00 18 00 38 00 20 00 11 11 16 38 61 61 7B 00 11 11 16 00 4B 4B 5F 00

18 00 00 00 20 00 28 00 61 61 7B 38 78 78 98 00 4B 4B 5F 00 61 61 7B 00 08 00 10 00 30 00 38 00

20 20 28 38 11 11 16 00 20 20 28 00 11 11 16 00 00 00 08 00 28 00 30 00 78 78 98 38 20 20 28 00

61 61 7B 00 20 20 28 00 38 00 20 00 58 00 40 00 0A 08 00 38 2F 25 00 00 0A 08 00 00 2C 23 00 00

20 00 28 00 40 00 48 00 2F 25 00 38 3D 31 00 00 2C 23 00 00 3A 2E 00 00 30 00 38 00 50 00 58 00

13 0F 00 38 0A 08 00 00 13 0F 00 00 0A 08 00 00 28 00 30 00 48 00 50 00 3D 31 00 38 13 0F 00 00

3A 2E 00 00 13 0F 00 00

  
  
  
  
15th Weapon Bone Data \[at offset 0x0001677C\]:

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 90 02 00 00 0B 00 47 00 20 FF 00 00 07 00 31 00 24 FD 00 00

F8 FF CE FF 24 FD 00 00 F5 FF B8 FF 20 FF 00 00 00 00 00 00 6E FC 00 00 F7 FF C8 FF 5D FF 00 00

08 00 37 00 5D FF 00 00 0F 00 5F 00 79 FF 00 00 11 00 6E 00 C7 FE 00 00 EE FF 92 FF C7 FE 00 00

F0 FF 9E FF 79 FF 00 00 1B 00 37 00 5D FF 00 00 08 00 C3 FF 5D FF 00 00 EA FF 79 FF EE FF 00 00

15 00 87 00 EE FF 00 00 01 00 BC FF 94 FF 00 00 16 00 3D 00 94 FF 00 00 0C 00 E8 FF AB FF 00 00

13 00 12 00 AB FF 00 00 0C 00 50 00 C2 FF 00 00 F3 FF B0 FF C3 FF 00 00 17 00 93 00 2E FF 00 00

1D 00 6B 00 1D FF 00 00 FB FF 91 FF 1D FF 00 00 E8 FF 6D FF 2E FF 00 00 FF FF 41 00 94 FF 00 00

F4 FF 18 00 AB FF 00 00 EC FF ED FF AB FF 00 00 E9 FF C0 FF 94 FF 00 00 E2 FF 95 FF 1D FF 00 00

E4 FF C9 FF 5D FF 00 00 F7 FF 3D 00 5D FF 00 00 05 00 6F 00 1D FF 00 00 F7 FF 12 00 C8 FF 00 00

0E 00 0E 00 C8 FF 00 00 09 00 EE FF C8 FF 00 00 F1 FF F2 FF C8 FF 00 00 09 00 0D 00 92 00 00 00

12 00 11 00 C8 FF 00 00 0B 00 EA FF C8 FF 00 00 04 00 F0 FF 92 00 00 00 F7 FF F2 FF 92 00 00 00

EE FF EE FF C8 FF 00 00 F5 FF 16 00 C8 FF 00 00 FC FF 0F 00 92 00 00 00 07 00 31 00 89 00 00 00

F8 FF CE FF 89 00 00 00 00 00 00 00 8D 00 00 00 04 00 1E 00 A6 00 00 00 03 00 17 00 9B 00 00 00

FD FF E9 FF 9B 00 00 00 FB FF E1 FF A6 00 00 00 16 00 16 00 5D FF 00 00 0E 00 E4 FF 5D FF 00 00

F2 FF 1C 00 5D FF 00 00 EA FF EA FF 5D FF 00 00 F3 FF 01 00 FB FE 00 00 0D 00 FE FF FB FE 00 00

19 00 9B 00 BC FF 00 00 E7 FF 64 FF BC FF 00 00 EB FF 7F FF C3 FF 00 00 14 00 81 00 C3 FF 00 00

08 00 D8 FF 63 FF 00 00 0C 00 FE FF 9A FF 00 00 14 00 23 00 63 FF 00 00 F8 FF 28 00 63 FF 00 00

F4 FF 01 00 9A FF 00 00 EB FF DD FF 63 FF 00 00 09 00 39 00 F6 FC 00 00 F7 FF C7 FF F5 FC 00 00

F7 FF C4 FF 37 FF 00 00 09 00 3B 00 37 FF 00 00 FE FF DB FF 21 FD 00 00 FC FF D5 FF FD FC 00 00

02 00 00 00 95 FC 00 00 09 00 29 00 FD FC 00 00 09 00 23 00 21 FD 00 00 F7 FF DC FF 21 FD 00 00

F6 FF D6 FF FD FC 00 00 03 00 2A 00 FD FC 00 00 02 00 24 00 21 FD 00 00 FE FF 00 00 95 FC 00 00

00 00 20 00 00 00 00 00 4C 00 00 00 98 01 90 01 70 01 00 00 41 39 0E 30 29 24 09 00 A9 92 24 00

90 01 98 01 70 01 00 00 29 24 09 30 41 39 0E 00 A9 92 24 00 78 01 90 01 88 01 00 00 6F 61 18 30

29 24 09 00 60 54 15 00 88 01 80 01 68 01 00 00 60 54 15 30 60 54 15 00 1D 19 06 00 80 01 88 01

68 01 00 00 60 54 15 30 60 54 15 00 1D 19 06 00 88 01 90 01 78 01 00 00 60 54 15 30 29 24 09 00

6F 61 18 00 F8 01 00 02 F0 01 00 00 09 06 15 30 08 06 13 00 07 05 10 00 10 02 18 02 08 02 00 00

03 02 08 30 03 02 08 00 04 02 08 00 D8 01 E0 00 E0 01 00 00 6C 56 20 30 14 10 0C 00 21 1A 09 00

D8 01 E0 01 68 00 00 00 6C 56 20 30 21 1A 09 00 6C 56 20 00 E0 01 D8 01 68 00 00 00 2D 26 11 30

92 7B 38 00 92 7B 38 00 D8 01 E0 01 78 00 00 00 92 7B 38 30 2D 26 11 00 32 28 00 00 E0 01 E0 00

78 00 00 00 1F 19 08 30 45 37 14 00 24 1D 0A 00 78 00 50 00 D8 01 00 00 32 28 00 30 32 28 00 00

92 7B 38 00 D8 01 50 00 E0 00 00 00 6C 56 20 30 14 10 0C 00 14 10 0C 00 C0 00 E8 00 F0 00 00 00

49 3A 16 30 17 12 07 00 14 10 0C 00 50 00 C0 00 F0 00 00 00 14 10 0C 30 49 3A 16 00 14 10 0C 00

50 00 F0 00 E0 00 00 00 6C 56 20 30 19 15 07 00 49 3A 16 00 D8 00 E0 00 F0 00 00 00 1C 17 08 30

49 3A 16 00 19 15 07 00 D8 00 18 02 10 02 00 00 37 2D 00 30 3C 32 0F 00 3C 32 0F 00 48 00 B8 00

E8 00 00 00 66 51 1D 30 88 6C 27 00 15 11 06 00 C0 00 48 00 E8 00 00 00 49 3A 16 30 6C 56 20 00

17 12 07 00 A0 00 78 00 E0 00 00 00 66 51 1D 30 24 1D 0A 00 45 37 14 00 E0 00 D8 00 A0 00 00 00

14 10 0C 30 14 10 0C 00 6C 56 20 00 C0 00 B8 00 48 00 00 00 63 53 26 30 C2 A4 4A 00 92 7B 38 00

C0 00 60 00 B8 00 00 00 63 53 26 30 32 28 00 00 C2 A4 4A 00 60 00 C0 00 50 00 00 00 32 28 00 30

63 53 26 00 32 28 00 00 88 00 78 00 A0 00 00 00 32 28 00 30 32 28 00 00 92 7B 38 00 88 00 A0 00

D8 00 00 00 44 36 13 30 66 51 1D 00 1B 15 07 00 60 00 50 00 78 00 00 00 96 7D 2D 30 92 7B 38 00

34 2C 14 00 60 00 78 00 88 00 00 00 96 7D 2D 30 34 2C 14 00 23 14 00 00 D0 01 80 00 E8 01 00 00

C2 A4 4A 30 32 28 00 00 2D 26 11 00 D0 01 E8 01 70 00 00 00 C2 A4 4A 30 2D 26 11 00 92 7B 38 00

E8 01 D0 01 70 00 00 00 21 1A 09 30 8F 73 2B 00 6C 56 20 00 D0 01 E8 01 C8 00 00 00 8F 73 2B 30

21 1A 09 00 14 10 0C 00 E8 01 80 00 C8 00 00 00 1F 19 08 30 24 1D 0A 00 45 37 14 00 38 00 80 00

D0 01 00 00 32 28 00 30 32 28 00 00 C2 A4 4A 00 D0 01 C8 00 38 00 00 00 8F 73 2B 30 14 10 0C 00

14 10 0C 00 A8 00 F8 00 00 01 00 00 49 3A 16 30 14 10 0C 00 1C 16 08 00 40 00 A8 00 00 01 00 00

6C 56 20 30 49 3A 16 00 1C 16 08 00 B0 00 40 00 00 01 00 00 88 6C 27 30 66 51 1D 00 1A 15 07 00

08 02 D0 00 10 02 00 00 3C 32 0F 30 37 2D 00 00 3C 32 0F 00 F8 00 C8 00 D0 00 00 00 1C 16 08 30

49 3A 16 00 18 13 07 00 F8 00 38 00 C8 00 00 00 1C 16 08 30 49 3A 16 00 49 3A 16 00 A8 00 38 00

F8 00 00 00 49 3A 16 30 14 10 0C 00 14 10 0C 00 D0 00 C8 00 98 00 00 00 14 10 0C 30 14 10 0C 00

6C 56 20 00 80 00 98 00 C8 00 00 00 24 1D 0A 30 66 51 1D 00 45 37 14 00 B0 00 A8 00 40 00 00 00

C2 A4 4A 30 63 53 26 00 92 7B 38 00 A8 00 B0 00 58 00 00 00 63 53 26 30 C2 A4 4A 00 32 28 00 00

A8 00 58 00 38 00 00 00 63 53 26 30 32 28 00 00 32 28 00 00 80 00 90 00 98 00 00 00 32 28 00 30

32 28 00 00 92 7B 38 00 98 00 90 00 D0 00 00 00 66 51 1D 30 44 36 13 00 17 12 06 00 90 00 80 00

58 00 00 00 23 14 00 30 34 2C 14 00 96 7D 2D 00 38 00 58 00 80 00 00 00 63 53 26 30 96 7D 2D 00

34 2C 14 00 88 00 90 00 F8 01 00 00 61 52 25 30 61 52 25 00 C2 A4 4A 00 D0 00 D8 00 10 02 00 00

37 2D 00 30 37 2D 00 00 3C 32 0F 00 C8 01 A8 01 A0 01 00 00 69 50 19 30 96 7D 32 00 96 7D 32 00

B8 01 C0 01 B0 01 00 00 19 15 07 30 48 3C 14 00 19 15 07 00 18 02 D8 00 F0 00 00 00 3C 32 0F 30

37 2D 00 00 3C 32 00 00 D0 00 08 02 F8 00 00 00 37 2D 00 30 3C 32 0F 00 3C 32 00 00 C8 01 60 02

40 02 00 00 37 4C 5D 30 0F 15 1A 00 07 0A 0D 00 38 02 A0 01 30 00 00 00 07 0A 0D 30 1F 2B 35 00

04 05 06 00 28 00 A8 01 30 02 00 00 0B 0F 12 30 1F 2B 35 00 07 0A 0D 00 B0 01 38 02 30 00 00 00

15 1E 25 30 04 07 09 00 02 03 04 00 B8 01 28 00 30 02 00 00 15 1E 25 30 07 0A 0C 00 04 07 09 00

78 02 70 02 88 02 00 00 04 07 09 30 04 07 09 00 04 07 09 00 48 02 58 02 50 02 00 00 07 0A 0D 30

07 0A 0D 00 07 0A 0D 00 80 02 C0 01 68 02 00 00 0A 0E 12 30 26 35 41 00 0A 0E 12 00 30 02 C8 01

40 02 00 00 07 0A 0D 30 37 4C 5D 00 07 0A 0D 00 30 02 A8 01 C8 01 00 00 07 0A 0D 30 1F 2B 35 00

37 4C 5D 00 C8 01 38 02 60 02 00 00 37 4C 5D 30 07 0A 0D 00 0F 15 1A 00 A0 01 38 02 C8 01 00 00

1F 2B 35 30 07 0A 0D 00 37 4C 5D 00 C0 01 30 02 68 02 00 00 26 35 41 30 04 07 09 00 0A 0E 12 00

B8 01 30 02 C0 01 00 00 15 1E 25 30 04 07 09 00 26 35 41 00 38 02 C0 01 80 02 00 00 04 07 09 30

26 35 41 00 0A 0E 12 00 38 02 B0 01 C0 01 00 00 04 07 09 30 15 1E 25 00 26 35 41 00 20 00 00 00

48 01 50 01 60 01 58 01 04 03 09 38 07 05 11 00 03 02 07 00 03 02 06 00 60 01 58 01 28 01 30 01

03 02 07 38 03 02 06 00 02 02 06 00 04 03 09 00 28 01 30 01 40 01 38 01 02 02 06 38 04 03 09 00

46 2D 32 00 46 2D 32 00 40 01 38 01 48 01 50 01 46 2D 32 38 46 2D 32 00 04 03 09 00 07 05 11 00

30 01 58 01 38 01 50 01 04 03 09 38 03 02 06 00 0E 0A 21 00 07 05 11 00 90 01 88 01 98 01 80 01

29 24 09 38 60 54 15 00 41 39 0E 00 60 54 15 00 88 01 90 01 80 01 98 01 60 54 15 38 29 24 09 00

60 54 15 00 41 39 0E 00 B8 00 60 00 E8 00 F0 00 88 6C 27 38 88 6C 27 00 15 11 06 00 18 13 06 00

F0 00 F8 00 18 02 08 02 19 15 07 38 1C 16 08 00 3C 32 0F 00 3C 32 0F 00 60 00 58 00 F0 00 F8 00

88 6C 27 38 88 6C 27 00 18 13 06 00 1A 15 07 00 58 00 60 00 00 02 F0 01 C2 A4 4A 38 C2 A4 4A 00

C2 A4 4A 00 C2 A4 4A 00 60 00 88 00 F0 01 F8 01 C2 A4 4A 38 61 52 25 00 C2 A4 4A 00 C2 A4 4A 00

58 00 B0 00 F8 00 00 01 88 6C 27 38 88 6C 27 00 1A 15 07 00 1A 15 07 00 90 00 58 00 F8 01 00 02

61 52 25 38 C2 A4 4A 00 C2 A4 4A 00 C2 A4 4A 00 90 00 88 00 10 01 18 01 61 52 25 38 61 52 25 00

92 7B 38 00 92 7B 38 00 D8 00 D0 00 20 01 08 01 37 2D 00 38 37 2D 08 00 37 2D 00 00 17 12 07 00

88 00 D8 00 18 01 20 01 44 36 13 38 1B 15 07 00 66 51 1D 00 1B 15 07 00 D0 00 90 00 08 01 10 01

17 12 06 38 44 36 13 00 15 11 06 00 66 51 1D 00 80 02 68 02 78 02 70 02 0A 0E 12 38 0A 0E 12 00

04 07 09 00 04 07 09 00 58 02 48 02 60 02 40 02 07 0A 0D 38 07 0A 0D 00 0F 15 1A 00 07 0A 0D 00

30 02 40 02 18 00 10 00 2D 2D 41 38 2D 2D 41 00 A5 A5 B4 00 A5 A5 B4 00 48 02 28 02 40 02 10 00

2D 2D 41 38 A5 A5 B4 00 2D 2D 41 00 A5 A5 B4 00 28 02 48 02 20 00 50 02 A5 A5 B4 38 2D 2D 41 00

C0 C0 C0 00 2D 2D 41 00 50 02 58 02 20 00 20 02 2D 2D 41 38 2D 2D 41 00 C0 C0 C0 00 A5 A5 B4 00

58 02 60 02 20 02 08 00 2D 2D 41 38 2D 2D 41 00 A5 A5 B4 00 A5 A5 B4 00 68 02 30 02 10 00 18 00

1F 1F 2D 38 1F 1F 2D 00 74 74 7E 00 74 74 7E 00 70 02 68 02 28 02 10 00 1F 1F 2D 38 1F 1F 2D 00

74 74 7E 00 74 74 7E 00 88 02 70 02 20 00 28 02 1F 1F 2D 38 1F 1F 2D 00 87 87 87 00 74 74 7E 00

78 02 88 02 20 02 20 00 1F 1F 2D 38 1F 1F 2D 00 74 74 7E 00 87 87 87 00 80 02 78 02 08 00 20 02

1F 1F 2D 38 1F 1F 2D 00 74 74 7E 00 74 74 7E 00 08 00 00 00 80 02 38 02 74 74 7E 38 74 74 7E 00

1F 1F 2D 00 1F 1F 2D 00 38 02 00 00 60 02 08 00 2D 2D 41 38 A5 A5 B4 00 2D 2D 41 00 A5 A5 B4 00

  
  
16th Weapon Bone Data \[at offset 0x0001731C\]

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 20 03 00 00 08 00 4D 00 35 00 00 00 19 00 49 00 35 00 00 00

29 00 35 00 EE FF 00 00 F3 FF 3F 00 EE FF 00 00 15 00 62 00 3F 00 00 00 30 00 5C 00 EB FF 00 00

FA FF 66 00 EB FF 00 00 19 00 78 00 F5 FF 00 00 FC FF A9 FF 35 00 00 00 EA FF AC FF 35 00 00 00

DB FF C4 FF EE FF 00 00 11 00 B9 FF EE FF 00 00 EE FF 93 FF 3F 00 00 00 D3 FF 9A FF EB FF 00 00

09 00 8F FF EB FF 00 00 EA FF 7D FF F6 FF 00 00 01 00 FB FF BA 00 00 00 04 00 0A 00 90 00 00 00

10 00 F8 FF 90 00 00 00 04 00 06 00 B8 FF 00 00 0D 00 F9 FF B6 FF 00 00 F4 FF FE FF 90 00 00 00

F7 FF FD FF B6 FF 00 00 00 00 EC FF 90 00 00 00 00 00 EF FF B8 FF 00 00 06 00 51 00 C6 FF 00 00

05 00 47 00 B3 FF 00 00 0E 00 86 00 71 FF 00 00 12 00 99 00 86 FF 00 00 1C 00 48 00 BC FF 00 00

2D 00 8A 00 7C FF 00 00 09 00 5D 00 DF FF 00 00 07 00 53 00 CB FF 00 00 15 00 A9 00 9E FF 00 00

17 00 B5 00 B8 FF 00 00 1E 00 54 00 D5 FF 00 00 33 00 AA 00 AB FF 00 00 19 00 3D 00 9B FF 00 00

20 00 1D 00 BD FF 00 00 2B 00 5D 00 EB FF 00 00 04 00 41 00 9B FF 00 00 F2 FF 25 00 BD FF 00 00

24 00 3A 00 EE FF 00 00 FA FF 42 00 EE FF 00 00 00 00 65 00 EB FF 00 00 EB FF B8 FF 9B FF 00 00

E4 FF D9 FF BD FF 00 00 D9 FF 98 FF EB FF 00 00 FF FF B4 FF 9B FF 00 00 11 00 CF FF BD FF 00 00

E0 FF BF FF EE FF 00 00 0B 00 B7 FF EE FF 00 00 04 00 90 FF EB FF 00 00 D2 FF 45 FF B8 FF 00 00

E5 FF 9C FF DF FF 00 00 FC FF 9D FF D5 FF 00 00 F0 FF 46 FF AB FF 00 00 E7 FF A6 FF CB FF 00 00

D5 FF 51 FF 9E FF 00 00 D8 FF 61 FF 86 FF 00 00 E7 FF A9 FF C6 FF 00 00 FF FF A9 FF BC FF 00 00

F6 FF 65 FF 7C FF 00 00 E9 FF B3 FF B3 FF 00 00 DB FF 75 FF 71 FF 00 00 0E 00 3B 00 30 FD 00 00

02 00 FB FF 4A FC 00 00 F6 FF BA FF 30 FD 00 00 F4 FF B0 FF 88 FD 00 00 10 00 45 00 88 FD 00 00

12 00 F8 FF 88 FD 00 00 F0 FF 98 FF 7A FF 00 00 11 00 D7 FF 0C FE 00 00 14 00 5D 00 7A FF 00 00

1D 00 16 00 0C FE 00 00 19 00 F7 FF CD FE 00 00 0F 00 C6 FF 7A FF 00 00 12 00 D4 FF 91 FF 00 00

11 00 D0 FF BD FF 00 00 15 00 E1 FF 7A FF 00 00 20 00 1D 00 BD FF 00 00 1F 00 19 00 91 FF 00 00

22 00 26 00 7A FF 00 00 1D 00 0C 00 7A FF 00 00 19 00 F7 FF 3C FF 00 00 19 00 F7 FF B6 FF 00 00

EC FF FF FF B6 FF 00 00 EC FF FF FF 3C FF 00 00 F0 FF 15 00 7A FF 00 00 F5 FF 2F 00 7A FF 00 00

F2 FF 22 00 91 FF 00 00 F3 FF 25 00 BD FF 00 00 E7 FF E9 FF 7A FF 00 00 E4 FF D8 FF BD FF 00 00

E5 FF DC FF 91 FF 00 00 E2 FF CF FF 7A FF 00 00 EC FF FF FF CD FE 00 00 F3 FF 1E 00 0C FE 00 00

E7 FF DF FF 0C FE 00 00 F2 FF FE FF 88 FD 00 00 00 00 20 00 00 00 00 00 58 00 00 00 38 02 40 02

20 02 00 00 DB E0 FE 32 6F 72 81 00 DB E0 FE 00 60 02 40 02 38 02 00 00 6F 72 81 32 6F 72 81 00

DB E0 FE 00 20 02 40 02 30 02 00 00 DB E0 FE 32 6F 72 81 00 6F 72 81 00 30 02 28 02 08 02 00 00

6F 72 81 32 DB E0 FE 00 DB E0 FE 00 30 02 50 02 28 02 00 00 6F 72 81 32 6F 72 81 00 DB E0 FE 00

50 02 48 02 28 02 00 00 6F 72 81 32 DB E0 FE 00 DB E0 FE 00 48 02 50 02 90 02 00 00 DB E0 FE 32

6F 72 81 00 6F 72 81 00 30 02 18 02 20 02 00 00 6F 72 81 32 DB E0 FE 00 DB E0 FE 00 68 02 38 02

70 02 00 00 6F 72 81 32 DB E0 FE 00 00 00 00 00 38 02 68 02 60 02 00 00 DB E0 FE 32 6F 72 81 00

6F 72 81 00 60 02 68 02 78 02 00 00 6F 72 81 32 6F 72 81 00 6F 72 81 00 98 02 88 02 90 02 00 00

6F 72 81 32 6F 72 81 00 6F 72 81 00 88 02 48 02 90 02 00 00 6F 72 81 32 DB E0 FE 00 6F 72 81 00

48 02 88 02 80 02 00 00 DB E0 FE 32 6F 72 81 00 00 00 00 00 30 02 10 02 18 02 00 00 6F 72 81 32

DB E0 FE 00 DB E0 FE 00 10 02 30 02 08 02 00 00 DB E0 FE 32 6F 72 81 00 DB E0 FE 00 48 02 80 02

D8 02 00 00 DB E0 FE 32 00 00 00 00 00 00 00 00 E8 02 70 02 38 02 00 00 00 00 00 32 00 00 00 00

DB E0 FE 00 10 03 38 02 20 02 00 00 6F 72 81 32 DB E0 FE 00 DB E0 FE 00 10 03 F8 02 38 02 00 00

6F 72 81 32 6F 72 81 00 DB E0 FE 00 10 03 20 02 18 03 00 00 6F 72 81 32 DB E0 FE 00 6F 72 81 00

28 02 18 03 08 02 00 00 DB E0 FE 32 6F 72 81 00 DB E0 FE 00 08 03 18 03 28 02 00 00 6F 72 81 32

6F 72 81 00 DB E0 FE 00 48 02 08 03 28 02 00 00 DB E0 FE 32 6F 72 81 00 DB E0 FE 00 08 03 48 02

C8 02 00 00 6F 72 81 32 DB E0 FE 00 6F 72 81 00 18 02 18 03 20 02 00 00 DB E0 FE 32 6F 72 81 00

DB E0 FE 00 38 02 F0 02 E8 02 00 00 DB E0 FE 32 6F 72 81 00 00 00 00 00 F0 02 38 02 F8 02 00 00

6F 72 81 32 DB E0 FE 00 6F 72 81 00 F0 02 F8 02 E0 02 00 00 6F 72 81 32 6F 72 81 00 6F 72 81 00

D0 02 C0 02 C8 02 00 00 6F 72 81 32 6F 72 81 00 6F 72 81 00 48 02 D0 02 C8 02 00 00 DB E0 FE 32

6F 72 81 00 6F 72 81 00 D0 02 48 02 D8 02 00 00 6F 72 81 32 DB E0 FE 00 00 00 00 00 10 02 18 03

18 02 00 00 DB E0 FE 32 6F 72 81 00 DB E0 FE 00 18 03 10 02 08 02 00 00 6F 72 81 32 DB E0 FE 00

DB E0 FE 00 A0 00 B0 00 C0 00 00 00 02 02 03 30 00 00 00 00 02 03 04 00 A0 00 98 00 B0 00 00 00

02 02 03 30 00 00 00 00 00 00 00 00 88 00 90 00 80 00 00 00 4A 37 08 30 72 63 27 00 90 74 28 00

90 00 B8 00 80 00 00 00 72 63 27 30 80 73 32 00 90 74 28 00 A8 00 88 00 80 00 00 00 54 42 0F 30

4A 37 08 00 90 74 28 00 B8 00 A8 00 80 00 00 00 80 73 32 30 54 42 0F 00 90 74 28 00 F0 01 00 02

D8 01 00 00 3B 10 16 30 0D 03 05 00 5A 19 23 00 C0 01 D0 01 A8 01 00 00 3B 10 16 30 0D 03 05 00

5A 19 23 00 08 01 20 01 10 01 00 00 5A 19 23 30 8B 26 36 00 0D 03 05 00 D8 00 F0 00 E0 00 00 00

5A 19 23 30 8B 26 36 00 0D 03 05 00 78 00 70 00 68 00 00 00 00 00 00 30 00 00 00 00 00 00 00 00

28 00 38 00 30 00 00 00 00 00 00 30 00 00 00 00 00 00 00 00 58 00 70 00 40 00 00 00 0A 0D 08 30

91 8C 73 00 80 7D 4A 00 60 00 70 00 78 00 00 00 3D 3B 22 30 91 8C 73 00 27 25 15 00 40 00 70 00

60 00 00 00 80 7D 4A 30 91 8C 73 00 3D 3B 22 00 60 00 78 00 68 00 00 00 3D 3B 22 30 27 25 15 00

0A 0D 08 00 28 00 10 00 08 00 00 00 91 8C 73 30 09 0B 08 00 80 7D 4A 00 28 00 08 00 20 00 00 00

91 8C 73 30 80 7D 4A 00 3D 3B 22 00 20 00 38 00 28 00 00 00 3D 3B 22 30 3D 3B 22 00 91 8C 73 00

20 00 30 00 38 00 00 00 3D 3B 22 30 0A 0D 08 00 3D 3B 22 00 18 00 30 00 00 00 00 00 91 8C 73 30

0A 0D 08 00 0A 0D 08 00 00 00 30 00 20 00 00 00 0A 0D 08 30 0A 0D 08 00 3D 3B 22 00 20 00 08 00

00 00 00 00 0A 0D 08 30 05 05 04 00 0A 0D 08 00 68 00 48 00 60 00 00 00 0A 0D 08 30 0A 0D 08 00

3D 3B 22 00 68 00 50 00 48 00 00 00 0A 0D 08 30 91 8C 73 00 0A 0D 08 00 60 00 48 00 40 00 00 00

0A 0D 08 30 0A 0D 08 00 00 01 00 00 A0 01 88 01 80 01 00 00 34 34 3B 30 14 08 0A 00 3A 3C 42 00

98 01 88 01 A0 01 00 00 17 0D 0F 30 14 08 0A 00 34 34 3B 00 30 01 38 01 28 01 00 00 3C 41 4B 30

2D 2D 32 00 28 28 2D 00 30 01 50 01 38 01 00 00 3C 41 4B 30 26 20 24 00 2D 2D 32 00 70 01 78 01

68 01 00 00 15 0A 0B 30 1C 12 15 00 25 1F 22 00 78 01 70 01 90 01 00 00 1C 12 15 30 15 0A 0B 00

19 0F 10 00 48 01 60 01 58 01 00 00 22 1D 1F 30 16 0B 0D 00 1B 11 13 00 60 01 48 01 40 01 00 00

16 0B 0D 30 22 1D 1F 00 1A 10 12 00 30 02 58 02 50 02 00 00 03 01 4D 30 56 36 AC 00 1F 13 6D 00

40 02 58 02 30 02 00 00 1F 13 6D 30 56 36 AC 00 03 01 4D 00 00 03 18 03 08 03 00 00 2E 1C 6B 30

02 00 39 00 17 0E 50 00 00 03 10 03 18 03 00 00 2E 1C 6B 30 17 0E 50 00 02 00 39 00 A8 02 98 02

A0 02 00 00 08 00 00 30 72 0E 3A 00 C8 3C 69 00 B0 02 B8 02 C0 02 00 00 00 00 00 30 A0 32 55 00

5C 0A 2E 00 A8 02 A0 02 78 02 00 00 08 00 00 30 C8 3C 69 00 72 0E 3A 00 B8 02 B0 02 E0 02 00 00

A0 32 55 30 00 00 00 00 5C 0A 2E 00 A8 02 68 02 70 02 00 00 63 5B 2E 30 39 2E 17 00 3B 30 18 00

68 02 A8 02 78 02 00 00 39 2E 17 30 63 5B 2E 00 2A 1E 0F 00 A8 02 88 02 98 02 00 00 63 5B 2E 30

39 2E 17 00 2A 1E 0F 00 88 02 A8 02 80 02 00 00 39 2E 17 30 63 5B 2E 00 3B 30 18 00 78 02 A0 02

58 02 00 00 2D 14 41 30 2D 14 41 00 2D 14 41 00 98 02 58 02 A0 02 00 00 2D 14 41 30 2D 14 41 00

2D 14 41 00 F0 02 B0 02 E8 02 00 00 39 2E 17 30 4F 45 23 00 2F 24 12 00 B0 02 F0 02 E0 02 00 00

4F 45 23 30 39 2E 17 00 2A 1E 0F 00 D0 02 B0 02 C0 02 00 00 39 2E 17 30 4F 45 23 00 2A 1E 0F 00

B0 02 D0 02 D8 02 00 00 4F 45 23 30 39 2E 17 00 2F 24 12 00 B8 02 E0 02 00 03 00 00 1E 0F 2D 30

1E 0F 2D 00 1E 0F 2D 00 00 03 C0 02 B8 02 00 00 1E 0F 2D 30 1E 0F 2D 00 1E 0F 2D 00 20 00 00 00

88 00 98 00 90 00 A0 00 00 00 00 38 00 00 00 00 43 43 4A 00 22 22 26 00 90 00 A0 00 B8 00 C0 00

43 43 4A 38 22 22 26 00 02 02 03 00 02 03 04 00 B8 00 C0 00 A8 00 B0 00 02 02 03 38 02 03 04 00

00 00 00 00 00 00 00 00 A8 00 B0 00 88 00 98 00 00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00

F0 01 E8 01 00 02 F8 01 A0 19 37 38 59 18 22 00 0D 03 05 00 0D 03 05 00 E0 01 E8 01 D8 01 F0 01

5A 19 23 38 59 18 22 00 5A 19 23 00 A0 19 37 00 00 02 F8 01 D8 01 E0 01 0D 03 05 38 0D 03 05 00

5A 19 23 00 5A 19 23 00 C0 01 B8 01 D0 01 C8 01 A0 19 37 38 59 18 22 00 0D 03 05 00 0D 03 05 00

B0 01 B8 01 A8 01 C0 01 5A 19 23 38 59 18 22 00 5A 19 23 00 A0 19 37 00 D0 01 C8 01 A8 01 B0 01

0D 03 05 38 0D 03 05 00 5A 19 23 00 5A 19 23 00 18 01 20 01 00 01 08 01 59 18 22 38 A0 19 37 00

5A 19 23 00 5A 19 23 00 00 01 08 01 F8 00 10 01 5A 19 23 38 5A 19 23 00 0D 03 05 00 0D 03 05 00

F8 00 10 01 18 01 20 01 0D 03 05 38 0D 03 05 00 59 18 22 00 A0 19 37 00 E8 00 F0 00 D0 00 D8 00

59 18 22 38 A0 19 37 00 5A 19 23 00 5A 19 23 00 D0 00 D8 00 C8 00 E0 00 5A 19 23 38 5A 19 23 00

0D 03 05 00 0D 03 05 00 C8 00 E0 00 E8 00 F0 00 0D 03 05 38 0D 03 05 00 59 18 22 00 A0 19 37 00

98 01 90 01 88 01 70 01 00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00 30 01 48 01 50 01 58 01

00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00 48 00 50 00 40 00 58 00 00 00 00 38 00 00 00 00

00 00 00 00 00 00 00 00 08 00 10 00 00 00 18 00 00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00

70 00 58 00 68 00 50 00 00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00 30 00 18 00 28 00 10 00

00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00 28 01 38 01 40 01 60 01 28 28 2D 38 2D 2D 32 00

1A 10 12 00 16 0B 0D 00 A0 01 80 01 78 01 68 01 34 34 3B 38 3A 3C 42 00 1C 12 15 00 25 1F 22 00

88 01 70 01 80 01 68 01 14 08 0A 38 15 0A 0B 00 3A 3C 42 00 25 1F 22 00 48 01 30 01 40 01 28 01

22 1D 1F 38 40 44 4B 00 1A 10 12 00 2F 2C 31 00 60 02 78 02 40 02 58 02 82 41 FA 38 82 41 FA 00

1F 13 6D 00 56 36 AC 00 58 02 98 02 50 02 90 02 56 36 AC 38 82 41 FA 00 1F 13 6D 00 82 41 FA 00

E0 02 F8 02 00 03 10 03 5A 32 B9 38 5A 32 B9 00 2E 1C 6B 00 17 0E 50 00 C0 02 00 03 C8 02 08 03

5A 32 B9 38 2E 1C 6B 00 5A 32 B9 00 17 0E 50 00 D8 02 80 02 B0 02 A8 02 07 05 0C 38 06 05 0A 00

07 06 0C 00 0A 08 12 00 B0 02 A8 02 E8 02 70 02 07 06 0C 38 0A 08 12 00 08 06 0D 00 0E 0A 17 00

  
  

- \*\* \*\*\* Weapon Bone Data Section runs until the end of the file\*\*\*

  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Example of LZS enemy battle model file breakdown, using ENEMY016.LZS

\[Lazy Bastard\]: Using data from Akari's Q-Gears utilities source, information from the wiki, and my own intuition, I've mapped out ENEMY016.LZS, the Shinra MP's battle model, in entirety. I've deliberately avoided dissecting animation data and similar data sections, as these are outlined already in the wiki, and would make this breakdown even more verbose than it already is. Anyway, without further ado:

  
  
**Header** \[at offset 0x00000000\]:

  
24 00 00 00 94 00 00 00 9C 67 00 00

  
Breakdown:

24 00 00 00 - Number of sections (0x00000024)

94 00 00 00 - Offset to Bone Description Section (0x00000094)

9C 67 00 00 - Offset to Model Settings (0x0000679C)

  
  
  

- \*\* \*\*\* Header runs until Offsets to Animations, Weapon Bone Data, and Texture\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Offsets to Animations, Weapon Bone Data, and Texture** \[at offset 0x0000000C\]:

  
  
Note: These are four-byte offsets. The last one is the offset to the Texture Data Section; the second to last one is the offset to the Weapon Bone Data Section. All offsets before the second-to-last are Animation Data offsets, starting with the first offset listed, for the first animation data. You'll notice that texture and weapon bones are swapped when you compare this with a playable character battle model...I'm not sure why.

  
44 69 00 00 E4 6C 00 00 10 6F 00 00 A0 71 00 00 18 72 00 00 78 72 00 00 28 76 00 00 6C 78 00 00

88 79 00 00 DC 7B 00 00 78 7C 00 00 7C 7C 00 00 80 7C 00 00 84 7C 00 00 88 7C 00 00 8C 7C 00 00

90 7C 00 00 E8 7C 00 00 2C 7D 00 00 80 7D 00 00 94 7D 00 00 A4 7D 00 00 24 7E 00 00 74 7E 00 00

98 7E 00 00 F8 7E 00 00 10 7F 00 00 14 7F 00 00 18 7F 00 00 1C 7F 00 00 20 7F 00 00 24 7F 00 00

28 7F 00 00 D0 80 00 00

  
  

- \*\* \*\*\* Offsets to Animations, Weapon Bone Data, and Texture runs until Bone Description Section\*\*\*

  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
  
**Bone Description Section** \[at offset 0x00000094\]:

  
Number of Bones \[at offset 0x00000094\]:

1B 00 00 00

  
  
  
***Individual Bone Descriptions*** \[at offset 0x00000098\]:

  
  
Note: According to the wiki, the length of these bones (see below) is signed, not unsigned, and "all FF7 bone lengths are negative".

Note2: If 'Bone offset from Bone Description Section' is 0, bone is actually a joint (and will have no bone data in the next section, incidentally).

  
  
Root Bone Description \[at offset 0x00000098\]:

  
00 00 00 00 00 00 00 00

  
Note: According to the wiki page, this is the 'root bone', which is 'always zeroed'.

  
  
  
1st bone description \[at offset 0x000000A0\]:

00 00 AF FF E4 00 00 00

  
Breakdown:

00 00 - Parent ID

AF FF - Bone length

E4 00 00 00 - Bone offset from Bone Description Section

  
  
  
2nd bone description \[at offset 0x000000A8\]:

01 00 40 FF B8 05 00 00

  
Breakdown:

01 00 - Parent ID

40 FF - Bone Length

B8 05 00 00 - Bone offset from Bone Description Section

  
  
  
3rd bone description \[at offset 0x000000B0\]:

02 00 92 FF 2C 16 00 00

  
Breakdown:

02 00 - Parent ID

92 FF - Bone Length

2C 16 00 00 - Bone offset from Bone Description Section

  
  
4th bone description \[at offset 0x000000B8\]:

01 00 6E FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

6E FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
5th bone description \[at offset 0x000000C0\]:

04 00 BE FF 00 00 00 00

  
Breakdown:

04 00 - Parent ID

BE FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
6th bone description \[at offset 0x000000C8\]:

05 00 75 FF 2C 24 00 00

  
Breakdown:

05 00 - Parent ID

75 FF - Bone Length

2C 24 00 00 - Bone offset from Bone Description Section

  
  
7th bone description \[at offset 0x000000D0\]:

06 00 90 FF 70 29 00 00

  
Breakdown:

06 00 - Parent ID

90 FF - Bone Length

70 29 00 00 - Bone offset from Bone Description Section

  
  
8th bone description \[at offset 0x000000D8\]:

07 00 55 FE 04 2B 00 00

  
Breakdown:

07 00 - Parent ID

55 FE - Bone Length

04 2B 00 00 - Bone offset from Bone Description Section

  
  
9th bone description \[at offset 0x000000E0\]:

01 00 9A FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

9A FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
10th bone description \[at offset 0x000000E8\]:

09 00 43 FF AC 3D 00 00

  
Breakdown:

09 00 - Parent ID

43 FF - Bone Length

AC 3D 00 00 - Bone offset from Bone Description Section

  
  
11th bone description \[at offset 0x000000F0\]:

01 00 A8 FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

A8 FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
12th bone description \[at offset 0x000000F8\]:

0B 00 43 FF EC 3E 00 00

  
Breakdown:

0B 00 - Parent ID

43 FF - Bone Length

EC 3E 00 00 - Bone offset from Bone Description Section

  
  
13th bone description \[at offset 0x00000100\]:

01 00 6E FF 00 00 00 00

  
Breakdown:

01 00 - Parent ID

6E FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
14th bone description \[at offset 0x00000108\]:

0D 00 BE FF 00 00 00 00

  
Breakdown:

0D 00 - Parent ID

BE FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
15th bone description \[at offset 0x00000110\]:

0E 00 75 FF 2C 40 00 00

  
Breakdown:

0E 00 - Parent ID

75 FF - Bone Length

2C 40 00 00 - Bone offset from Bone Description Section

  
  
16th bone description \[at offset 0x00000118\]:

0F 00 90 FF 70 45 00 00

  
Breakdown:

0F 00 - Parent ID

90 FF - Bone Length

70 45 00 00 - Bone offset from Bone Description Section

  
  
17th bone description \[at offset 0x00000120\]:

10 00 BB FF 04 47 00 00

  
Breakdown:

10 00 - Parent ID

BB FF - Bone Length

04 47 00 00 - Bone offset from Bone Description Section

  
  
18th bone description \[at offset 0x00000128\]:

00 00 DA FF 00 00 00 00

  
Breakdown:

00 00 - Parent ID

DA FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
19th bone description \[at offset 0x00000130\]:

12 00 06 FF 08 4C 00 00

  
Breakdown:

12 00 - Parent ID

06 FF - Bone Length

08 4C 00 00 - Bone offset from Bone Description Section

  
  
20th bone description \[at offset 0x00000138\]:

13 00 25 FF 7C 50 00 00

  
Breakdown:

13 00 - Parent ID

25 FF - Bone Length

7C 50 00 00 - Bone offset from Bone Description Section

  
  
21th bone description \[at offset 0x00000140\]:

14 00 A9 FF 10 54 00 00

  
Breakdown:

14 00 - Parent ID

A9 FF - Bone Length

10 54 00 00 - Bone offset from Bone Description Section

  
  
22th bone description \[at offset 0x00000148\]:

15 00 87 FF 04 57 00 00

  
Breakdown:

15 00 - Parent ID

87 FF - Bone Length

04 57 00 00 - Bone offset from Bone Description Section

  
  
23th bone description \[at offset 0x00000150\]:

00 00 DA FF 00 00 00 00

  
Breakdown:

00 00 - Parent ID

DA FF - Bone Length

00 00 00 00 - Bone offset from Bone Description Section

  
  
24th bone description \[at offset 0x00000158\]:

17 00 06 FF 88 59 00 00

  
Breakdown:

17 00 - Parent ID

06 FF - Bone Length

88 59 00 00 - Bone offset from Bone Description Section

  
  
25th bone description \[at offset 0x00000160\]:

18 00 25 FF FC 5D 00 00

  
Breakdown:

18 00 - Parent ID

25 FF - Bone Length

FC 5D 00 00 - Bone offset from Bone Description Section

  
  
26th bone description \[at offset 0x00000168\]:

19 00 A9 FF 90 61 00 00

  
Breakdown:

19 00 - Parent ID

A9 FF - Bone Length

90 61 00 00 - Bone offset from Bone Description Section

  
  
27th bone description \[at offset 0x00000170\]:

1A 00 87 FF 84 64 00 00

  
Breakdown:

1A 00 - Parent ID

87 FF - Bone Length

84 64 00 00 - Bone offset from Bone Description Section

  
  

- \*\* \*\*\* Individual Bone Descriptions runs until Bone Data Section\*\*\*

  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Bone Data Section** \[at offset 0x00000178\]:

  
  
  
Note: These offsets are from the previous section, per bone. If a bone is actually a joint (offset of all zeroes in the previous section), there will be no data for it in this section, and it will be skipped as if it doesn't exist.

  
  
Bone 1 \[at offset 0x00000178\]:

  
E8 00 00 00 00 00 BB FF 15 00 00 00 4F 00 D6 FF 11 00 00 00 00 00 B6 FF D8 FF 00 00 63 00 0B 00

0E 00 00 00 00 00 05 00 01 00 00 00 59 00 0B 00 DC FF 00 00 47 00 41 00 DC FF 00 00 A7 FF 0B 00

DC FF 00 00 B9 FF 41 00 DC FF 00 00 9C FF 0B 00 0E 00 00 00 B1 FF D6 FF 11 00 00 00 46 00 10 00

AC FF 00 00 BA FF 10 00 AC FF 00 00 47 00 D6 FF DC FF 00 00 00 00 D6 FF AF FF 00 00 B9 FF D6 FF

DC FF 00 00 00 00 0B 00 9C FF 00 00 38 00 E7 FF AF FF 00 00 38 00 3A 00 AF FF 00 00 B1 FF 41 00

0E 00 00 00 4F 00 41 00 0E 00 00 00 C8 FF E7 FF AF FF 00 00 C8 FF 3A 00 AF FF 00 00 F9 FF 52 00

D9 FF 00 00 07 00 52 00 D9 FF 00 00 07 00 4A 00 AF FF 00 00 F9 FF 4A 00 AF FF 00 00 F9 FF 52 00

10 00 00 00 07 00 52 00 10 00 00 00 00 00 20 00 00 00 00 00 2A 00 00 00 08 00 10 00 00 00 00 00

14 30 34 30 10 10 14 00 10 14 18 00 08 00 20 00 18 00 00 00 0C 14 18 30 00 0C 18 00 00 0C 18 00

18 00 30 00 28 00 00 00 00 0C 10 30 60 70 78 00 14 30 34 00 40 00 48 00 38 00 00 00 34 54 5C 30

00 14 16 00 14 30 34 00 20 00 50 00 48 00 00 00 00 0C 18 30 10 10 14 00 00 14 16 00 30 00 58 00

28 00 00 00 60 70 78 30 08 22 26 00 14 30 34 00 60 00 40 00 38 00 00 00 10 10 18 30 34 54 5C 00

14 30 34 00 88 00 10 00 68 00 00 00 18 3C 48 30 10 10 14 00 18 3C 48 00 A8 00 10 00 70 00 00 00

10 18 1C 30 10 10 14 00 00 08 18 00 10 00 50 00 00 00 00 00 10 10 14 30 10 10 14 00 10 14 18 00

90 00 80 00 58 00 00 00 30 48 50 30 0C 19 21 00 08 22 26 00 28 00 88 00 68 00 00 00 14 20 2C 30

18 3C 48 00 18 3C 48 00 28 00 08 00 18 00 00 00 14 20 2C 30 14 30 34 00 00 0C 1C 00 98 00 20 00

48 00 00 00 00 0C 1B 30 00 0C 18 00 00 14 16 00 20 00 A0 00 18 00 00 00 00 0C 18 30 10 18 1C 00

00 0C 18 00 48 00 78 00 38 00 00 00 00 14 16 30 18 28 34 00 14 30 34 00 A8 00 38 00 78 00 00 00

10 18 1C 30 14 30 34 00 18 28 34 00 80 00 60 00 A8 00 00 00 0C 19 21 30 10 10 18 00 10 18 1C 00

60 00 38 00 A8 00 00 00 10 10 18 30 14 30 34 00 10 18 1C 00 78 00 48 00 50 00 00 00 18 28 34 30

00 14 16 00 10 10 14 00 A0 00 20 00 E0 00 00 00 10 18 1C 30 00 0C 18 00 10 18 1C 00 20 00 98 00

D8 00 00 00 00 0C 04 30 00 0C 1B 00 10 14 20 00 08 00 28 00 68 00 00 00 14 30 34 30 14 20 2C 00

18 3C 48 00 28 00 58 00 88 00 00 00 14 20 2C 30 08 22 26 00 18 3C 48 00 90 00 C8 00 80 00 00 00

30 48 50 30 4C 5C 6C 00 0C 19 21 00 70 00 88 00 80 00 00 00 00 08 18 30 18 3C 48 00 0C 19 21 00

A8 00 70 00 80 00 00 00 10 18 1C 30 00 08 18 00 0C 19 21 00 B0 00 60 00 80 00 00 00 28 34 3C 30

10 10 18 00 0C 19 21 00 D0 00 B0 00 80 00 00 00 38 44 4C 30 28 34 3C 00 0C 19 21 00 50 00 10 00

78 00 00 00 10 10 14 30 10 10 14 00 18 28 34 00 10 00 A8 00 78 00 00 00 10 10 14 30 10 18 1C 00

18 28 34 00 10 00 88 00 70 00 00 00 10 10 14 30 18 3C 48 00 00 08 18 00 40 00 60 00 B0 00 00 00

34 54 5C 30 10 10 18 00 28 34 3C 00 58 00 30 00 90 00 00 00 08 22 26 30 60 70 78 00 30 48 50 00

50 00 20 00 00 00 00 00 10 10 14 30 00 0C 18 00 10 14 18 00 48 00 40 00 98 00 00 00 00 14 16 30

34 54 5C 00 14 30 34 00 30 00 18 00 A0 00 00 00 60 70 78 30 00 0C 10 00 18 3C 48 00 20 00 08 00

00 00 00 00 00 0C 18 30 0C 14 18 00 10 14 18 00 08 00 68 00 10 00 00 00 14 30 34 30 18 3C 48 00

10 10 14 00 58 00 80 00 88 00 00 00 08 22 26 30 0C 19 21 00 18 3C 48 00 80 00 C8 00 D0 00 00 00

0C 19 21 30 4C 5C 6C 00 38 44 4C 00 20 00 D8 00 E0 00 00 00 00 0C 18 30 10 14 20 00 10 18 1C 00

06 00 00 00 B8 00 C0 00 D8 00 E0 00 14 30 34 38 40 58 54 00 18 3C 48 00 18 3C 48 00 B8 00 D0 00

C0 00 C8 00 14 30 34 38 18 3C 48 00 40 58 54 00 4C 5C 6C 00 30 00 C0 00 90 00 C8 00 60 70 78 38

20 38 40 00 30 48 50 00 4C 5C 6C 00 B8 00 40 00 D0 00 B0 00 1C 24 28 38 34 54 5C 00 38 44 4C 00

28 34 3C 00 C0 00 30 00 E0 00 A0 00 20 38 40 38 60 70 78 00 20 38 40 00 20 38 40 00 B8 00 D8 00

40 00 98 00 1C 24 28 38 3C 48 50 00 34 54 5C 00 14 30 34 00

  
  
  
Bone 2 \[at offset 0x0000064C\]:

  
00 03 00 00 D6 FF DB FF 2E FF 00 00 BF FF FA FF 37 FF 00 00 BC FF DD FF 48 FF 00 00 B9 FF 30 00

65 FF 00 00 CF FF 1B 00 2B FF 00 00 B8 FF 20 00 FD FF 00 00 CD FF 41 00 01 00 00 00 B8 FF F5 FF

F7 FF 00 00 00 00 07 00 17 00 00 00 D5 FF DD FF F3 FF 00 00 F8 FF 4F 00 09 00 00 00 DB FF 4A 00

02 00 00 00 EF FF 51 00 FB FF 00 00 A9 FF BD FF 92 FF 00 00 BF FF D1 FF C1 FF 00 00 C8 FF B7 FF

91 FF 00 00 87 FF D5 FF 9A FF 00 00 96 FF E4 FF 51 FF 00 00 CB FF C4 FF 5E FF 00 00 F9 FF E1 FF

E2 FF 00 00 2B 00 DD FF F3 FF 00 00 07 00 E1 FF E2 FF 00 00 D5 FF E1 FF E2 FF 00 00 F9 FF C4 FF

BC FF 00 00 07 00 C4 FF BC FF 00 00 B8 FF FA FF E5 FF 00 00 AC FF F0 FF D1 FF 00 00 9A FF 39 00

74 FF 00 00 97 FF 14 00 5D FF 00 00 88 FF 0B 00 A2 FF 00 00 AF FF 5E 00 A6 FF 00 00 C2 FF 61 00

A3 FF 00 00 D2 FF 61 00 A0 FF 00 00 D6 FF 41 00 7D FF 00 00 E7 FF 61 00 9D FF 00 00 F8 FF 59 00

88 FF 00 00 00 00 C3 FF 29 FF 00 00 00 00 C1 FF 69 FF 00 00 CE FF 58 00 BD FF 00 00 C0 FF 54 00

BF FF 00 00 BE FF 49 00 DC FF 00 00 CD FF 46 00 F0 FF 00 00 DB FF 4F 00 F1 FF 00 00 DB FF 59 00

BC FF 00 00 D3 FF BA FF 86 FF 00 00 FC FF C1 FF AE FF 00 00 03 00 C1 FF AE FF 00 00 F8 FF 53 00

ED FF 00 00 07 00 53 00 ED FF 00 00 11 00 51 00 FB FF 00 00 07 00 4F 00 09 00 00 00 F8 FF 57 00

DF FF 00 00 07 00 57 00 DF FF 00 00 AC FF 1D 00 DB FF 00 00 00 00 53 00 54 FF 00 00 F8 FF 59 00

B9 FF 00 00 07 00 59 00 B9 FF 00 00 07 00 59 00 88 FF 00 00 B8 FF 24 00 EB FF 00 00 00 00 51 00

75 FF 00 00 2D 00 BA FF 86 FF 00 00 38 00 B7 FF 91 FF 00 00 41 00 D1 FF C1 FF 00 00 35 00 C4 FF

5E FF 00 00 57 00 BD FF 92 FF 00 00 47 00 30 00 65 FF 00 00 2A 00 41 00 7D FF 00 00 66 00 39 00

74 FF 00 00 69 00 14 00 5D FF 00 00 44 00 DD FF 48 FF 00 00 41 00 FA FF 37 FF 00 00 31 00 1B 00

2B FF 00 00 40 00 54 00 BF FF 00 00 51 00 5E 00 A6 FF 00 00 78 00 0B 00 A2 FF 00 00 3E 00 61 00

A3 FF 00 00 32 00 58 00 BD FF 00 00 2E 00 61 00 A0 FF 00 00 24 00 59 00 BC FF 00 00 19 00 61 00

9D FF 00 00 48 00 20 00 FD FF 00 00 33 00 41 00 01 00 00 00 33 00 46 00 F0 FF 00 00 48 00 24 00

EB FF 00 00 25 00 4F 00 F1 FF 00 00 25 00 4A 00 02 00 00 00 42 00 49 00 DC FF 00 00 2B 00 E1 FF

E2 FF 00 00 48 00 F5 FF F7 FF 00 00 48 00 FA FF E5 FF 00 00 54 00 1D 00 DB FF 00 00 79 00 D5 FF

9A FF 00 00 54 00 F0 FF D1 FF 00 00 6A 00 E4 FF 51 FF 00 00 2A 00 DB FF 2E FF 00 00 00 00 00 00

1A FF 00 00 00 00 20 00 00 00 00 00 92 00 00 00 10 02 68 02 78 02 00 00 16 1B 2A 30 1C 30 4C 00

11 16 22 00 10 02 58 02 68 02 00 00 16 1B 2A 30 15 32 4C 00 1C 30 4C 00 58 02 18 02 48 02 00 00

15 32 4C 30 17 28 4C 00 0A 2B 40 00 08 02 18 02 10 02 00 00 18 1E 2F 30 17 28 4C 00 16 1B 2A 00

20 02 28 02 E8 02 00 00 17 28 4C 30 11 15 21 00 18 2C 58 00 08 02 20 02 18 02 00 00 18 1E 2F 30

17 28 4C 00 17 28 4C 00 28 02 20 02 08 02 00 00 11 15 21 30 17 28 4C 00 18 1E 2F 00 E8 02 28 02

F8 01 00 00 18 2C 58 30 11 15 21 00 04 08 12 00 F8 01 00 02 E8 02 00 00 04 08 12 30 07 08 18 00

18 2C 58 00 E0 01 E8 01 F8 01 00 00 09 0B 11 30 0B 18 20 00 04 08 12 00 F8 01 E8 01 00 02 00 00

04 08 12 30 0B 18 20 00 07 14 1C 00 00 01 08 01 10 01 00 00 12 24 45 30 10 28 48 00 12 17 24 00

F8 00 08 01 00 01 00 00 10 24 38 30 10 28 48 00 12 24 45 00 D8 00 F8 00 F0 00 00 00 0C 0F 18 30

10 24 38 00 06 10 1C 00 D8 00 18 00 08 01 00 00 0C 0F 18 30 12 24 45 00 10 28 48 00 10 00 E0 00

88 00 00 00 09 0B 11 30 0D 10 19 00 08 15 1E 00 E0 00 18 00 D8 00 00 00 0D 10 19 30 12 24 45 00

0C 0F 18 00 E0 00 10 00 18 00 00 00 0D 10 19 30 09 0B 11 00 12 24 45 00 10 00 88 00 90 00 00 00

09 0B 11 30 08 15 1E 00 09 0B 11 00 68 00 90 00 88 00 00 00 08 0C 28 30 09 0B 11 00 08 15 1E 00

78 00 60 01 90 00 00 00 08 14 20 30 09 0B 11 00 09 0B 11 00 78 00 90 00 68 00 00 00 08 0C 28 30

09 0B 11 00 08 0C 28 00 58 02 10 02 18 02 00 00 15 32 4C 30 16 1B 2A 00 17 28 4C 00 08 01 F8 00

D8 00 00 00 10 28 48 30 10 24 38 00 0C 0F 18 00 68 02 60 02 70 02 00 00 2C 1C 10 30 0F 0B 0C 00

25 1C 0D 00 60 02 90 02 A0 02 00 00 0F 0B 0C 30 38 28 18 00 24 1D 12 00 E0 01 70 01 E8 01 00 00

18 10 08 30 24 18 0A 00 24 18 0A 00 30 01 00 01 58 01 00 00 0B 09 09 30 5C 44 24 00 0F 0B 0C 00

48 01 30 01 50 01 00 00 20 18 07 30 0B 09 09 00 38 24 24 00 68 01 60 01 78 00 00 00 2A 18 10 30

18 10 08 00 0B 09 09 00 60 02 A0 02 70 02 00 00 0F 0B 0C 30 24 1D 12 00 25 1C 0D 00 60 02 68 02

58 02 00 00 0F 0B 0C 30 2C 1C 10 00 5C 44 24 00 E8 01 70 01 C0 00 00 00 24 18 0A 30 24 18 0A 00

14 0B 08 00 68 01 78 00 B8 00 00 00 2A 18 10 30 0B 09 09 00 14 0B 08 00 00 01 30 01 F8 00 00 00

5C 44 24 30 0B 09 09 00 16 11 12 00 50 01 30 01 58 01 00 00 34 24 10 30 0B 09 09 00 0F 0B 0C 00

A8 02 88 01 A0 02 00 00 24 1C 0C 30 24 18 0D 00 24 18 0D 00 A8 00 A0 00 B8 02 00 00 21 1B 10 30

1E 17 11 00 07 07 07 00 60 00 58 00 50 01 00 00 40 28 1C 30 05 05 05 00 44 2C 10 00 48 00 98 00

B0 00 00 00 07 07 07 30 21 1B 10 00 21 1B 10 00 B0 01 20 00 F8 02 00 00 38 28 05 30 28 1C 05 00

20 18 08 00 B0 01 F8 02 38 02 00 00 38 28 05 30 20 18 08 00 34 24 0E 00 18 00 08 00 20 00 00 00

8C 58 20 30 34 24 0E 00 28 1C 05 00 18 00 10 00 08 00 00 00 8C 58 20 30 24 20 08 00 34 24 0E 00

B0 01 18 00 20 00 00 00 38 28 05 30 8C 58 20 00 28 1C 05 00 18 00 B0 01 D8 01 00 00 8C 58 20 30

38 28 05 00 C8 88 0C 00 18 00 D8 01 18 01 00 00 8C 58 20 30 C8 88 0C 00 2D 23 1E 00 D8 01 C8 01

18 01 00 00 C8 88 0C 30 34 28 18 00 2D 23 1E 00 D8 01 08 02 C8 01 00 00 C8 88 0C 30 94 84 21 00

34 28 18 00 B0 01 08 02 D8 01 00 00 38 28 05 30 A4 88 2C 00 C8 88 0C 00 08 02 B0 01 38 02 00 00

A8 80 2C 30 38 28 05 00 34 24 0E 00 28 02 08 02 30 02 00 00 19 14 14 30 A4 88 2C 00 28 20 18 00

30 02 08 02 38 02 00 00 28 20 18 30 A8 80 2C 00 34 24 0E 00 28 02 30 02 F0 02 00 00 19 14 14 30

28 20 18 00 20 1C 05 00 F0 02 28 01 28 02 00 00 20 1C 05 30 13 15 1A 00 19 14 14 00 28 01 F0 02

20 01 00 00 13 15 1A 30 20 1C 05 00 24 20 08 00 00 00 28 01 20 01 00 00 15 14 0C 30 13 15 1A 00

24 20 08 00 28 01 00 00 10 00 00 00 13 15 1A 30 15 14 0C 00 24 20 08 00 08 00 10 00 00 00 00 00

34 24 0E 30 24 20 08 00 15 14 0C 00 F0 02 30 02 F8 02 00 00 20 1C 05 30 28 20 18 00 20 18 08 00

30 02 38 02 F8 02 00 00 28 20 18 30 34 24 0E 00 20 18 08 00 20 01 F0 02 F8 02 00 00 24 20 08 30

20 1C 05 00 20 18 08 00 00 00 20 01 F8 02 00 00 15 14 0C 30 24 20 08 00 20 18 08 00 08 00 00 00

F8 02 00 00 34 24 0E 30 15 14 0C 00 20 18 08 00 20 00 08 00 F8 02 00 00 28 1C 05 30 34 24 0E 00

20 18 08 00 50 00 90 01 40 00 00 00 00 03 0D 30 00 03 0B 00 00 02 08 00 C0 00 A8 00 B8 02 00 00

0C 18 20 30 10 20 30 00 0C 18 20 00 50 02 18 02 20 02 00 00 14 1A 21 30 44 58 70 00 3C 50 58 00

F0 01 D8 02 00 02 00 00 05 0F 14 30 06 10 18 00 09 14 18 00 E8 02 00 02 D8 02 00 00 10 1C 24 30

09 14 18 00 06 10 18 00 28 02 28 01 F8 01 00 00 10 28 3C 30 14 14 1B 00 1C 28 38 00 70 02 A0 01

C0 01 00 00 0C 18 24 30 0C 18 20 00 0A 20 1C 00 B8 02 E0 02 F0 01 00 00 00 14 14 30 00 04 0F 00

05 0F 14 00 E0 02 B8 02 C8 02 00 00 00 04 0F 30 05 0C 14 00 00 04 11 00 C8 02 D0 02 E0 02 00 00

00 04 11 30 08 0C 14 00 00 04 0F 00 E0 02 D0 02 50 02 00 00 00 04 0F 30 08 0C 14 00 14 1A 21 00

E0 02 50 02 D8 02 00 00 00 04 0F 30 14 1A 21 00 00 08 1D 00 F0 01 E0 02 D8 02 00 00 05 0F 14 30

00 04 0F 00 00 08 1D 00 70 02 A0 02 A0 01 00 00 0C 18 24 30 0A 20 1C 00 0C 18 20 00 A0 02 80 01

A0 01 00 00 0A 20 1C 30 18 30 3C 00 0C 18 20 00 B0 02 60 02 40 02 00 00 10 14 1C 30 10 14 1C 00

05 0C 14 00 B0 02 40 02 50 02 00 00 14 1A 21 30 05 0C 14 00 14 1A 21 00 B0 02 50 02 D0 02 00 00

14 1A 21 30 14 1A 21 00 08 0C 14 00 D0 02 C8 02 98 02 00 00 08 0C 14 30 00 04 11 00 0A 19 1E 00

98 02 B0 02 D0 02 00 00 0A 19 1E 30 14 1A 21 00 10 14 18 00 A0 02 88 01 80 01 00 00 0A 20 1C 30

14 1A 21 00 18 30 3C 00 40 00 80 02 C0 02 00 00 00 04 0F 30 00 07 19 00 00 04 11 00 A0 00 40 00

C0 02 00 00 00 14 14 30 00 04 0F 00 00 04 11 00 60 02 B0 02 90 02 00 00 10 14 1C 30 10 14 1C 00

28 30 38 00 90 02 B0 02 98 02 00 00 28 30 38 30 14 1A 21 00 0A 19 1E 00 90 01 88 02 40 00 00 00

00 05 15 30 00 07 1A 00 00 04 0F 00 78 02 C8 01 10 02 00 00 64 88 94 30 48 6C 78 00 3C 50 58 00

C0 01 C8 01 78 02 00 00 0A 20 1C 30 48 6C 78 00 64 88 94 00 58 02 40 02 60 02 00 00 48 6C 78 30

05 0C 14 00 14 1A 21 00 50 02 48 02 18 02 00 00 14 1A 21 30 5C 70 78 00 44 58 70 00 48 02 50 02

40 02 00 00 5C 70 78 30 14 1A 21 00 05 0C 14 00 C8 01 08 02 10 02 00 00 48 6C 78 30 24 48 58 00

3C 50 58 00 28 01 E0 01 F8 01 00 00 14 14 1B 30 08 19 1F 00 1C 28 38 00 E8 01 F0 01 00 02 00 00

08 19 1F 30 05 0F 14 00 09 14 18 00 E8 01 C0 00 F0 01 00 00 08 19 1F 30 0C 18 20 00 05 0F 14 00

60 01 E0 01 28 01 00 00 06 10 18 30 08 19 1F 00 14 14 1B 00 40 01 48 01 D0 01 00 00 0C 18 20 30

0A 19 20 00 05 0F 14 00 40 01 D0 01 A8 01 00 00 0C 18 20 30 05 0F 14 00 00 07 1A 00 A8 01 C8 00

D0 00 00 00 00 07 1A 30 0A 20 20 00 00 07 1A 00 C8 00 A8 01 D0 01 00 00 0A 20 20 30 00 07 1A 00

05 0F 14 00 18 01 B8 01 10 01 00 00 32 50 5A 30 0A 20 1C 00 64 88 94 00 98 01 58 01 B8 01 00 00

14 28 2C 30 0A 14 1C 00 0A 20 1C 00 50 01 58 01 98 01 00 00 0A 14 1C 30 0A 14 1C 00 14 28 2C 00

E8 00 F0 00 38 01 00 00 05 0F 14 30 24 34 38 00 0C 18 20 00 38 01 40 01 E8 00 00 00 0C 18 20 30

0C 18 20 00 05 0F 14 00 E8 00 40 01 A8 01 00 00 05 0F 14 30 0C 18 20 00 00 07 1A 00 A8 01 D0 00

E8 00 00 00 00 07 1A 30 00 07 1A 00 05 0F 14 00 E8 00 D0 00 80 00 00 00 05 0F 14 30 00 07 1A 00

0C 18 20 00 60 00 50 01 78 01 00 00 1C 34 2C 30 14 1A 21 00 28 30 38 00 78 01 50 01 98 01 00 00

20 2C 34 30 14 1A 21 00 14 28 2C 00 60 01 28 01 90 00 00 00 06 10 18 30 14 14 1B 00 14 14 1B 00

28 01 10 00 90 00 00 00 10 14 1C 30 1C 1C 24 00 10 14 1C 00 40 01 30 01 48 01 00 00 0C 18 20 30

10 10 1C 00 0A 19 20 00 30 01 40 01 38 01 00 00 10 10 1C 30 0C 18 20 00 0C 18 20 00 38 01 F8 00

30 01 00 00 0C 18 20 30 30 40 58 00 1C 1C 24 00 B8 00 78 00 70 00 00 00 0C 18 20 30 0C 18 24 00

00 05 14 00 D0 00 70 00 80 00 00 00 00 07 1A 30 05 0F 14 00 0C 18 20 00 18 00 18 01 08 01 00 00

20 3C 4C 30 30 40 58 00 34 44 5A 00 18 01 10 01 08 01 00 00 32 50 5A 30 64 88 94 00 34 44 5A 00

F0 00 E8 00 D8 00 00 00 24 34 38 30 05 0F 14 00 28 30 38 00 D8 00 E8 00 E0 00 00 00 28 30 38 30

05 0F 14 00 18 30 3C 00 D0 00 B0 00 70 00 00 00 00 07 1A 30 14 1A 21 00 05 0F 14 00 B0 00 D0 00

C8 00 00 00 14 1A 21 30 00 07 1A 00 0A 20 20 00 40 00 A0 00 48 00 00 00 00 04 0F 30 00 14 14 00

00 1C 20 00 98 00 B8 00 B0 00 00 00 0C 20 2D 30 0C 18 20 00 14 1A 21 00 68 00 88 00 80 00 00 00

14 1C 24 30 14 1C 24 00 0C 18 20 00 80 00 70 00 68 00 00 00 0C 18 20 30 00 05 14 00 0C 18 24 00

70 00 78 00 68 00 00 00 00 05 14 30 0C 18 24 00 0C 18 24 00 50 00 40 00 30 00 00 00 00 06 18 30

00 04 0F 00 10 14 18 00 40 00 48 00 38 00 00 00 00 04 0F 30 00 1C 20 00 0C 18 20 00 40 00 38 00

28 00 00 00 00 04 0F 30 0C 18 20 00 00 07 1A 00 40 00 28 00 30 00 00 00 00 04 0F 30 00 07 1A 00

10 14 18 00 40 00 88 02 80 02 00 00 00 04 0F 30 00 07 1A 00 00 07 19 00 A8 02 90 01 88 01 00 00

0B 14 17 30 00 05 15 00 14 1A 21 00 50 00 58 00 60 00 00 00 00 06 18 30 10 14 18 00 1C 34 2C 00

88 02 90 01 A8 02 00 00 00 07 1A 30 00 05 15 00 0B 14 17 00 50 00 30 00 58 00 00 00 00 06 18 30

10 14 18 00 10 14 18 00 C0 00 B8 02 F0 01 00 00 0C 18 20 30 0C 18 20 00 05 0F 14 00 40 02 58 02

48 02 00 00 05 0C 14 30 48 6C 78 00 5C 70 78 00 F8 00 38 01 F0 00 00 00 30 40 58 30 0C 18 20 00

24 34 38 00 B0 00 B8 00 70 00 00 00 14 1A 21 30 0C 18 20 00 05 0F 14 00 15 00 00 00 90 02 88 02

A0 02 A8 02 60 64 8C 38 44 3C 60 00 24 1D 12 00 05 04 04 00 98 00 A8 00 B8 00 C0 00 1F 18 0F 38

1F 18 0F 00 14 0B 08 00 14 0B 08 00 30 00 48 01 58 00 50 01 07 05 05 38 20 18 07 00 44 3C 60 00

64 64 88 00 88 02 90 02 80 02 98 02 24 1C 0C 38 34 20 0C 00 24 1C 0C 00 09 09 09 00 A0 00 C0 02

B8 02 C8 02 1E 17 11 38 03 03 03 00 07 07 07 00 03 03 03 00 C0 02 80 02 C8 02 98 02 03 03 03 38

24 1C 0C 00 03 03 03 00 09 09 09 00 48 00 A0 00 98 00 A8 00 07 07 07 38 1E 17 11 00 21 1B 10 00

21 1B 10 00 B8 00 C0 00 68 01 70 01 38 34 4C 38 38 34 4C 00 20 1C 05 00 20 1C 05 00 48 01 30 00

D0 01 28 00 30 24 18 38 05 05 05 00 05 05 05 00 24 1C 0C 00 38 00 48 00 C8 00 B0 00 1E 17 11 38

07 07 07 00 1E 17 11 00 21 1B 10 00 28 00 38 00 D0 01 C8 00 24 1C 0C 38 30 24 18 00 05 05 05 00

30 24 18 00 60 00 88 01 50 00 90 01 1C 20 20 38 B0 94 94 00 28 28 23 00 1C 20 20 00 88 01 60 00

80 01 78 01 B0 94 94 38 1C 20 20 00 C7 C7 C7 00 3C 54 BC 00 18 01 C8 01 B8 01 C0 01 40 58 64 38

60 78 84 00 05 0F 14 00 0C 18 20 00 B8 01 C0 01 98 01 A0 01 05 0F 14 38 0C 18 20 00 18 24 2C 00

0C 18 20 00 98 01 A0 01 78 01 80 01 18 24 2C 38 0C 18 20 00 10 23 28 00 00 34 27 00 D8 02 50 02

E8 02 20 02 06 10 18 38 14 1A 21 00 10 1C 24 00 3C 50 58 00 78 02 68 02 C0 01 70 02 64 90 94 38

44 6C 70 00 0A 20 1C 00 0C 18 24 00 68 01 70 01 60 01 E0 01 14 1A 21 38 14 1A 21 00 06 10 18 00

08 19 1F 00 00 01 10 01 58 01 B8 01 20 46 54 38 64 88 94 00 14 1A 21 00 0A 20 1C 00 E8 00 80 00

E0 00 88 00 05 0F 14 38 0C 18 20 00 18 30 3C 00 1C 1C 24 00

  
  
  
Bone 3 \[at offset 0x000016C0\]:

  
E8 02 00 00 C5 FF EF FF 8C FF 00 00 C2 FF 13 00 C2 FF 00 00 D6 FF 3B 00 97 FF 00 00 E3 FF 28 00

6D FF 00 00 E8 FF 47 00 7F FF 00 00 E0 FF FE FF 64 FF 00 00 20 00 FE FF 64 FF 00 00 1D 00 28 00

6D FF 00 00 18 00 47 00 7F FF 00 00 B2 FF ED FF C3 FF 00 00 B8 FF EF FF BE FF 00 00 D7 FF BC FF

8F FF 00 00 CF FF B7 FF B9 FF 00 00 C4 FF B0 FF BE FF 00 00 E6 FF CB FF 67 FF 00 00 1A 00 CB FF

67 FF 00 00 00 00 A7 FF BE FF 00 00 00 00 AF FF B9 FF 00 00 00 00 B4 FF 8F FF 00 00 CE FF 11 00

C1 FF 00 00 CC FF 10 00 D8 FF 00 00 D2 FF 32 00 C2 FF 00 00 C2 FF 13 00 EF FF 00 00 B1 FF ED FF

EF FF 00 00 CA FF F1 FF E6 FF 00 00 D3 FF 0E 00 EF FF 00 00 C0 FF B0 FF EF FF 00 00 00 00 BC FF

DD FF 00 00 00 00 A7 FF EF FF 00 00 00 00 50 00 B4 FF 00 00 D6 FF 2C 00 DE FF 00 00 DA FF 2D 00

F5 FF 00 00 FA FF 48 00 E9 FF 00 00 E9 FF 3B 00 DA FF 00 00 00 00 4A 00 FE FF 00 00 00 00 50 00

E4 FF 00 00 00 00 4B 00 D1 FF 00 00 C0 FF F6 FF 01 00 00 00 D7 FF 17 00 16 00 00 00 00 00 C3 FF

11 00 00 00 00 00 47 00 16 00 00 00 33 00 11 00 C1 FF 00 00 34 00 10 00 D8 FF 00 00 2A 00 2C 00

DE FF 00 00 2D 00 0E 00 EF FF 00 00 3E 00 13 00 EF FF 00 00 3E 00 13 00 C2 FF 00 00 3E 00 F8 FF

00 00 00 00 2C 00 17 00 16 00 00 00 26 00 2D 00 F5 FF 00 00 36 00 F1 FF E6 FF 00 00 2A 00 3B 00

97 FF 00 00 2E 00 32 00 C2 FF 00 00 40 00 B0 FF EF FF 00 00 4F 00 ED FF EF FF 00 00 17 00 3B 00

DA FF 00 00 06 00 48 00 E9 FF 00 00 3C 00 B0 FF BE FF 00 00 31 00 B7 FF B9 FF 00 00 4E 00 ED FF

C3 FF 00 00 48 00 EF FF BE FF 00 00 3B 00 EF FF 8C FF 00 00 29 00 BC FF 8F FF 00 00 00 00 FA FF

1A 00 00 00 13 00 76 00 C1 FF 00 00 0F 00 7D 00 C1 FF 00 00 0E 00 79 00 B8 FF 00 00 08 00 76 00

C1 FF 00 00 ED FF 76 00 C1 FF 00 00 F1 FF 7D 00 C1 FF 00 00 F2 FF 79 00 B8 FF 00 00 F8 FF 76 00

C1 FF 00 00 00 00 79 00 BA FF 00 00 00 00 80 00 B8 FF 00 00 FB FF 7C 00 B1 FF 00 00 05 00 7C 00

B1 FF 00 00 2A 00 3B 00 97 FF 00 00 2E 00 32 00 C2 FF 00 00 21 00 59 00 CD FF 00 00 18 00 47 00

7F FF 00 00 E8 FF 47 00 7F FF 00 00 D6 FF 3B 00 97 FF 00 00 DF FF 59 00 CD FF 00 00 D2 FF 32 00

C2 FF 00 00 E9 FF 76 00 C0 FF 00 00 EC FF 71 00 CD FF 00 00 F2 FF 7B 00 B3 FF 00 00 00 00 7E 00

AE FF 00 00 0E 00 7B 00 B3 FF 00 00 17 00 76 00 C0 FF 00 00 14 00 71 00 CD FF 00 00 00 00 74 00

C6 FF 00 00 00 00 50 00 B4 FF 00 00 00 00 20 00 00 00 00 00 7B 00 00 00 08 01 E8 00 20 01 00 00

06 06 06 30 0B 0B 0B 00 0C 0C 0C 00 E8 00 B8 01 20 01 00 00 0B 0B 0B 30 0E 0E 0E 00 0C 0C 0C 00

B8 01 A0 01 58 01 00 00 0E 0E 0E 30 0C 0C 0C 00 0D 0D 0D 00 58 01 A0 01 48 01 00 00 0D 0D 0D 30

0C 0C 0C 00 03 03 03 00 A8 00 F0 00 98 00 00 00 06 06 06 30 06 06 06 00 04 04 04 00 F0 00 A8 00

08 01 00 00 06 06 06 30 06 06 06 00 06 06 06 00 50 01 58 01 48 01 00 00 0E 0E 0E 30 0D 0D 0D 00

03 03 03 00 F0 00 A0 00 98 00 00 00 06 06 06 30 08 08 08 00 04 04 04 00 A0 01 B8 01 E8 00 00 00

0C 0C 0C 30 0E 0E 0E 00 0B 0B 0B 00 08 01 A8 00 E8 00 00 00 06 06 06 30 06 06 06 00 0B 0B 0B 00

00 01 08 01 20 01 00 00 34 24 05 30 34 24 05 00 34 24 0A 00 00 01 F0 00 08 01 00 00 34 24 05 30

44 2C 10 00 34 24 05 00 F8 00 F0 00 00 01 00 00 44 2C 10 30 44 2C 10 00 34 24 05 00 F8 00 C8 00

F0 00 00 00 44 2C 10 30 44 2C 10 00 44 2C 10 00 C8 00 F8 00 28 01 00 00 44 2C 10 30 44 2C 10 00

34 24 05 00 F8 00 30 01 28 01 00 00 44 2C 10 30 34 24 0A 00 34 24 05 00 F8 00 10 01 30 01 00 00

44 2C 10 30 94 68 10 00 34 24 0A 00 10 01 F8 00 00 01 00 00 94 68 10 30 44 2C 10 00 34 24 05 00

00 01 18 01 10 01 00 00 34 24 05 30 28 1B 08 00 94 68 10 00 00 01 20 01 18 01 00 00 34 24 05 30

34 24 0A 00 28 1B 08 00 20 01 C0 01 18 01 00 00 34 24 0A 30 B8 98 20 00 28 1B 08 00 18 01 C0 01

10 01 00 00 28 1B 08 30 B8 98 20 00 94 68 10 00 58 01 88 01 C0 01 00 00 64 48 18 30 64 48 18 00

B8 98 20 00 B8 01 C0 01 20 01 00 00 28 1B 08 30 B8 98 20 00 34 24 0A 00 58 01 C0 01 B8 01 00 00

64 48 18 30 B8 98 20 00 28 1B 08 00 88 01 10 01 C0 01 00 00 64 48 18 30 94 68 10 00 B8 98 20 00

10 01 40 01 30 01 00 00 94 68 10 30 34 24 0A 00 34 24 0A 00 40 01 10 01 80 01 00 00 34 24 0A 30

94 68 10 00 20 18 08 00 60 01 88 01 58 01 00 00 28 1B 08 30 64 48 18 00 64 48 18 00 10 01 88 01

80 01 00 00 94 68 10 30 64 48 18 00 20 18 08 00 80 01 88 01 78 01 00 00 20 18 08 30 64 48 18 00

0E 10 14 00 88 01 60 01 78 01 00 00 64 48 18 30 28 1B 08 00 0E 10 14 00 78 01 60 01 90 01 00 00

0E 10 14 30 28 1B 08 00 06 06 08 00 90 01 38 01 78 01 00 00 06 06 08 30 0E 0F 13 00 0E 10 14 00

38 01 C0 00 28 01 00 00 0E 0F 13 30 34 24 0A 00 34 24 05 00 C8 00 28 01 C0 00 00 00 44 2C 10 30

34 24 05 00 34 24 0A 00 A0 00 F0 00 C8 00 00 00 11 13 17 30 44 2C 10 00 44 2C 10 00 58 01 50 01

60 01 00 00 64 48 18 30 30 22 18 00 28 1B 08 00 38 01 28 01 F8 01 00 00 0E 0F 13 30 34 24 05 00

20 18 08 00 28 01 30 01 F8 01 00 00 34 24 05 30 34 24 0A 00 20 18 08 00 30 01 40 01 F8 01 00 00

34 24 0A 30 34 24 0A 00 20 18 08 00 40 01 80 01 F8 01 00 00 34 24 0A 30 20 18 08 00 20 18 08 00

80 01 78 01 F8 01 00 00 20 18 08 30 0E 10 14 00 20 18 08 00 78 01 38 01 F8 01 00 00 0E 10 14 30

0E 0F 13 00 20 18 08 00 38 01 90 01 D8 00 00 00 0E 0F 13 30 06 06 08 00 20 18 08 00 C0 00 38 01

D8 00 00 00 34 24 0A 30 0E 0F 13 00 20 18 08 00 78 00 90 00 F0 01 00 00 14 28 32 30 14 1E 28 00

0F 1E 28 00 E8 01 78 00 F0 01 00 00 14 28 32 30 14 28 32 00 0F 1E 28 00 78 00 E8 01 30 00 00 00

14 28 32 30 14 28 32 00 5C 80 B4 00 70 01 E8 01 E0 01 00 00 05 1E 23 30 14 28 32 00 5C 80 B4 00

E0 00 D8 00 A8 01 00 00 00 03 0D 30 0A 1E 28 00 0A 0F 14 00 70 01 E0 01 D8 01 00 00 05 1E 23 30

5C 80 B4 00 40 5C 68 00 D8 01 A8 01 B0 01 00 00 40 5C 68 30 0A 0F 14 00 19 1E 23 00 E0 01 D0 01

D8 01 00 00 5C 80 B4 30 14 28 32 00 40 5C 68 00 A0 01 70 01 48 01 00 00 19 23 28 30 05 1E 23 00

0A 1E 28 00 90 01 60 01 68 01 00 00 0A 1E 28 30 05 1E 23 00 0A 1E 28 00 90 01 68 01 B0 01 00 00

0A 1E 28 30 0A 1E 28 00 0A 1E 28 00 A8 01 90 01 B0 01 00 00 0A 0F 14 30 0A 1E 28 00 0A 1E 28 00

D8 00 90 01 A8 01 00 00 0A 1E 28 30 0A 1E 28 00 0A 0F 14 00 98 01 70 01 A0 01 00 00 1E 32 37 30

05 1E 23 00 19 23 28 00 98 01 40 00 38 00 00 00 1E 32 37 30 5C 80 B4 00 5C 80 B4 00 70 01 98 01

E8 01 00 00 05 1E 23 30 1E 32 37 00 14 28 32 00 70 01 50 01 48 01 00 00 28 3C 46 30 28 3C 46 00

0A 1E 28 00 68 01 50 01 70 01 00 00 0A 1E 28 30 28 3C 46 00 28 3C 46 00 68 01 60 01 50 01 00 00

0A 1E 28 30 28 3C 46 00 28 3C 46 00 D0 00 48 00 B8 00 00 00 0A 14 19 30 19 2D 37 00 0A 0F 14 00

C0 00 D0 00 B8 00 00 00 00 03 0C 30 0A 14 19 00 0A 0F 14 00 C0 00 D8 00 D0 00 00 00 00 03 0C 30

0A 1E 28 00 0A 14 19 00 D8 00 E0 00 D0 00 00 00 0A 1E 28 30 00 03 0D 00 0A 14 19 00 C8 00 B0 00

A0 00 00 00 0A 14 19 30 0F 14 14 00 0A 0F 14 00 C8 00 C0 00 B0 00 00 00 0A 14 19 30 00 03 0C 00

0F 14 14 00 B0 00 C0 00 B8 00 00 00 0F 14 14 30 00 03 0C 00 0A 0F 14 00 A0 00 B0 00 08 00 00 00

0A 0F 14 30 0F 14 14 00 0A 1E 28 00 08 00 10 00 A8 00 00 00 0A 1E 28 30 14 1E 28 00 0A 14 19 00

08 00 A8 00 98 00 00 00 0A 1E 28 30 0A 14 19 00 0F 14 14 00 A0 00 08 00 98 00 00 00 0A 0F 14 30

0A 1E 28 00 0F 14 14 00 90 00 78 00 70 00 00 00 14 1E 28 30 14 28 32 00 0F 1E 28 00 90 00 70 00

58 00 00 00 14 1E 28 30 0F 1E 28 00 14 19 1E 00 70 00 00 00 58 00 00 00 0F 1E 28 30 0A 1E 28 00

14 19 1E 00 00 00 70 00 28 00 00 00 0A 1E 28 30 0F 1E 28 00 23 50 60 00 60 00 50 00 48 00 00 00

0C 14 1C 30 0A 0F 14 00 19 2D 37 00 00 00 08 00 50 00 00 00 0A 1E 28 30 0A 1E 28 00 0A 0F 14 00

50 00 08 00 48 00 00 00 0A 0F 14 30 0A 1E 28 00 19 2D 37 00 20 00 10 00 18 00 00 00 48 58 6C 30

14 1E 28 00 28 4B 50 00 08 00 00 00 10 00 00 00 0A 1E 28 30 0A 1E 28 00 14 1E 28 00 98 01 38 00

E8 01 00 00 1E 32 37 30 5C 80 B4 00 14 28 32 00 E8 01 38 00 30 00 00 00 14 28 32 30 5C 80 B4 00

5C 80 B4 00 18 00 00 00 28 00 00 00 28 4B 50 30 0A 1E 28 00 23 50 60 00 18 00 10 00 00 00 00 00

28 4B 50 30 14 1E 28 00 14 1E 28 00 A8 01 D8 01 C8 01 00 00 0A 0F 14 30 40 5C 68 00 48 58 6C 00

D8 01 D0 01 C8 01 00 00 40 5C 68 30 14 28 32 00 48 58 6C 00 48 00 D0 00 68 00 00 00 19 2D 37 30

0A 14 19 00 19 2D 37 00 60 00 48 00 68 00 00 00 0C 14 1C 30 19 2D 37 00 19 2D 37 00 20 02 30 02

28 02 00 00 84 00 00 30 FF 4B 23 00 5A 00 00 00 20 02 28 02 38 02 00 00 84 00 00 30 5A 00 00 00

5B 00 00 00 28 02 30 02 38 02 00 00 5A 00 00 30 FF 4B 23 00 5B 00 00 00 40 02 50 02 48 02 00 00

6E 00 00 30 97 00 00 00 52 00 00 00 40 02 48 02 58 02 00 00 6E 00 00 30 52 00 00 00 FF 4B 23 00

48 02 50 02 58 02 00 00 52 00 00 30 97 00 00 00 FF 4B 23 00 10 02 08 02 18 02 00 00 FF 4B 23 30

64 00 00 00 86 00 00 00 08 02 00 02 18 02 00 00 64 00 00 30 4C 00 00 00 86 00 00 00 10 02 00 02

08 02 00 00 FF 4B 23 30 4C 00 00 00 64 00 00 00 78 02 B8 02 80 02 00 00 5C 80 B4 30 5C 80 B4 00

48 58 6C 00 78 02 C0 02 B8 02 00 00 5C 80 B4 30 8C AC C8 00 5C 80 B4 00 B8 02 D8 02 B0 02 00 00

1E 32 37 30 0F 1E 28 00 00 09 21 00 D8 02 B8 02 C0 02 00 00 0F 1E 28 30 1E 32 37 00 28 4B 50 00

80 02 B8 02 B0 02 00 00 48 58 6C 30 5C 80 B4 00 28 38 4C 00 D8 02 C0 02 C8 02 00 00 0F 1E 28 30

28 4B 50 00 00 14 28 00 68 02 C8 02 60 02 00 00 10 20 27 30 23 50 60 00 1E 32 37 00 D8 02 C8 02

D0 02 00 00 0F 1E 28 30 00 14 28 00 0A 28 2D 00 C8 02 70 02 D0 02 00 00 23 50 60 30 0A 1E 28 00

0A 1E 28 00 70 02 C8 02 68 02 00 00 0A 1E 28 30 23 50 60 00 10 20 27 00 70 02 68 02 E0 02 00 00

0A 1E 28 30 10 20 27 00 0A 14 19 00 E0 02 D0 02 70 02 00 00 0A 14 19 30 0A 1E 28 00 0A 1E 28 00

D0 02 E0 02 D8 02 00 00 0A 1E 28 30 0A 14 19 00 00 03 0D 00 E0 02 A8 02 D8 02 00 00 0A 14 19 30

0A 1E 28 00 00 03 0D 00 A8 02 E0 02 90 02 00 00 0A 1E 28 30 0A 14 19 00 00 1C 1C 00 98 02 90 02

E0 02 00 00 0A 14 19 30 00 1C 1C 00 0A 14 19 00 A0 02 98 02 88 02 00 00 28 38 4C 30 0A 14 19 00

14 1E 28 00 98 02 A0 02 90 02 00 00 0A 14 19 30 28 38 4C 00 00 1C 1C 00 D8 02 A0 02 B0 02 00 00

0F 1E 28 30 0A 1E 28 00 00 09 21 00 A0 02 D8 02 A8 02 00 00 0A 1E 28 30 0F 1E 28 00 10 20 27 00

90 02 A0 02 A8 02 00 00 00 1C 1C 30 1C 34 38 00 1C 34 38 00 0F 00 00 00 90 00 88 00 F0 01 D0 01

14 1E 28 38 0C 14 1C 00 0F 1E 28 00 14 28 32 00 E0 01 E8 01 D0 01 F0 01 5C 80 B4 38 14 28 32 00

14 28 32 00 0F 1E 28 00 D8 01 B0 01 70 01 68 01 40 5C 68 38 19 1E 23 00 28 3C 46 00 19 1E 23 00

88 00 80 00 D0 01 C8 01 0C 14 1C 38 14 1E 28 00 14 28 32 00 48 58 6C 00 80 00 E0 00 C8 01 A8 01

14 1E 28 38 00 03 0D 00 48 58 6C 00 0A 0F 14 00 E0 00 80 00 D0 00 68 00 00 03 0D 38 14 1E 28 00

0A 14 19 00 19 2D 37 00 B8 00 48 00 B0 00 08 00 0A 0F 14 38 19 2D 37 00 0F 14 14 00 0A 1E 28 00

88 00 90 00 60 00 58 00 0C 14 1C 38 14 1E 28 00 0C 14 1C 00 14 19 1E 00 80 00 88 00 68 00 60 00

14 1E 28 38 0C 14 1C 00 19 2D 37 00 0C 14 1C 00 70 00 78 00 28 00 30 00 0F 1E 28 38 14 28 32 00

23 50 60 00 5C 80 B4 00 00 00 50 00 58 00 60 00 0A 1E 28 38 0A 0F 14 00 14 19 1E 00 0C 14 1C 00

18 00 38 00 20 00 40 00 28 4B 50 38 5C 80 B4 00 48 58 6C 00 5C 80 B4 00 28 00 30 00 18 00 38 00

23 50 60 38 5C 80 B4 00 28 4B 50 00 5C 80 B4 00 C0 02 78 02 C8 02 60 02 8C AC C8 38 5C 80 B4 00

23 50 60 00 1E 32 37 00 A0 02 88 02 B0 02 80 02 28 38 4C 38 14 1E 28 00 28 38 4C 00 48 58 6C 00

  
  
  
Bone 6 \[at offset 0x000024C0\]:

  
F0 00 00 00 1B 00 00 00 9B FF 00 00 1A 00 00 00 78 FF 00 00 00 00 E8 FF 91 FF 00 00 E8 FF 00 00

3F 00 00 00 C3 FF 00 00 00 00 00 00 E0 FF C1 FF EA FF 00 00 DC FF C9 FF 2D 00 00 00 1E 00 C5 FF

EA FF 00 00 0E 00 D2 FF 2E 00 00 00 D5 FF 00 00 DB FF 00 00 01 00 D2 FF EA FF 00 00 23 00 00 00

34 00 00 00 2E 00 00 00 EB FF 00 00 01 00 00 00 63 FF 00 00 00 00 EA FF 78 FF 00 00 EB FF 00 00

78 FF 00 00 E9 FF 00 00 9B FF 00 00 56 00 E2 FF EF FF 00 00 56 00 1E 00 EF FF 00 00 00 00 16 00

78 FF 00 00 01 00 2E 00 EA FF 00 00 0E 00 2E 00 2E 00 00 00 1E 00 3B 00 EA FF 00 00 DC FF 37 00

2D 00 00 00 E0 FF 3F 00 EA FF 00 00 00 00 18 00 91 FF 00 00 2E 00 00 00 C3 FF 00 00 00 00 D5 FF

BD FF 00 00 00 00 2B 00 BD FF 00 00 DD FF 00 00 AE FF 00 00 00 00 20 00 00 00 00 00 34 00 00 00

20 00 30 00 28 00 00 00 27 24 28 30 68 60 70 00 74 68 4C 00 28 00 40 00 38 00 00 00 74 68 4C 30

FC E8 DC 00 98 80 58 00 40 00 18 00 58 00 00 00 FC E8 DC 30 48 44 38 00 41 3C 4E 00 50 00 38 00

60 00 00 00 03 03 05 30 08 14 32 00 03 03 05 00 60 00 38 00 88 00 00 00 03 03 05 30 08 14 32 00

98 80 58 00 18 00 40 00 30 00 00 00 48 44 38 30 FC E8 DC 00 68 60 70 00 40 00 88 00 38 00 00 00

FC E8 DC 30 20 20 40 00 98 80 58 00 40 00 28 00 30 00 00 00 FC E8 DC 30 74 68 4C 00 68 60 70 00

28 00 38 00 50 00 00 00 74 68 4C 30 08 14 32 00 03 03 05 00 18 00 30 00 20 00 00 00 48 44 38 30

68 60 70 00 27 24 28 00 50 00 20 00 28 00 00 00 03 03 05 30 04 10 1C 00 74 68 4C 00 58 00 88 00

40 00 00 00 41 3C 4E 30 20 20 40 00 FC E8 DC 00 88 00 58 00 90 00 00 00 20 20 40 30 41 3C 4E 00

0D 06 05 00 60 00 88 00 90 00 00 00 03 03 05 30 98 80 58 00 0D 06 05 00 B8 00 20 00 C0 00 00 00

08 0A 11 30 27 24 28 00 27 24 28 00 A8 00 C0 00 B0 00 00 00 15 10 20 30 27 24 28 00 27 24 28 00

18 00 A8 00 58 00 00 00 48 44 38 30 15 10 20 00 41 3C 4E 00 B0 00 A0 00 60 00 00 00 08 10 1C 30

04 05 07 00 03 03 05 00 B0 00 60 00 90 00 00 00 08 10 1C 30 03 03 05 00 0D 06 05 00 A8 00 18 00

B8 00 00 00 15 10 20 30 48 44 38 00 08 0A 11 00 90 00 A8 00 B0 00 00 00 0D 06 05 30 15 10 20 00

27 24 28 00 C0 00 A8 00 B8 00 00 00 27 24 28 30 15 10 20 00 08 0A 11 00 B0 00 C0 00 A0 00 00 00

14 14 0C 30 14 14 0C 00 04 05 07 00 B8 00 18 00 20 00 00 00 08 0A 11 30 48 44 38 00 27 24 28 00

20 00 A0 00 C0 00 00 00 14 14 18 30 04 05 07 00 14 14 18 00 90 00 58 00 A8 00 00 00 0D 06 05 30

41 3C 4E 00 15 10 20 00 78 00 70 00 68 00 00 00 48 34 20 30 5F 40 34 00 3C 30 20 00 98 00 78 00

68 00 00 00 38 20 1C 30 48 34 20 00 3C 30 20 00 08 00 98 00 68 00 00 00 80 5C 3E 30 38 20 1C 00

3C 30 20 00 70 00 08 00 68 00 00 00 5F 40 34 30 80 5C 3E 00 3C 30 20 00 E8 00 E0 00 48 00 00 00

10 19 1F 30 18 20 20 00 14 20 28 00 80 00 E0 00 E8 00 00 00 00 10 0C 30 18 20 20 00 10 19 1F 00

48 00 E0 00 A0 00 00 00 14 20 28 30 18 20 20 00 00 06 15 00 D8 00 E8 00 48 00 00 00 5C 8C A0 30

10 19 1F 00 14 20 28 00 E8 00 D8 00 80 00 00 00 10 19 1F 30 5C 8C A0 00 00 10 0C 00 D8 00 48 00

50 00 00 00 5C 8C A0 30 14 20 28 00 00 04 0F 00 E0 00 00 00 D0 00 00 00 18 20 20 30 18 20 20 00

1C 24 2C 00 E0 00 D0 00 60 00 00 00 18 20 20 30 1C 24 2C 00 00 04 0F 00 E0 00 60 00 A0 00 00 00

18 20 20 30 00 04 0F 00 00 06 15 00 60 00 D8 00 50 00 00 00 00 04 0F 30 5C 8C A0 00 00 04 0F 00

D0 00 D8 00 60 00 00 00 1C 24 2C 30 5C 8C A0 00 00 04 0F 00 00 00 D8 00 D0 00 00 00 18 20 20 30

5C 8C A0 00 1C 24 2C 00 A0 00 20 00 48 00 00 00 00 06 15 30 00 14 14 00 14 20 28 00 C8 00 98 00

08 00 00 00 18 20 20 30 48 58 60 00 18 20 20 00 E0 00 80 00 C8 00 00 00 18 20 20 30 00 10 0C 00

18 20 20 00 00 00 E0 00 C8 00 00 00 18 20 20 30 18 20 20 00 18 20 20 00 20 00 50 00 48 00 00 00

00 14 14 30 00 04 0F 00 14 20 28 00 D8 00 00 00 10 00 00 00 5C 8C A0 30 18 20 20 00 48 58 60 00

80 00 D8 00 10 00 00 00 00 10 0C 30 5C 8C A0 00 48 58 60 00 10 00 08 00 70 00 00 00 48 58 60 30

18 20 20 00 58 7C 88 00 C8 00 08 00 00 00 00 00 18 20 20 30 18 20 20 00 18 20 20 00 08 00 10 00

00 00 00 00 18 20 20 30 48 58 60 00 18 20 20 00 02 00 00 00 98 00 C8 00 78 00 80 00 48 58 60 38

18 20 20 00 14 20 28 00 00 10 0C 00 10 00 70 00 80 00 78 00 48 58 60 38 58 7C 88 00 00 10 0C 00

14 20 28 00

  
  
  
Bone 7 \[at offset 0x00002A04\]:

  
58 00 00 00 00 00 22 00 EA FF 00 00 00 00 22 00 91 FF 00 00 E0 FF 02 00 E7 FF 00 00 E1 FF 00 00

90 FF 00 00 22 00 FE FF 91 FF 00 00 00 00 E1 FF 90 FF 00 00 EB FF 00 00 FE FF 00 00 22 00 FF FF

E9 FF 00 00 15 00 00 00 FF FF 00 00 00 00 E0 FF F3 FF 00 00 00 00 00 00 10 00 00 00 00 00 20 00

00 00 00 00 0A 00 00 00 10 00 08 00 00 00 00 00 38 24 1C 30 2C 18 18 00 40 30 24 00 00 00 30 00

10 00 00 00 40 30 24 30 40 2C 20 00 38 24 1C 00 48 00 40 00 38 00 00 00 D8 A0 78 30 44 24 1C 00

60 40 2C 00 30 00 48 00 10 00 00 00 40 2C 20 30 D8 A0 78 00 38 24 1C 00 40 00 00 00 38 00 00 00

44 24 1C 30 40 30 24 00 60 40 2C 00 00 00 40 00 50 00 00 00 40 30 24 30 44 24 1C 00 4C 34 1C 00

48 00 30 00 50 00 00 00 D8 A0 78 30 40 2C 20 00 4C 34 1C 00 40 00 48 00 50 00 00 00 44 24 1C 30

D8 A0 78 00 4C 34 1C 00 30 00 00 00 50 00 00 00 40 2C 20 30 40 30 24 00 4C 34 1C 00 08 00 10 00

18 00 00 00 2C 18 18 30 38 24 1C 00 4C 33 29 00 04 00 00 00 20 00 08 00 28 00 18 00 50 38 28 38

2C 18 18 00 4C 33 29 00 4C 33 29 00 18 00 10 00 28 00 48 00 4C 33 29 38 38 24 1C 00 4C 33 29 00

D8 A0 78 00 28 00 48 00 20 00 38 00 4C 33 29 38 D8 A0 78 00 50 38 28 00 60 40 2C 00 20 00 38 00

08 00 00 00 50 38 28 38 60 40 2C 00 2C 18 18 00 40 30 24 00

  
  
  
Bone 8 \[at offset 0x00002B98\]:

  
08 05 00 00 FE FF D8 FF D3 FF 00 00 04 00 F7 FF 39 FF 00 00 04 00 BA FF 2D FF 00 00 FF FF 9B FF

C7 FF 00 00 EA FF F7 FF 38 FF 00 00 EA FF BA FF 2C FF 00 00 E4 FF 9B FF C6 FF 00 00 E3 FF D8 FF

D2 FF 00 00 FB FF F2 FF 51 FF 00 00 F9 FF F9 FF 6B FF 00 00 F9 FF 05 00 73 FF 00 00 F8 FF FF FF

99 FF 00 00 F7 FF F1 FF 9E FF 00 00 FA FF F5 FF A7 FF 00 00 F9 FF DB FF C0 FF 00 00 F9 FF 34 00

C2 FF 00 00 F8 FF 2E 00 E0 FF 00 00 EB FF F5 FF A6 FF 00 00 EF FF F1 FF 9D FF 00 00 EA FF 34 00

C2 FF 00 00 EF FF FE FF 99 FF 00 00 F0 FF 05 00 73 FF 00 00 F1 FF F9 FF 6B FF 00 00 F2 FF F2 FF

51 FF 00 00 EA FF DB FF C0 FF 00 00 EF FF E4 FF 97 FF 00 00 E9 FF 2E 00 DF FF 00 00 F8 FF E4 FF

97 FF 00 00 EE FF E3 FF 7B FE 00 00 EE FF 07 00 82 FE 00 00 E6 FF E5 FF 32 FF 00 00 E7 FF C0 FF

2A FF 00 00 F1 FF E3 FF 7B FE 00 00 F1 FF 07 00 82 FE 00 00 EA FF C0 FF 2A FF 00 00 EA FF E5 FF

32 FF 00 00 0C 00 DE FF 7B FE 00 00 04 00 BA FF 2D FF 00 00 04 00 F7 FF 39 FF 00 00 0B 00 1A 00

87 FE 00 00 EA FF BA FF 2C FF 00 00 EA FF F7 FF 38 FF 00 00 F2 FF DE FF 7A FE 00 00 F1 FF 1A 00

86 FE 00 00 08 00 C0 FF 2C FF 00 00 07 00 E5 FF 33 FF 00 00 0F 00 07 00 83 FE 00 00 0F 00 E4 FF

7C FE 00 00 0B 00 07 00 83 FE 00 00 0C 00 E4 FF 7C FE 00 00 04 00 C0 FF 2C FF 00 00 04 00 E5 FF

33 FF 00 00 0C 00 46 00 48 FF 00 00 F7 FF 49 00 3B FF 00 00 F8 FF 0F 00 2F FF 00 00 0C 00 0D 00

3D FF 00 00 0A 00 41 00 61 FF 00 00 0B 00 08 00 56 FF 00 00 F5 FF 3F 00 6D FF 00 00 F5 FF 05 00

61 FF 00 00 DF FF 41 00 5F FF 00 00 E0 FF 08 00 54 FF 00 00 E0 FF 46 00 46 FF 00 00 E1 FF 0D 00

3B FF 00 00 F7 FF F7 FF 37 FF 00 00 F6 FF F2 FF 50 FF 00 00 F7 FF FD FF 38 FF 00 00 F6 FF F8 FF

51 FF 00 00 FD FF 9F FF C7 FF 00 00 FD FF D4 FF D2 FF 00 00 E5 FF D4 FF D1 FF 00 00 E6 FF 9F FF

C7 FF 00 00 E5 FF 9D FF D4 FF 00 00 E5 FF D1 FF DE FF 00 00 FC FF D1 FF DF FF 00 00 FD FF 9D FF

D5 FF 00 00 FC FF A4 FF F4 FF 00 00 EF FF B1 FF F6 FF 00 00 F1 FF B6 FF DA FF 00 00 FE FF AA FF

D8 FF 00 00 F0 FF 98 FF F1 FF 00 00 F1 FF 9D FF D5 FF 00 00 E3 FF A4 FF F3 FF 00 00 E4 FF AA FF

D7 FF 00 00 0B 00 F8 FF 80 FE 00 00 FF FF 04 00 82 FE 00 00 00 00 0C 00 58 FE 00 00 0D 00 00 00

56 FE 00 00 FF FF EB FF 7D FE 00 00 00 00 F4 FF 53 FE 00 00 F2 FF F8 FF 7F FE 00 00 F4 FF 00 00

55 FE 00 00 07 00 10 00 85 FE 00 00 FF FF 19 00 86 FE 00 00 FF FF 1C 00 77 FE 00 00 08 00 13 00

75 FE 00 00 FF FF 06 00 82 FE 00 00 FF FF 09 00 73 FE 00 00 F5 FF 10 00 84 FE 00 00 F6 FF 13 00

74 FE 00 00 0E 00 CD FF 7C FE 00 00 FF FF DC FF 7F FE 00 00 EF FF CD FF 7B FE 00 00 FF FF BE FF

78 FE 00 00 FF FF DB FF 87 FE 00 00 0D 00 CB FF 84 FE 00 00 FF FF BC FF 81 FE 00 00 EF FF CB FF

83 FE 00 00 0F 00 FE FF 7D FE 00 00 10 00 E3 FF 69 FE 00 00 0D 00 F5 FF AD FE 00 00 0D 00 FB FF

AE FE 00 00 0F 00 05 00 79 FE 00 00 10 00 E7 FF 64 FE 00 00 14 00 E3 FF 65 FE 00 00 13 00 01 00

7B FE 00 00 11 00 F8 FF AE FE 00 00 E8 FF F8 FF AC FE 00 00 EA FF 01 00 79 FE 00 00 EB FF E3 FF

63 FE 00 00 EF FF E7 FF 62 FE 00 00 EE FF 05 00 78 FE 00 00 EC FF FB FF AD FE 00 00 EC FF F5 FF

AB FE 00 00 EF FF E3 FF 68 FE 00 00 EE FF FE FF 7C FE 00 00 01 00 F4 FF 44 FF 00 00 EC FF F4 FF

43 FF 00 00 01 00 FB FF 45 FF 00 00 EB FF FB FF 44 FF 00 00 E2 FF DB FF B5 FF 00 00 DB FF EA FF

BF FF 00 00 D3 FF D2 FF BC FF 00 00 F6 FF 38 00 A5 FF 00 00 F1 FF 32 00 B6 FF 00 00 D3 FF 31 00

A8 FF 00 00 CB FF E0 FF C5 FF 00 00 DD FF DD FF D8 FF 00 00 F9 FF D4 FF C6 FF 00 00 E9 FF E7 FF

C9 FF 00 00 0E 00 36 00 BF FF 00 00 F8 FF FD FF 8F FF 00 00 F3 FF F6 FF A1 FF 00 00 12 00 EE FF

A4 FF 00 00 15 00 22 00 03 00 00 00 FA FF 33 00 C7 FF 00 00 21 00 FF FF FD FF 00 00 13 00 E5 FF

C8 FF 00 00 F7 FF 06 00 DA FF 00 00 FC FF EC FF AE FF 00 00 01 00 FD FF 0E 00 00 00 E7 FF 00 00

FB FF 00 00 E7 FF 22 00 01 00 00 00 E4 FF E0 FF F4 FF 00 00 16 00 E0 FF F7 FF 00 00 F8 FF E6 FF

C7 FF 00 00 EF FF C8 FF D2 FF 00 00 E7 FF F4 FF EC FF 00 00 D5 FF 2B 00 B8 FF 00 00 D7 FF F5 FF

A5 FF 00 00 D5 FF FB FF 95 FF 00 00 00 00 20 00 00 00 00 00 3F 00 00 00 70 03 78 03 A0 03 00 00

42 58 78 30 21 22 24 00 4F 51 55 00 70 00 60 00 D8 00 00 00 1C 1C 1C 30 24 34 44 00 24 28 40 00

70 00 68 00 60 00 00 00 1C 1C 1C 30 18 20 20 00 24 34 44 00 58 00 D8 00 60 00 00 00 24 30 3C 30

24 28 40 00 24 34 44 00 48 00 40 00 D8 00 00 00 14 16 16 30 18 20 20 00 24 28 40 00 C8 00 A0 00

90 00 00 00 14 1C 1C 30 34 39 39 00 14 20 36 00 C0 00 90 00 88 00 00 00 0C 14 2C 30 14 20 36 00

22 2C 30 00 C8 00 90 00 C0 00 00 00 14 1C 1C 30 14 20 36 00 0C 14 2C 00 C8 00 B8 00 B0 00 00 00

14 1C 1C 30 16 19 18 00 0C 18 2B 00 A8 00 C8 00 B0 00 00 00 00 08 00 30 14 1C 1C 00 0C 18 2B 00

A0 00 C8 00 A8 00 00 00 34 39 39 30 14 1C 1C 00 00 08 00 00 D8 00 50 00 48 00 00 00 24 28 40 30

20 23 22 00 14 16 16 00 D8 00 58 00 50 00 00 00 24 28 40 30 24 30 3C 00 20 23 22 00 E8 01 D8 01

18 02 00 00 2D 31 31 30 04 08 10 00 10 2C 34 00 D8 01 C8 01 18 02 00 00 04 08 10 30 14 1C 24 00

10 2C 34 00 F8 01 E8 01 08 04 00 00 1F 22 22 30 2D 31 31 00 26 29 29 00 08 04 E8 01 18 02 00 00

26 29 29 30 2D 31 31 00 10 2C 34 00 18 02 C8 01 00 04 00 00 10 2C 34 30 14 1C 24 00 10 2C 34 00

C8 01 B8 01 00 04 00 00 14 1C 24 30 5C 64 6C 00 10 2C 34 00 B8 01 B0 01 10 02 00 00 5C 64 6C 30

18 20 20 00 12 13 13 00 B0 01 F8 01 10 02 00 00 18 20 20 30 1F 22 22 00 12 13 13 00 00 04 B8 01

10 02 00 00 10 2C 34 30 5C 64 6C 00 12 13 13 00 10 02 F8 01 08 04 00 00 12 13 13 30 1F 22 22 00

26 29 29 00 70 04 78 04 68 04 00 00 34 24 18 30 34 1C 14 00 31 21 1B 00 78 04 70 04 A8 04 00 00

34 1C 14 30 34 24 18 00 77 51 41 00 30 04 60 04 88 04 00 00 34 20 10 30 38 28 20 00 34 20 10 00

60 04 30 04 28 04 00 00 38 28 20 30 34 20 10 00 1C 10 08 00 30 04 38 04 28 04 00 00 34 20 10 30

6C 48 34 00 1C 10 08 00 38 04 30 04 F0 04 00 00 6C 48 34 30 34 20 10 00 48 30 1C 00 20 04 18 04

40 04 00 00 64 34 2C 30 4C 34 24 00 44 34 18 00 18 04 20 04 10 04 00 00 4C 34 24 30 64 34 2C 00

31 21 1B 00 58 04 10 04 50 04 00 00 88 5C 4A 30 31 21 1B 00 31 21 1B 00 10 04 58 04 18 04 00 00

31 21 1B 30 88 5C 4A 00 4C 34 24 00 58 04 48 04 18 04 00 00 88 5C 4A 30 54 40 34 00 4C 34 24 00

18 04 48 04 40 04 00 00 4C 34 24 30 54 40 34 00 44 34 18 00 E0 04 98 04 50 04 00 00 30 32 2C 30

26 1C 18 00 08 08 07 00 58 04 E8 04 48 04 00 00 15 15 13 30 15 16 13 00 16 16 14 00 E8 04 C8 04

48 04 00 00 15 16 13 30 23 24 20 00 16 16 14 00 A0 04 D8 04 A8 04 00 00 12 13 11 30 0A 0B 09 00

12 13 10 00 D8 04 98 04 78 04 00 00 0A 0B 09 30 26 1C 18 00 13 13 11 00 A0 04 C0 04 B8 04 00 00

12 13 11 30 19 1A 16 00 16 17 14 00 D0 04 E0 04 C8 04 00 00 50 44 38 30 30 32 2C 00 23 24 20 00

50 04 98 04 D8 04 00 00 08 08 07 30 26 1C 18 00 0A 0B 09 00 D8 04 78 04 A8 04 00 00 0A 0B 09 30

13 13 11 00 12 13 10 00 E8 04 A0 04 B8 04 00 00 15 16 13 30 12 13 11 00 16 17 14 00 C8 04 E8 04

B8 04 00 00 23 24 20 30 15 16 13 00 16 17 14 00 60 04 90 04 80 04 00 00 10 11 0F 30 18 19 18 00

14 14 10 00 90 04 98 04 D0 04 00 00 18 19 18 30 26 1C 18 00 50 44 38 00 E8 04 D8 04 A0 04 00 00

15 16 13 30 0A 0B 09 00 12 13 11 00 E8 04 58 04 D8 04 00 00 15 16 13 30 15 15 13 00 0A 0B 09 00

C8 04 E0 04 48 04 00 00 23 24 20 30 30 32 2C 00 16 16 14 00 98 04 E0 04 D0 04 00 00 26 1C 18 30

30 32 2C 00 50 44 38 00 50 04 D8 04 58 04 00 00 08 08 07 30 0A 0B 09 00 15 15 13 00 C0 04 80 04

B0 04 00 00 19 1A 16 30 14 14 10 00 0C 14 18 00 80 04 90 04 B0 04 00 00 14 14 10 30 18 19 18 00

0C 14 18 00 90 04 D0 04 B0 04 00 00 18 19 18 30 50 44 38 00 0C 14 18 00 D0 04 C8 04 B0 04 00 00

50 44 38 30 23 24 20 00 0C 14 18 00 C8 04 B8 04 B0 04 00 00 23 24 20 30 16 17 14 00 0C 14 18 00

B8 04 C0 04 B0 04 00 00 16 17 14 30 19 1A 16 00 0C 14 18 00 A0 04 A8 04 88 04 00 00 12 13 11 30

12 13 10 00 19 19 16 00 90 04 78 04 98 04 00 00 18 19 18 30 13 13 11 00 26 1C 18 00 90 04 60 04

78 04 00 00 18 19 18 30 10 11 0F 00 13 13 11 00 C0 04 A0 04 88 04 00 00 19 1A 16 30 12 13 11 00

19 19 16 00 5C 00 00 00 60 03 70 03 98 03 A0 03 30 40 34 38 42 58 78 00 25 26 27 00 4F 51 55 00

60 03 80 03 70 03 78 03 30 40 34 38 1C 1D 1E 00 42 58 78 00 21 22 24 00 68 03 88 03 60 03 80 03

57 59 5D 38 00 00 08 00 30 40 34 00 1C 1D 1E 00 60 03 98 03 68 03 90 03 30 40 34 38 25 26 27 00

57 59 5D 00 29 2A 2C 00 98 03 A0 03 80 03 78 03 25 26 27 38 4F 51 55 00 1C 1D 1E 00 21 22 24 00

80 03 88 03 98 03 90 03 1C 1D 1E 38 00 00 08 00 25 26 27 00 29 2A 2C 00 C0 03 88 03 E0 03 68 03

0D 0E 0E 38 00 00 08 00 5B 5D 61 00 57 59 5D 00 E0 03 68 03 B8 03 90 03 5B 5D 61 38 57 59 5D 00

16 17 18 00 29 2A 2C 00 B8 03 90 03 C0 03 88 03 16 17 18 38 29 2A 2C 00 0D 0E 0E 00 00 00 08 00

C0 03 C8 03 B8 03 B0 03 0D 0E 0E 38 18 18 1A 00 16 17 18 00 1D 1D 1F 00 C0 03 E0 03 C8 03 E8 03

0D 0E 0E 38 5B 5D 61 00 18 18 1A 00 54 56 5A 00 B0 03 E8 03 B8 03 E0 03 1D 1D 1F 38 54 56 5A 00

16 17 18 00 5B 5D 61 00 A8 03 B0 03 D0 03 C8 03 1E 1F 20 38 1D 1D 1F 00 37 38 3B 00 18 18 1A 00

C8 03 E8 03 D0 03 D8 03 18 18 1A 38 54 56 5A 00 37 38 3B 00 5A 5C 60 00 D8 03 E8 03 A8 03 B0 03

5A 5C 60 38 54 56 5A 00 1E 1F 20 00 1D 1D 1F 00 28 03 30 03 20 03 38 03 1B 1B 1C 38 12 12 13 00

2C 2C 2C 00 30 4C 60 00 40 03 58 03 28 03 30 03 2B 2C 2E 38 20 21 22 00 1B 1B 1C 00 12 12 13 00

40 03 28 03 48 03 20 03 2B 2C 2E 38 1B 1B 1C 00 50 52 56 00 2C 2C 2C 00 30 03 58 03 38 03 50 03

12 12 13 38 20 21 22 00 68 90 88 00 52 54 58 00 20 03 38 03 48 03 50 03 2C 2C 2C 38 98 B0 CC 00

50 52 56 00 74 94 B0 00 48 03 50 03 40 03 58 03 18 30 08 38 28 28 34 00 2B 2C 2E 00 20 21 22 00

68 02 60 02 90 02 80 02 29 2A 2C 38 50 52 56 00 08 14 38 00 34 3C 2C 00 68 02 70 02 60 02 78 02

29 2A 2C 38 1C 1C 1E 00 50 52 56 00 2C 2C 2C 00 90 02 98 02 68 02 70 02 1D 1E 1F 38 13 14 15 00

29 2A 2C 00 1C 1C 1E 00 60 02 78 02 80 02 88 02 50 52 56 38 2C 2C 2C 00 74 94 B0 00 10 10 11 00

80 02 88 02 90 02 98 02 74 94 B0 38 10 10 11 00 1D 1E 1F 00 13 14 15 00 B0 02 D8 02 B8 02 C8 02

00 00 00 38 00 00 00 00 00 00 00 00 00 00 00 00 F0 02 18 03 F8 02 08 03 00 00 00 38 00 00 00 00

00 00 00 00 00 00 00 00 A8 02 B0 02 A0 02 B8 02 19 1D 18 38 0F 12 0F 00 38 3C 3C 00 4C 6C 64 00

D0 02 D8 02 A8 02 B0 02 12 15 12 38 0A 08 28 00 19 1D 18 00 0F 12 0F 00 C0 02 C8 02 D0 02 D8 02

30 37 2E 38 9C A4 B0 00 12 15 12 00 0A 08 28 00 A0 02 B8 02 C0 02 C8 02 38 3C 3C 38 4C 6C 64 00

30 37 2E 00 9C A4 B0 00 E8 02 F0 02 E0 02 F8 02 19 1D 18 38 0F 12 0F 00 38 3C 3C 00 4C 6C 64 00

10 03 18 03 E8 02 F0 02 12 15 12 38 0A 08 28 00 19 1D 18 00 0F 12 0F 00 00 03 08 03 10 03 18 03

30 37 2F 38 9C A4 B0 00 12 15 12 00 0A 08 28 00 E0 02 F8 02 00 03 08 03 38 3C 3C 38 4C 6C 64 00

30 37 2F 00 9C A4 B0 00 68 01 70 01 60 01 78 01 0C 14 18 38 08 18 20 00 2E 2E 2E 00 2C 38 48 00

98 01 80 01 68 01 70 01 11 11 11 38 0C 0C 0C 00 0C 14 18 00 09 09 09 00 90 01 98 01 60 01 68 01

1B 1B 1B 38 11 11 11 00 2E 2E 2E 00 0C 14 18 00 80 01 88 01 70 01 78 01 0C 0C 0C 38 0A 0A 0A 00

09 09 09 00 08 09 08 00 88 01 90 01 78 01 60 01 0A 0A 0A 38 1B 1B 1B 00 08 09 08 00 2E 2E 2E 00

E8 00 F0 00 E0 00 F8 00 0C 20 24 38 11 11 11 00 1C 20 2C 00 1B 1B 1B 00 08 01 18 01 E8 00 F0 00

09 09 09 38 0C 14 18 00 0C 0C 0C 00 11 11 11 00 00 01 08 01 E0 00 E8 00 08 09 08 38 09 09 09 00

0A 0A 0A 00 0C 0C 0C 00 18 01 10 01 F0 00 F8 00 0C 14 18 38 2E 2E 2E 00 11 11 11 00 1B 1B 1B 00

10 01 00 01 F8 00 E0 00 2E 2E 2E 38 08 09 08 00 1B 1B 1B 00 0A 0A 0A 00 50 01 20 01 58 01 38 01

08 09 08 38 1C 20 2C 00 0A 08 28 00 1C 20 2C 00 48 01 40 01 58 01 50 01 0E 10 0E 38 17 1A 16 00

0A 08 14 00 08 09 08 00 40 01 28 01 50 01 20 01 24 2C 38 38 26 34 48 00 2C 38 48 00 40 44 54 00

28 01 30 01 20 01 38 01 26 34 48 38 1B 1F 28 00 07 08 07 00 07 08 07 00 58 01 38 01 48 01 30 01

0A 08 28 38 07 08 07 00 0E 10 0E 00 1B 1F 1A 00 68 00 70 00 78 00 80 00 04 02 01 38 25 11 08 00

08 04 02 00 2C 0C 06 00 88 00 98 00 C0 00 D0 00 09 04 02 38 44 38 28 00 16 0A 05 00 14 0F 09 00

88 00 68 00 98 00 78 00 09 04 02 38 04 02 01 00 44 38 28 00 08 04 02 00 D0 00 80 00 C0 00 70 00

14 0F 09 38 2C 0C 06 00 16 0A 05 00 25 11 08 00 A0 00 58 00 90 00 60 00 34 39 39 38 24 30 3C 00

14 20 36 00 24 34 44 00 90 00 60 00 88 00 68 00 14 20 36 38 24 34 44 00 22 2C 30 00 18 20 20 00

40 00 48 00 B8 00 B0 00 18 20 20 38 14 16 16 00 16 19 18 00 0C 18 2B 00 A8 00 50 00 A0 00 58 00

00 08 00 38 20 23 22 00 34 39 39 00 24 30 3C 00 98 00 78 00 D0 00 80 00 2B 2F 2E 38 1E 21 21 00

33 38 37 00 38 2C 48 00 B0 00 48 00 A8 00 50 00 0C 18 2B 38 14 16 16 00 00 08 00 00 20 23 22 00

08 00 10 00 00 00 18 00 0A 08 28 38 0C 14 18 00 25 2A 24 00 30 44 48 00 30 00 18 00 28 00 10 00

24 2C 38 38 48 48 4C 00 48 50 54 00 28 30 40 00 28 00 20 00 30 00 38 00 0B 18 20 38 0F 11 0E 00

1F 1C 28 00 00 00 12 00 00 00 38 00 08 00 20 00 25 2A 24 38 00 00 12 00 0A 08 28 00 0F 11 0E 00

38 00 00 00 30 00 18 00 00 00 12 38 25 2A 24 00 1F 24 1E 00 34 3C 33 00 48 02 50 02 40 02 58 02

10 10 10 38 0C 14 18 00 1B 1B 1B 00 2E 2E 2E 00 30 02 28 02 48 02 50 02 0D 0D 0D 38 09 09 09 00

10 10 10 00 0C 14 18 00 38 02 30 02 40 02 48 02 0A 0A 0A 38 0D 0D 0D 00 1B 1B 1B 00 10 10 10 00

28 02 20 02 50 02 58 02 09 09 09 38 09 09 09 00 0C 14 18 00 2E 2E 2E 00 20 02 38 02 58 02 40 02

09 09 09 38 0A 0A 0A 00 2E 2E 2E 00 1B 1B 1B 00 F0 03 08 02 00 04 18 02 0C 14 18 38 2D 2D 2D 00

1F 1F 1F 00 2C 2C 2C 00 00 04 10 02 F0 03 00 02 1F 1F 1F 38 06 06 06 00 0C 14 18 00 06 06 06 00

08 04 18 02 F8 03 08 02 0C 0C 0C 38 2C 2C 2C 00 0C 0C 0C 00 2D 2D 2D 00 10 02 08 04 00 02 F8 03

06 06 06 38 0C 0C 0C 00 06 06 06 00 0C 0C 0C 00 D0 01 A8 01 C0 01 A0 01 10 14 23 38 21 2C 30 00

18 1C 24 00 4C 3C 74 00 A8 01 D0 01 F0 01 E0 01 21 2C 30 38 10 14 23 00 18 1C 24 00 14 1C 14 00

D0 01 D8 01 E0 01 E8 01 10 23 23 38 04 08 10 00 35 3A 3A 00 2D 31 31 00 C0 01 C8 01 D0 01 D8 01

56 5E 5E 38 14 1C 24 00 10 23 23 00 04 08 10 00 A8 01 B0 01 A0 01 B8 01 21 2C 30 38 18 20 20 00

C0 D4 E4 00 5C 64 6C 00 F0 01 F8 01 A8 01 B0 01 2B 2F 2F 38 1F 22 22 00 21 2C 30 00 18 20 20 00

A0 01 B8 01 C0 01 C8 01 C0 D4 E4 38 5C 64 6C 00 56 5E 5E 00 14 1C 24 00 E0 01 E8 01 F0 01 F8 01

35 3A 3A 38 2D 31 31 00 2B 2F 2F 00 1F 22 22 00 70 04 30 04 A8 04 88 04 34 24 18 38 34 20 10 00

77 51 41 00 34 20 10 00 70 04 F8 04 30 04 F0 04 34 24 18 38 9C 6C 4C 00 34 20 10 00 48 30 1C 00

F0 04 F8 04 38 04 00 05 48 30 1C 38 9C 6C 4C 00 6C 48 34 00 61 42 35 00 70 04 68 04 F8 04 00 05

34 24 18 38 31 21 1B 00 9C 6C 4C 00 61 42 35 00 68 04 28 04 00 05 38 04 31 21 1B 38 1C 10 08 00

61 42 35 00 6C 48 34 00 28 04 68 04 60 04 78 04 1C 10 08 38 31 21 1B 00 38 28 20 00 34 1C 14 00

48 04 E0 04 40 04 20 04 54 40 34 38 FF D7 AE 00 44 34 18 00 64 34 2C 00 E0 04 50 04 20 04 10 04

FF D7 AE 38 31 21 1B 00 64 34 2C 00 31 21 1B 00 C0 04 88 04 80 04 60 04 19 1A 16 38 19 19 16 00

14 14 10 00 10 11 0F 00

  
  
  
Bone 10 \[at offset 0x00003E40\]:

  
60 00 00 00 00 00 F9 FF 91 FF 00 00 F9 FF 03 00 91 FF 00 00 07 00 03 00 91 FF 00 00 07 00 03 00

F4 FF 00 00 00 00 F9 FF F4 FF 00 00 F9 FF 03 00 F4 FF 00 00 00 00 F5 FF 91 FF 00 00 00 00 F5 FF

43 FF 00 00 0B 00 05 00 91 FF 00 00 0B 00 05 00 43 FF 00 00 F5 FF 05 00 91 FF 00 00 F5 FF 05 00

43 FF 00 00 00 00 20 00 00 00 00 00 03 00 00 00 48 00 58 00 38 00 00 00 04 07 04 30 08 0E 07 00

28 30 0C 00 50 00 40 00 30 00 00 00 0D 16 0C 30 38 50 2C 00 30 4C 24 00 28 00 18 00 20 00 00 00

1C 24 43 30 38 44 74 00 C8 D0 C8 00 06 00 00 00 38 00 30 00 48 00 40 00 28 30 0C 38 30 4C 24 00

04 07 04 00 38 50 2C 00 50 00 58 00 40 00 48 00 0D 16 0C 38 08 0E 07 00 38 50 2C 00 04 07 04 00

58 00 50 00 38 00 30 00 08 0E 07 38 0D 16 0C 00 28 30 0C 00 30 4C 24 00 00 00 08 00 20 00 28 00

1F 2C 2C 38 08 14 1C 00 C8 D0 C8 00 1C 24 43 00 28 00 08 00 18 00 10 00 1C 24 43 38 08 14 1C 00

38 44 74 00 28 2C 34 00 10 00 00 00 18 00 20 00 28 2C 34 38 1F 2C 2C 00 38 44 74 00 C8 D0 C8 00

  
  
  
Bone 12 \[at offset 0x00003F80\]:

  
60 00 00 00 00 00 F9 FF 91 FF 00 00 F9 FF 03 00 91 FF 00 00 07 00 03 00 91 FF 00 00 07 00 03 00

F4 FF 00 00 00 00 F9 FF F4 FF 00 00 F9 FF 03 00 F4 FF 00 00 00 00 F5 FF 91 FF 00 00 00 00 F5 FF

43 FF 00 00 0B 00 05 00 91 FF 00 00 0B 00 05 00 43 FF 00 00 F5 FF 05 00 91 FF 00 00 F5 FF 05 00

43 FF 00 00 00 00 20 00 00 00 00 00 03 00 00 00 48 00 58 00 38 00 00 00 24 30 0C 30 08 0E 07 00

06 0A 05 00 50 00 40 00 30 00 00 00 0D 16 0C 30 3C 54 24 00 21 37 1D 00 28 00 18 00 20 00 00 00

1F 24 10 30 CD CC C4 00 30 4C 7C 00 06 00 00 00 38 00 30 00 48 00 40 00 06 0A 05 38 21 37 1D 00

24 30 0C 00 3C 54 24 00 50 00 58 00 40 00 48 00 0D 16 0C 38 08 0E 07 00 3C 54 24 00 24 30 0C 00

58 00 50 00 38 00 30 00 08 0E 07 38 0D 16 0C 00 06 0A 05 00 21 37 1D 00 00 00 08 00 20 00 28 00

1F 22 1F 38 14 14 10 00 30 4C 7C 00 1F 24 10 00 28 00 08 00 18 00 10 00 1F 24 10 38 14 14 10 00

CD CC C4 00 17 19 17 00 10 00 00 00 18 00 20 00 17 19 17 38 1F 22 1F 00 CD CC C4 00 30 4C 7C 00

  
  
  
Bone 15 \[at offset 0x000040C0\]:

  
F0 00 00 00 E4 FF 00 00 9B FF 00 00 E6 FF 00 00 78 FF 00 00 00 00 E8 FF 91 FF 00 00 18 00 00 00

3F 00 00 00 3D 00 00 00 00 00 00 00 20 00 C1 FF EA FF 00 00 24 00 C9 FF 1F 00 00 00 E2 FF C5 FF

EA FF 00 00 F2 FF D2 FF 2E 00 00 00 2B 00 00 00 DB FF 00 00 FF FF D2 FF EA FF 00 00 DD FF 00 00

34 00 00 00 D2 FF 00 00 EB FF 00 00 FF FF 00 00 63 FF 00 00 00 00 EA FF 78 FF 00 00 15 00 00 00

78 FF 00 00 17 00 00 00 9B FF 00 00 AA FF E2 FF EF FF 00 00 AA FF 1E 00 EF FF 00 00 00 00 16 00

78 FF 00 00 FF FF 2E 00 EA FF 00 00 F2 FF 2E 00 2E 00 00 00 E2 FF 3B 00 EA FF 00 00 24 00 37 00

2D 00 00 00 20 00 3F 00 EA FF 00 00 00 00 18 00 91 FF 00 00 D2 FF 00 00 C3 FF 00 00 00 00 D5 FF

BD FF 00 00 00 00 2B 00 BD FF 00 00 23 00 00 00 AE FF 00 00 00 00 20 00 00 00 00 00 34 00 00 00

30 00 20 00 28 00 00 00 48 44 40 30 0B 0E 15 00 50 4C 58 00 40 00 28 00 38 00 00 00 FF EC E0 30

50 4C 58 00 40 38 48 00 18 00 40 00 58 00 00 00 68 5C 4C 30 FF EC E0 00 58 50 54 00 38 00 50 00

60 00 00 00 10 18 24 30 00 0C 14 00 00 0C 14 00 38 00 60 00 88 00 00 00 10 18 24 30 00 0C 14 00

14 08 18 00 40 00 18 00 30 00 00 00 FF EC E0 30 68 5C 4C 00 48 44 40 00 88 00 40 00 38 00 00 00

50 64 6C 30 FF EC E0 00 40 38 48 00 28 00 40 00 30 00 00 00 50 4C 58 30 FF EC E0 00 48 44 40 00

38 00 28 00 50 00 00 00 10 18 24 30 00 0C 14 00 00 0C 14 00 30 00 18 00 20 00 00 00 48 44 40 30

68 5C 4C 00 0B 0E 15 00 20 00 50 00 28 00 00 00 0B 0E 15 30 00 0C 14 00 00 0C 14 00 88 00 58 00

40 00 00 00 50 64 6C 30 58 50 54 00 FF EC E0 00 58 00 88 00 90 00 00 00 58 50 54 30 50 64 6C 00

64 68 70 00 88 00 60 00 90 00 00 00 14 08 18 30 00 0C 14 00 64 68 70 00 20 00 B8 00 C0 00 00 00

0B 0E 15 30 0F 13 1E 00 24 1F 20 00 C0 00 A8 00 B0 00 00 00 24 1F 20 30 0A 0C 14 00 28 20 24 00

A8 00 18 00 58 00 00 00 0A 0C 14 30 68 5C 4C 00 58 50 54 00 A0 00 B0 00 60 00 00 00 04 04 07 30

28 20 24 00 00 0C 14 00 60 00 B0 00 90 00 00 00 00 0C 14 30 28 20 24 00 64 68 70 00 18 00 A8 00

B8 00 00 00 68 5C 4C 30 0A 0C 14 00 0F 13 1E 00 A8 00 90 00 B0 00 00 00 0A 0C 14 30 64 68 70 00

28 20 24 00 A8 00 C0 00 B8 00 00 00 0A 0C 14 30 24 1F 20 00 0F 13 1E 00 C0 00 B0 00 A0 00 00 00

24 1F 20 30 28 20 24 00 04 04 07 00 18 00 B8 00 20 00 00 00 68 5C 4C 30 0F 13 1E 00 0B 0E 15 00

A0 00 20 00 C0 00 00 00 04 04 07 30 0B 0E 15 00 24 1F 20 00 58 00 90 00 A8 00 00 00 58 50 54 30

64 68 70 00 0A 0C 14 00 08 00 70 00 68 00 00 00 34 24 19 30 70 4C 3D 00 31 21 1B 00 98 00 08 00

68 00 00 00 32 1E 14 30 34 24 19 00 31 21 1B 00 78 00 98 00 68 00 00 00 3C 32 1E 30 32 1E 14 00

31 21 1B 00 70 00 78 00 68 00 00 00 70 4C 3D 30 3C 32 1E 00 31 21 1B 00 E0 00 E8 00 48 00 00 00

0C 12 1B 30 24 30 3C 00 0C 12 1B 00 E0 00 80 00 E8 00 00 00 0C 12 1B 30 06 12 14 00 24 30 3C 00

E0 00 48 00 A0 00 00 00 0C 12 1B 30 0C 12 1B 00 00 05 14 00 E8 00 D8 00 48 00 00 00 24 30 3C 30

60 7C 88 00 0C 12 1B 00 D8 00 E8 00 80 00 00 00 60 7C 88 30 24 30 3C 00 06 12 14 00 48 00 D8 00

50 00 00 00 0C 12 1B 30 60 7C 88 00 09 11 12 00 00 00 E0 00 D0 00 00 00 00 1C 20 30 0C 12 1B 00

28 34 3C 00 D0 00 E0 00 60 00 00 00 28 34 3C 30 0C 12 1B 00 09 11 12 00 60 00 E0 00 A0 00 00 00

09 11 12 30 0C 12 1B 00 00 05 14 00 D8 00 60 00 50 00 00 00 60 7C 88 30 09 11 12 00 09 11 12 00

D8 00 D0 00 60 00 00 00 60 7C 88 30 28 34 3C 00 09 11 12 00 D8 00 00 00 D0 00 00 00 60 7C 88 30

00 1C 20 00 28 34 3C 00 20 00 A0 00 48 00 00 00 05 11 14 30 00 05 14 00 0C 12 1B 00 98 00 C8 00

08 00 00 00 06 12 14 30 28 34 3C 00 05 10 18 00 80 00 E0 00 C8 00 00 00 06 12 14 30 0C 12 1B 00

28 34 3C 00 E0 00 00 00 C8 00 00 00 0C 12 1B 30 00 1C 20 00 28 34 3C 00 50 00 20 00 48 00 00 00

09 11 12 30 05 11 14 00 0C 12 1B 00 00 00 D8 00 10 00 00 00 00 1C 20 30 60 7C 88 00 34 50 58 00

D8 00 80 00 10 00 00 00 60 7C 88 30 06 12 14 00 34 50 58 00 08 00 10 00 70 00 00 00 05 10 18 30

34 50 58 00 40 4C 58 00 08 00 C8 00 00 00 00 00 05 10 18 30 28 34 3C 00 00 1C 20 00 10 00 08 00

00 00 00 00 34 50 58 30 05 10 18 00 00 1C 20 00 02 00 00 00 C8 00 98 00 80 00 78 00 28 34 3C 38

06 12 14 00 06 12 14 00 64 68 70 00 70 00 10 00 78 00 80 00 40 4C 58 38 34 50 58 00 64 68 70 00

06 12 14 00

  
  
  
Bone 16 \[at offset 0x00004604\]:

  
58 00 00 00 00 00 22 00 EA FF 00 00 00 00 22 00 91 FF 00 00 20 00 02 00 E7 FF 00 00 1F 00 00 00

90 FF 00 00 DD FF FE FF 91 FF 00 00 00 00 E1 FF 90 FF 00 00 15 00 00 00 FE FF 00 00 DE FF FF FF

E9 FF 00 00 EB FF 00 00 FF FF 00 00 00 00 E0 FF F3 FF 00 00 00 00 00 00 10 00 00 00 00 00 20 00

00 00 00 00 0A 00 00 00 08 00 10 00 00 00 00 00 2C 1C 10 30 9C 64 50 00 44 28 18 00 30 00 00 00

10 00 00 00 94 68 48 30 44 28 18 00 9C 64 50 00 40 00 48 00 38 00 00 00 3C 2C 10 30 E0 C4 98 00

34 1C 18 00 48 00 30 00 10 00 00 00 E0 C4 98 30 94 68 48 00 9C 64 50 00 00 00 40 00 38 00 00 00

44 28 18 30 3C 2C 10 00 34 1C 18 00 40 00 00 00 50 00 00 00 3C 2C 10 30 44 28 18 00 34 1C 18 00

30 00 48 00 50 00 00 00 94 68 48 30 E0 C4 98 00 34 1C 18 00 48 00 40 00 50 00 00 00 E0 C4 98 30

3C 2C 10 00 34 1C 18 00 00 00 30 00 50 00 00 00 44 28 18 30 94 68 48 00 34 1C 18 00 10 00 08 00

18 00 00 00 9C 64 50 30 2C 1C 10 00 31 21 1B 00 04 00 00 00 08 00 20 00 18 00 28 00 2C 1C 10 38

4E 35 2B 00 31 21 1B 00 74 4C 3C 00 10 00 18 00 48 00 28 00 9C 64 50 38 31 21 1B 00 E0 C4 98 00

74 4C 3C 00 48 00 28 00 38 00 20 00 E0 C4 98 38 74 4C 3C 00 34 1C 18 00 4E 35 2B 00 38 00 20 00

00 00 08 00 34 1C 18 38 4E 35 2B 00 44 28 18 00 2C 1C 10 00

  
  
  
Bone 17 \[at offset 0x00004798\]:

  
F8 00 00 00 21 00 CD FF BF FF 00 00 28 00 DE FF C6 FF 00 00 30 00 C5 FF C8 FF 00 00 0D 00 25 00

9C FF 00 00 12 00 23 00 AE FF 00 00 30 00 1E 00 A2 FF 00 00 38 00 D5 FF CE FF 00 00 24 00 D6 FF

E1 FF 00 00 0A 00 CA FF D0 FF 00 00 19 00 DD FF D0 FF 00 00 F4 FF 28 00 B5 FF 00 00 0C 00 E6 FF

93 FF 00 00 11 00 E3 FF A6 FF 00 00 F2 FF DC FF A9 FF 00 00 EB FF 22 00 FC FF 00 00 08 00 26 00

BE FF 00 00 DF FF FE FF FC FF 00 00 EF FF DA FF CE FF 00 00 0B 00 FF FF DA FF 00 00 08 00 DC FF

B4 FF 00 00 FF FF 00 00 0E 00 00 00 19 00 00 00 FC FF 00 00 19 00 22 00 FC FF 00 00 1C 00 DF FF

FC FF 00 00 EB FF DF FF FC FF 00 00 0A 00 DC FF CE FF 00 00 13 00 C0 FF DE FF 00 00 19 00 F1 FF

F0 FF 00 00 2E 00 1C 00 B2 FF 00 00 2C 00 E3 FF AB FF 00 00 2F 00 E6 FF 9A FF 00 00 00 00 20 00

00 00 00 00 28 00 00 00 68 00 60 00 58 00 00 00 20 18 0C 30 60 40 38 00 24 14 10 00 60 00 68 00

98 00 00 00 60 40 38 30 20 18 0C 00 9C 74 58 00 50 00 20 00 78 00 00 00 44 34 30 30 38 28 14 00

48 2C 20 00 20 00 50 00 18 00 00 00 38 28 14 30 44 34 30 00 58 38 28 00 28 00 20 00 18 00 00 00

51 37 2C 30 38 28 14 00 58 38 28 00 20 00 28 00 E0 00 00 00 38 28 14 30 51 37 2C 00 D0 B0 88 00

08 00 10 00 30 00 00 00 7A 53 43 30 BB 7E 66 00 D8 92 77 00 10 00 08 00 00 00 00 00 BB 7E 66 30

7A 53 43 00 31 21 1B 00 00 00 48 00 40 00 00 00 31 21 1B 30 80 56 46 00 34 24 14 00 48 00 00 00

08 00 00 00 80 56 46 30 31 21 1B 00 7A 53 43 00 38 00 48 00 08 00 00 00 50 2C 24 30 80 56 46 00

7A 53 43 00 38 00 08 00 30 00 00 00 50 2C 24 30 7A 53 43 00 D8 92 77 00 88 00 D0 00 40 00 00 00

11 12 10 30 30 32 2C 00 0C 0C 0B 00 D8 00 48 00 38 00 00 00 13 14 11 30 13 14 12 00 36 37 31 00

B8 00 D8 00 38 00 00 00 43 45 3C 30 13 14 11 00 36 37 31 00 C8 00 90 00 98 00 00 00 08 08 07 30

18 18 15 00 2C 2E 28 00 88 00 C8 00 68 00 00 00 11 12 10 30 08 08 07 00 0F 0F 0D 00 B0 00 90 00

A8 00 00 00 2A 2B 26 30 18 18 15 00 31 33 2D 00 D0 00 C0 00 B8 00 00 00 30 32 2C 30 26 27 23 00

43 45 3C 00 88 00 40 00 C8 00 00 00 11 12 10 30 0C 0C 0B 00 08 08 07 00 68 00 C8 00 98 00 00 00

0F 0F 0D 30 08 08 07 00 2C 2E 28 00 90 00 D8 00 A8 00 00 00 18 18 15 30 13 14 11 00 31 33 2D 00

D8 00 B8 00 A8 00 00 00 13 14 11 30 43 45 3C 00 31 33 2D 00 80 00 50 00 70 00 00 00 0C 04 13 30

0C 04 13 00 19 1A 17 00 88 00 80 00 C0 00 00 00 11 12 10 30 0C 04 13 00 26 27 23 00 C8 00 D8 00

90 00 00 00 08 08 07 30 13 14 11 00 18 18 15 00 48 00 D8 00 C8 00 00 00 13 14 12 30 13 14 11 00

08 08 07 00 D0 00 B8 00 38 00 00 00 30 32 2C 30 43 45 3C 00 36 37 31 00 D0 00 88 00 C0 00 00 00

30 32 2C 30 11 12 10 00 26 27 23 00 C8 00 40 00 48 00 00 00 08 08 07 30 0C 0C 0B 00 13 14 12 00

70 00 B0 00 A0 00 00 00 19 1A 17 30 2A 2B 26 00 3E 3F 38 00 80 00 70 00 A0 00 00 00 0C 04 13 30

19 1A 17 00 3E 3F 38 00 C0 00 80 00 A0 00 00 00 26 27 23 30 0C 04 13 00 3E 3F 38 00 B8 00 C0 00

A0 00 00 00 43 45 3C 30 26 27 23 00 3E 3F 38 00 A8 00 B8 00 A0 00 00 00 31 33 2D 30 43 45 3C 00

3E 3F 38 00 B0 00 A8 00 A0 00 00 00 2A 2B 26 30 31 33 2D 00 3E 3F 38 00 98 00 90 00 78 00 00 00

2C 2E 28 30 18 18 15 00 16 17 14 00 68 00 80 00 88 00 00 00 0F 0F 0D 30 0C 04 13 00 11 12 10 00

50 00 80 00 68 00 00 00 0C 04 13 30 0C 04 13 00 0F 0F 0D 00 90 00 B0 00 78 00 00 00 18 18 15 30

2A 2B 26 00 16 17 14 00 09 00 00 00 20 00 60 00 78 00 98 00 38 28 14 38 60 40 38 00 48 2C 20 00

9C 74 58 00 E8 00 60 00 E0 00 20 00 F0 BC A4 38 60 40 38 00 D0 B0 88 00 38 28 14 00 E8 00 E0 00

F0 00 28 00 F0 BC A4 38 D0 B0 88 00 5E 40 33 00 51 37 2C 00 58 00 60 00 F0 00 E8 00 24 14 10 38

60 40 38 00 5E 40 33 00 F0 BC A4 00 18 00 58 00 28 00 F0 00 58 38 28 38 24 14 10 00 51 37 2C 00

5E 40 33 00 58 00 18 00 68 00 50 00 24 14 10 38 58 38 28 00 20 18 0C 00 44 34 30 00 D0 00 38 00

10 00 30 00 B8 90 6C 38 50 2C 24 00 BB 7E 66 00 D8 92 77 00 40 00 D0 00 00 00 10 00 34 24 14 38

B8 90 6C 00 31 21 1B 00 BB 7E 66 00 78 00 B0 00 50 00 70 00 16 17 14 38 2A 2B 26 00 0C 04 13 00

19 1A 17 00

  
  
  
Bone 19 \[at offset 0x00004C9C\]:

  
D0 00 00 00 30 00 F3 FF 0F 00 00 00 42 00 F4 FF 5B FF 00 00 1E 00 32 00 43 FF 00 00 13 00 C5 FF

43 FF 00 00 13 00 D1 FF EF FE 00 00 13 00 F9 FF EF FE 00 00 22 00 D4 FF 1A FF 00 00 0B 00 B4 FF

1A FF 00 00 21 00 FC FF 0C FF 00 00 24 00 FC FF 21 FF 00 00 DC FF FC FF 21 FF 00 00 DF FF FC FF

0C FF 00 00 F5 FF B4 FF 1A FF 00 00 DE FF D4 FF 1A FF 00 00 ED FF F9 FF EF FE 00 00 ED FF D1 FF

EF FE 00 00 ED FF C5 FF 43 FF 00 00 E2 FF 32 00 43 FF 00 00 C6 FF F4 FF 43 FF 00 00 D6 FF F3 FF

0F 00 00 00 00 00 B6 FF 5F FF 00 00 00 00 BB FF 0F 00 00 00 00 00 2A 00 0F 00 00 00 00 00 F3 FF

2E 00 00 00 00 00 1D 00 21 FF 00 00 00 00 1E 00 0C FF 00 00 00 00 20 00 00 00 00 00 2A 00 00 00

38 00 18 00 30 00 00 00 BC A8 68 30 BC A8 68 00 2A 2B 26 00 20 00 38 00 30 00 00 00 3C 30 07 30

BC A8 68 00 2A 2B 26 00 60 00 78 00 68 00 00 00 48 34 08 30 48 34 08 00 2C 20 0F 00 80 00 60 00

68 00 00 00 48 2C 08 30 48 34 08 00 2C 20 0F 00 40 00 30 00 48 00 00 00 19 19 08 30 2A 2B 26 00

2C 20 0F 00 C8 00 40 00 C0 00 00 00 17 17 15 30 19 19 08 00 14 15 12 00 C0 00 58 00 C8 00 00 00

14 15 12 30 28 20 10 00 17 17 15 00 68 00 58 00 50 00 00 00 2C 20 0F 30 28 20 10 00 11 12 10 00

58 00 C0 00 50 00 00 00 28 20 10 30 14 15 12 00 11 12 10 00 C0 00 40 00 48 00 00 00 14 15 12 30

19 19 08 00 2C 20 0F 00 08 00 00 00 10 00 00 00 24 38 50 30 24 58 5C 00 10 14 1B 00 A0 00 08 00

18 00 00 00 6C A4 B6 30 24 38 50 00 20 40 44 00 20 00 40 00 28 00 00 00 00 04 0F 30 07 0E 16 00

00 04 0F 00 48 00 30 00 18 00 00 00 05 0C 10 30 0C 16 1C 00 20 40 44 00 10 00 48 00 08 00 00 00

10 14 1B 30 05 0C 10 00 24 38 50 00 88 00 C0 00 10 00 00 00 0C 19 21 30 1C 3C 44 00 10 14 1B 00

70 00 28 00 C8 00 00 00 0D 10 10 30 00 04 0F 00 14 1D 1A 00 A8 00 A0 00 90 00 00 00 24 58 5C 30

6C A4 B6 00 1C 3C 44 00 88 00 10 00 B0 00 00 00 0C 19 21 30 10 14 1B 00 10 14 1B 00 50 00 88 00

90 00 00 00 06 14 14 30 0C 19 21 00 1C 3C 44 00 68 00 50 00 80 00 00 00 05 0C 10 30 06 14 14 00

00 20 28 00 58 00 78 00 70 00 00 00 00 0A 18 30 0D 10 10 00 0D 10 10 00 98 00 90 00 88 00 00 00

1C 3C 44 30 1C 3C 44 00 0C 19 21 00 48 00 18 00 08 00 00 00 05 0C 10 30 20 40 44 00 24 38 50 00

80 00 50 00 90 00 00 00 00 20 28 30 06 14 14 00 1C 3C 44 00 40 00 20 00 30 00 00 00 07 0E 16 30

00 04 0F 00 0C 16 1C 00 78 00 58 00 68 00 00 00 0D 10 10 30 00 0A 18 00 05 0C 10 00 80 00 A0 00

18 00 00 00 00 20 28 30 6C A4 B6 00 20 40 44 00 08 00 A0 00 A8 00 00 00 24 38 50 30 6C A4 B6 00

24 58 5C 00 90 00 A0 00 80 00 00 00 1C 3C 44 30 6C A4 B6 00 00 20 28 00 B0 00 10 00 00 00 00 00

10 14 1B 30 10 14 1B 00 24 58 5C 00 88 00 B0 00 98 00 00 00 0C 19 21 30 10 14 1B 00 1C 3C 44 00

08 00 A8 00 00 00 00 00 24 38 50 30 24 58 5C 00 24 58 5C 00 A8 00 90 00 98 00 00 00 24 58 5C 30

1C 3C 44 00 1C 3C 44 00 A8 00 98 00 B8 00 00 00 24 58 5C 30 1C 3C 44 00 05 13 1C 00 98 00 B0 00

B8 00 00 00 1C 3C 44 30 10 14 1B 00 05 13 1C 00 B0 00 00 00 B8 00 00 00 10 14 1B 30 24 58 5C 00

05 13 1C 00 00 00 A8 00 B8 00 00 00 24 58 5C 30 24 58 5C 00 05 13 1C 00 40 00 C8 00 28 00 00 00

07 0E 16 30 14 1D 1A 00 00 04 0F 00 70 00 C8 00 58 00 00 00 0D 10 10 30 14 1D 1A 00 00 0A 18 00

C0 00 48 00 10 00 00 00 1C 3C 44 30 05 0C 10 00 10 14 1B 00 50 00 C0 00 88 00 00 00 06 14 14 30

1C 3C 44 00 0C 19 21 00 03 00 00 00 80 00 18 00 60 00 38 00 48 2C 08 38 BC A8 68 00 48 34 08 00

BC A8 68 00 60 00 38 00 78 00 20 00 48 34 08 38 BC A8 68 00 48 34 08 00 3C 30 07 00 28 00 70 00

20 00 78 00 00 04 0F 38 0D 10 10 00 00 04 0F 00 0D 10 10 00

  
  
  
Bone 20 \[at offset 0x00005110\]:

  
B0 00 00 00 28 00 0A 00 EA FF 00 00 0D 00 D5 FF EA FF 00 00 F3 FF D5 FF EA FF 00 00 D8 FF 0A 00

EA FF 00 00 E3 FF F9 FF 04 00 00 00 1D 00 F9 FF 04 00 00 00 30 00 FE FF 71 FF 00 00 D0 FF FE FF

71 FF 00 00 03 00 C8 FF 74 FF 00 00 00 00 31 00 7C FF 00 00 00 00 DB FF 04 00 00 00 00 00 E7 FF

5B FF 00 00 20 00 02 00 5B FF 00 00 00 00 1E 00 5B FF 00 00 E0 FF 02 00 5B FF 00 00 00 00 EB FF

19 FF 00 00 1C 00 02 00 19 FF 00 00 00 00 1A 00 19 FF 00 00 E4 FF 02 00 19 FF 00 00 00 00 17 00

04 00 00 00 FD FF CE FF 91 FF 00 00 00 00 29 00 EA FF 00 00 00 00 20 00 00 00 00 00 1E 00 00 00

20 00 28 00 50 00 00 00 06 14 1C 30 3C 54 58 00 3C 54 58 00 10 00 18 00 20 00 00 00 2C 4C 54 30

24 40 50 00 06 14 1C 00 50 00 10 00 20 00 00 00 3C 54 58 30 2C 4C 54 00 06 14 1C 00 20 00 98 00

28 00 00 00 06 14 1C 30 05 0B 0F 00 3C 54 58 00 18 00 98 00 20 00 00 00 24 40 50 30 05 0B 0F 00

06 14 1C 00 28 00 08 00 50 00 00 00 3C 54 58 30 45 6C 7C 00 3C 54 58 00 00 00 08 00 28 00 00 00

20 3C 40 30 45 6C 7C 00 3C 54 58 00 98 00 00 00 28 00 00 00 05 0B 0F 30 20 3C 40 00 3C 54 58 00

08 00 10 00 50 00 00 00 45 6C 7C 30 2C 4C 54 00 3C 54 58 00 18 00 10 00 38 00 00 00 24 40 50 30

2C 4C 54 00 24 40 50 00 10 00 A0 00 38 00 00 00 2C 4C 54 30 78 98 A4 00 24 40 50 00 A0 00 10 00

08 00 00 00 78 98 A4 30 2C 4C 54 00 45 6C 7C 00 48 00 A8 00 18 00 00 00 00 18 1C 30 00 18 1C 00

24 40 50 00 00 00 A8 00 48 00 00 00 20 3C 40 30 00 18 1C 00 00 18 1C 00 A0 00 08 00 30 00 00 00

78 98 A4 30 45 6C 7C 00 10 24 28 00 08 00 00 00 30 00 00 00 45 6C 7C 30 20 3C 40 00 10 24 28 00

70 00 48 00 38 00 00 00 08 13 1A 30 00 18 1C 00 24 40 50 00 38 00 58 00 70 00 00 00 24 40 50 30

00 0B 18 00 08 13 1A 00 58 00 38 00 40 00 00 00 00 0B 18 30 24 40 50 00 08 10 14 00 A0 00 40 00

38 00 00 00 78 98 A4 30 08 10 14 00 24 40 50 00 40 00 A0 00 30 00 00 00 08 10 14 30 78 98 A4 00

10 24 28 00 68 00 30 00 48 00 00 00 10 30 34 30 10 24 28 00 00 18 1C 00 48 00 70 00 68 00 00 00

00 18 1C 30 08 13 1A 00 10 30 34 00 60 00 40 00 30 00 00 00 05 10 14 30 08 10 14 00 10 24 28 00

30 00 68 00 60 00 00 00 10 24 28 30 10 30 34 00 05 10 14 00 40 00 60 00 58 00 00 00 08 10 14 30

05 10 14 00 00 0B 18 00 98 00 18 00 A8 00 00 00 05 0B 0F 30 24 40 50 00 00 18 1C 00 00 00 98 00

A8 00 00 00 20 3C 40 30 05 0B 0F 00 00 14 18 00 48 00 18 00 38 00 00 00 00 18 1C 30 24 40 50 00

24 40 50 00 00 00 48 00 30 00 00 00 20 3C 40 30 00 18 1C 00 10 24 28 00 05 00 00 00 80 00 88 00

78 00 90 00 28 28 23 38 0E 0E 06 00 32 32 2D 00 17 14 10 00 58 00 60 00 78 00 80 00 17 14 10 38

0A 0A 0A 00 32 32 2D 00 28 28 23 00 60 00 68 00 80 00 88 00 0A 0A 0A 38 0F 0F 0F 00 28 28 23 00

0E 0E 06 00 68 00 70 00 88 00 90 00 0F 0F 0F 38 0A 0A 0A 00 0E 0E 06 00 17 14 10 00 70 00 58 00

90 00 78 00 0A 0A 0A 38 17 14 10 00 17 14 10 00 32 32 2D 00

  
  
  
Bone 21 \[at offset 0x000054A4\]:

  
88 00 00 00 FF FF E5 FF 00 00 00 00 DF FF 05 00 0B 00 00 00 1E 00 05 00 0B 00 00 00 00 00 D1 FF

D1 FF 00 00 25 00 ED FF BD FF 00 00 E7 FF F0 FF B8 FF 00 00 2C 00 00 00 AA FF 00 00 E1 FF FF FF

AB FF 00 00 2C 00 36 00 C8 FF 00 00 02 00 4C 00 D5 FF 00 00 DD FF 36 00 C8 FF 00 00 E9 FF F7 FF

E7 FF 00 00 D9 FF 23 00 EA FF 00 00 02 00 3A 00 F7 FF 00 00 FF FF 1A 00 13 00 00 00 2F 00 23 00

EA FF 00 00 15 00 F4 FF EC FF 00 00 00 00 20 00 00 00 00 00 1E 00 00 00 40 00 30 00 20 00 00 00

05 05 05 30 0C 0C 0C 00 23 23 23 00 40 00 20 00 78 00 00 00 05 05 05 30 23 23 23 00 1A 1A 1A 00

20 00 80 00 78 00 00 00 23 23 23 30 37 37 32 00 1A 1A 1A 00 20 00 18 00 80 00 00 00 23 23 23 30

3C 3C 37 00 37 37 32 00 80 00 18 00 00 00 00 00 37 37 32 30 3C 3C 37 00 32 32 2D 00 10 00 80 00

00 00 00 00 28 28 23 30 37 37 32 00 32 32 2D 00 78 00 80 00 10 00 00 00 1A 1A 1A 30 37 37 32 00

28 28 23 00 70 00 78 00 10 00 00 00 0C 0C 0C 30 1A 1A 1A 00 28 28 23 00 78 00 70 00 68 00 00 00

1A 1A 1A 30 0C 0C 0C 00 11 11 11 00 68 00 40 00 78 00 00 00 11 11 11 30 05 05 05 00 1A 1A 1A 00

40 00 68 00 48 00 00 00 05 05 05 30 11 11 11 00 11 11 11 00 70 00 60 00 68 00 00 00 0C 0C 0C 30

10 10 10 00 11 11 11 00 08 00 60 00 70 00 00 00 13 13 13 30 10 10 10 00 0C 0C 0C 00 70 00 10 00

08 00 00 00 0C 0C 0C 30 28 28 23 00 13 13 13 00 68 00 50 00 48 00 00 00 11 11 11 30 0F 0F 0F 00

11 11 11 00 50 00 68 00 60 00 00 00 0F 0F 0F 30 11 11 11 00 10 10 10 00 28 00 50 00 60 00 00 00

0C 0C 0C 30 0F 0F 0F 00 10 10 10 00 60 00 58 00 28 00 00 00 10 10 10 30 0C 0C 0C 00 0C 0C 0C 00

58 00 60 00 08 00 00 00 0C 0C 0C 30 10 10 10 00 13 13 13 00 00 00 58 00 08 00 00 00 32 32 2D 30

0C 0C 0C 00 13 13 13 00 38 00 50 00 28 00 00 00 07 07 07 30 0F 0F 0F 00 0C 0C 0C 00 18 00 58 00

00 00 00 00 3C 3C 37 30 0C 0C 0C 00 32 32 2D 00 18 00 28 00 58 00 00 00 3C 3C 37 30 0C 0C 0C 00

0C 0C 0C 00 40 00 50 00 38 00 00 00 05 05 05 30 0B 0B 0B 00 05 05 05 00 40 00 38 00 30 00 00 00

05 05 05 30 05 05 05 00 09 09 09 00 48 00 50 00 40 00 00 00 0E 0E 0E 30 0B 0B 0B 00 05 05 05 00

30 00 28 00 20 00 00 00 0C 0C 0C 30 0C 0C 0C 00 23 23 23 00 20 00 28 00 18 00 00 00 23 23 23 30

0C 0C 0C 00 3C 3C 37 00 08 00 10 00 00 00 00 00 13 13 13 30 28 28 23 00 32 32 2D 00 28 00 30 00

38 00 00 00 0C 0C 0C 30 0C 0C 0C 00 07 07 07 00 00 00 00 00

  
  
  
Bone 22 \[at offset 0x00005798\]:

  
80 00 00 00 00 00 C6 FF EC FF 00 00 E7 FF EB FF FA FF 00 00 25 00 E5 FF FA FF 00 00 E1 FF FE FF

00 00 00 00 2C 00 FF FF 00 00 00 00 02 00 00 00 85 FF 00 00 31 00 FF FF A2 FF 00 00 D3 FF FF FF

A2 FF 00 00 01 00 CF FF 8E FF 00 00 DC FF DD FF A0 FF 00 00 27 00 DB FF A0 FF 00 00 2D 00 FF FF

F1 FF 00 00 DF FF FF FF F1 FF 00 00 25 00 E4 FF EA FF 00 00 00 00 C8 FF DA FF 00 00 E5 FF E9 FF

EA FF 00 00 00 00 20 00 00 00 00 00 14 00 00 00 68 00 70 00 00 00 00 00 A4 7C 3C 30 74 60 1C 00

A8 78 24 00 70 00 78 00 00 00 00 00 74 60 1C 30 23 1C 05 00 A8 78 24 00 08 00 10 00 00 00 00 00

24 20 00 30 A8 88 20 00 A8 78 24 00 08 00 20 00 10 00 00 00 24 20 00 30 4D 2F 00 00 A8 88 20 00

00 00 78 00 08 00 00 00 A8 78 24 30 23 1C 05 00 24 20 00 00 68 00 00 00 10 00 00 00 A4 7C 3C 30

A8 78 24 00 A8 88 20 00 20 00 08 00 18 00 00 00 4D 2F 00 30 24 20 00 00 24 20 00 00 30 00 38 00

28 00 00 00 05 05 05 30 08 08 08 00 05 05 05 00 40 00 48 00 70 00 00 00 41 41 37 30 12 12 12 00

28 28 28 00 28 00 38 00 48 00 00 00 14 14 14 30 08 08 08 00 12 12 12 00 28 00 48 00 40 00 00 00

14 14 14 30 12 12 12 00 41 41 37 00 50 00 28 00 40 00 00 00 37 37 32 30 14 14 14 00 41 41 37 00

28 00 50 00 30 00 00 00 14 14 14 30 37 37 32 00 24 24 24 00 50 00 58 00 30 00 00 00 37 37 32 30

0B 0B 0B 00 24 24 24 00 70 00 68 00 50 00 00 00 28 28 28 30 27 27 27 00 37 37 32 00 60 00 48 00

38 00 00 00 0C 0C 0C 30 12 12 12 00 08 08 08 00 70 00 50 00 40 00 00 00 28 28 28 30 37 37 32 00

41 41 37 00 70 00 48 00 78 00 00 00 28 28 28 30 12 12 12 00 10 10 10 00 58 00 50 00 68 00 00 00

0B 0B 0B 30 37 37 32 00 27 27 27 00 48 00 60 00 78 00 00 00 12 12 12 30 0C 0C 0C 00 10 10 10 00

04 00 00 00 58 00 68 00 20 00 10 00 3D 26 00 38 A4 7C 3C 00 4D 2F 00 00 A8 88 20 00 18 00 60 00

20 00 58 00 51 32 00 38 3D 26 00 00 4D 2F 00 00 3D 26 00 00 60 00 18 00 78 00 08 00 3D 26 00 38

24 20 00 00 23 1C 05 00 24 20 00 00 58 00 60 00 30 00 38 00 0B 0B 0B 38 0C 0C 0C 00 05 05 05 00

08 08 08 00

  
  
  
Bone 24 \[at offset 0x00005A1C\]:

  
D0 00 00 00 D0 FF F3 FF 0F 00 00 00 BE FF F4 FF 5B FF 00 00 E2 FF 32 00 43 FF 00 00 ED FF C5 FF

43 FF 00 00 ED FF D1 FF EF FE 00 00 ED FF F9 FF EF FE 00 00 DD FF D5 FF 1A FF 00 00 F5 FF B4 FF

1A FF 00 00 DF FF FC FF 0C FF 00 00 DC FF FC FF 21 FF 00 00 23 00 FC FF 21 FF 00 00 21 00 FC FF

0C FF 00 00 0B 00 B4 FF 1A FF 00 00 22 00 D5 FF 1A FF 00 00 13 00 F9 FF EF FE 00 00 13 00 D1 FF

EF FE 00 00 13 00 C5 FF 43 FF 00 00 1E 00 32 00 43 FF 00 00 3A 00 F4 FF 43 FF 00 00 29 00 F3 FF

0F 00 00 00 00 00 B6 FF 5F FF 00 00 00 00 BB FF 0F 00 00 00 00 00 2A 00 0F 00 00 00 00 00 F3 FF

2E 00 00 00 00 00 1E 00 21 FF 00 00 00 00 1E 00 0C FF 00 00 00 00 20 00 00 00 00 00 2A 00 00 00

60 00 80 00 68 00 00 00 C0 AC 58 30 8C 68 28 00 3C 34 26 00 78 00 60 00 68 00 00 00 40 24 07 30

C0 AC 58 00 3C 34 26 00 38 00 20 00 30 00 00 00 7C 5C 18 30 50 48 0A 00 64 40 08 00 18 00 38 00

30 00 00 00 44 34 11 30 7C 5C 18 00 64 40 08 00 40 00 C8 00 C0 00 00 00 30 24 0C 30 24 20 15 00

30 24 0C 00 30 00 40 00 48 00 00 00 64 40 08 30 30 24 0C 00 12 12 10 00 58 00 C0 00 C8 00 00 00

0F 0F 0D 30 38 28 12 00 24 20 15 00 58 00 68 00 50 00 00 00 0F 0F 0D 30 3C 34 26 00 34 2C 1C 00

C0 00 58 00 50 00 00 00 38 28 12 30 0F 0F 0D 00 34 2C 1C 00 40 00 C0 00 48 00 00 00 30 24 0C 30

30 24 0C 00 12 12 10 00 00 00 08 00 10 00 00 00 0A 0F 15 30 34 4C 50 00 10 1C 24 00 08 00 A0 00

18 00 00 00 34 4C 50 30 80 9C A8 00 00 0A 0C 00 40 00 20 00 28 00 00 00 05 10 16 30 0A 0F 15 00

0A 0F 15 00 30 00 48 00 18 00 00 00 1C 2C 34 30 05 0E 14 00 00 0A 0C 00 48 00 10 00 08 00 00 00

05 0E 14 30 10 1C 24 00 34 4C 50 00 C0 00 88 00 10 00 00 00 00 05 0A 30 05 0E 14 00 10 1C 24 00

28 00 70 00 C8 00 00 00 0A 0F 15 30 07 08 0F 00 10 1C 24 00 A0 00 A8 00 90 00 00 00 80 9C A8 30

30 44 50 00 30 44 50 00 10 00 88 00 B0 00 00 00 10 1C 24 30 05 0E 14 00 08 0F 10 00 88 00 50 00

90 00 00 00 05 0E 14 30 0A 0F 10 00 30 44 50 00 50 00 68 00 80 00 00 00 0A 0F 10 30 1C 2C 34 00

20 38 3C 00 78 00 58 00 70 00 00 00 07 08 0F 30 0A 0F 10 00 07 08 0F 00 90 00 98 00 88 00 00 00

30 44 50 30 30 44 50 00 05 0E 14 00 18 00 48 00 08 00 00 00 00 0A 0C 30 05 0E 14 00 34 4C 50 00

50 00 80 00 90 00 00 00 0A 0F 10 30 20 38 3C 00 30 3A 4C 00 20 00 40 00 30 00 00 00 0A 0F 15 30

05 10 16 00 1C 2C 34 00 58 00 78 00 68 00 00 00 0A 0F 10 30 07 08 0F 00 1C 2C 34 00 A0 00 80 00

18 00 00 00 80 9C A8 30 20 38 3C 00 00 0A 0C 00 A0 00 08 00 A8 00 00 00 80 9C A8 30 34 4C 50 00

34 4C 50 00 A0 00 90 00 80 00 00 00 80 9C A8 30 30 40 4C 00 20 38 3C 00 10 00 B0 00 00 00 00 00

10 1C 24 30 08 0F 10 00 0A 0F 15 00 B0 00 88 00 98 00 00 00 08 0F 10 30 05 0E 14 00 30 48 50 00

A8 00 08 00 00 00 00 00 34 4C 50 30 34 4C 50 00 0A 0F 15 00 90 00 A8 00 98 00 00 00 30 44 50 30

30 44 50 00 30 44 50 00 98 00 A8 00 B8 00 00 00 30 44 50 30 30 44 50 00 08 0F 10 00 B0 00 98 00

B8 00 00 00 08 0F 10 30 30 48 50 00 08 0F 10 00 00 00 B0 00 B8 00 00 00 0A 0F 15 30 08 0F 10 00

08 0F 10 00 A8 00 00 00 B8 00 00 00 30 44 50 30 0A 0F 15 00 08 0F 10 00 C8 00 40 00 28 00 00 00

10 1C 24 30 05 10 16 00 0A 0F 15 00 C8 00 70 00 58 00 00 00 10 1C 24 30 07 08 0F 00 0A 0F 10 00

48 00 C0 00 10 00 00 00 05 0E 14 30 00 05 0A 00 10 1C 24 00 C0 00 50 00 88 00 00 00 00 05 0A 30

0A 0F 10 00 05 0E 14 00 03 00 00 00 38 00 60 00 20 00 78 00 7C 5C 18 38 C0 AC 58 00 50 48 0A 00

40 24 07 00 18 00 80 00 38 00 60 00 44 34 11 38 8C 68 28 00 7C 5C 18 00 C0 AC 58 00 70 00 28 00

78 00 20 00 07 08 0F 38 0A 0F 15 00 07 08 0F 00 0A 0F 15 00

  
  
  
Bone 25 \[at offset 0x00005E90\]:

  
B0 00 00 00 D8 FF 0A 00 EA FF 00 00 F3 FF D5 FF EA FF 00 00 0D 00 D5 FF EA FF 00 00 28 00 0A 00

EA FF 00 00 1D 00 F9 FF 04 00 00 00 E3 FF F9 FF 04 00 00 00 D0 FF FE FF 71 FF 00 00 30 00 FE FF

71 FF 00 00 FD FF C8 FF 74 FF 00 00 00 00 31 00 7C FF 00 00 00 00 DB FF 04 00 00 00 00 00 E7 FF

5B FF 00 00 E0 FF 02 00 5B FF 00 00 00 00 1F 00 5B FF 00 00 20 00 02 00 5B FF 00 00 00 00 EB FF

19 FF 00 00 E4 FF 02 00 19 FF 00 00 00 00 1B 00 19 FF 00 00 1C 00 02 00 19 FF 00 00 00 00 17 00

04 00 00 00 03 00 CE FF 91 FF 00 00 00 00 29 00 EA FF 00 00 00 00 20 00 00 00 00 00 1E 00 00 00

28 00 20 00 50 00 00 00 10 30 40 30 14 3C 4C 00 48 64 68 00 00 00 98 00 28 00 00 00 30 3C 48 30

09 14 1B 00 10 30 40 00 08 00 00 00 28 00 00 00 30 50 5C 30 30 3C 48 00 10 30 40 00 08 00 28 00

50 00 00 00 30 50 5C 30 10 30 40 00 48 64 68 00 98 00 20 00 28 00 00 00 09 14 1B 30 14 3C 4C 00

10 30 40 00 98 00 18 00 20 00 00 00 09 14 1B 30 14 2C 38 00 14 3C 4C 00 10 00 50 00 20 00 00 00

44 5C 64 30 48 64 68 00 14 3C 4C 00 18 00 10 00 20 00 00 00 14 2C 38 30 44 5C 64 00 14 3C 4C 00

10 00 08 00 50 00 00 00 44 5C 64 30 30 50 5C 00 48 64 68 00 00 00 08 00 30 00 00 00 30 3C 48 30

30 50 5C 00 30 4C 4D 00 A8 00 00 00 48 00 00 00 05 0C 13 30 30 3C 48 00 07 12 14 00 A8 00 48 00

18 00 00 00 05 0C 13 30 07 12 14 00 14 2C 38 00 08 00 A0 00 30 00 00 00 30 50 5C 30 80 94 A0 00

30 4C 4D 00 10 00 A0 00 08 00 00 00 44 5C 64 30 80 94 A0 00 30 50 5C 00 10 00 18 00 38 00 00 00

44 5C 64 30 14 2C 38 00 30 3C 48 00 A0 00 10 00 38 00 00 00 80 94 A0 30 44 5C 64 00 30 3C 48 00

30 00 68 00 48 00 00 00 30 4C 4D 30 24 38 40 00 07 12 14 00 68 00 30 00 60 00 00 00 24 38 40 30

30 4C 4D 00 07 12 14 00 40 00 60 00 30 00 00 00 24 38 40 30 07 12 14 00 30 4C 4D 00 A0 00 40 00

30 00 00 00 80 94 A0 30 24 38 40 00 30 4C 4D 00 48 00 70 00 38 00 00 00 07 12 14 30 07 12 14 00

30 3C 48 00 70 00 48 00 68 00 00 00 07 12 14 30 07 12 14 00 24 38 40 00 40 00 A0 00 38 00 00 00

24 38 40 30 80 94 A0 00 30 3C 48 00 38 00 58 00 40 00 00 00 30 3C 48 30 20 30 38 00 24 38 40 00

58 00 38 00 70 00 00 00 20 30 38 30 30 3C 48 00 07 12 14 00 60 00 40 00 58 00 00 00 07 12 14 30

24 38 40 00 20 30 38 00 18 00 98 00 A8 00 00 00 14 2C 38 30 09 14 1B 00 05 0C 13 00 98 00 00 00

A8 00 00 00 09 14 1B 30 30 3C 48 00 05 0C 13 00 18 00 48 00 38 00 00 00 14 2C 38 30 07 12 14 00

30 3C 48 00 48 00 00 00 30 00 00 00 07 12 14 30 30 3C 48 00 30 4C 4D 00 05 00 00 00 88 00 80 00

90 00 78 00 0C 0C 0C 38 1E 1E 19 00 28 28 23 00 32 32 2D 00 70 00 68 00 90 00 88 00 0B 0B 0B 38

0F 0F 0F 00 28 28 23 00 0C 0C 0C 00 68 00 60 00 88 00 80 00 0F 0F 0F 38 0B 0B 0B 00 0C 0C 0C 00

1E 1E 19 00 60 00 58 00 80 00 78 00 0B 0B 0B 38 1E 1E 19 00 1E 1E 19 00 32 32 2D 00 58 00 70 00

78 00 90 00 1E 1E 19 38 0B 0B 0B 00 32 32 2D 00 28 28 23 00

  
  
  
Bone 26 \[at offset 0x00006224\]:

  
88 00 00 00 01 00 E6 FF 00 00 00 00 21 00 05 00 0B 00 00 00 E2 FF 05 00 0B 00 00 00 00 00 D1 FF

D1 FF 00 00 DB FF ED FF BD FF 00 00 19 00 F0 FF B8 FF 00 00 D4 FF 00 00 AA FF 00 00 1F 00 00 00

AB FF 00 00 D4 FF 36 00 C8 FF 00 00 FE FF 4C 00 D5 FF 00 00 23 00 36 00 C8 FF 00 00 17 00 F7 FF

E7 FF 00 00 27 00 23 00 EA FF 00 00 FE FF 3A 00 F7 FF 00 00 00 00 1A 00 13 00 00 00 D1 FF 23 00

EA FF 00 00 EB FF F4 FF EC FF 00 00 00 00 20 00 00 00 00 00 1E 00 00 00 30 00 40 00 20 00 00 00

0C 0C 0C 30 10 10 10 00 0E 0E 0E 00 20 00 40 00 78 00 00 00 0E 0E 0E 30 10 10 10 00 10 10 10 00

80 00 20 00 78 00 00 00 13 13 13 30 0E 0E 0E 00 10 10 10 00 18 00 20 00 80 00 00 00 37 37 32 30

0E 0E 0E 00 13 13 13 00 18 00 80 00 00 00 00 00 37 37 32 30 13 13 13 00 32 32 2D 00 80 00 10 00

00 00 00 00 13 13 13 30 16 16 16 00 32 32 2D 00 80 00 78 00 10 00 00 00 13 13 13 30 10 10 10 00

16 16 16 00 78 00 70 00 10 00 00 00 10 10 10 30 08 09 09 00 16 16 16 00 70 00 78 00 68 00 00 00

08 09 09 30 10 10 10 00 11 11 11 00 40 00 68 00 78 00 00 00 10 10 10 30 11 11 11 00 10 10 10 00

68 00 40 00 48 00 00 00 11 11 11 30 10 10 10 00 0D 0D 0D 00 60 00 70 00 68 00 00 00 16 16 16 30

08 09 09 00 11 11 11 00 60 00 08 00 70 00 00 00 16 16 16 30 2D 2D 26 00 08 09 09 00 10 00 70 00

08 00 00 00 16 16 16 30 08 09 09 00 2D 2D 26 00 50 00 68 00 48 00 00 00 05 05 05 30 11 11 11 00

0D 0D 0D 00 68 00 50 00 60 00 00 00 11 11 11 30 05 05 05 00 16 16 16 00 50 00 28 00 60 00 00 00

05 05 05 30 1D 1D 1D 00 16 16 16 00 58 00 60 00 28 00 00 00 2D 2D 26 30 16 16 16 00 1D 1D 1D 00

60 00 58 00 08 00 00 00 16 16 16 30 2D 2D 26 00 2D 2D 26 00 58 00 00 00 08 00 00 00 2D 2D 26 30

32 32 2D 00 2D 2D 26 00 50 00 38 00 28 00 00 00 05 05 05 30 1D 1D 1D 00 1D 1D 1D 00 58 00 18 00

00 00 00 00 2D 2D 26 30 37 37 32 00 32 32 2D 00 28 00 18 00 58 00 00 00 1D 1D 1D 30 37 37 32 00

2D 2D 26 00 50 00 40 00 38 00 00 00 05 05 05 30 09 09 09 00 05 05 05 00 38 00 40 00 30 00 00 00

05 05 05 30 09 09 09 00 0A 0A 0A 00 50 00 48 00 40 00 00 00 05 05 05 30 05 05 05 00 09 09 09 00

28 00 30 00 20 00 00 00 1D 1D 1D 30 0C 0C 0C 00 0E 0E 0E 00 28 00 20 00 18 00 00 00 1D 1D 1D 30

0E 0E 0E 00 37 37 32 00 10 00 08 00 00 00 00 00 16 16 16 30 2D 2D 26 00 32 32 2D 00 30 00 28 00

38 00 00 00 0C 0C 0C 30 1D 1D 1D 00 1D 1D 1D 00 00 00 00 00

  
  
  
Bone 27 \[at offset 0x00006518\]:

  
80 00 00 00 00 00 C6 FF EC FF 00 00 19 00 EC FF FA FF 00 00 DB FF E5 FF FA FF 00 00 1F 00 FF FF

00 00 00 00 D4 FF FF FF 00 00 00 00 FE FF 00 00 85 FF 00 00 CF FF FF FF A2 FF 00 00 2D 00 FF FF

A2 FF 00 00 FF FF CF FF 8E FF 00 00 24 00 DD FF A0 FF 00 00 D9 FF DB FF A0 FF 00 00 D3 FF FF FF

F1 FF 00 00 21 00 FF FF F1 FF 00 00 DB FF E4 FF EA FF 00 00 00 00 C8 FF DA FF 00 00 1A 00 E9 FF

EA FF 00 00 00 00 20 00 00 00 00 00 14 00 00 00 20 00 08 00 10 00 00 00 20 28 00 30 9C 7C 40 00

30 28 14 00 10 00 08 00 00 00 00 00 30 28 14 30 9C 7C 40 00 BC 88 38 00 78 00 70 00 00 00 00 00

9C 7C 40 30 9C 7C 40 00 BC 88 38 00 70 00 68 00 00 00 00 00 9C 7C 40 30 18 18 14 00 BC 88 38 00

78 00 00 00 08 00 00 00 9C 7C 40 30 BC 88 38 00 9C 7C 40 00 00 00 68 00 10 00 00 00 BC 88 38 30

18 18 14 00 30 28 14 00 08 00 20 00 18 00 00 00 9C 7C 40 30 20 28 00 00 38 34 00 00 38 00 30 00

28 00 00 00 05 05 05 30 05 05 05 00 14 14 14 00 48 00 40 00 70 00 00 00 2D 2D 28 30 46 46 41 00

2D 2D 28 00 38 00 28 00 48 00 00 00 05 05 05 30 1E 1E 1E 00 2D 2D 28 00 48 00 28 00 40 00 00 00

2D 2D 28 30 1E 1E 1E 00 46 46 41 00 28 00 50 00 40 00 00 00 1E 1E 1E 30 14 14 14 00 46 46 41 00

50 00 28 00 30 00 00 00 14 14 14 30 1E 1E 1E 00 08 08 08 00 58 00 50 00 30 00 00 00 0B 0B 0B 30

14 14 14 00 08 08 08 00 68 00 70 00 50 00 00 00 0F 0F 0F 30 2D 2D 28 00 14 14 14 00 48 00 60 00

38 00 00 00 2D 2D 28 30 0B 0B 0B 00 05 05 05 00 50 00 70 00 40 00 00 00 14 14 14 30 2D 2D 28 00

46 46 41 00 48 00 70 00 78 00 00 00 2D 2D 28 30 2D 2D 28 00 38 34 2D 00 50 00 58 00 68 00 00 00

14 14 14 30 0B 0B 0B 00 0F 0F 0F 00 60 00 48 00 78 00 00 00 0B 0B 0B 30 2D 2D 28 00 38 34 2D 00

04 00 00 00 18 00 60 00 08 00 78 00 38 34 00 38 14 10 04 00 9C 7C 40 00 9C 7C 40 00 60 00 18 00

58 00 20 00 14 10 04 38 3C 25 00 00 14 10 04 00 20 28 00 00 68 00 58 00 10 00 20 00 18 18 14 38

14 10 04 00 30 28 14 00 20 28 00 00 60 00 58 00 38 00 30 00 0B 0B 0B 38 0B 0B 0B 00 05 05 05 00

05 05 05 00

  
  
  

- \*\* \*\*\* Bone Data Section runs until Model Settings Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Model Settings Section** \[at offset 0x0000679C\]:

  
00 00 80 00 5E 01 40 06 40 06 00 00 96 00 A8 FD 18 FC 02 00 00 00 00 00 11 08 00 00 03 1B 16 00

00 00 00 00 88 01 00 00 8C 01 00 00 90 01 00 00 94 01 00 00 98 01 00 00 9C 01 00 00 A0 01 00 00

A4 01 00 00 72 01 32 01 72 01 00 00 02 0C B9 F9 79 05 00 00 60 FF 00 00 45 01 79 FE 6F 0D 00 00

20 FF 80 00 C8 00 00 00 E8 00 00 00 EC 00 00 00 F0 00 00 00 F4 00 00 00 08 01 00 00 1C 01 00 00

20 01 00 00 24 01 00 00 28 01 00 00 2C 01 00 00 30 01 00 00 38 01 00 00 44 01 00 00 50 01 00 00

58 01 00 00 60 01 00 00 68 01 00 00 70 01 00 00 78 01 00 00 80 01 00 00 34 01 00 00 40 01 00 00

4C 01 00 00 54 01 00 00 5C 01 00 00 64 01 00 00 6C 01 00 00 74 01 00 00 7C 01 00 00 84 01 00 00

3C 01 00 00 48 01 00 00 3C 01 00 00 48 01 00 00 A9 C9 00 C1 01 F6 E5 EE E5 EE 00 00 FC EA 02 AD

07 B8 01 01 0A D8 01 10 00 F7 08 03 04 05 E5 EE FC F0 06 D1 20 03 00 00 04 F0 07 F7 04 08 FA F0

09 E5 EE 54 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00

  
  

- \*\* \*\*\* Model Settings Section runs until Animation Data Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
**Animation Data Section** \[at offset 0x00006944\]:

  
1st Animation Data \[at offset 0x00006944\]

  
0F 00 98 03 00 00 00 FE 84 FF F7 00 00 00 00 0C 48 00 0F 63 0F 90 35 F3 CF 40 F6 71 AC 00 EF 19

18 FE 02 DF A2 76 D4 4F C5 44 8D 95 3C 1C 4D E2 AF F2 15 32 53 C7 EC 64 3E 05 4C 3A 72 EB CD AC

C8 39 66 7C 57 80 C3 1B 2D 31 E0 22 06 D8 AE A5 3D A8 5C ED 9D BE 14 10 98 03 EC BF FE FB 64 7B

AD F3 F9 76 6A 3D 60 00 00 0C F3 22 AE A2 D3 00 00 00 00 11 36 48 46 F5 83 21 83 B3 8B 00 00 00

E2 BF 97 04 6D 50 00 00 00 00 05 7A 0B 57 B2 AF CB 41 8F 73 32 FD A1 99 5D BC 0E E3 92 B9 A2 BC

29 F1 28 F1 27 19 FE 0E FE 0E F9 97 2E 86 1D EC 4D 5E C3 2A 71 09 4A EE E7 18 B1 5D 9C C2 48 C0

9C F5 A6 E6 FD A8 1F C0 DE 03 88 EE 2E DD 96 06 05 FB D7 2C 0C FA ED 5B D9 70 B7 71 EF 87 84 3F

84 38 BD C7 F1 F7 AE 56 18 57 F0 B4 9B 8C C8 8A 92 BD 4F 7F 51 87 95 A4 DF 16 11 62 29 E0 0D BD

DC 00 FA 06 EE 1E 08 FF F7 4B 88 95 72 B8 17 A7 62 CE FB 51 56 0D 62 5B BD D8 95 CB AB 81 16 6A

C0 C6 C8 B9 0B B2 A3 2F 17 B9 DE 9A 2D DE BB 74 5B 94 E4 B5 C0 1B 6B 98 21 F4 05 D0 53 E0 B7 FF

4B 6F 3E 59 F5 C5 9C F9 8A E2 8A 73 71 AB B5 31 47 FB 0F FB 10 B3 D6 F5 B6 6E 58 0B 13 B1 6E E5

51 19 B2 A7 23 4F D8 F7 E6 9F 75 C1 ED CC 39 57 12 C2 D0 7C 00 7C 00 6D B3 B0 E4 3E 80 BC 0A 7C

11 FF EE 70 2E B3 6F B0 2E D6 26 94 AA B5 14 04 FF BD BF BD C5 9F FB 3F FB 2B 77 EC 89 4A 28 A6

AA 8B 92 A3 2F 4D DC EC 8D 1E 46 AB 7A 60 4A 71 46 0E E0 DF 5C C1 0F E0 0F A2 5A 7D D5 B4 AE 5F

5B 89 89 04 4E 20 67 FF 7F 7F 7F 8B 3F F5 5F F5 56 56 40 25 5C 2B 4A AC 0C CC E2 DD 56 EF 94 A0

A2 E9 54 E8 90 02 FE 06 23 73 A6 B5 62 8B D7 E8 B5 62 04 91 3B 57 62 B9 0C 8F F5 5F F5 51 47 FD

17 FD 15 8B 56 44 A7 2A EA B1 7C A5 14 DE D0 60 17 6C 5C B6 56 94 95 E1 18 76 2F 80 37 F0 A1 5F

FD CF 82 3D 9C 3A 27 55 16 70 82 C5 15 D7 87 95 17 68 1B AF F9 BF F9 B1 2F F9 DF F9 DA 70 EC 8A

2B 95 57 30 6F C3 02 27 89 BB E2 F5 46 F3 41 B6 D2 97 22 8A 19 FA A3 55 85 9B 00 1B F0 60 AF FE

A3 C1 62 9C 3A 67 55 36 30 82 CC AB AB 1F 7B 2C FA 06 F3 B2 EC C4 7F D9 7F D9 51 89 60 4A FD 17

B3 B1 26 8C 28 AF 41 BA E4 35 C6 E7 4D DF 6A 8C E8 A6 88 CE DA FC 00 7C 00 6B B0 B3 00 1B E8 48

7F DF 78 21 51 82 8A AC 53 80 16 68 AE AD 16 E6 9C FA 45 DC EC F1 1D F7 7B 2C 0A 04 AF 51 77 2F

1E C2 56 D3 C4 CC E1 74 66 46 8F 69 A4 2E A8 2F 6C CD 4E 05 C0 02 FC 0E 1D C7 0F 2B 31 15 D2 B5

31 6E 8B F7 F4 DB 4B 59 D6 05 9D 06 38 95 BB 74 5A 81 17 AC 5D C9 D1 62 50 B3 11 6E AD 65 A3 37

17 7B 8E 5F 89 56 AF 6A 69 2C DE 00 0F A0 81 95 8C A2 B9 D7 62 29 98 B7 45 57 F5 5B 0C 0C DB 03

43 C9 F2 62 5C 97 25 2A 2B 11 72 CD DD F6 97 45 44 A4 8A 28 D1 DF 2A B5 73 0C 84 AE CA 5B 93 1A

9A 80 03 E8 18 13 8A A5 14 D5 29 8B 52 AE BD 26 DF 02 E5 23 49 E0 CF E0 CC 25 E0 A3 E0 A4 54 22

F5 8B D9 5A 0D 0D 12 11 63 0E E1 39 45 90 5E 95 19 05 BA 27 20 00 00 00 0B D1 3B 56 17 A0 24 88

B1 7E C4 06 87 C2 A3 C2 9C 3C 19 BC 19 AA AE F8 88 A2 27 4E 0C A4 09 40 24 09 95 00 00 00 00 00

  
  
2nd Animation Data \[at offset 0x00006CE4\]

  
09 00 24 02 04 00 00 FE 7E FF FD 00 00 00 C5 00 F6 0F 09 F5 F1 FF 2B 01 F7 1A E0 E0 27 D5 FD 44

D9 3F C1 E3 FE 16 25 C8 C6 3D 48 2E 2F CE CD 3A 5E 4E 0B 21 D3 E0 20 D9 EA 3D 86 ED DA 17 0B 04

CC FF B6 7C DF FA 68 3C 00 00 CF 23 EA D4 00 00 01 36 84 F5 32 84 37 00 00 E4 FA 04 D5 00 00 00

26 03 03 0F 81 E5 30 E3 3B 83 D3 F0 80 47 DA 7A 54 A7 90 37 9D FF 7C 2F F6 BD A5 DC 6E 3C 60 77

DA CC 1D 1E F8 0A 71 73 2B 28 9D 35 82 DD 15 E0 00 7F E3 7F EE 70 10 F1 85 EE 7F 1B DA 77 1B 9C

B8 DF F5 FD E5 A0 31 F3 E8 C1 DC E2 8D E6 CF 7C 33 3B 6E E7 BD DC F7 43 6B CC 77 76 71 6A B9 9F

C2 9A 3D EE E7 3B 68 6A 7B DE 0A 80 DE ED AF CF 68 00 90 13 00 90 03 1F 07 1E DD BC 3D 26 2D 91

A7 DE 70 56 70 EE 59 C7 CD 15 58 B0 33 30 B0 6D CF 50 38 1F 8A F8 8D EF A2 74 5B 5D BE 88 45 8B

FB 33 1E 99 81 8B 66 2F 18 1B DC 10 3A 47 00 5A 14 5F B1 25 EC 4A F3 E7 17 45 56 F3 2E DA 9D 56

31 86 8A F6 70 C6 C3 C1 B1 4D E1 DD 6D 31 F0 96 04 E2 89 6D 35 B8 45 FA 02 88 9E 5E 4E 1E 8B E0

3E 03 3A BC 0B C0 F1 14 01 6C 51 5D 34 2E E0 5D CB 9C 5E 13 C1 CA BD 81 7E F4 F4 03 1F 71 B4 18

3C 1F 07 4D 17 85 78 37 33 95 09 C5 16 B7 BA 2C 12 FC A0 51 13 AF AF E6 30 3E 03 E0 33 EE E1 5E

1D 42 82 00 C4 A2 82 BC 45 F1 9B 67 3A E6 7D BA 29 81 77 B0 EA 85 79 59 58 6B 42 79 B8 56 AB B7

63 13 3C 51 25 A2 94 A0 0A 67 60 8A AC C8 75 09 08 03 16 89 25 5E 14 EE 0B 9A 0D FD EC 9C 7A 29

81 BF CE DF 0B F7 6E 62 4A C8 9E 5E 2D 98 B7 6F 0A F0 A6 51 64 A0 80 45 13 B0 45 56 24 40 21 81

BF B3 23 2B E5 7D B2 E6 6F 7B B9 BD AC DC C6 E4 51 BF D1 E0 7A A7 D6 E7 D1 94 38 3F 92 F9 E1 8D

C9 72 96 DB 11 AF F8 BF 63 BD F4 1E 8D A8 C4 EE 2C 51 B9 B3 C9 EF 75 C7 77 AF EF 69 2A A3 4F A7

E6 7A 7B 86 2F 0B DE 61 1E 00 00 00

  
  
3rd Animation Data \[at offset 0x00006F10\]

  
0C 00 8B 02 04 FF D5 FD FB FF 57 00 00 00 CD 10 E7 0F 03 F3 F0 F3 1C 00 F2 19 E0 E0 27 D4 FB 46

DD 3A C8 E5 00 15 25 C8 C6 3A E1 C7 2F CE CD 33 5A 4A 0C 1B D3 E0 20 D9 E6 40 87 E9 E2 13 0B 06

C1 F9 B8 75 CD DD 6D 24 00 00 FB FB 0E D5 00 00 07 38 8B E1 33 88 23 00 00 E9 00 FD CA 00 00 7D

6A FF A5 88 A2 72 9A 9A 22 53 81 3B 98 16 AE E1 AD D4 2E DE BA 2F 12 98 5F AA D0 CF 90 A3 49 B5

D1 E8 7E 03 E0 0C F0 4F 6D BC D2 6F 0B B4 CE C0 18 71 FF 35 0D CE 9B 3E 89 D8 B2 CF A2 81 46 16

75 FB 59 D1 01 5E 66 60 8B 36 AE CA F0 9C E8 9A 59 B4 C5 A8 AE DC EB C9 F8 0F 80 DB 4A AA 8B D1

4C 7C AF AE DA 30 EA A3 33 E0 3E 00 89 93 FE 18 25 9F 83 78 B1 61 7A 28 02 C5 56 E5 20 AF 3F 34

2D DB BF 17 C5 F9 D9 8B 35 59 CC 51 11 BE C1 B9 59 83 83 7B 27 E0 3E 02 71 27 B6 7C 9E 98 C1 BB

46 8F E0 3E 01 6C 5B FE A6 16 EF 4E 88 A2 49 D1 21 3A A9 25 4D 88 12 01 28 A2 04 8B 38 F9 B7 A4

9A 59 9C 7F 69 92 5B 8A 2D 14 1C 4E 8F 33 4B F0 1F 01 B9 9E 1E 68 00 CF FF A2 11 8D 95 66 25 17

96 53 13 EE 38 9B 15 5B D1 CA C8 B1 C6 72 22 59 1B EB 0A 45 D9 51 63 0A FD 8B F8 D5 50 A7 BB E1

B5 26 04 4B 17 E0 3E 02 C5 11 9D 5D 5D 87 C0 7C 05 8B 59 B8 23 B8 67 FE 0C 4F 57 B4 9D E6 0D B9

C5 D9 08 E1 FB 8B D6 F3 23 02 06 5E AF 5A 2B DE 6E A2 EC 0C D8 B2 CE B1 93 5E BA A8 B7 85 91 8F

86 59 AD 96 58 8B B3 CC C2 D1 91 81 7E 81 5D 85 90 57 89 99 7A 16 29 5E 8A 44 49 A3 DF F0 7B D9

F7 02 AA 29 17 F2 F2 6F 2B 16 F5 FD FE 3E 15 52 D2 E3 51 16 27 15 5E 2A B5 16 09 C5 59 4A 33 0A

2B A0 3B 89 87 85 BB B0 CE 2D 5F A7 38 5F EF B8 1B 35 60 55 63 38 4A 73 17 EE 67 59 8C F1 81 DD

F0 37 36 F6 D7 70 49 67 E9 33 F3 4C BB 35 5E 08 B1 29 E0 93 AA 89 83 24 45 82 BC BC 5A E8 BB 45

36 EF D8 BA 29 4A DD 8B 78 13 BC 28 9D 62 AA AA 2E 0C EC BD 16 75 BA 2C E0 65 D8 45 17 69 A4 C8

A2 FC 8A 92 B7 6A 2D 02 80 00 14 24 09 13 9C 4A 40 9D 10 42 05 AB D7 85 AA 6C 49 21 2B F6 A2 25

38 AC 2C C4 89 CA 24 0A 24 91 29 00 00 28 50 12 22 69 4A 04 4E 44 24 16 B3 B3 46 06 06 1C A5 21

2A AC 21 38 A8 4A C4 50 45 13 90 28 94 50 50 00

  
  
4th Animation Data \[at offset 0x000071A0\]

  
02 00 72 00 04 FF B9 FE 2D FB 87 00 00 00 C4 28 CE FC 00 E0 08 01 25 E7 F4 0D E0 E0 27 CB D7 6A

FE 28 FD E9 16 DA 25 C8 C6 33 F3 DA 2F CE CD 2D 3B 2A 06 14 B7 E0 20 D9 D1 1C B8 EB FC 02 EC 07

F1 FD B6 7F CF DA 70 2D 00 00 D9 11 F0 C9 00 00 03 36 81 E4 2C 84 29 00 00 E3 FD FE D5 00 00 00

01 7E 00 00 11 20 04 B3 73 45 18 38 20 09 D5 4C 4E 40 48 00 09 10 02 00

  
  
5th Animation Data \[at offset 0x00007218\]

  
01 00 5A 00 04 FF B9 FE 30 FB 83 00 00 00 C4 28 CE FC 00 E0 08 01 25 E7 F4 0D E0 E0 27 CB D5 6C

FE 28 FD E9 16 DA 25 C8 C6 35 DD C3 2F CE CD 30 4E 3D 06 14 B7 E0 20 D9 D1 1C B7 E8 F3 07 EA 03

F3 FD B6 7F CF DA 70 2E 00 00 D8 12 EF C9 00 00 03 36 81 E4 2C 84 2B 00 00 E2 FD FF D5 00 00 00

  
  
6th Animation Data \[at offset 0x00007278\]

  
15 00 AA 03 04 FF B9 FE 21 FB A7 00 00 00 C4 28 CE F8 FE DC 09 03 28 E3 F4 0A E0 E0 27 CE DD 65

FE 29 FC EE 17 DD 25 C8 C6 34 D5 BA 2F CE CD 30 57 47 04 12 B2 E0 20 D9 CE 22 B1 F0 ED 08 E5 10

EE FD B6 7F D0 D4 76 2C 00 00 D7 0E F3 CD 00 00 03 36 81 E3 2D 84 22 00 00 EA FF FD D5 00 00 00

01 73 02 52 A1 13 92 81 3B F4 A2 53 88 0B D7 82 D5 B2 81 2A AC 56 95 8A E4 22 89 8A 25 13 00 A4

9A 40 01 F0 9C 0A A2 FC A9 B3 7E 57 85 9C 3C F8 A2 76 6C 52 25 A6 D3 88 CA C8 89 DE 15 E2 65 E0

2A CD C0 A8 51 7A D4 15 55 45 A0 41 9C 5B 94 00 00 27 30 24 A1 13 A1 40 9D 74 22 53 9C 08 DD 6E

44 B1 B4 09 50 25 7E CD 6A 2C 57 40 8A 26 25 42 60 16 09 C0 00 01 8D 01 5C 54 95 35 CA A1 4D 9A

94 4E C5 34 09 69 B4 E2 32 B2 22 75 09 E1 E7 59 57 72 DD F1 2A AC 41 3A E8 B0 08 92 E9 66 40 00

0E 36 22 D5 E9 A5 2A 65 38 A0 4A 50 A2 54 56 11 BA DC 89 63 68 26 09 E1 67 53 4C 20 10 B0 4A 15

82 48 A0 80 00 3E 39 89 57 4C 84 44 90 20 42 24 12 D3 69 C4 65 64 48 12 BD 66 20 90 45 33 99 12

89 00 50 4C 00 01 44 E2 30 B3 AB 84 AC 4A B9 D0 25 44 4A 95 17 E4 23 75 B9 12 C6 D0 57 10 27 A3

DF 53 62 68 12 A2 AA 6D 12 8A 2F 84 48 91 20 00 3E B9 85 76 24 26 94 A0 21 10 50 12 D3 69 C4 65

64 48 12 BB 6A 22 40 4E 9A E6 25 14 00 50 4C 00 00 C3 41 81 72 64 A9 94 E7 40 4A 25 42 55 84 6E

B7 22 58 DA 09 82 31 B2 E8 A2 00 A2 BB 16 04 E5 58 25 24 14 00 01 EA 00 BC 30 79 CE 8F 4F 6A 2E

6F AB D3 61 DD 15 77 DC 06 66 76 66 55 8C 21 7B D3 3D 38 67 F5 7D 3E 97 03 04 59 DE E8 76 DA CC

DB 3D EE B2 96 25 58 99 95 11 62 BC 22 B6 66 FA A8 DB 95 C2 A0 05 90 40 2C 56 25 40 00 00 B5 5D

62 CD 16 10 00 09 13 B1 55 C2 CC E8 10 4A 96 30 24 00 B6 88 05 35 40 92 20 00 02 DF 7D DE 8C 0C

7D 04 20 4A 40 25 24 ED 5E B8 58 89 08 92 54 31 40 00 5B C4 42 C5 70 28 40 00 02 FF 49 D1 8A 38

7E 1E 00 40 12 27 81 9F 70 B0 90 82 54 B1 81 20 09 D8 40 4A 9A C4 A8 00 04 02 F5 EB 82 AD 2E 98

00 04 88 C5 CB B8 59 89 08 25 4B 14 82 40 0B E0 80 53 5C 41 29 40 00 02 84 82 AB F1 10 12 01 29

23 43 91 70 B0 90 89 25 4A AF 80 F8 01 21 C0 BA 01 78 06 35 38 88 BB A0 AF 04 0A F0 33 2F E7 5A

16 F4 9A 51 2D F6 FA DE 0E 90 01 45 8E F0 58 E9 B9 9B C5 EB 35 5E 06 F7 A9 E3 46 E5 21 00 8C 2C

80 92 8B B9 B8 59 CA C6 68 30 B7 9A 1C EA EF D8 B9 AA 17 B9 5E 5C 55 BC DD DC AB 3C 53 39 62 63

DF A5 B4 AA 77 B5 3B AC 7C 03 59 73 02 D1 62 76 B0 EC 5E BF F0 1F 01 67 2F 0B 20 4B FF D6 40 3E

83 E9 7D 71 54 A7 34 AB 90 CF C0 BD 4D 76 AD 63 E6 0B 98 38 82 BC FC F5 60 36 5C 07 61 C5 CE AB

D2 CF B5 6F 7D C6 FC 07 C0 77 D8 F9 22 D4 B0 5A 9D C7 5C 6A B1 33 B4 00 C9 C4 01 10 46 56 2D 99

60 DC BD 7E DD 76 C5 7C 47 75 9F 81 93 77 3F 08 5B B5 48 B5 62 C2 8C 31 8B 4E 7D 1F 5F E9 F1 6E

D5 11 17 B5 B7 AD 17 2D C0 9C 4B 49 87 77 56 5C AA 90 C3 00 61 1F 0D EE 8E D5 38 59 D5 5F C1 8B

43 03 57 B5 BD 8F BC AF 2F 14 61 F3 9C D8 C0 D4 6A 62 C6 20 C4 8B BA AD E5 BA ED 5A A0 AB 5D 9D

1F 01 F0 17 70 2A 82 66 8B 02 F6 B0 B8 A4 00 00

  
  
7th Animation Data \[at offset 0x00007628\]

  
0C 00 3E 02 04 00 00 FE 9A FF EA 00 00 00 C5 00 F6 03 00 F1 FF 00 1B F4 EF 1C E0 E0 27 D5 FA 47

D8 52 AC EC FD 30 25 C8 C6 3D 48 2E 2F CE CD 3A 5E 4E 03 17 C9 E0 20 D9 DA 2D A0 ED DA 17 0B 04

CC FF B6 7C E3 FE 66 3F 80 80 CF 23 EA D0 00 00 01 36 84 F9 31 83 40 00 00 E0 F9 05 D5 00 00 00

0D 00 02 6D 3C A3 7B 85 7B 4A 2D 5F B5 9D 5D 88 AB 7C 00 19 75 E9 06 17 D2 F3 FB 6F 86 F8 7D D6

E2 05 15 AF 92 00 A1 15 FC 07 C0 00 00 C8 4A 01 65 66 E5 2B 21 4D 79 D8 79 C9 D9 17 36 7B 30 EE

FB B9 CE C8 D2 EF F4 B9 3E BB F4 BA 6D 66 AC 57 76 8B 24 B3 71 20 15 97 BE 03 E0 2D C0 04 B6 92

89 8A 2C CA 53 A2 8B 02 B4 60 FB DF C2 58 A2 05 9B 16 03 43 A1 AD 60 4E 88 D0 6F 34 F8 6D 49 2A

EF A7 F0 1F 01 4D 11 50 45 E4 B3 0C 0A 6B 00 0F 41 40 09 40 00 C5 CB 02 CF 1F C7 06 8B 44 05 F8

9C ED DC 01 5A 05 DB 60 41 7C A4 00 0F 20 60 44 04 44 82 88 A3 0F 34 09 EC 76 42 33 73 20 16 62

8A 73 F0 80 88 94 0A AC 48 10 4C A1 00 31 FC 0C 37 BA 39 54 92 52 AA 04 D1 6E DD D0 27 76 E8 67

E7 CA FC 86 2D 9B 73 DF E8 33 EB AE 81 39 48 55 4C C9 93 4A B2 88 00 D7 E0 31 2C BC 55 52 91 2A

82 25 16 EC 5F 90 28 B7 6C 30 70 55 06 0E 0E 1D 1B ED 06 7D 73 91 28 48 55 4C C8 22 15 94 40 3F

01 88 85 AB D2 A2 29 82 88 09 D1 4C A2 54 DD 14 6B F5 C2 58 78 94 50 17 EE DD CC EE F8 58 BA 82

2A 48 AE 25 41 20 54 52 07 E0 41 01 16 EE D1 42 98 4A 88 09 D3 62 51 45 17 84 FB 4E D4 51 9D 9D

2A 02 ED EB F8 1D 5F 2D 17 60 45 F9 48 AE 6A 01 09 5F 2C 20 3F 01 88 86 0E 7C A8 53 11 2A 02 53

A2 C4 A2 8A 2F 09 E7 E7 89 6D F6 F2 A2 42 E5 55 E8 2E E3 4E EA 08 AA 52 2B 9D 14 12 22 15 14 81

55 5F FA 58 31 B5 39 56 CD C6 26 4D A8 A8 58 F4 4F B9 BB D6 F2 37 EB 90 DB FC CF C8 8B BC 3F 0F

69 48 A6 25 65 40 BD 89 97 A4 CB C4 DD FC 07 C0 73 F5 CA D9 6B 13 17 63 F6 1E AD 78 DD D1 4D DF

80 F8 00 00

  
  
8th Animation Data \[at offset 0x0000786C\]

  
04 00 14 01 04 FF F1 FD F2 00 05 00 00 00 D1 0B F5 0B FC 15 F2 09 EF 0D E4 37 E0 E0 27 DB 3B 04

E0 D2 28 EF FA 11 25 C8 C6 1F BD 99 2F CE CD 34 66 56 F9 0A ED E0 20 D9 00 BE F9 E3 23 E5 FC EA

FC FC C1 70 FD C4 7F 3D 80 80 F4 09 FC CB 00 00 04 41 90 CD DC DF 13 00 00 10 02 01 D5 00 00 09

32 00 17 77 DA 2A E5 2C 5B 92 9D 14 09 CE 85 8B F2 90 63 F0 3C 58 A3 B0 EC 27 20 A2 25 42 81 6A

76 B6 D4 51 9F F0 1F 01 5E 75 35 7C 07 C0 5E 9D EB 5E 95 F5 DA 5F 80 F8 0D F5 70 03 FF F7 00 02

D5 8C 99 60 60 E7 D3 3B 38 38 02 C5 9B F2 A6 A0 33 FB BE D0 4B D4 FD 4A BB 18 22 82 88 A2 9A 27

7F 3E F6 E7 D8 FE 4B 64 69 64 C6 F8 0F 80 B3 9F 6B 8A C3 CA D1 95 CD BC F8 0F 80 00 80 32 00 09

6A 77 37 E7 44 AB 8A E2 C8 59 AE FD 99 D7 01 8D ED 7E E4 32 BE 83 E7 EF D7 21 29 4A 99 51 5C E8

B9 45 8C 5F 96 F6 BC 7F 80 F8 0A E1 98 60 51 56 45 76 DF 01 F0 19 76 63 14 00 00 00

  
  
9th Animation Data \[at offset 0x00007988\]

  
0C 00 4C 02 04 FF E8 FD F2 FE 8F 00 00 00 D1 09 F7 0B FA 1D F2 09 EB 11 E3 3D E0 E0 27 DE 37 07

DB D2 2A ED FB 11 25 C8 C6 22 C2 A0 2F CE CD 2B 53 43 F7 06 F4 E0 20 D9 00 BE F9 E3 23 E5 FC EA

FC FD C1 70 FD C4 7F 3D 80 80 F4 09 FC CB 00 00 04 41 90 CA CA EF 13 00 00 10 02 01 D5 00 00 00

80 46 7F CF C5 ED 05 79 74 D1 85 9F 9B 9D 67 04 0D 26 B3 BD C0 CF A0 5E CF CC 14 D9 B3 97 4C 0C

6C 4C 2D 05 18 77 67 65 89 6B 2A D6 FF AD F8 0F 80 C4 CD B8 23 12 F6 9B D2 BE 0F 83 F8 0F 80 FB

CD 06 FB 2C 00 19 FF CF 8A B4 9B C9 C9 45 51 39 50 29 C2 B9 19 F6 93 90 C6 D0 69 C5 8D BE DA 72

80 9A 95 88 89 4D 66 F4 B3 6F 97 E5 45 92 85 FB 5B FC 4A 89 6F B4 30 00 0C FF E7 C4 70 BD D5 CA

22 9B F1 76 8A 45 8C 0B F4 E8 73 D1 21 4F 09 C5 8A F6 9B 4B B6 2A 0A E3 0A 78 95 4A 88 8B 57 E9

CA BE 4E 9C 1B 24 A2 F6 0E 5D AB E5 19 38 D0 3F FF EF FF DD A3 0B A0 E3 6D 6F FB 08 A3 80 DE E5

76 42 D7 65 AD A6 22 7A 49 06 CB BD 17 B9 7E 67 59 73 B4 1B ED B6 7B 66 D5 EB BE F2 BD F6 56 9B

23 8F E2 8D BD 8A 85 3B EC 6D B6 CF D4 76 9F 01 F0 1C 25 AC DC 0F 80 F8 00 00 F5 40 EF 35 5A 3B

17 E7 2D 1E 3E 06 60 A1 3C D9 51 79 02 D7 0D C4 88 DB 6C F4 56 2D 0C 7F 64 F8 75 E6 7D AE 57 0B

36 BB 72 AB 00 C0 B9 64 67 E6 D3 9D DD 71 B8 05 84 5F 03 58 47 00 DC D1 9F 4E 03 71 4C C5 89 CE

CE 15 FA AF 50 33 F8 1E 08 5C DF EE F2 A3 7A 2C F2 58 FB 6D E6 28 17 A6 CD 2D C0 0B F6 6F D0 60

A7 64 04 7C 03 01 00 80 84 A7 44 40 32 B1 30 46 5D CC C8 01 28 27 20 88 40 00 53 5C 89 10 02 BE

01 01 00 84 84 25 3A 22 25 03 26 D0 65 D5 72 20 24 08 94 01 32 40 11 62 B1 22 60 1B E8 18 11 12

08 09 CA 53 A2 22 41 55 53 14 4A 82 04 88 27 28 11 08 24 01 16 6F 89 4A 20 04 7C 02 00 08 89 08

4A 74 4E 10 2A AA 05 14 4A 20 00 9C 82 09 92 00 59 BE 24 40 0A F8 06 04 40 20 26 A2 74 4E 24 1A

35 03 43 16 C0 90 92 28 81 10 80 00 B7 76 44 88 00 00 00 00

  
  
10th Animation Data \[at offset 0x00007BDC\]

  
02 00 97 00 04 00 1F FE 1D FF DE 00 00 00 C5 13 E3 0B 01 EA FD F9 20 F9 F3 12 E0 E0 27 CD E2 5F

DF 30 D5 E6 0B 09 25 C8 C6 2B 23 09 2F CE CD 2D 2A 18 0E 18 C8 E0 20 D9 DE 3E 8D D3 EE 10 0E FE

C6 FD B6 7C E3 DC 72 3D 80 80 D6 1B EE D5 00 00 03 36 84 E3 2A 8A 1B 00 00 EC FA 01 D5 00 00 61

80 30 8F 86 F7 47 6A 9C 2C EA AF E0 C5 A1 81 AB DA DE C7 DE 57 97 8A 34 5C 2F 0A 31 79 4E 5A 2C

62 0C 48 BB AA DE 5B AE D5 AA 0A B5 D9 D1 F0 1F 01 77 02 A8 26 68 B0 2F 6B 0B 8A 43

  
  
11th Animation Data \[at offset 0x00007C78\]

  
0D 0A 00 00

  
  
12th Animation Data \[at offset 0x00007C7C\]

  
0D 0A 00 00

  
  
13th Animation Data \[at offset 0x00007C80\]

  
0D 0A 00 00

  
  
14th Animation Data \[at offset 0x00007C84\]

  
0D 0A 00 00

  
  
15th Animation Data \[at offset 0x00007C88\]

  
0D 0A 00 00

  
  
16th Animation Data \[at offset 0x00007C8C\]

  
0D 0A 00 00

  
  
17th Animation Data \[at offset 0x00007C90\]

  
0F 00 52 00 00 FF 97 FE 83 00 14 FE 28 30 7C 80 00 57 BC CB 12 7F 04 78 C8 A2 87 D0 37 7C D8 A1

F0 09 D2 BA A4 FA 02 EF 6E A9 3F 80 3E E8 EB 00 BF 82 6B 22 40 6F E1 5A 89 01 1F 42 F4 54 40 13

F0 4D B9 4C 09 F4 1E B4 00 3E 02 65 A6 00 FA 05 91 10 00 00 03 93 28 00

  
  
18th Animation Data \[at offset 0x00007CE8\]

  
09 00 3E 00 04 FF 97 FE 7D 00 19 FF 83 7C 00 31 02 C3 8A 3F F2 BF F8 48 08 C6 0D AB 48 E3 10 08

1D 68 4A 29 00 70 CE 67 93 B1 40 15 FB CA F7 AE 81 20 D7 6C D0 E8 10 0B 9F 6E 50 07 02 CF EC 9E

2E 56 84 00

  
  
19th Animation Data \[at offset 0x00007D2C\]

  
0C 00 4C 00 04 FF 67 FD FD FF 76 ED 7E 7F 79 62 FF A9 E6 55 41 29 0F FD 52 BD 2D D2 17 1F F8 8E

34 E1 34 7B FE 51 81 9F 20 C0 BF FD EE 05 AC 17 D2 8F FC 4E 2D 8A 15 1F D8 F1 67 6D D0 84 07 06

8A 02 46 C6 6C DC BC 06 EA 25 9F 20 1B 80 7E 6A 20 00 00 00

  
  
20th Animation Data \[at offset 0x00007D80\]

  
02 00 0E 00 04 FF 54 FE 54 FB B7 04 87 85 00 76 7E B8 66 00

  
  
21st Animation Data \[at offset 0x00007D94\]

  
01 00 09 00 04 FF 54 FE 4E FB B3 00 87 85 00 00

  
  
22nd Animation Data \[at offset 0x00007DA4\]

  
15 00 79 00 04 FF 54 FE 40 FB D7 03 87 85 00 71 70 B8 80 00 C2 AB 71 20 07 17 0B 92 87 F1 31 DB

71 20 07 91 6B C0 00 63 BD B4 80 1F 08 EF 20 00 35 DB 01 20 07 71 6B A8 0B 2F 80 32 E9 AD 61 3D

2E 07 45 53 7C 5D 0E BD 5D 6F 8B 41 97 6B AD FD 90 2A EC EB 7F 73 0A 89 CD EA 00 B1 00 E2 C4 C0

C0 80 3C C0 12 A0 23 9A 6B B9 EC 3F FA 18 08 46 F6 DE 08 88 D9 6D F9 DC 64 3F 0B B9 17 80 00 00

  
  
23rd Animation Data \[at offset 0x00007E24\]

  
0C 00 48 00 04 FF 99 FE 9E 00 0A 03 84 7D 00 10 7F A5 20 06 12 6A 80 96 82 6A 80 07 90 9B 68 00

78 03 EB 2D D4 16 B1 00 58 E2 7D E3 E3 84 13 C3 2B AA 14 45 CE 30 2D DB 68 0B 3B B5 83 64 04 14

CE D6 0D 80 EF F9 EF F4 9F 4F A8 D3 00 00 00 00

  
  
24th Animation Data \[at offset 0x00007E74\]

  
04 00 1E 00 04 FF A5 FD 14 00 EE 1E 2B 24 30 80 28 93 DE 8A 81 7F EF 4C 58 B8 B8 CF 10 08 62 1C

0C ED FB 00

  
  
25th Animation Data \[at offset 0x00007E98\]

  
0C 00 59 00 04 FF DA FD 0A FF 7B 18 33 28 80 2F C0 24 BF F3 DA 6D F6 C8 4A 00 9D FF BF AF 37 24

66 00 D6 83 7F 77 B9 FF 58 7F D9 3F C3 FD 7F 19 BD 80 4B 13 7F 45 FB 4F 9C DB C0 50 7F E3 D0 1B

6D 67 C3 70 20 0E 81 54 45 6F EE 81 54 CE B0 07 60 AA 62 B7 E7 50 AA 27 5B FB B0 55 31 50 00 00

  
  
26th Animation Data \[at offset 0x00007EF8\]

  
02 00 11 00 04 00 96 FD C9 FE E7 C7 A1 2F 53 80 3F 92 D8 D2 6D ED 00 00

  
  
27th Animation Data \[at offset 0x00007F10\]

  
0D 0A 00 00

  
  
28th Animation Data \[at offset 0x00007F14\]

  
0D 0A 00 00

  
  
29th Animation Data \[at offset 0x00007F18\]

  
0D 0A 00 00

  
  
30th Animation Data \[at offset 0x00007F1C\]

  
0D 0A 00 00

  
  
31st Animation Data \[at offset 0x00007F20\]

  
0D 0A 00 00

  
  
32nd Animation Data \[at offset 0x00007F24\]

  
0D 0A 00 00

  
  

- \*\* \*\*\* Animation Data Section runs until Weapon Bone Data Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Weapon Bone Data Section** \[at offset 0x00007F28\]:

  
Note: The first 0x0C bytes of any weapon bone data is the same type of data in normal Individual Bone Structure data (far above).

  
  
1st Weapon Bone Data \[at offset 0x00007F28\]:

  
00 00 00 00 00 00 E7 FF 0C 00 00 00 80 00 00 00 00 00 F2 FF 4E 00 00 00 00 00 F2 FF BB FF 00 00

0E 00 00 00 4E 00 00 00 0E 00 00 00 BB FF 00 00 00 00 0E 00 4E 00 00 00 00 00 0E 00 BB FF 00 00

F2 FF 00 00 4E 00 00 00 F2 FF 00 00 BB FF 00 00 00 00 4F 00 65 00 00 00 00 00 F0 FE 65 00 00 00

14 00 4F 00 50 00 00 00 14 00 F0 FE 50 00 00 00 00 00 4F 00 3C 00 00 00 00 00 F0 FE 3C 00 00 00

EC FF 4F 00 50 00 00 00 EC FF F0 FE 50 00 00 00 00 00 20 00 00 00 00 00 00 00 00 00 0B 00 00 00

48 00 58 00 78 00 68 00 0F 0F 10 38 0A 0A 0B 00 00 00 0F 00 19 1A 1B 00 40 00 70 00 50 00 60 00

52 55 58 38 1F 1F 21 00 FF F0 E1 00 2B 2C 2E 00 78 00 70 00 48 00 40 00 00 00 0F 38 1F 1F 21 00

0F 0F 10 00 52 55 58 00 68 00 60 00 78 00 70 00 19 1A 1B 38 2B 2C 2E 00 00 00 0F 00 1F 1F 21 00

58 00 50 00 68 00 60 00 0A 0A 0B 38 FF F0 E1 00 19 1A 1B 00 2B 2C 2E 00 48 00 40 00 58 00 50 00

0F 0F 10 38 52 55 58 00 0A 0A 0B 00 FF F0 E1 00 08 00 18 00 38 00 28 00 13 13 14 38 00 00 0A 00

1F 20 21 00 3D 3E 41 00 38 00 30 00 08 00 00 00 1F 20 21 38 18 19 1A 00 13 13 14 00 0C 0C 0D 00

28 00 20 00 38 00 30 00 3D 3E 41 38 FF F0 DC 00 1F 20 21 00 18 19 1A 00 18 00 10 00 28 00 20 00

22 23 24 38 3E 3F 42 00 3D 3E 41 00 FF F0 DC 00 08 00 00 00 18 00 10 00 13 13 14 38 0C 0C 0D 00

22 23 24 00 3E 3F 42 00

  
  
  

- \*\* \*\*\* Weapon Bone Data Section runs until Texture Data Section\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**Texture Data Section** - \[at offset 0x000080D0\]:

  
  
Note: This section is modified TIM data.

  
  
Texture Data (modified TIM format) - \[at offset 0x000080D0\]:

  
10 00 00 00 08 00 00 00 2C 00 00 00 00 00 E0 01 10 00 01 00 00 00 FF 7F 00 7C E0 03 E0 7F 1F 00

1F 7C FF 03 00 00 DE 7B 00 78 C0 03 C0 7B 1E 00 1E 78 DE 03 0C 00 00 00 40 01 00 00 00 00 01 00

  
  

- \*\* \*\*\* Texture Section runs until the end of the file\*\*\*

  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
