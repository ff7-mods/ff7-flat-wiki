---
title: BSX
---

[Home](../../Main%20Page.md) > [FF7](../../FF7.md) > [Field](../Field.md) > BSX

# BSX file structure (thanks to [Micky's tool][], Akari's work, and Lazy Bastard's work)

## BSX Header

The BSX file, after it is decompressed, begin with a header of 8 bytes :

`struct StrBsxHeader {`  
`    u32 size_file;     // Size of the file`  
`    u32 offset_models; // Offset to the models section`  
`};`

Note: The end of the BSX Header is directly before the beginning of the
Skeleton Data Section.

## Skeleton Data Section

This section contains the parts of the model's skeleton. For each model,
there is :

| Offset                                                | Size                                          | Data                |
|-------------------------------------------------------|-----------------------------------------------|---------------------|
| offset\_vertex                                        | 4                                             | *Blank*             |
| offset\_vertices = offset\_vertex + 4                 | size\_vertices = num\_vertex \* 8             | Vertices            |
| offset\_qct = offset\_vertex + offset\_poly           | size\_qct = 1 + num\_quad\_color\_tex \* 0x18 | Quad color textures |
| offset\_tct = offset\_qct + size\_qct                 | size\_tct = 1 + num\_tri\_color\_tex \* 0x14  | Tri color textures  |
| offset\_qmt = offset\_tct + size\_tct                 | size\_qmt = 1 + num\_quad\_mono\_tex \* 0x0C  | Quad mono textures  |
| offset\_tmt = offset\_qmt + size\_qmt                 | size\_tmt = 1 + num\_tri\_mono\_tex \* 0x0C   | Tri mono textures   |
| offset\_tm = offset\_tmt + size\_tmt                  | size\_tm = num\_tri\_mono \* 8                | Tri mono            |
| offset\_qm = offset\_tm + size\_tm                    | size\_qm = num\_quad\_mono \* 8               | Quad mono           |
| offset\_tc = offset\_qm + size\_qm                    | size\_tc = num\_tri\_color \* 0x10            | Tri color           |
| offset\_qc = offset\_tc + size\_tc                    | size\_qc = num\_quad\_color \* 0x14           | Quad color          |
| offset\_texcoords = offset\_vertex + offset\_texcoord | size\_texcoords = num\_texcoord \* 2          | Textures coord      |
| offset\_flags = offset\_vertex + offset\_flags        | size\_flags = unknown \* 4                    | Flags               |
| offset\_control = offset\_vertex + offset\_control    | size\_control = textureCount \* 1             | Control             |

Structures:

`typedef struct {`  
`   s16 x, z, y;`  
`} Vertex;// sizeof = 0x06`

`typedef struct {`  
`   u8 red, green, blue;`  
`   u8 unknown; // alpha? padding?`  
`} Color;// sizeof = 0x04`

`typedef struct {`  
`   u8 vertexIndex[4];`  
`   Color color[4];`  
`   u8 texCoordId[4];`  
`} ColorTexturedQuad;// sizeof = 0x18`

**Note for quads:** it is possible that the vertices are not in the
correct order for display, If you see they display wrong, try swapping
the last two vertices.

`typedef struct {`  
`   u8 vertexIndex[3];`  
`   u8 padding1;`  
`   Color color[3];`  
`   u8 texCoordId[3];`  
`   u8 padding2;`  
`} ColorTexturedTriangle;// sizeof = 0x14`

`typedef struct {`  
`   u8 vertexIndex[4];`  
`   Color color;`  
`   u8 texCoordId[4];`  
`} MonochromeTexturedQuad;// sizeof = 0x0C`

`typedef struct {`  
`   u8 vertexIndex[3];`  
`   u8 padding1;`  
`   Color color;`  
`   u8 texCoordId[3];`  
`   u8 padding2;`  
`} MonochromeTexturedTriangle;// sizeof = 0x0C`

`typedef struct {`  
`   u8 vertexIndex[3];`  
`   u8 padding;`  
`   Color color;`  
`} MonochromeTriangle;// sizeof = 0x08`

`typedef struct {`  
`   u8 vertexIndex[4];`  
`   Color color;`  
`} MonochromeQuad;// sizeof = 0x08`

`typedef struct {`  
`   u8 vertexIndex[3];`  
`   u8 padding;`  
`   Color color[3];`  
`} ColorTriangle;// sizeof = 0x10`

`typedef struct {`  
`   u8 vertexIndex[4];`  
`   Color color[4];`  
`} ColorQuad;// sizeof = 0x14`

`typedef struct {`  
`   u8 x, y;`  
`} TextureCoord;// sizeof = 0x02`

## Animation Data Section

`First, there are the channels, at offset`

`offset_data + 4`

, which size is

`num_channel * 8`

. Then, for each channel :

| Offset                                     | Size                                    | Data                      |
|--------------------------------------------|-----------------------------------------|---------------------------|
| offset\_data + offset\_frames\_translation | num\_frames\_translation \* num\_frames | Translation frames        |
| offset\_data + offset\_static\_translation | num\_static\_translation \* 2           | Static translation frames |
| offset\_data + offset\_frames\_rotation    | num\_frames\_rotation \* num\_frames    | Rotation frames           |

`typedef struct {`  
`   u8 flag;`  
`   u8 rx, ry, rz;`  
`   u8 tx, ty, tz;`  
`   u8 unknown; // padding?`  
`} FrameTranslation; // sizeof = 8`

`typedef struct {`  
`   s16 translation;`  
`} StaticTranslation;`

## Models Section

This section begins first with a model header of 16 bytes:

`struct StrModelHeader {`  
`    u32 psx_memory;  // = StrBsxHeader.offset_models | 0x80000000`  
`    u32 num_models;  // Number of models.`  
`    u32 texture_pointer; // Pointer to texture data.`  
`    u32 buffer_size; // Total buffer_size to reserve (see notes below)`  
`}`

Notes: The buffer\_size formula is the addition of buffer sizes of
models.  
To calculate a model buffer size, you need to add every part's
buffer\_size together (see StrPart structure), then do: 2 \* (16 \*
bone\_count + parts\_buffer\_size).

  
Which is followed by num\_models number of :

`struct StrModel {`  
`    u16 model_id;          // ID of the model`  
`    u16 scale;             // (12 bit fixed point)`  
`    u32 offset_skeleton;   // Offset to the parts, bones and animations of the model`  
`    byte global_r, global_g, global_b;`  
`    byte unknown;`  
`    s16 color1_x;`  
`    s16 color1_y;`  
`    s16 color1_z;`  
`    byte index_bones_start;  // Start index of bones (255 if no bones)`  
`    byte index_bones_end;    // End index of bones`  
`    byte r1, g1, b1;`  
`    byte num_bones;        // Additional number of bones in the model's skeleton`  
`    s16 color2_x;`  
`    s16 color2_y;`  
`    s16 color2_z;`  
`    byte index_parts_start; // Start index of parts`  
`    byte index_parts_end;   // End index of parts`  
`    byte r2, g2, b2;`  
`    byte num_parts;        // Additional number of parts in the model's skeleton`  
`    s16 color3_x;`  
`    s16 color3_y;`  
`    s16 color3_z;`  
`    byte index_anim_start; // Start index of animations`  
`    byte index_anim_end;   // End index of animations`  
`    byte r3, g3, b3;`  
`    byte num_animations;   // Additional number of animations`  
`} // sizeof = 48`

Please note that this is additional number of animations in case of
settings for models that has BCX file. They load BCX animations, parts
and bones first, then add BSX parts. For example cloud's sword in some
fields added to normal BCX cloud file.

Then, for each model, we have the parts, bones and animations (at the
offset offset\_skeleton) :

`// Bones (if num_bones > 0)`  
`struct StrBone {`  
`    s16 length;`  
`    s8 parent_id;`  
`    u8 unknown;`  
`}`  
`// Parts (if num_parts > 0)`  
`struct StrPart {`  
`    byte unknown;            // 0 - not calculate stage lighting and color. 1 - calculate.`  
`    byte bone_index;         // bone to which this part attached to.`  
`    byte num_vertex;         // Number of vertices`  
`    byte num_texcoord;       // Number of Texture coord`  
`    byte num_quad_color_tex; // number of textured quads (Gourad Shading)`  
`    byte num_tri_color_tex;  // number of textured triangles (Gourad Shading)`  
`    byte num_quad_mono_tex;  // number of textured quads (Flat Shading)`  
`    byte num_tri_mono_tex;   // number of textured triangles (Flat Shading)`  
`    byte num_tri_mono;       // number of monochrome triangles`  
`    byte num_quad_mono;      // number of monochrome quads`  
`    byte num_tri_color;      // number of gradated triangles`  
`    byte num_quad_color;     // number of gradated quads`  
`    byte num_flags;          // number of data in block 4 (flags).`  
`    byte num_control;        // number of data in block 5 (control).`  
`    u16 offset_poly;         // Relative offset toÂ ?`  
`    u16 offset_texcoord;     // Relative offset toÂ ?`  
`    u16 offset_flags;        // Relative offset to texture settings. Indexed by 5th block data (control).`  
`    u16 offset_control;      // Relative offset to one byte stream for every packet with texture.`  
`    u16 buffer_size;         // Relative offset toÂ ?`  
`    u32 offset_vertex;       // Offset to skeleton data section, substract by 0x80000000 to obtain the right offset`  
`    u32 offset_prec;         // Offset toÂ ?`  
`}`  
`// Animations (if num_animations > 0)`  
`struct StrAnimation {`  
`    u16 num_frames;                // Number of frames`  
`    byte num_bones;                // Number of bones`  
`    byte num_frames_translation;   // Number of translation frames`  
`    byte num_static_translation;   // Number of static translation frames`  
`    byte num_frames_rotation;      // Number of rotation frames`  
`    u16 offset_frames_translation; // Relative offset to translation frames`  
`    u16 offset_static_translation; // Relative offset to static translation frames`  
`    u16 offset_frames_rotation;    // Relative offset to rotation frames`  
`    u32 offset_data;               // Offset to animation data section, substract by 0x80000000 to obtain the right offset`  
`}`

  
Note: Some characters, especially playable characters with BCX files,
will sometimes not have bones or parts specified in the above
subsection. In these cases, their animations may be immediately after
the animations of other models.

## Textures Section

This section begins first with a texture section header of 8 bytes:

`struct TexSectionHeader {`  
`    u32 size_section;              // Size of texture section (from the beginning of this header to the end of the file)`  
`    byte num_textures;             // Number of textures`  
`    byte unknown2[3];              // Maybe always empty`  
`}`

And just after, a list of texture header for each texture:

`struct TexHeader {`  
`    u16 width, height;`  
`    u16 vramX, vramY;`  
`    u32 offset_data; // relative to texture_pointer`  
`}`

And finally, these headers are followed by texture data.

## EXAMPLE, USING MD1STIN.BSX

\[Lazy Bastard\]: ../../Using Akari's notes from Q-Gears, the source from.md
Micky's BSX/BCX viewer, information from the wiki, snippets of things
from across the forums, and my own logical deduction, I've broken down
MD1STIN.BSX (BSX file from the first field encountered in the game) as
an example of BSX structure. Without further ado:

  
**'BSX Header Section**' \[at offset 0x00000000\]:

  

`30 07 01 00 9C F0 00 00`

  
Breakdown:

30 07 01 00 - size of the (decompressed) file in bytes (little-endian,
so 0x00010730; 67376 bytes)

9C F0 00 00 - offset to the 'Models Section' (little-endian, so
0x0000F09C)

  
  
Note: 'BSX Header Section' runs until 'Skeleton Data Section'.

  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**'Skeleton Data Section**' \[at offset 0x00000008\]:

  
Note: Model's 0 and 1, Cloud and Barret respectively, have no skeleton
data in this BSX file, because theirs are already contained in their own
BCX files. Sometimes playable characters will have extra skeleton data
stored in BSX files, but not this time.

Note2: Offset to 'Skeleton Data Section' contained in 'Models Section',
Individual Bones/Parts/Animations Data.

Note3: Number of parts contained in 'Models Section', Individual Model
Data.

  
  
Model 2 and Model 3, skeleton data for 1st part \[at offset
0x00000008\]:

  

`00 00 00 00 4A 00 4A 00 9C FF 00 00 7D 00 45 00 16 00 00 00 82 00 B6 FF 16 00 00 00 4B 00 E2 FF 9C FF 00 00 0D 00 59 00 9C FF 00 00 0F 00 60 00 16 `  
  
`00 00 00 EB FF 5F 00 16 00 00 00 ED FF 58 00 9C FF 00 00 B7 FF DE FF 9C FF 00 00 83 FF AE FF 16 00 00 00 7F FF 3D 00 16 00 00 00 B2 FF 45 00 9C FF `  
  
`00 00 04 03 00 00 1B 3E 9F 70 1B 3E 9F 3D 1B 3E 9F 43 02 05 01 00 1B 3E 9F 26 1B 3E 9F 77 1B 3E 9F 19 06 09 0A 00 1B 3E 9F 88 1B 3E 9F C9 1B 3E 9F `  
  
`D5 08 07 0B 00 1B 3E 9F 9D 1B 3E 9F 7F 1B 3E 9F AD 05 06 04 07 00 13 4B 77 00 13 4B 88 00 13 4B 70 00 13 4B 7F 02 01 03 00 1B 3E 9F 26 1B 3E 9F 19 `  
  
`1B 3E 9F 3D 1B 3E 9F 43 01 05 00 04 1B 3E 9F 19 1B 3E 9F 77 1B 3E 9F 43 1B 3E 9F 70 08 03 07 04 1B 3E 9F 9D 1B 3E 9F 3D 1B 3E 9F 7F 1B 3E 9F 70 09 `  
  
`06 02 05 1B 3E 9F C9 1B 3E 9F 88 1B 3E 9F 26 1B 3E 9F 77 02 03 09 08 1B 3E 9F 26 1B 3E 9F 3D 1B 3E 9F C9 1B 3E 9F 9D 0A 0B 06 07 1B 3E 9F D5 1B 3E `  
  
`9F AD 1B 3E 9F 88 1B 3E 9F 7F 09 08 0A 0B 1B 3E 9F C9 1B 3E 9F 9D 1B 3E 9F D5 1B 3E 9F AD`

  
  
Model 2 and Model 3, skeleton data for 2nd part \[at offset
0x0000014C\]:

  

`00 00 00 00 4D 00 35 00 63 FF 00 00 81 00 23 00 5D FF 00 00 81 00 C7 FF 50 FF 00 00 47 00 3C 00 01 00 00 00 49 00 EA FF FF FF 00 00 4A 00 65 00 D1 `  
  
`FF 00 00 6C 00 53 00 CD FF 00 00 47 00 3E 00 E8 FF 00 00 49 00 E9 FF E1 FF 00 00 6A 00 B0 FF C6 FF 00 00 11 00 75 00 D9 FF 00 00 10 00 56 00 83 FF `  
  
`00 00 00 00 B2 FF 7D FF 00 00 54 00 F0 FF 3E FF 00 00 53 00 4B 00 8F FF 00 00 36 00 53 00 8E FF 00 00 2E 00 6F 00 D6 FF 00 00 0F 00 5B 00 E6 FF 00 `  
  
`00 0F 00 5A 00 02 00 00 00 F1 FF 5A 00 02 00 00 00 F1 FF 5B 00 E6 FF 00 00 D2 FF 6F 00 D6 FF 00 00 CA FF 53 00 8E FF 00 00 AD FF 4B 00 8F FF 00 00 `  
  
`AC FF F0 FF 3E FF 00 00 F0 FF 56 00 83 FF 00 00 EF FF 75 00 D9 FF 00 00 96 FF B0 FF C6 FF 00 00 B7 FF E9 FF E1 FF 00 00 B9 FF 3E 00 E8 FF 00 00 94 `  
  
`FF 53 00 CD FF 00 00 B6 FF 65 00 D1 FF 00 00 B7 FF EA FF FF FF 00 00 B9 FF 3C 00 01 00 00 00 7F FF C7 FF 50 FF 00 00 7E FF 23 00 5D FF 00 00 B3 FF `  
  
`35 00 63 FF 00 00 0D 01 00 00 0D 10 19 6C 0D 10 19 23 0D 10 19 70 0D 02 01 00 0D 10 19 6C 0D 10 19 2F 0D 10 19 23 00 0F 0B 00 0D 10 19 70 0D 10 19 `  
  
`6E 0D 10 19 6E 23 18 24 00 0D 10 19 CE 0D 10 19 83 0D 10 19 7F 22 18 23 00 0D 10 19 C1 0D 10 19 83 0D 10 19 CE 16 24 19 00 0D 10 19 80 0D 10 19 7F `  
  
`0D 10 19 80 0C 09 02 00 1B 3E 9F 7A 1B 3E 9F 38 1B 3E 9F 2F 0C 02 22 00 1B 3E 9F 7A 1B 3E 9F 2F 1B 3E 9F C1 09 0C 1B 00 1B 3E 9F 38 1B 3E 9F 7A 1B `  
  
`3E 9F B4 1B 0C 22 00 1B 3E 9F B4 1B 3E 9F 7A 1B 3E 9F C1 1A 19 0A 0B 00 13 4B 89 00 13 4B 80 00 13 4B 66 00 13 4B 6E 01 0E 00 0F 0D 10 19 23 0D 10 `  
  
`19 4B 0D 10 19 70 0D 10 19 6E 23 24 17 16 0D 10 19 CE 0D 10 19 7F 0D 10 19 A5 0D 10 19 80 0F 0E 10 05 11 0D 0E 6E 11 0D 0E 4B 11 0D 0E 4E 11 0D 0E `  
  
`4E 16 15 17 1F 11 0D 0E 80 11 0D 0E A0 11 0D 0E A5 11 0D 0E A0 14 11 13 12 CC CC CC 88 CC CC CC 67 CC CC CC 88 CC CC CC 67 12 11 03 07 0C 0C 0C 67 `  
  
`0C 0C 0C 67 0C 0C 0C 33 0C 0C 0C 2C 08 04 07 03 0C 0C 0C 28 0C 0C 0C 28 0C 0C 0C 2C 0C 0C 0C 33 08 1C 04 20 0C 0C 0C 28 0C 0C 0C C6 0C 0C 0C 28 0C `  
  
`0C 0C C6 13 21 14 1D 0C 0C 0C 88 0C 0C 0C BC 0C 0C 0C 88 0C 0C 0C C0 1C 1D 20 21 0C 0C 0C C6 0C 0C 0C C0 0C 0C 0C C6 0C 0C 0C BC 18 0D 24 00 88 54 `  
  
`00 83 88 54 00 6C 88 54 00 7F 88 54 00 70 00 0B 24 19 88 54 00 70 88 54 00 6E 88 54 00 7F 88 54 00 80 07 10 06 05 1B 3E 9F 2C 1B 3E 9F 4E 1B 3E 9F `  
  
`19 1B 3E 9F 4E 07 11 10 0A 1B 3E 9F 2C 1B 3E 9F 67 1B 3E 9F 4E 1B 3E 9F 66 0B 0F 0A 10 1B 3E 9F 6E 1B 3E 9F 6E 1B 3E 9F 66 1B 3E 9F 4E 09 06 02 01 `  
  
`1B 3E 9F 38 1B 3E 9F 19 1B 3E 9F 2F 1B 3E 9F 23 06 09 07 08 1B 3E 9F 19 1B 3E 9F 38 1B 3E 9F 2C 1B 3E 9F 28 01 06 0E 05 1B 3E 9F 23 1B 3E 9F 19 1B `  
  
`3E 9F 4B 1B 3E 9F 4E 04 20 03 21 1B 3E 9F 28 1B 3E 9F C6 1B 3E 9F 33 1B 3E 9F BC 21 13 03 12 1B 3E 9F BC 1B 3E 9F 88 1B 3E 9F 33 1B 3E 9F 67 0A 11 `  
  
`1A 14 1B 3E 9F 66 1B 3E 9F 67 1B 3E 9F 89 1B 3E 9F 88 22 02 18 0D 1B 3E 9F C1 1B 3E 9F 2F 1B 3E 9F 83 1B 3E 9F 6C 1B 1C 09 08 1B 3E 9F B4 1B 3E 9F `  
  
`C6 1B 3E 9F 38 1B 3E 9F 28 1D 1E 15 1F 1B 3E 9F C0 1B 3E 9F D5 1B 3E 9F A0 1B 3E 9F A0 1D 15 14 1A 1B 3E 9F C0 1B 3E 9F A0 1B 3E 9F 88 1B 3E 9F 89 `  
  
`19 1A 16 15 1B 3E 9F 80 1B 3E 9F 89 1B 3E 9F 80 1B 3E 9F A0 1B 22 1E 23 1B 3E 9F B4 1B 3E 9F C1 1B 3E 9F D5 1B 3E 9F CE 1E 1D 1B 1C 1B 3E 9F D5 1B `  
  
`3E 9F C0 1B 3E 9F B4 1B 3E 9F C6 23 17 1E 1F 1B 3E 9F CE 1B 3E 9F A5 1B 3E 9F D5 1B 3E 9F A0`  

  
  
  
  
  
Model 2 and Model 3, skeleton data for 3rd part \[at offset
0x00000570\]:

  

`00 00 00 00 00 00 9D FF 2A 00 00 00 62 00 DA FF E5 FF 00 00 53 00 0F 00 EE FF 00 00 46 00 43 00 FB FF 00 00 00 00 91 FF D1 FF 00 00 00 00 7A 00 0A 00 00 00 5A 00 `  
  
`6F FF EC FF 00 00 88 00 D4 FF EE FF 00 00 6B 00 0F 00 F6 FF 00 00 4E 00 44 00 CC FF 00 00 58 00 11 00 C9 FF 00 00 00 00 82 00 DC FF 00 00 55 00 6F FF 9F FF 00 00 `  
  
`87 00 D7 FF A6 FF 00 00 6D 00 11 00 A4 FF 00 00 5C 00 12 00 A3 FF 00 00 52 00 4B 00 A6 FF 00 00 2A 00 57 00 C0 FF 00 00 00 00 74 00 B6 FF 00 00 42 00 7E FF 97 FF `  
  
`00 00 73 00 DC FF A0 FF 00 00 64 00 E1 FF 51 FF 00 00 57 00 62 00 63 FF 00 00 00 00 80 00 8F FF 00 00 35 00 87 FF 51 FF 00 00 26 00 A7 FF 1D FF 00 00 3D 00 F2 FF `  
  
`08 FF 00 00 29 00 71 00 49 FF 00 00 45 00 6C 00 6A FF 00 00 48 00 52 00 A0 FF 00 00 3C 00 A0 00 AE FF 00 00 00 00 BE 00 9E FF 00 00 21 00 B8 00 64 FF 00 00 3B 00 `  
  
`AC 00 7F FF 00 00 00 00 C2 00 82 FF 00 00 0D 00 BE 00 6D FF 00 00 32 00 AA 00 A3 FF 00 00 18 00 B7 00 95 FF 00 00 30 00 B1 00 89 FF 00 00 3B 00 62 00 23 FF 00 00 `  
  
`00 00 2D 00 36 00 00 00 65 00 04 00 20 00 00 00 9B FF 04 00 20 00 00 00 C5 FF 62 00 23 FF 00 00 D0 FF B1 00 89 FF 00 00 E8 FF B7 00 95 FF 00 00 CE FF AA 00 A3 FF `  
  
`00 00 F3 FF BE 00 6D FF 00 00 C5 FF AC 00 7F FF 00 00 DF FF B8 00 64 FF 00 00 C4 FF A0 00 AE FF 00 00 B8 FF 52 00 A0 FF 00 00 BB FF 6C 00 6A FF 00 00 D7 FF 71 00 `  
  
`49 FF 00 00 C3 FF F2 FF 08 FF 00 00 DA FF A7 FF 1D FF 00 00 CB FF 87 FF 51 FF 00 00 A9 FF 62 00 63 FF 00 00 9C FF E1 FF 51 FF 00 00 8D FF DC FF A0 FF 00 00 BE FF `  
  
`7E FF 97 FF 00 00 D6 FF 57 00 C0 FF 00 00 AE FF 4B 00 A6 FF 00 00 A4 FF 12 00 A3 FF 00 00 93 FF 11 00 A4 FF 00 00 79 FF D7 FF A6 FF 00 00 AB FF 6F FF 9F FF 00 00 `  
  
`A8 FF 11 00 C9 FF 00 00 B2 FF 44 00 CC FF 00 00 95 FF 0F 00 F6 FF 00 00 78 FF D4 FF EE FF 00 00 A6 FF 6F FF EC FF 00 00 BA FF 43 00 FB FF 00 00 AD FF 0F 00 EE FF `  
  
`00 00 9E FF DA FF E5 FF 00 00 03 28 05 00 FF FF FF 19 FF FF FF 84 FF FF FF 77 00 01 02 01 28 48 05 00 FF FF FF 84 FF FF FF D5 FF FF FF 77 01 03 02 88 17 11 12 00 `  
  
`0C 0C 0C 78 0C 0C 0C 3E 0C 0C 0C 79 11 10 09 00 0C 0C 0C 3E 0C 0C 0C 18 0C 0C 0C 0F 3D 17 12 00 0C 0C 0C B0 0C 0C 0C 78 0C 0C 0C 79 3E 3D 44 00 0C 0C 0C D6 0C 0C `  
  
`0C B0 0C 0C 0C E0 11 09 0B 00 88 54 00 3E 88 54 00 0F 88 54 00 85 00 01 04 00 88 54 00 72 88 54 00 73 88 54 00 6D 00 28 29 00 88 54 00 72 88 54 00 84 88 54 00 10 `  
  
`00 29 01 00 88 54 00 72 88 54 00 10 88 54 00 73 28 03 29 00 88 54 00 84 88 54 00 19 88 54 00 10 11 0B 12 00 88 54 00 3E 88 54 00 85 88 54 00 79 44 3D 0B 00 88 54 `  
  
`00 E0 88 54 00 B0 88 54 00 85 4A 00 04 00 88 54 00 7C 88 54 00 72 88 54 00 6D 28 00 2A 00 88 54 00 84 88 54 00 72 88 54 00 DC 2A 00 4A 00 88 54 00 DC 88 54 00 72 `  
  
`88 54 00 7C 48 28 2A 00 88 54 00 D5 88 54 00 84 88 54 00 DC 0B 3D 12 00 88 54 00 85 88 54 00 B0 88 54 00 79 25 26 24 00 FF 00 00 55 FF 00 00 55 FF 00 00 4E 2F 23 `  
  
`22 00 FF 00 00 92 FF 00 00 5C FF 00 00 79 2C 2D 2E 00 FF 00 00 9A FF 00 00 9A FF 00 00 A0 26 20 21 00 0D 22 5B 55 0D 22 5B 46 0D 22 5B 1E 1E 1F 24 00 0D 22 5B 34 `  
  
`0D 22 5B 77 0D 22 5B 4E 24 1F 25 00 0D 22 5B 4E 0D 22 5B 77 0D 22 5B 55 31 2C 30 00 0D 22 5B A9 0D 22 5B 9A 0D 22 5B B0 1F 32 2E 00 0D 22 5B 77 0D 22 5B BB 0D 22 `  
  
`5B A0 1F 2E 2D 00 0D 22 5B 77 0D 22 5B A0 0D 22 5B 9A 10 0E 0F 00 1B 3E 9F 18 1B 3E 9F 0F 1B 3E 9F 4D 16 0E 10 00 1B 3E 9F 13 1B 3E 9F 0F 1B 3E 9F 18 0E 14 0D 00 `  
  
`1B 3E 9F 0F 1B 3E 9F 25 1B 3E 9F 08 08 02 0A 00 1B 3E 9F 52 1B 3E 9F 0F 1B 3E 9F 31 04 06 47 00 1B 3E 9F 6D 1B 3E 9F 42 1B 3E 9F AC 40 3E 3F 00 1B 3E 9F E0 1B 3E `  
  
`9F D6 1B 3E 9F A2 40 39 3E 00 1B 3E 9F E0 1B 3E 9F DF 1B 3E 9F D6 3B 40 41 00 1B 3E 9F CB 1B 3E 9F E0 1B 3E 9F E6 49 45 43 00 1B 3E 9F E0 1B 3E 9F 9C 1B 3E 9F BF `  
  
`03 28 05 00 88 54 00 19 88 54 00 84 88 54 00 77 28 48 05 00 88 54 00 84 88 54 00 D5 88 54 00 77 10 0F 09 0A 0C 0C 0C 18 0C 0C 0C 4D 0C 0C 0C 0F 0C 0C 0C 31 11 17 `  
  
`10 1D 0C 0C 0C 3E 0C 0C 0C 78 0C 0C 0C 18 0C 0C 0C 34 3E 44 3F 43 0C 0C 0C D6 0C 0C 0C E0 0C 0C 0C A2 0C 0C 0C BF 3D 3E 17 33 0C 0C 0C B0 0C 0C 0C D6 0C 0C 0C 78 `  
  
`0C 0C 0C B8 09 03 0B 05 88 54 00 0F 88 54 00 19 88 54 00 85 88 54 00 77 03 09 02 0A 88 54 00 19 88 54 00 0F 88 54 00 0F 88 54 00 31 29 03 01 02 88 54 00 10 88 54 `  
  
`00 19 88 54 00 73 88 54 00 0F 44 0B 48 05 88 54 00 E0 88 54 00 85 88 54 00 D5 88 54 00 77 48 49 44 43 88 54 00 D5 88 54 00 E0 88 54 00 E0 88 54 00 BF 2A 4A 48 49 `  
  
`88 54 00 DC 88 54 00 7C 88 54 00 D5 88 54 00 E0 21 1E 26 24 0D 22 5B 1E 0D 22 5B 34 0D 22 5B 55 0D 22 5B 4E 1D 1E 1C 21 0D 22 5B 39 0D 22 5B 39 0D 22 5B 1E 0D 22 `  
  
`5B 0B 1B 1C 20 21 0D 22 5B 46 0D 22 5B 1E 0D 22 5B 46 0D 22 5B 0B 1D 17 1E 1F 0D 22 5B 39 0D 22 5B 77 0D 22 5B 39 0D 22 5B 7C 22 26 1F 25 0D 22 5B 79 0D 22 5B 55 `  
  
`0D 22 5B 77 0D 22 5B 55 26 22 20 23 0D 22 5B 55 0D 22 5B 79 0D 22 5B 46 0D 22 5B 5C 35 1B 31 20 0D 22 5B AF 0D 22 5B 46 0D 22 5B A9 0D 22 5B 46 31 20 2F 23 0D 22 `  
  
`5B A9 0D 22 5B 46 0D 22 5B 92 0D 22 5B 5C 30 2C 32 2E 0D 22 5B B0 0D 22 5B 9A 0D 22 5B BB 0D 22 5B A0 33 34 32 30 0D 22 5B B6 0D 22 5B D9 0D 22 5B B8 0D 22 5B D1 `  
  
`35 31 34 30 0D 22 5B AF 0D 22 5B A9 0D 22 5B D9 0D 22 5B D1 33 32 17 1F 0D 22 5B B6 0D 22 5B B8 0D 22 5B 77 0D 22 5B 7C 22 1F 2C 2D 0D 22 5B 79 0D 22 5B 77 0D 22 `  
  
`5B 9A 0D 22 5B 9A 2C 31 22 2F 0D 22 5B 9A 0D 22 5B A9 0D 22 5B 79 0D 22 5B 92 16 10 1C 1D 1B 3E 9F 13 1B 3E 9F 18 1B 3E 9F 3E 1B 3E 9F 34 15 16 1A 27 1B 3E 9F 0D `  
  
`1B 3E 9F 13 1B 3E 9F 3A 1B 3E 9F 43 15 1A 18 19 1B 3E 9F 0D 1B 3E 9F 3A 1B 3E 9F 36 1B 3E 9F 53 14 15 13 18 1B 3E 9F 25 1B 3E 9F 0D 1B 3E 9F 53 1B 3E 9F 36 15 14 `  
  
`16 0E 1B 3E 9F 0D 1B 3E 9F 25 1B 3E 9F 13 1B 3E 9F 0F 0C 0D 13 14 1B 3E 9F 37 1B 3E 9F 08 1B 3E 9F 53 1B 3E 9F 25 08 0A 0E 0F 1B 3E 9F 52 1B 3E 9F 31 1B 3E 9F 0F `  
  
`1B 3E 9F 4D 08 0E 07 0D 1B 3E 9F 52 1B 3E 9F 0F 1B 3E 9F 24 1B 3E 9F 08 0C 06 0D 07 1B 3E 9F 37 1B 3E 9F 42 1B 3E 9F 08 1B 3E 9F 24 07 01 08 02 1B 3E 9F 24 1B 3E `  
  
`9F 73 1B 3E 9F 52 1B 3E 9F 0F 06 04 07 01 1B 3E 9F 42 1B 3E 9F 6D 1B 3E 9F 24 1B 3E 9F 73 27 16 1B 1C 1B 3E 9F 43 1B 3E 9F 13 1B 3E 9F 5C 1B 3E 9F 3E 06 0C 47 42 `  
  
`1B 3E 9F 42 1B 3E 9F 37 1B 3E 9F AC 1B 3E 9F B9 0C 13 42 3C 1B 3E 9F 37 1B 3E 9F 53 1B 3E 9F B9 1B 3E 9F 9D 13 18 3C 38 1B 3E 9F 53 1B 3E 9F 36 1B 3E 9F 9D 1B 3E `  
  
`9F BA 2B 27 35 1B 1B 3E 9F AD 1B 3E 9F 43 1B 3E 9F A9 1B 3E 9F 5C 36 1A 2B 27 1B 3E 9F B7 1B 3E 9F 3A 1B 3E 9F AD 1B 3E 9F 43 1A 36 19 37 1B 3E 9F 3A 1B 3E 9F B7 `  
  
`1B 3E 9F 53 1B 3E 9F 9D 38 18 37 19 1B 3E 9F BA 1B 3E 9F 36 1B 3E 9F 9D 1B 3E 9F 53 39 34 3E 33 1B 3E 9F DF 1B 3E 9F D1 1B 3E 9F D6 1B 3E 9F B8 3A 36 39 2B 1B 3E `  
  
`9F E3 1B 3E 9F B7 1B 3E 9F DF 1B 3E 9F AD 3A 38 36 37 1B 3E 9F E3 1B 3E 9F BA 1B 3E 9F B7 1B 3E 9F 9D 3B 3C 3A 38 1B 3E 9F CB 1B 3E 9F 9D 1B 3E 9F E3 1B 3E 9F BA `  
  
`3A 39 3B 40 1B 3E 9F E3 1B 3E 9F DF 1B 3E 9F CB 1B 3E 9F E0 42 3C 41 3B 1B 3E 9F B9 1B 3E 9F 9D 1B 3E 9F E6 1B 3E 9F CB 45 40 43 3F 1B 3E 9F 9C 1B 3E 9F E0 1B 3E `  
  
`9F BF 1B 3E 9F A2 45 46 40 41 1B 3E 9F 9C 1B 3E 9F C8 1B 3E 9F E0 1B 3E 9F E6 42 41 47 46 1B 3E 9F B9 1B 3E 9F E6 1B 3E 9F AC 1B 3E 9F C8 46 45 4A 49 1B 3E 9F C8 `  
  
`1B 3E 9F 9C 1B 3E 9F 7C 1B 3E 9F E0 47 46 04 4A 1B 3E 9F AC 1B 3E 9F C8 1B 3E 9F 6D 1B 3E 9F 7C 2B 35 39 34 1B 3E 9F AD 1B 3E 9F A9 1B 3E 9F DF 1B 3E 9F D1 01 1C `  
  
`14 78 1F A0 0F BE 0F AA 00 A0 00 00 BF BF`

  
  
  
  
Model 2 and Model 3, skeleton data for 4th part \[at offset
0x00000E90\]:

  

`00 00 00 00 DC FF BB FF 15 00 00 00 DE FF 03 00 54 00 00 00 24 00 BB FF 13 00 00 00 DC FF 4A 00 15 00 00 00 24 00 4A 00 13 00 00 00 1F 00 03 00 55 00 00 00 5C 00 `  
  
`03 00 13 00 00 00 A2 FF 03 00 00 00 00 00 11 00 14 00 D8 FF 00 00 11 00 F2 FF D8 FF 00 00 F0 FF F2 FF D8 FF 00 00 F0 FF 14 00 D8 FF 00 00 11 00 14 00 A3 FF 00 00 `  
  
`11 00 F2 FF A3 FF 00 00 F0 FF 14 00 A3 FF 00 00 F0 FF F2 FF A3 FF 00 00 07 03 01 00 99 99 99 EF 99 99 99 9A 99 99 99 B6 00 07 01 00 99 99 99 B1 99 99 99 EF 99 99 `  
  
`99 B6 05 06 02 00 99 99 99 39 99 99 99 03 99 99 99 3F 04 06 05 00 99 99 99 3E 99 99 99 03 99 99 99 39 08 06 04 00 1B 3E 9F 43 1B 3E 9F 03 1B 3E 9F 3E 06 09 02 00 `  
  
`1B 3E 9F 03 1B 3E 9F 37 1B 3E 9F 3F 0B 07 0A 00 1B 3E 9F AD 1B 3E 9F EF 1B 3E 9F B9 0A 07 00 00 1B 3E 9F B9 1B 3E 9F EF 1B 3E 9F B1 08 09 06 00 1B 3E 9F 43 1B 3E `  
  
`9F 37 1B 3E 9F 03 07 0B 03 00 1B 3E 9F EF 1B 3E 9F AD 1B 3E 9F 9A 04 05 03 01 99 99 99 3E 99 99 99 39 99 99 99 9A 99 99 99 B6 02 00 05 01 99 99 99 3F 99 99 99 B1 `  
  
`99 99 99 39 99 99 99 B6 03 0B 04 08 1B 3E 9F 9A 1B 3E 9F AD 1B 3E 9F 3E 1B 3E 9F 43 00 02 0A 09 1B 3E 9F B1 1B 3E 9F 3F 1B 3E 9F B9 1B 3E 9F 37 0D 09 0C 08 1B 3E `  
  
`9F 2F 1B 3E 9F 37 1B 3E 9F 2B 1B 3E 9F 43 08 0B 0C 0E 1B 3E 9F 43 1B 3E 9F AD 1B 3E 9F 2B 1B 3E 9F C5 0A 0F 0B 0E 1B 3E 9F B9 1B 3E 9F C1 1B 3E 9F AD 1B 3E 9F C5 `  
  
`0F 0A 0D 09 1B 3E 9F C1 1B 3E 9F B9 1B 3E 9F 2F 1B 3E 9F 37 0C 0E 0D 0F 1B 3E 9F 2B 1B 3E 9F C5 1B 3E 9F 2F 1B 3E 9F C1`

  
  
  
  
Model 2 and Model 3, skeleton data for 5th part \[at offset
0x00001068\]:

  

`00 00 00 00 11 00 14 00 00 00 00 00 11 00 14 00 E0 FF 00 00 11 00 F2 FF E0 FF 00 00 11 00 F2 FF 00 00 00 00 F0 FF 14 00 00 00 00 00 F0 FF 14 00 E0 FF 00 00 F0 FF `  
  
`F2 FF 00 00 00 00 F0 FF F2 FF E0 FF 00 00 D1 FF D4 FF 83 FF 00 00 D1 FF 32 00 83 FF 00 00 30 00 32 00 83 FF 00 00 30 00 D4 FF 83 FF 00 00 03 02 06 07 F8 A7 87 28 `  
  
`F8 A7 87 26 F8 A7 87 C6 F8 A7 87 C9 08 07 0B 02 F8 A7 87 D4 F8 A7 87 C9 F8 A7 87 1B F8 A7 87 26 07 05 06 04 F8 A7 87 C9 F8 A7 87 C3 F8 A7 87 C6 F8 A7 87 C0 09 05 `  
  
`08 07 F8 A7 87 CA F8 A7 87 C3 F8 A7 87 D4 F8 A7 87 C9 01 00 05 04 F8 A7 87 2D F8 A7 87 2C F8 A7 87 C3 F8 A7 87 C0 09 0A 05 01 F8 A7 87 CA F8 A7 87 27 F8 A7 87 C3 `  
  
`F8 A7 87 2D 02 03 01 00 F8 A7 87 26 F8 A7 87 28 F8 A7 87 2D F8 A7 87 2C 0A 0B 01 02 F8 A7 87 27 F8 A7 87 1B F8 A7 87 2D F8 A7 87 26 04 00 06 03 F8 A7 87 C0 F8 A7 `  
  
`87 2C F8 A7 87 C6 F8 A7 87 28 0A 09 0B 08 F8 A7 87 27 F8 A7 87 CA F8 A7 87 1B F8 A7 87 D4`

  
  
  
Model 2 and Model 3, skeleton data for 6th part \[at offset
0x00001194\]:

  

`00 00 00 00 37 00 CD FF AB FF 00 00 30 00 D4 FF 00 00 00 00 30 00 32 00 00 00 00 00 37 00 39 00 AB FF 00 00 CA FF CD FF AB FF 00 00 D1 FF D4 FF 00 00 00 00 CA FF `  
  
`39 00 AB FF 00 00 D1 FF 32 00 00 00 00 00 01 00 03 00 8E FF 00 00 00 03 08 00 F8 A7 87 37 F8 A7 87 27 F8 A7 87 6C 04 00 08 00 F8 A7 87 B9 F8 A7 87 37 F8 A7 87 6C `  
  
`06 04 08 00 F8 A7 87 CA F8 A7 87 B9 F8 A7 87 6C 03 06 08 00 F8 A7 87 27 F8 A7 87 CA F8 A7 87 6C 07 02 05 01 25 26 22 C0 25 26 22 2C 25 26 22 AC 25 26 22 42 04 05 `  
  
`00 01 25 26 22 B9 25 26 22 AC 25 26 22 37 25 26 22 42 04 06 05 07 25 26 22 B9 25 26 22 CA 25 26 22 AC 25 26 22 C0 06 03 07 02 25 26 22 CA 25 26 22 27 25 26 22 C0 `  
  
`25 26 22 2C 00 01 03 02 25 26 22 37 25 26 22 42 25 26 22 27 25 26 22 2C`

  
  
Model 2 and Model 3, skeleton data for 7th part \[at offset
0x00001284\]:

  

`00 00 00 00 10 00 F2 FF A3 FF 00 00 10 00 14 00 A3 FF 00 00 EF FF F2 FF A3 FF 00 00 EF FF 14 00 A3 FF 00 00 10 00 14 00 D8 FF 00 00 10 00 F2 FF D8 FF 00 00 EF FF `  
  
`F2 FF D8 FF 00 00 EF FF 14 00 D8 FF 00 00 5E 00 03 00 00 00 00 00 A4 FF 03 00 13 00 00 00 E1 FF 03 00 55 00 00 00 DC FF 4A 00 13 00 00 00 24 00 4A 00 15 00 00 00 `  
  
`DC FF BB FF 13 00 00 00 22 00 03 00 54 00 00 00 24 00 BB FF 15 00 00 00 0C 08 0E 00 99 99 99 55 99 99 99 03 99 99 99 39 08 0F 0E 00 99 99 99 03 99 99 99 3F 99 99 `  
  
`99 39 09 0A 0D 00 99 99 99 EF 99 99 99 B6 99 99 99 B1 09 0B 0A 00 99 99 99 EF 99 99 99 B0 99 99 99 B6 09 07 0B 00 1B 3E 9F EF 1B 3E 9F AD 1B 3E 9F B0 06 09 0D 00 `  
  
`1B 3E 9F B9 1B 3E 9F EF 1B 3E 9F B1 08 04 05 00 1B 3E 9F 03 1B 3E 9F 43 1B 3E 9F 37 08 05 0F 00 1B 3E 9F 03 1B 3E 9F 37 1B 3E 9F 3F 06 07 09 00 1B 3E 9F B9 1B 3E `  
  
`9F AD 1B 3E 9F EF 04 08 0C 00 1B 3E 9F 43 1B 3E 9F 03 1B 3E 9F 55 0B 0C 0A 0E 99 99 99 B0 99 99 99 55 99 99 99 B6 99 99 99 39 0D 0A 0F 0E 99 99 99 B1 99 99 99 B6 `  
  
`99 99 99 3F 99 99 99 39 0C 0B 04 07 1B 3E 9F 55 1B 3E 9F B0 1B 3E 9F 43 1B 3E 9F AD 0F 05 0D 06 1B 3E 9F 3F 1B 3E 9F 37 1B 3E 9F B1 1B 3E 9F B9 02 03 06 07 1B 3E `  
  
`9F C1 1B 3E 9F C5 1B 3E 9F B9 1B 3E 9F AD 07 03 04 01 1B 3E 9F AD 1B 3E 9F C5 1B 3E 9F 43 1B 3E 9F 2B 04 01 05 00 1B 3E 9F 43 1B 3E 9F 2B 1B 3E 9F 37 1B 3E 9F 2F `  
  
`02 06 00 05 1B 3E 9F C1 1B 3E 9F B9 1B 3E 9F 2F 1B 3E 9F 37 02 00 03 01 1B 3E 9F C1 1B 3E 9F 2F 1B 3E 9F C5 1B 3E 9F 2B`

  
  
Model 2 and Model 3, skeleton data for 8th part \[at offset
0x0000145C\]:

  

`00 00 00 00 D0 FF D4 FF 83 FF 00 00 D0 FF 32 00 83 FF 00 00 2F 00 32 00 83 FF 00 00 2F 00 D4 FF 83 FF 00 00 10 00 F2 FF E0 FF 00 00 10 00 F2 FF 00 00 00 00 10 00 `  
  
`14 00 E0 FF 00 00 10 00 14 00 00 00 00 00 EF FF F2 FF 00 00 00 00 EF FF F2 FF E0 FF 00 00 EF FF 14 00 E0 FF 00 00 EF FF 14 00 00 00 00 00 09 08 04 05 F8 A7 87 C9 `  
  
`F8 A7 87 C6 F8 A7 87 26 F8 A7 87 28 03 00 04 09 F8 A7 87 1B F8 A7 87 D4 F8 A7 87 26 F8 A7 87 C9 06 04 07 05 F8 A7 87 2D F8 A7 87 26 F8 A7 87 2C F8 A7 87 28 03 04 `  
  
`02 06 F8 A7 87 1B F8 A7 87 26 F8 A7 87 27 F8 A7 87 2D 0A 06 0B 07 F8 A7 87 C3 F8 A7 87 2D F8 A7 87 C0 F8 A7 87 2C 02 06 01 0A F8 A7 87 27 F8 A7 87 2D F8 A7 87 CA `  
  
`F8 A7 87 C3 0A 0B 09 08 F8 A7 87 C3 F8 A7 87 C0 F8 A7 87 C9 F8 A7 87 C6 00 01 09 0A F8 A7 87 D4 F8 A7 87 CA F8 A7 87 C9 F8 A7 87 C3 07 05 0B 08 F8 A7 87 2C F8 A7 `  
  
`87 28 F8 A7 87 C0 F8 A7 87 C6 01 00 02 03 F8 A7 87 CA F8 A7 87 D4 F8 A7 87 27 F8 A7 87 1B`

  
  
Model 2 and Model 3, skeleton data for 9th part \[at offset
0x00001588\]:

  

`00 00 00 00 FF FF 03 00 8E FF 00 00 2F 00 32 00 00 00 00 00 36 00 39 00 AB FF 00 00 2F 00 D4 FF 00 00 00 00 36 00 CD FF AB FF 00 00 C9 FF 39 00 AB FF 00 00 D0 FF `  
  
`32 00 00 00 00 00 D0 FF D4 FF 00 00 00 00 C9 FF CD FF AB FF 00 00 05 08 00 00 F8 A7 87 CA F8 A7 87 B9 F8 A7 87 83 08 04 00 00 F8 A7 87 B9 F8 A7 87 37 F8 A7 87 83 `  
  
`04 02 00 00 F8 A7 87 37 F8 A7 87 27 F8 A7 87 83 02 05 00 00 F8 A7 87 27 F8 A7 87 CA F8 A7 87 83 01 03 06 07 25 26 22 2C 25 26 22 42 25 26 22 C0 25 26 22 AC 04 08 `  
  
`03 07 25 26 22 37 25 26 22 B9 25 26 22 42 25 26 22 AC 02 04 01 03 25 26 22 27 25 26 22 37 25 26 22 2C 25 26 22 42 02 01 05 06 25 26 22 27 25 26 22 2C 25 26 22 CA `  
  
`25 26 22 C0 05 06 08 07 25 26 22 CA 25 26 22 C0 25 26 22 B9 25 26 22 AC`

  
  
Model 2 and Model 3, skeleton data for 10th part \[at offset
0x00001678\]:

  

`00 00 00 00 01 00 E9 FF 03 FF 00 00 04 00 60 00 55 FF 00 00 A7 FF F8 FF 52 FF 00 00 63 00 FF FF 4F FF 00 00 FA FF AE FF 0E 00 00 00 34 00 EA FF 0E 00 00 00 F8 FF `  
  
`2C 00 0E 00 00 00 BB FF E5 FF 0E 00 00 00 DB FF A5 FF 2F FF 00 00 2A 00 A8 FF 2F FF 00 00 FF FF 1E 00 03 FF 00 00 08 00 A2 FF 53 FF 00 00 0A 02 00 00 1B 3E 9F 7D `  
  
`1B 3E 9F EF 1B 3E 9F 87 03 0A 00 00 1B 3E 9F 03 1B 3E 9F 7D 1B 3E 9F 87 0A 03 01 00 1B 3E 9F 7D 1B 3E 9F 03 1B 3E 9F 85 02 0A 01 00 1B 3E 9F EF 1B 3E 9F 7D 1B 3E `  
  
`9F 85 00 0B 03 00 1B 3E 9F 87 1B 3E 9F 60 1B 3E 9F 03 0B 00 02 00 1B 3E 9F 60 1B 3E 9F 87 1B 3E 9F EF 00 09 0B 00 25 26 22 87 25 26 22 06 25 26 22 60 00 0B 08 00 `  
  
`25 26 22 87 25 26 22 60 25 26 22 E9 09 00 08 00 25 26 22 06 25 26 22 87 25 26 22 E9 09 08 0B 00 25 26 22 06 25 26 22 E9 25 26 22 60 03 0B 05 04 1B 3E 9F 03 1B 3E `  
  
`9F 60 1B 3E 9F 24 1B 3E 9F 57 03 05 01 06 1B 3E 9F 03 1B 3E 9F 24 1B 3E 9F 85 1B 3E 9F 77 02 07 0B 04 1B 3E 9F EF 1B 3E 9F CC 1B 3E 9F 60 1B 3E 9F 57 02 01 07 06 `  
  
`1B 3E 9F EF 1B 3E 9F 85 1B 3E 9F CC 1B 3E 9F 77 06 05 07 04 1B 3E 9F 77 1B 3E 9F 24 1B 3E 9F CC 1B 3E 9F 57`

  
  
Model 2 and Model 3, skeleton data for 11th part \[at offset
0x000017E0\]:

  

`00 00 00 00 00 00 23 00 9C FF 00 00 DE FF 02 00 9C FF 00 00 00 00 E0 FF 9C FF 00 00 22 00 02 00 9C FF 00 00 DE FF 02 00 FD FF 00 00 00 00 E0 FF FD FF 00 00 22 00 `  
  
`02 00 FD FF 00 00 00 00 23 00 FD FF 00 00 04 07 05 06 00 0A 28 E7 00 0A 28 77 00 0A 28 6F 00 0A 28 0A 01 02 00 03 19 19 19 E6 19 19 19 65 19 19 19 80 19 19 19 08 `  
  
`04 05 01 02 19 19 19 E7 19 19 19 6F 19 19 19 E6 19 19 19 65 07 04 00 01 19 19 19 77 19 19 19 E7 19 19 19 80 19 19 19 E6 06 03 05 02 19 19 19 0A 19 19 19 08 19 19 `  
  
`19 6F 19 19 19 65 07 00 06 03 19 19 19 77 19 19 19 80 19 19 19 0A 19 19 19 08`

  
  
Model 2 and Model 3, skeleton data for 12th part \[at offset
0x0000189C\]:

  

`00 00 00 00 3B 00 3C 00 03 00 00 00 C6 FF 3C 00 03 00 00 00 5A 00 3A 00 44 FF 00 00 00 00 3A 00 34 00 00 00 00 00 F9 FF 34 00 00 00 A6 FF 3A 00 44 FF 00 00 00 00 `  
` `  
` E7 FF 03 00 00 00 00 00 3A 00 11 FF 00 00 00 00 01 00 8D FF 00 00 00 00 00 00 BD FF 00 00 BA FF 3A 00 CD FF 00 00 BA FF 3B`  
` `  
` Note: The end of the BSX Header is directly before the beginning of the Skeleton Data Section.`  
` `  
` == Skeleton Data Section ==`  
` `  
` This section contains the parts of the model's skeleton. For each model, there isÂ :`  
` `  
` {| border= 00 9F FF 00 00 46 00 3B 00 9F FF 00 00 `  
` `  
` 46 00 3A 00 CD FF 00 00 02 05 07 00 19 19 19 15 19 19 19 D8 19 19 19 6C 01 00 03 00 19 19 19 D5 19 19 19 19 19 19 19 76 04 01 03 00 19 19 19 7E 19 19 19 D5 19 19 `  
` `  
` 19 76 00 04 03 00 19 19 19 19 19 19 19 7E 19 19 19 76 05 0B 08 00 19 19 19 D8 19 19 19 E8 19 19 19 7A 0C 02 08 00 19 19 19 07 19 19 19 15 19 19 19 7A 08 07 05 00 `  
` `  
` 19 19 19 7A 19 19 19 6C 19 19 19 D8 07 08 02 00 19 19 19 6C 19 19 19 7A 19 19 19 15 0A 06 09 00 19 19 19 E0 19 19 19 68 19 19 19 7A 0D 09 06 00 19 19 19 0F 19 19 `  
` `  
` 19 7A 19 19 19 68 08 09 0C 0D 88 54 00 7A 88 54 00 7A 88 54 00 07 88 54 00 0F 08 0B 09 0A 88 54 00 7A 88 54 00 E8 88 54 00 7A 88 54 00 E0 06 0A 04 01 19 19 19 68 `  
` `  
` 19 19 19 E0 19 19 19 7E 19 19 19 D5 0B 0C 0A 0D 19 19 19 E8 19 19 19 07 19 19 19 E0 19 19 19 0F 0D 00 0A 01 19 19 19 0F 19 19 19 19 19 19 19 E0 19 19 19 D5 02 0C `  
` `  
` 05 0B 19 19 19 15 19 19 19 07 19 19 19 D8 19 19 19 E8 06 04 0D 00 19 19 19 68 19 19 19 7E 19 19 19 0F 19 19 19 19`  
` `

  
  
Model 2 and Model 3, skeleton data for 13th part \[at offset
0x00001A3C\]:

  

`00 00 00 00 F8 FF A2 FF 53 FF 00 00 01 00 1E 00 03 FF 00 00 D6 FF A8 FF 2F FF 00 00 25 00 A5 FF 2F FF 00 00 45 00 E5 FF 0E 00 00 00 08 00 2C 00 0E 00 00 00 CC FF `  
  
`EA FF 0E 00 00 00 06 00 AE FF 0E 00 00 00 9D FF FF FF 4F FF 00 00 59 00 F8 FF 52 FF 00 00 FC FF 60 00 55 FF 00 00 FF FF E9 FF 03 FF 00 00 09 01 0B 00 1B 3E 9F 03 `  
  
`1B 3E 9F 71 1B 3E 9F 6B 01 08 0B 00 1B 3E 9F 71 1B 3E 9F EF 1B 3E 9F 6B 08 01 0A 00 1B 3E 9F EF 1B 3E 9F 71 1B 3E 9F 69 01 09 0A 00 1B 3E 9F 71 1B 3E 9F 03 1B 3E `  
  
`9F 69 00 0B 08 00 1B 3E 9F 8F 1B 3E 9F 6B 1B 3E 9F EF 0B 00 09 00 1B 3E 9F 6B 1B 3E 9F 8F 1B 3E 9F 03 02 0B 00 00 25 26 22 E9 25 26 22 6B 25 26 22 8F 00 0B 03 00 `  
  
`25 26 22 8F 25 26 22 6B 25 26 22 06 0B 02 03 00 25 26 22 6B 25 26 22 E9 25 26 22 06 03 02 00 00 25 26 22 06 25 26 22 E9 25 26 22 8F 08 06 00 07 1B 3E 9F EF 1B 3E `  
  
`9F C8 1B 3E 9F 8F 1B 3E 9F 98 08 0A 06 05 1B 3E 9F EF 1B 3E 9F 69 1B 3E 9F C8 1B 3E 9F 77 09 00 04 07 1B 3E 9F 03 1B 3E 9F 8F 1B 3E 9F 20 1B 3E 9F 98 09 04 0A 05 `  
  
`1B 3E 9F 03 1B 3E 9F 20 1B 3E 9F 69 1B 3E 9F 77 05 04 06 07 1B 3E 9F 77 1B 3E 9F 20 1B 3E 9F C8 1B 3E 9F 98`

  
  
Model 2 and Model 3, skeleton data for 14th part \[at offset
0x00001BA4\]:

  

`00 00 00 00 00 00 23 00 FD FF 00 00 DE FF 02 00 FD FF 00 00 00 00 E0 FF FD FF 00 00 22 00 02 00 FD FF 00 00 DE FF 02 00 9C FF 00 00 00 00 E0 FF 9C FF 00 00 22 00 `  
  
`02 00 9C FF 00 00 00 00 23 00 9C FF 00 00 03 02 00 01 00 0A 28 0A 00 0A 28 81 00 0A 28 77 00 0A 28 E7 06 07 05 04 19 19 19 08 19 19 19 80 19 19 19 8B 19 19 19 E6 `  
  
`06 05 03 02 19 19 19 08 19 19 19 8B 19 19 19 0A 19 19 19 81 03 00 06 07 19 19 19 0A 19 19 19 77 19 19 19 08 19 19 19 80 05 04 02 01 19 19 19 8B 19 19 19 E6 19 19 `  
  
`19 81 19 19 19 E7 00 01 07 04 19 19 19 77 19 19 19 E7 19 19 19 80 19 19 19 E6`

  
  
  
Model 2 and Model 3, skeleton data for 15th part \[at offset
0x00001C60\]:

  

`00 00 00 00 BA FF 3A 00 CD FF 00 00 BA FF 3B 00 9F FF 00 00 46 00 3B 00 9F FF 00 00 46 00 3A 00 CD FF 00 00 00 00 00 00 BD FF 00 00 00 00 01 00 8D FF 00 00 00 00 `  
  
`3A 00 11 FF 00 00 00 00 E7 FF 03 00 00 00 5A 00 3A 00 44 FF 00 00 00 00 F9 FF 34 00 00 00 00 00 3A 00 34 00 00 00 A6 FF 3A 00 44 FF 00 00 3A 00 3C 00 03 00 00 00 `  
  
`C5 FF 3C 00 03 00 00 00 08 0B 06 00 19 19 19 15 19 19 19 D8 19 19 19 83 0D 0C 0A 00 19 19 19 D5 19 19 19 19 19 19 19 76 0C 09 0A 00 19 19 19 19 19 19 19 72 19 19 `  
  
`19 76 09 0D 0A 00 19 19 19 72 19 19 19 D5 19 19 19 76 02 08 05 00 19 19 19 07 19 19 19 15 19 19 19 7A 0B 01 05 00 19 19 19 D8 19 19 19 E8 19 19 19 7A 06 05 08 00 `  
  
`19 19 19 83 19 19 19 7A 19 19 19 15 05 06 0B 00 19 19 19 7A 19 19 19 83 19 19 19 D8 07 03 04 00 19 19 19 86 19 19 19 0F 19 19 19 7A 04 00 07 00 19 19 19 7A 19 19 `  
  
`19 E0 19 19 19 86 05 01 04 00 88 54 00 7A 88 54 00 E8 88 54 00 7A 88 54 00 E0 05 04 02 03 88 54 00 7A 88 54 00 7A 88 54 00 07 88 54 00 0F 07 09 03 0C 19 19 19 86 `  
  
`19 19 19 72 19 19 19 0F 19 19 19 19 02 03 01 00 19 19 19 07 19 19 19 0F 19 19 19 E8 19 19 19 E0 00 03 0D 0C 19 19 19 E0 19 19 19 0F 19 19 19 D5 19 19 19 19 0B 08 `  
  
`01 02 19 19 19 D8 19 19 19 15 19 19 19 E8 19 19 19 07 07 00 09 0D 19 19 19 86 19 19 19 E0 19 19 19 72 19 19 19 D5`

  
  
  
  
Model 4, skeleton data for 1st part \[at offset 0x00001E00\]:

  

`00 00 00 00 5B 00 25 00 E3 FF 00 00 48 00 25 00 B7 FF 00 00 48 00 CF FF B7 FF 00 00 5B 00 C7 FF E3 FF 00 00 41 00 42 00 EE FF 00 00 00 00 C7 FF 0C 00 00 00 00 00 `  
  
`37 00 0C 00 00 00 A5 FF C8 FF E3 FF 00 00 B8 FF CF FF B7 FF 00 00 BF FF 42 00 EE FF 00 00 D3 FF 3E 00 B7 FF 00 00 2D 00 3E 00 B7 FF 00 00 B8 FF 25 00 B7 FF 00 00 `  
  
`A5 FF 26 00 E3 FF 00 00 09 07 0D 00 35 33 29 BB 35 33 29 C9 35 33 29 E8 03 04 00 00 35 33 29 26 35 33 29 35 35 33 29 07 03 07 05 00 35 33 29 26 35 33 29 C9 35 33 `  
  
`29 7E 09 04 06 00 35 33 29 BB 35 33 29 35 35 33 29 76 07 09 05 06 35 33 29 C9 35 33 29 BB 35 33 29 7E 35 33 29 76 03 02 07 08 35 33 29 26 35 33 29 53 35 33 29 C9 `  
  
`35 33 29 9D 03 05 04 06 35 33 29 26 35 33 29 7E 35 33 29 35 35 33 29 76 09 0D 0A 0C 35 33 29 BB 35 33 29 E8 35 33 29 7F 35 33 29 C7 04 09 0B 0A 35 33 29 35 35 33 `  
  
`29 BB 35 33 29 70 35 33 29 7F 07 08 0D 0C 35 33 29 C9 35 33 29 9D 35 33 29 E8 35 33 29 C7 00 01 03 02 35 33 29 07 35 33 29 2A 35 33 29 26 35 33 29 53 04 0B 00 01 `  
  
`35 33 29 35 35 33 29 70 35 33 29 07 35 33 29 2A 0C 01 0A 0B 35 33 29 C7 35 33 29 2A 35 33 29 7F 35 33 29 70 02 01 08 0C 35 33 29 53 35 33 29 2A 35 33 29 9D 35 33 `  
  
`29 C7`

  
  
  
  
Model 4, skeleton data for 2nd part \[at offset 0x00001F7C\]:

  

`00 00 00 00 D5 FF 40 00 F7 FF 00 00 D5 FF 46 00 D1 FF 00 00 2B 00 46 00 D1 FF 00 00 2B 00 40 00 F7 FF 00 00 43 00 DB FF E8 FF 00 00 45 00 DF FF C3 FF 00 00 BB FF `  
  
`DF FF C3 FF 00 00 BD FF DB FF E8 FF 00 00 AB FF D6 FF 51 FF 00 00 AD FF 32 00 5E FF 00 00 BD FF 26 00 F3 FF 00 00 43 00 26 00 F3 FF 00 00 43 00 2B 00 D2 FF 00 00 `  
  
`BD FF 2B 00 D2 FF 00 00 9C FF 34 00 AC FF 00 00 9B FF B9 FF 99 FF 00 00 53 00 32 00 5E FF 00 00 44 00 55 00 AC FF 00 00 BC FF 55 00 AC FF 00 00 66 00 B9 FF 99 FF `  
  
`00 00 55 00 D6 FF 51 FF 00 00 64 00 34 00 AC FF 00 00 D2 FF 38 00 57 FF 00 00 2E 00 38 00 57 FF 00 00 33 00 D7 FF 49 FF 00 00 CD FF D7 FF 49 FF 00 00 11 17 10 00 `  
  
`60 58 26 55 60 58 26 70 60 58 26 2B 18 13 14 00 60 58 26 63 60 58 26 1C 60 58 26 32 10 15 11 00 60 58 26 2B 60 58 26 07 60 58 26 55 0E 09 12 00 60 58 26 E8 60 58 `  
  
`26 C5 60 58 26 9A 16 12 09 00 60 58 26 7F 60 58 26 9A 60 58 26 C5 0F 19 08 00 60 58 26 D0 60 58 26 8C 60 58 26 BE 13 15 14 10 F8 A7 87 1C F8 A7 87 07 F8 A7 87 32 `  
  
`F8 A7 87 2B 0F 08 0E 09 F8 A7 87 D0 F8 A7 87 BE F8 A7 87 E8 F8 A7 87 C5 18 17 19 16 F8 A7 87 63 F8 A7 87 70 F8 A7 87 8C F8 A7 87 7F 15 13 0C 05 60 58 26 07 60 58 `  
  
`26 1C 60 58 26 0C 60 58 26 28 11 02 12 01 60 58 26 55 60 58 26 4E 60 58 26 9A 60 58 26 A0 0E 0D 0F 06 60 58 26 E8 60 58 26 E2 60 58 26 D0 60 58 26 C6 13 0F 05 06 `  
  
`60 58 26 1C 60 58 26 D0 60 58 26 28 60 58 26 C6 0E 12 0D 01 60 58 26 E8 60 58 26 9A 60 58 26 E2 60 58 26 A0 15 0C 11 02 60 58 26 07 60 58 26 0C 60 58 26 55 60 58 `  
  
`26 4E 17 18 10 14 60 58 26 70 60 58 26 63 60 58 26 2B 60 58 26 32 16 09 19 08 60 58 26 7F 60 58 26 C5 60 58 26 8C 60 58 26 BE 11 12 17 16 60 58 26 55 60 58 26 9A `  
  
`60 58 26 70 60 58 26 7F 0F 13 19 18 60 58 26 D0 60 58 26 1C 60 58 26 8C 60 58 26 63 04 07 0B 0A 38 21 19 42 38 21 19 AC 38 21 19 1D 38 21 19 D3 0B 0A 03 00 38 21 `  
  
`19 1D 38 21 19 D3 38 21 19 4D 38 21 19 A2 01 02 00 03 38 21 19 A0 38 21 19 4E 38 21 19 A2 38 21 19 4D 01 00 0D 0A 38 21 19 A0 38 21 19 A2 38 21 19 E2 38 21 19 D3 `  
  
`02 0C 03 0B 38 21 19 4E 38 21 19 0C 38 21 19 4D 38 21 19 1D 05 04 0C 0B 38 21 19 28 38 21 19 42 38 21 19 0C 38 21 19 1D 06 0D 07 0A 38 21 19 C6 38 21 19 E2 38 21 `  
  
`19 AC 38 21 19 D3 06 07 05 04 38 21 19 C6 38 21 19 AC 38 21 19 28 38 21 19 42`

  
  
  
Model 4, skeleton data for 3rd part \[at offset 0x00002254\]:

  

`00 00 00 00 ED FF 16 00 12 00 00 00 ED FF 16 00 D6 FF 00 00 13 00 16 00 D6 FF 00 00 13 00 16 00 12 00 00 00 13 00 F0 FF 12 00 00 00 13 00 F0 FF D6 FF 00 00 ED FF `  
  
`F0 FF D6 FF 00 00 ED FF F0 FF 12 00 00 00 63 00 F8 FF 6C FF 00 00 5D 00 2D 00 6C FF 00 00 2E 00 26 00 E7 FE 00 00 28 00 65 00 14 FF 00 00 4C 00 4B 00 6C FF 00 00 `  
  
`00 00 72 00 6C FF 00 00 1F 00 B7 FF 12 FF 00 00 6A 00 12 00 10 FF 00 00 5A 00 B0 FF 36 FF 00 00 00 00 8D FF 6C FF 00 00 56 00 AC FF 6C FF 00 00 00 00 A5 FF C1 FF `  
  
`00 00 49 00 AF FF AE FF 00 00 43 00 48 00 AC FF 00 00 49 00 19 00 C4 FF 00 00 39 00 4A 00 D2 FF 00 00 5B 00 19 00 91 FF 00 00 78 00 01 00 77 FF 00 00 2F 00 1D 00 `  
  
`E5 FF 00 00 52 00 F8 FF BE FF 00 00 6B 00 F4 FF BB FF 00 00 00 00 49 00 F4 FF 00 00 00 00 6A 00 A9 FF 00 00 7E 00 E6 FF A4 FF 00 00 2F 00 DF FF DE FF 00 00 6A 00 `  
  
`13 00 33 FF 00 00 55 00 29 00 8D FF 00 00 00 00 73 00 BC FF 00 00 AB FF 29 00 8D FF 00 00 96 FF 13 00 33 FF 00 00 D1 FF DF FF DE FF 00 00 82 FF E6 FF A4 FF 00 00 `  
  
`95 FF F4 FF BB FF 00 00 AE FF F8 FF BE FF 00 00 D1 FF 1D 00 E5 FF 00 00 88 FF 01 00 77 FF 00 00 A5 FF 19 00 91 FF 00 00 C7 FF 4A 00 D2 FF 00 00 B7 FF 19 00 C4 FF `  
  
`00 00 BD FF 48 00 AC FF 00 00 B7 FF AF FF AE FF 00 00 AA FF AC FF 6C FF 00 00 A6 FF B0 FF 36 FF 00 00 99 FF 16 00 15 FF 00 00 E3 FF B8 FF 15 FF 00 00 B4 FF 4B 00 `  
  
`6C FF 00 00 D8 FF 52 00 20 FF 00 00 DA FF 25 00 F2 FE 00 00 A3 FF 2D 00 6C FF 00 00 9D FF F8 FF 6C FF 00 00 4E 00 4A 00 32 FF 00 00 00 00 70 00 30 FF 00 00 B2 FF `  
  
`4A 00 32 FF 00 00 00 00 8F FF 3B FF 00 00 83 FF 83 00 03 FF 00 00 BE FF 88 00 30 FF 00 00 A4 FF 60 00 3F FF 00 00 60 FF 7D 00 E3 FF 00 00 EA FF 78 FF E4 FF 00 00 `  
  
`18 00 89 FF E0 FF 00 00 01 00 7C FF 12 00 00 00 09 00 75 FF D0 FF 00 00 0C 15 0D 1E FF FF FF 31 FF FF FF 18 FF FF FF 79 FF 31 33 85 03 04 05 06 35 0D 2F 1E FF FF `  
  
`FF BF FF FF FF 79 FF FF FF D6 FF 33 20 85 08 09 0A 0B 23 17 1D 00 FF FF FF 79 FF FF FF 2C FF FF FF 84 00 01 02 37 2D 23 1D 00 FF FF FF C0 FF FF FF 79 FF FF FF 84 `  
  
`07 00 02 30 15 23 1E 00 F8 A7 87 18 F8 A7 87 79 F8 A7 87 85 17 23 15 00 F8 A7 87 2C F8 A7 87 79 F8 A7 87 18 22 0C 09 00 F8 A7 87 07 F8 A7 87 31 F8 A7 87 07 22 18 `  
  
`15 00 F8 A7 87 07 F8 A7 87 0F F8 A7 87 18 1F 1B 1C 00 F8 A7 87 26 F8 A7 87 29 F8 A7 87 29 1B 1F 08 00 F8 A7 87 29 F8 A7 87 26 F8 A7 87 05 19 18 08 00 F8 A7 87 21 `  
  
`F8 A7 87 0F F8 A7 87 05 08 1F 19 00 F8 A7 87 05 F8 A7 87 26 F8 A7 87 21 1C 19 1F 00 F8 A7 87 29 F8 A7 87 21 F8 A7 87 26 17 1A 1D 00 F8 A7 87 2C F8 A7 87 39 F8 A7 `  
  
`87 84 1C 1B 16 00 F8 A7 87 29 F8 A7 87 29 F8 A7 87 10 1A 16 1B 00 F8 A7 87 39 F8 A7 87 10 F8 A7 87 29 1A 17 16 00 F8 A7 87 39 F8 A7 87 2C F8 A7 87 10 16 15 18 00 `  
  
`F8 A7 87 10 F8 A7 87 18 F8 A7 87 0F 16 17 15 00 F8 A7 87 10 F8 A7 87 2C F8 A7 87 18 0C 22 15 00 F8 A7 87 31 F8 A7 87 07 F8 A7 87 18 1D 1A 2A 00 F8 A7 87 84 F8 A7 `  
  
`87 39 F8 A7 87 B6 23 2F 1E 00 F8 A7 87 79 F8 A7 87 D6 F8 A7 87 85 23 2D 2F 00 F8 A7 87 79 F8 A7 87 C0 F8 A7 87 D6 35 24 38 00 F8 A7 87 BF F8 A7 87 E8 F8 A7 87 E8 `  
  
`2C 24 2F 00 F8 A7 87 E0 F8 A7 87 E8 F8 A7 87 D6 29 27 28 00 F8 A7 87 C4 F8 A7 87 C9 F8 A7 87 C4 27 29 39 00 F8 A7 87 C9 F8 A7 87 C4 F8 A7 87 EB 2A 29 2E 00 F8 A7 `  
  
`87 B6 F8 A7 87 C4 F8 A7 87 DC 2C 2B 39 00 F8 A7 87 E0 F8 A7 87 CF F8 A7 87 EB 27 39 2B 00 F8 A7 87 C9 F8 A7 87 EB F8 A7 87 CF 2B 28 27 00 F8 A7 87 CF F8 A7 87 C4 `  
  
`F8 A7 87 C9 2A 2D 1D 00 F8 A7 87 B6 F8 A7 87 C0 F8 A7 87 84 29 28 2E 00 F8 A7 87 C4 F8 A7 87 C4 F8 A7 87 DC 2D 2A 2E 00 F8 A7 87 C0 F8 A7 87 B6 F8 A7 87 DC 2F 2E `  
  
`2C 00 F8 A7 87 D6 F8 A7 87 DC F8 A7 87 E0 2D 2E 2F 00 F8 A7 87 C0 F8 A7 87 DC F8 A7 87 D6 24 35 2F 00 F8 A7 87 E8 F8 A7 87 BF F8 A7 87 D6 1A 1B 20 00 F8 A7 87 39 `  
  
`F8 A7 87 29 F8 A7 87 40 29 2A 26 00 F8 A7 87 C4 F8 A7 87 B6 F8 A7 87 AE 13 20 14 00 27 17 05 72 27 17 05 40 27 17 05 26 09 08 18 00 27 17 05 07 27 17 05 05 27 17 `  
  
`05 0F 09 18 22 00 27 17 05 07 27 17 05 0F 27 17 05 07 0F 0B 0A 00 27 17 05 15 27 17 05 5C 27 17 05 58 10 21 0F 00 27 17 05 1A 27 17 05 04 27 17 05 15 14 20 1B 00 `  
  
`27 17 05 26 27 17 05 40 27 17 05 29 26 20 13 00 27 17 05 AE 27 17 05 40 27 17 05 72 26 13 30 00 27 17 05 AE 27 17 05 72 27 17 05 C9 39 38 2C 00 27 17 05 EB 27 17 `  
  
`05 E8 27 17 05 E0 2C 38 24 00 27 17 05 E0 27 17 05 E8 27 17 05 E8 25 32 33 00 27 17 05 EE 27 17 05 D4 27 17 05 D8 3C 25 33 00 27 17 05 E5 27 17 05 EE 27 17 05 D8 `  
  
`26 30 29 00 27 17 05 AE 27 17 05 C9 27 17 05 C4 21 3A 0F 00 27 17 05 04 27 17 05 1E 27 17 05 15 3A 0B 0F 00 27 17 05 1E 27 17 05 5C 27 17 05 15 30 11 31 00 27 17 `  
  
`05 C9 27 17 05 68 27 17 05 D0 13 11 30 00 27 17 05 72 27 17 05 68 27 17 05 C9 11 13 14 00 27 17 05 68 27 17 05 72 27 17 05 26 11 14 12 00 27 17 05 68 27 17 05 26 `  
  
`27 17 05 1C 32 3D 34 00 27 17 05 D4 27 17 05 7B 27 17 05 8C 3D 0E 34 00 27 17 05 7B 27 17 05 63 27 17 05 8C 3D 10 0E 00 27 17 05 7B 27 17 05 1A 27 17 05 63 3A 3B `  
  
`0B 00 27 17 05 1E 27 17 05 69 27 17 05 5C 3B 36 0B 00 27 17 05 69 27 17 05 7D 27 17 05 5C 37 0B 36 00 27 17 05 AB 27 17 05 5C 27 17 05 7D 0A 0B 37 00 27 17 05 58 `  
  
`27 17 05 5C 27 17 05 AB 3E 3F 41 00 27 17 05 C7 27 17 05 4E 27 17 05 A6 40 3E 41 00 27 17 05 81 27 17 05 C7 27 17 05 A6 3F 40 41 00 27 17 05 4E 27 17 05 81 27 17 `  
  
`05 A6 3E 3B 3F 00 27 17 05 C7 27 17 05 69 27 17 05 4E 3F 3C 40 00 27 17 05 4E 27 17 05 E5 27 17 05 81 3C 3F 3B 00 27 17 05 E5 27 17 05 4E 27 17 05 69 3E 3C 36 00 `  
  
`27 17 05 C7 27 17 05 E5 27 17 05 7D 3C 3E 40 00 27 17 05 E5 27 17 05 C7 27 17 05 81 3B 3E 36 00 27 17 05 69 27 17 05 C7 27 17 05 7D 21 08 09 00 B3 1C 1C 04 B3 1C `  
  
`1C 05 B3 1C 1C 07 39 25 38 00 B3 1C 1C EB B3 1C 1C EE B3 1C 1C E8 43 11 45 00 B3 1C 1C 18 B3 1C 1C 83 B3 1C 1C 54 44 43 45 00 B3 1C 1C 82 B3 1C 1C 18 B3 1C 1C 54 `  
  
`42 44 45 00 B3 1C 1C ED B3 1C 1C 82 B3 1C 1C 54 11 42 45 00 B3 1C 1C 83 B3 1C 1C ED B3 1C 1C 54 23 17 1D 00 F8 A7 87 79 F8 A7 87 2C F8 A7 87 84 2D 23 1D 00 F8 A7 `  
  
`87 C0 F8 A7 87 79 F8 A7 87 84 06 01 07 00 F8 A7 87 C1 F8 A7 87 C5 F8 A7 87 C6 F8 A7 87 C0 03 02 04 05 F8 A7 87 2C F8 A7 87 2B F8 A7 87 28 F8 A7 87 2F 06 07 05 04 `  
  
`F8 A7 87 C1 F8 A7 87 C6 F8 A7 87 2F F8 A7 87 28 03 00 02 01 F8 A7 87 2C F8 A7 87 C0 F8 A7 87 2B F8 A7 87 C5 1C 16 19 18 F8 A7 87 29 F8 A7 87 10 F8 A7 87 21 F8 A7 `  
  
`87 0F 1A 20 2A 26 F8 A7 87 39 F8 A7 87 40 F8 A7 87 B6 F8 A7 87 AE 28 2B 2E 2C F8 A7 87 C4 F8 A7 87 CF F8 A7 87 DC F8 A7 87 E0 08 12 1B 14 27 17 05 05 27 17 05 1C `  
  
`27 17 05 29 27 17 05 26 37 36 33 3C 27 17 05 AB 27 17 05 7D 27 17 05 D8 27 17 05 E5 39 29 31 30 27 17 05 EB 27 17 05 C4 27 17 05 D0 27 17 05 C9 37 33 34 32 27 17 `  
  
`05 AB 27 17 05 D8 27 17 05 8C 27 17 05 D4 0A 0E 0F 10 27 17 05 58 27 17 05 63 27 17 05 15 27 17 05 1A 0A 37 0E 34 27 17 05 58 27 17 05 AB 27 17 05 63 27 17 05 8C `  
  
`3B 3A 0D 0C B3 1C 1C 69 B3 1C 1C 1E B3 1C 1C 79 B3 1C 1C 31 3B 0D 3C 35 B3 1C 1C 69 B3 1C 1C 79 B3 1C 1C E5 B3 1C 1C BF 3A 21 0C 09 B3 1C 1C 1E B3 1C 1C 04 B3 1C `  
  
`1C 31 B3 1C 1C 07 10 3D 12 11 B3 1C 1C 1A B3 1C 1C 7B B3 1C 1C 1C B3 1C 1C 68 32 31 3D 11 B3 1C 1C D4 B3 1C 1C D0 B3 1C 1C 7B B3 1C 1C 68 3C 35 25 38 B3 1C 1C E5 `  
  
`B3 1C 1C BF B3 1C 1C EE B3 1C 1C E8 21 10 08 12 B3 1C 1C 04 B3 1C 1C 1A B3 1C 1C 05 B3 1C 1C 1C 25 39 32 31 B3 1C 1C EE B3 1C 1C EB B3 1C 1C D4 B3 1C 1C D0 11 43 `  
  
`42 44 B3 1C 1C 83 B3 1C 1C 18 B3 1C 1C ED B3 1C 1C 82 35 0D 2F 1E F8 A7 87 BF F8 A7 87 79 F8 A7 87 D6 F8 A7 87 85 0C 15 0D 1E F8 A7 87 31 F8 A7 87 18 F8 A7 87 79 `  
  
`F8 A7 87 85 01 1C 14 78 00 1C 14 78 00 1C 14 78 10 A0 1F AA 10 BC 20 02 23 1B 3F 02 3F 1A 00 AA 00 02 1F 02 03 1B 1F 1A 02 01 00 00`

  
  
  
Model 4, skeleton data for 4th part \[at offset 0x00002BC8\]:

  

`00 00 00 00 D9 FF E6 FF 24 00 00 00 DC FF 2C 00 EB FF 00 00 F1 FF 10 00 C6 FF 00 00 0B 00 2C 00 EB FF 00 00 09 00 19 00 23 00 00 00 33 00 00 00 F9 FF 00 00 D9 FF `  
  
`17 00 23 00 00 00 BA FF 00 00 FF FF 00 00 09 00 E7 FF 24 00 00 00 0F 00 10 00 A9 FF 00 00 F1 FF 10 00 A9 FF 00 00 F1 FF F1 FF A9 FF 00 00 0F 00 F1 FF A9 FF 00 00 `  
  
`0B 00 D4 FF EB FF 00 00 0F 00 F1 FF C6 FF 00 00 F1 FF F1 FF C6 FF 00 00 0F 00 10 00 C6 FF 00 00 DC FF D1 FF EC FF 00 00 03 05 04 00 F8 A7 87 4B F8 A7 87 00 F8 A7 `  
  
`87 52 07 01 06 00 F8 A7 87 EF F8 A7 87 A5 F8 A7 87 9C 11 07 00 00 F8 A7 87 A1 F8 A7 87 EF F8 A7 87 9E 10 05 03 00 F8 A7 87 27 F8 A7 87 00 F8 A7 87 4B 05 0E 0D 00 `  
  
`F8 A7 87 00 F8 A7 87 1B F8 A7 87 54 02 07 0F 00 F8 A7 87 C5 F8 A7 87 EF F8 A7 87 B9 0F 07 11 00 F8 A7 87 B9 F8 A7 87 EF F8 A7 87 A1 10 0E 05 00 F8 A7 87 27 F8 A7 `  
  
`87 1B F8 A7 87 00 07 02 01 00 F8 A7 87 EF F8 A7 87 C5 F8 A7 87 A5 08 05 0D 00 F8 A7 87 51 F8 A7 87 00 F8 A7 87 54 04 05 08 00 F8 A7 87 52 F8 A7 87 00 F8 A7 87 51 `  
  
`08 0D 00 11 F8 A7 87 51 F8 A7 87 54 F8 A7 87 9E F8 A7 87 A1 11 0D 0F 0E F8 A7 87 A1 F8 A7 87 54 F8 A7 87 B9 F8 A7 87 1B 09 0C 10 0E F8 A7 87 2B F8 A7 87 2F F8 A7 `  
  
`87 27 F8 A7 87 1B 02 0A 10 09 F8 A7 87 C5 F8 A7 87 C5 F8 A7 87 27 F8 A7 87 2B 02 0F 0A 0B F8 A7 87 C5 F8 A7 87 B9 F8 A7 87 C5 F8 A7 87 C1 0B 0F 0C 0E F8 A7 87 C1 `  
  
`F8 A7 87 B9 F8 A7 87 2F F8 A7 87 1B 0C 09 0B 0A F8 A7 87 2F F8 A7 87 2B F8 A7 87 C1 F8 A7 87 C5 06 01 04 03 F8 A7 87 9C F8 A7 87 A5 F8 A7 87 52 F8 A7 87 4B 03 01 `  
  
`10 02 F8 A7 87 4B F8 A7 87 A5 F8 A7 87 27 F8 A7 87 C5 06 04 00 08 F8 A7 87 9C F8 A7 87 52 F8 A7 87 9E F8 A7 87 51`

  
  
  
Model 4, skeleton data for 5th part \[at offset 0x00002DD4\]:

  

`00 00 00 00 28 00 D9 FF 7E FF 00 00 D8 FF D9 FF 7E FF 00 00 D8 FF D9 FF B7 FF 00 00 28 00 D9 FF B7 FF 00 00 D8 FF 28 00 7E FF 00 00 28 00 28 00 7E FF 00 00 28 00 `  
  
`28 00 B7 FF 00 00 D8 FF 28 00 B7 FF 00 00 0F 00 F1 FF 00 00 00 00 F1 FF F1 FF 00 00 00 00 F1 FF 10 00 00 00 00 00 0F 00 10 00 00 00 00 00 0F 00 F1 FF DF FF 00 00 `  
  
`F1 FF F1 FF DF FF 00 00 F1 FF 10 00 DF FF 00 00 0F 00 10 00 DF FF 00 00 03 00 02 01 22 25 1D 26 22 25 1D 2F 22 25 1D C9 22 25 1D C1 06 07 05 04 22 25 1D 18 22 25 `  
  
`1D D6 22 25 1D 2B 22 25 1D C5 04 01 05 00 22 25 1D C5 22 25 1D C1 22 25 1D 2B 22 25 1D 2F 06 05 03 00 22 25 1D 18 22 25 1D 2B 22 25 1D 26 22 25 1D 2F 04 07 01 02 `  
  
`22 25 1D C5 22 25 1D D6 22 25 1D C1 22 25 1D C9 03 02 0C 0D 22 25 1D 26 22 25 1D C9 22 25 1D 26 22 25 1D C9 02 07 0D 0E 22 25 1D C9 22 25 1D D6 22 25 1D C9 22 25 `  
  
`1D D5 06 0F 07 0E 22 25 1D 18 22 25 1D 19 22 25 1D D6 22 25 1D D5 06 03 0F 0C 22 25 1D 18 22 25 1D 26 22 25 1D 19 22 25 1D 26 0A 0B 09 08 F8 A7 87 C0 F8 A7 87 2C `  
  
`F8 A7 87 C6 F8 A7 87 28 09 08 0D 0C F8 A7 87 C6 F8 A7 87 28 F8 A7 87 C9 F8 A7 87 26 0B 0F 08 0C F8 A7 87 2C F8 A7 87 19 F8 A7 87 28 F8 A7 87 26 0E 0F 0A 0B F8 A7 `  
  
`87 D5 F8 A7 87 19 F8 A7 87 C0 F8 A7 87 2C 0A 09 0E 0D F8 A7 87 C0 F8 A7 87 C6 F8 A7 87 D5 F8 A7 87 C9`

  
  
  
Model 4, skeleton data for 6th part \[at offset 0x00002F70\]:

  

`00 00 00 00 26 00 DA FF 00 00 00 00 DA FF DA FF 00 00 00 00 DA FF 27 00 00 00 00 00 26 00 27 00 00 00 00 00 20 00 21 00 C2 FF 00 00 E0 FF 21 00 C2 FF 00 00 E0 FF `  
  
`E0 FF C2 FF 00 00 20 00 E0 FF C2 FF 00 00 00 03 07 04 F8 A7 87 28 F8 A7 87 2C F8 A7 87 2F F8 A7 87 43 01 00 06 07 F8 A7 87 C6 F8 A7 87 28 F8 A7 87 C1 F8 A7 87 2F `  
  
`01 06 02 05 F8 A7 87 C6 F8 A7 87 C1 F8 A7 87 C0 F8 A7 87 AD 02 05 03 04 F8 A7 87 C0 F8 A7 87 AD F8 A7 87 2C F8 A7 87 43 04 05 07 06 F8 A7 87 43 F8 A7 87 AD F8 A7 `  
  
`87 2F F8 A7 87 C1 02 03 01 00 F8 A7 87 C0 F8 A7 87 2C F8 A7 87 C6 F8 A7 87 28`

  
  
  
Model 4, skeleton data for 7th part \[at offset 0x0000302C\]:

  

`00 00 00 00 24 00 D1 FF EC FF 00 00 F1 FF 10 00 C6 FF 00 00 0F 00 F1 FF C6 FF 00 00 F1 FF F1 FF C6 FF 00 00 F5 FF D4 FF EB FF 00 00 F1 FF F1 FF A9 FF 00 00 0F 00 `  
  
`F1 FF A9 FF 00 00 0F 00 10 00 A9 FF 00 00 F1 FF 10 00 A9 FF 00 00 F7 FF E7 FF 24 00 00 00 46 00 00 00 FF FF 00 00 27 00 17 00 23 00 00 00 CD FF 00 00 F9 FF 00 00 `  
  
`F7 FF 19 00 23 00 00 00 F5 FF 2C 00 EB FF 00 00 0F 00 10 00 C6 FF 00 00 24 00 2C 00 EB FF 00 00 27 00 E6 FF 24 00 00 00 0C 0E 0D 00 F8 A7 87 EC F8 A7 87 A5 F8 A7 `  
  
`87 9C 10 0A 0B 00 F8 A7 87 4B F8 A7 87 03 F8 A7 87 52 0A 00 11 00 F8 A7 87 03 F8 A7 87 4F F8 A7 87 51 0C 01 0E 00 F8 A7 87 EC F8 A7 87 CA F8 A7 87 A5 03 0C 04 00 `  
  
`F8 A7 87 D4 F8 A7 87 EC F8 A7 87 9B 0A 0F 02 00 F8 A7 87 03 F8 A7 87 2B F8 A7 87 37 0A 02 00 00 F8 A7 87 03 F8 A7 87 37 F8 A7 87 4F 03 01 0C 00 F8 A7 87 D4 F8 A7 `  
  
`87 CA F8 A7 87 EC 0F 0A 10 00 F8 A7 87 2B F8 A7 87 03 F8 A7 87 4B 0C 09 04 00 F8 A7 87 EC F8 A7 87 9E F8 A7 87 9B 0D 09 0C 00 F8 A7 87 9C F8 A7 87 9E F8 A7 87 EC `  
  
`09 11 04 00 F8 A7 87 9E F8 A7 87 51 F8 A7 87 9B F8 A7 87 4F 0B 11 0D 09 F8 A7 87 52 F8 A7 87 51 F8 A7 87 9C F8 A7 87 9E 0E 01 10 0F F8 A7 87 A5 F8 A7 87 CA F8 A7 `  
  
`87 4B F8 A7 87 2B 00 02 04 03 F8 A7 87 4F F8 A7 87 37 F8 A7 87 9B F8 A7 87 D4 08 01 05 03 F8 A7 87 C5 F8 A7 87 CA F8 A7 87 C1 F8 A7 87 D4 01 08 0F 07 F8 A7 87 CA `  
  
`F8 A7 87 C5 F8 A7 87 2B F8 A7 87 2B 02 0F 06 07 F8 A7 87 37 F8 A7 87 2B F8 A7 87 2F F8 A7 87 2B 06 05 02 03 F8 A7 87 2F F8 A7 87 C1 F8 A7 87 37 F8 A7 87 D4 08 05 `  
  
`07 06 F8 A7 87 C5 F8 A7 87 C1 F8 A7 87 2B F8 A7 87 2F 0B 0D 10 0E F8 A7 87 52 F8 A7 87 9C F8 A7 87 4B F8 A7 87 A5`

  
  
  
Model 4, skeleton data for 8th part \[at offset 0x00003238\]:

  

`00 00 00 00 F1 FF 10 00 DF FF 00 00 0F 00 10 00 DF FF 00 00 0F 00 F1 FF DF FF 00 00 F1 FF F1 FF DF FF 00 00 F1 FF 10 00 00 00 00 00 0F 00 10 00 00 00 00 00 0F 00 `  
  
`F1 FF 00 00 00 00 F1 FF F1 FF 00 00 00 00 28 00 28 00 B7 FF 00 00 D8 FF 28 00 B7 FF 00 00 D8 FF 28 00 7E FF 00 00 28 00 28 00 7E FF 00 00 D8 FF D9 FF B7 FF 00 00 `  
  
`28 00 D9 FF B7 FF 00 00 28 00 D9 FF 7E FF 00 00 D8 FF D9 FF 7E FF 00 00 0D 0E 0C 0F 22 25 1D 26 22 25 1D 2F 22 25 1D C9 22 25 1D C1 09 0A 08 0B 22 25 1D D6 22 25 `  
  
`1D C5 22 25 1D 18 22 25 1D 2B 0A 0F 0B 0E 22 25 1D C5 22 25 1D C1 22 25 1D 2B 22 25 1D 2F 0A 09 0F 0C 22 25 1D C5 22 25 1D D6 22 25 1D C1 22 25 1D C9 0D 08 0E 0B `  
  
`22 25 1D 26 22 25 1D 18 22 25 1D 2F 22 25 1D 2B 0C 03 0D 02 22 25 1D C9 22 25 1D C9 22 25 1D 26 22 25 1D 26 0D 02 08 01 22 25 1D 26 22 25 1D 26 22 25 1D 18 22 25 `  
  
`1D 19 08 01 09 00 22 25 1D 18 22 25 1D 19 22 25 1D D6 22 25 1D D5 09 00 0C 03 22 25 1D D6 22 25 1D D5 22 25 1D C9 22 25 1D C9 05 06 04 07 F8 A7 87 2C F8 A7 87 28 `  
  
`F8 A7 87 C0 F8 A7 87 C6 07 06 03 02 F8 A7 87 C6 F8 A7 87 28 F8 A7 87 C9 F8 A7 87 26 03 00 07 04 F8 A7 87 C9 F8 A7 87 D5 F8 A7 87 C6 F8 A7 87 C0 01 05 00 04 F8 A7 `  
  
`87 19 F8 A7 87 2C F8 A7 87 D5 F8 A7 87 C0 01 02 05 06 F8 A7 87 19 F8 A7 87 26 F8 A7 87 2C F8 A7 87 28`

  
  
  
Model 4, skeleton data for 9th part \[at offset 0x000033D4\]:

  

`00 00 00 00 E0 FF E0 FF C2 FF 00 00 20 00 E0 FF C2 FF 00 00 20 00 21 00 C2 FF 00 00 E0 FF 21 00 C2 FF 00 00 DA FF 27 00 00 00 00 00 26 00 27 00 00 00 00 00 26 00 `  
  
`DA FF 00 00 00 00 DA FF DA FF 00 00 00 00 04 07 03 00 F8 A7 87 C0 F8 A7 87 C6 F8 A7 87 AD F8 A7 87 C1 06 01 07 00 F8 A7 87 28 F8 A7 87 2F F8 A7 87 C6 F8 A7 87 C1 `  
  
`05 02 06 01 F8 A7 87 2C F8 A7 87 43 F8 A7 87 28 F8 A7 87 2F 05 04 02 03 F8 A7 87 2C F8 A7 87 C0 F8 A7 87 43 F8 A7 87 AD 03 00 02 01 F8 A7 87 AD F8 A7 87 C1 F8 A7 `  
  
`87 43 F8 A7 87 2F 05 06 04 07 F8 A7 87 2C F8 A7 87 28 F8 A7 87 C0 F8 A7 87 C6`

  
  
  
Model 4, skeleton data for 10th part \[at offset 0x00003490\]:

  

`00 00 00 00 33 00 E6 FF 1C 00 00 00 0C 00 BA FF 1C 00 00 00 0C 00 1A 00 1C 00 00 00 E6 FF E4 FF 1C 00 00 00 0C 00 A8 FF 65 FF 00 00 BE FF FF FF 65 FF 00 00 0C 00 `  
  
`4D 00 65 FF 00 00 5B 00 FF FF 65 FF 00 00 07 00 02 00 35 33 29 08 35 33 29 20 35 33 29 77 05 02 03 00 35 33 29 D8 35 33 29 77 35 33 29 CC 07 02 06 00 35 33 29 08 `  
  
`35 33 29 77 35 33 29 6E 02 05 06 00 35 33 29 77 35 33 29 D8 35 33 29 6E 07 04 00 01 35 33 29 08 35 33 29 8B 35 33 29 20 35 33 29 57 04 05 01 03 35 33 29 8B 35 33 `  
  
`29 D8 35 33 29 57 35 33 29 CC 04 07 05 06 35 33 29 8B 35 33 29 08 35 33 29 D8 35 33 29 6E 02 00 03 01 35 33 29 77 35 33 29 20 35 33 29 CC 35 33 29 57`

  
  
  
Model 4, skeleton data for 11th part \[at offset 0x00003564\]:

  

`00 00 00 00 3E 00 00 00 A1 FF 00 00 3E 00 F4 FF D5 FF 00 00 0C 00 27 00 D9 FF 00 00 0C 00 2C 00 C0 FF 00 00 DB FF F4 FF D5 FF 00 00 DB FF 00 00 A1 FF 00 00 0C 00 `  
  
`CF FF 98 FF 00 00 0C 00 C4 FF CC FF 00 00 59 00 FF FF 06 00 00 00 0C 00 4D 00 06 00 00 00 C0 FF FF FF 06 00 00 00 0C 00 A8 FF 06 00 00 00 39 00 00 00 3B FF 00 00 `  
  
`39 00 00 00 A1 FF 00 00 0C 00 2B 00 C0 FF 00 00 0C 00 2B 00 3B FF 00 00 E0 FF 00 00 3B FF 00 00 0C 00 D4 FF 3B FF 00 00 E0 FF 00 00 A1 FF 00 00 0C 00 D4 FF 99 FF `  
  
`00 00 0C 00 E9 FF 42 00 00 00 09 08 14 00 35 33 29 79 35 33 29 04 35 33 29 6D 0A 09 14 00 35 33 29 EA 35 33 29 79 35 33 29 6D 0B 0A 14 00 35 33 29 86 35 33 29 EA `  
  
`35 33 29 6D 08 0B 14 00 35 33 29 04 35 33 29 86 35 33 29 6D 13 12 0D 00 CC CC CC 81 CC CC CC DA CC CC CC 16 0D 12 0E 00 CC CC CC 16 CC CC CC DA CC CC CC 76 05 06 `  
  
`00 00 87 91 97 CF 87 91 97 8B 87 91 97 21 0B 07 0A 04 35 33 29 86 35 33 29 7B 35 33 29 EA 35 33 29 EF 0B 08 07 01 35 33 29 86 35 33 29 04 35 33 29 7B 35 33 29 03 `  
  
`0A 04 09 02 35 33 29 EA 35 33 29 EF 35 33 29 79 35 33 29 6E 08 09 01 02 35 33 29 04 35 33 29 79 35 33 29 03 35 33 29 6E 0D 0C 13 11 3C 21 1A 16 3C 21 1A 08 3C 21 `  
  
`1A 81 3C 21 1A 8B 10 12 11 13 3C 21 1A E6 3C 21 1A DA 3C 21 1A 8B 3C 21 1A 81 0F 0C 0E 0D 3C 21 1A 6E 3C 21 1A 08 3C 21 1A 76 3C 21 1A 16 0F 0E 10 12 3C 21 1A 6E `  
  
`3C 21 1A 76 3C 21 1A E6 3C 21 1A DA 05 04 06 07 87 91 97 CF 87 91 97 EF 87 91 97 8B 87 91 97 7B 00 06 01 07 87 91 97 21 87 91 97 8B 87 91 97 03 87 91 97 7B 01 02 `  
  
`00 03 19 19 0F 03 19 19 0F 6E 19 19 0F 21 19 19 0F 69`

  
  
  
Model 4, skeleton data for 12th part \[at offset 0x0000375C\]:

  

`00 00 00 00 49 00 E7 FF 06 00 00 00 2B 00 E1 FF 33 FF 00 00 EE FF E1 FF 33 FF 00 00 D0 FF E7 FF 06 00 00 00 D0 FF 23 00 FC FF 00 00 EE FF 00 00 2E FF 00 00 2B 00 `  
  
`00 00 2E FF 00 00 49 00 23 00 FC FF 00 00 0C 00 05 00 3F 00 00 00 0C 00 2D 00 38 00 00 00 00 03 08 00 3C 21 1A 26 3C 21 1A C9 3C 21 1A 73 04 07 09 00 23 1E 1D D6 `  
  
`23 1E 1D 18 23 1E 1D 77 02 01 05 06 3C 21 1A B9 3C 21 1A 37 3C 21 1A AD 3C 21 1A 43 03 04 08 09 3C 21 1A C9 3C 21 1A D6 3C 21 1A 73 3C 21 1A 77 00 08 07 09 3C 21 `  
  
`1A 26 3C 21 1A 73 3C 21 1A 18 3C 21 1A 77 00 07 01 06 3C 21 1A 26 3C 21 1A 18 3C 21 1A 37 3C 21 1A 43 03 02 04 05 3C 21 1A C9 3C 21 1A B9 3C 21 1A D6 3C 21 1A AD `  
  
`00 01 03 02 3C 21 1A 26 3C 21 1A 37 3C 21 1A C9 3C 21 1A B9 07 04 06 05 23 1E 1D 18 23 1E 1D D6 23 1E 1D 43 23 1E 1D AD`

  
  
  
Model 4, skeleton data for 13th part \[at offset 0x0000385C\]:

  

`00 00 00 00 A5 FF FF FF 65 FF 00 00 F4 FF 4D 00 65 FF 00 00 42 00 FF FF 65 FF 00 00 F4 FF A8 FF 65 FF 00 00 1A 00 E4 FF 1C 00 00 00 F4 FF 1A 00 1C 00 00 00 F4 FF `  
  
`BA FF 1C 00 00 00 CD FF E6 FF 1C 00 00 00 07 00 05 00 35 33 29 CC 35 33 29 E6 35 33 29 77 05 02 04 00 35 33 29 77 35 33 29 15 35 33 29 20 02 05 01 00 35 33 29 15 `  
  
`35 33 29 77 35 33 29 6E 05 00 01 00 35 33 29 77 35 33 29 E6 35 33 29 6E 00 07 03 06 35 33 29 E6 35 33 29 CC 35 33 29 65 35 33 29 98 03 06 02 04 35 33 29 65 35 33 `  
  
`29 98 35 33 29 15 35 33 29 20 03 02 00 01 35 33 29 65 35 33 29 15 35 33 29 E6 35 33 29 6E 05 04 07 06 35 33 29 77 35 33 29 20 35 33 29 CC 35 33 29 98`

  
  
  
Model 4, skeleton data for 14th part \[at offset 0x00003930\]:

  

`00 00 00 00 F4 FF E9 FF 42 00 00 00 F4 FF D4 FF 99 FF 00 00 20 00 00 00 A1 FF 00 00 F4 FF D4 FF 3B FF 00 00 20 00 00 00 3B FF 00 00 F4 FF 2B 00 3B FF 00 00 F4 FF `  
  
`2B 00 C0 FF 00 00 C7 FF 00 00 A1 FF 00 00 C7 FF 00 00 3B FF 00 00 F4 FF A8 FF 06 00 00 00 40 00 FF FF 06 00 00 00 F4 FF 4D 00 06 00 00 00 A7 FF FF FF 06 00 00 00 `  
  
`F4 FF C4 FF CC FF 00 00 F4 FF CF FF 98 FF 00 00 25 00 00 00 A1 FF 00 00 25 00 F4 FF D5 FF 00 00 F4 FF 2C 00 C0 FF 00 00 F4 FF 27 00 D9 FF 00 00 C2 FF F4 FF D5 FF `  
  
`00 00 C2 FF 00 00 A1 FF 00 00 0C 0B 00 00 35 33 29 EA 35 33 29 79 35 33 29 82 0B 0A 00 00 35 33 29 79 35 33 29 04 35 33 29 82 0A 09 00 00 35 33 29 04 35 33 29 86 `  
  
`35 33 29 82 09 0C 00 00 35 33 29 86 35 33 29 EA 35 33 29 82 07 02 01 00 CC CC CC DA CC CC CC 16 CC CC CC 81 02 07 06 00 CC CC CC 16 CC CC CC DA CC CC CC 76 0E 0F `  
  
`14 00 87 91 97 65 87 91 97 21 87 91 97 CF 09 0A 0D 10 35 33 29 86 35 33 29 04 35 33 29 7B 35 33 29 03 09 0D 0C 13 35 33 29 86 35 33 29 7B 35 33 29 EA 35 33 29 EF `  
  
`0A 0B 10 12 35 33 29 04 35 33 29 79 35 33 29 03 35 33 29 6E 0C 13 0B 12 35 33 29 EA 35 33 29 EF 35 33 29 79 35 33 29 6E 08 07 03 01 3C 21 1A E6 3C 21 1A DA 3C 21 `  
  
`1A 65 3C 21 1A 81 02 04 01 03 3C 21 1A 16 3C 21 1A 08 3C 21 1A 81 3C 21 1A 65 06 07 05 08 3C 21 1A 76 3C 21 1A DA 3C 21 1A 6E 3C 21 1A E6 06 05 02 04 3C 21 1A 76 `  
  
`3C 21 1A 6E 3C 21 1A 16 3C 21 1A 08 0F 0E 10 0D 87 91 97 21 87 91 97 65 87 91 97 03 87 91 97 7B 14 13 0E 0D 87 91 97 CF 87 91 97 EF 87 91 97 65 87 91 97 7B 10 12 `  
  
`0F 11 19 19 0F 03 19 19 0F 6E 19 19 0F 21 19 19 0F 85`

  
  
  
Model 4, skeleton data for 15th part \[at offset 0x00003B28\]:

  

`00 00 00 00 F4 FF 2D 00 38 00 00 00 F4 FF 05 00 3F 00 00 00 B7 FF 23 00 FC FF 00 00 D5 FF 00 00 2E FF 00 00 12 00 00 00 2E FF 00 00 30 00 23 00 FC FF 00 00 30 00 `  
  
`E7 FF 06 00 00 00 12 00 E1 FF 33 FF 00 00 D5 FF E1 FF 33 FF 00 00 B7 FF E7 FF 06 00 00 00 06 09 01 00 3C 21 1A 26 3C 21 1A C9 3C 21 1A 7C 02 05 00 00 23 1E 1D D6 `  
  
`23 1E 1D 18 23 1E 1D 77 04 03 07 08 3C 21 1A 43 3C 21 1A AD 3C 21 1A 37 3C 21 1A B9 05 06 00 01 3C 21 1A 18 3C 21 1A 26 3C 21 1A 77 3C 21 1A 7C 02 00 09 01 3C 21 `  
  
`1A D6 3C 21 1A 77 3C 21 1A C9 3C 21 1A 7C 02 09 03 08 3C 21 1A D6 3C 21 1A C9 3C 21 1A AD 3C 21 1A B9 05 04 06 07 3C 21 1A 18 3C 21 1A 43 3C 21 1A 26 3C 21 1A 37 `  
  
`09 06 08 07 3C 21 1A C9 3C 21 1A 26 3C 21 1A B9 3C 21 1A 37 02 03 05 04 23 1E 1D D6 23 1E 1D AD 23 1E 1D 18 23 1E 1D 43`

  
  
  
  
Model 5, skeleton data for 1st part \[at offset 0x00003C28\]:

  

`00 00 00 00 3A 00 C7 FF C5 FF 00 00 54 00 AC FF EF FF 00 00 54 00 2A 00 EF FF 00 00 00 00 C7 FF 19 00 00 00 00 00 2A 00 19 00 00 00 AC FF AC FF EF FF 00 00 C6 FF `  
  
`C7 FF C5 FF 00 00 AC FF 2A 00 EF FF 00 00 C6 FF 2A 00 C5 FF 00 00 3A 00 2A 00 C5 FF 00 00 C6 FF 2A 00 B1 FF 00 00 C6 FF C7 FF B1 FF 00 00 3A 00 C7 FF B1 FF 00 00 `  
  
`3A 00 2A 00 B1 FF 00 00 D9 FF 2A 00 06 00 00 00 67 00 14 00 19 00 00 00 57 00 1A 00 BF FF 00 00 57 00 D7 FF BF FF 00 00 67 00 DD FF 19 00 00 00 52 00 14 00 26 00 `  
  
`00 00 35 00 1A 00 B5 FF 00 00 52 00 DD FF 26 00 00 00 35 00 D7 FF B5 FF 00 00 03 0E 04 00 24 12 00 73 24 12 00 A2 24 12 00 76 01 05 03 00 7F 6B 23 1C 7F 6B 23 D0 `  
  
`7F 6B 23 73 09 02 0E 04 24 12 00 1E 24 12 00 18 24 12 00 A2 24 12 00 76 0D 0C 09 00 24 12 00 2B 24 12 00 2F 24 12 00 1E 24 12 00 1B 14 10 13 0F 24 12 00 C5 24 12 `  
  
`00 2B 24 12 00 9C 24 12 00 18 11 12 10 0F 24 12 00 37 24 12 00 22 24 12 00 2B 24 12 00 18 11 10 16 14 24 12 00 37 24 12 00 2B 24 12 00 C1 24 12 00 C5 16 15 11 12 `  
  
`24 12 00 C1 24 12 00 9E 24 12 00 37 24 12 00 22 15 13 12 0F 24 12 00 9E 24 12 00 9C 24 12 00 22 24 12 00 18 14 13 16 15 24 12 00 C5 24 12 00 9C 24 12 00 C1 24 12 `  
  
`00 9E 01 02 00 09 24 12 00 1C 24 12 00 18 24 12 00 1B 24 12 00 1E 0B 06 0C 00 24 12 00 C1 24 12 00 D4 24 12 00 2F 24 12 00 1B 0A 08 0B 06 24 12 00 C5 24 12 00 D1 `  
  
`24 12 00 C1 24 12 00 D4 0A 0B 0D 0C 24 12 00 C5 24 12 00 C1 24 12 00 2B 24 12 00 2F 01 00 05 06 7F 6B 23 1C 7F 6B 23 1B 7F 6B 23 D0 7F 6B 23 D4 07 05 08 06 7F 6B `  
  
`23 D6 7F 6B 23 D0 7F 6B 23 D1 7F 6B 23 D4 05 07 03 0E 7F 6B 23 D0 7F 6B 23 D6 7F 6B 23 73 7F 6B 23 A2 09 0E 08 07 7F 6B 23 1E 7F 6B 23 A2 7F 6B 23 D1 7F 6B 23 D6 `  
  
`01 03 02 04 7F 6B 23 1C 7F 6B 23 73 7F 6B 23 18 7F 6B 23 76 0A 0D 08 09 CC CC CC C5 CC CC CC 2B CC CC CC D1 CC CC CC 1E`

  
  
  
  
Model 5, skeleton data for 2nd part \[at offset 0x00003E6C\]:

  

`00 00 00 00 4F 00 E8 FF 79 FF 00 00 36 00 CD FF E8 FF 00 00 36 00 20 00 F7 FF 00 00 37 00 3C 00 95 FF 00 00 B1 FF E8 FF 79 FF 00 00 C9 FF CD FF E8 FF 00 00 C9 FF `  
  
`3C 00 95 FF 00 00 CA FF 20 00 F7 FF 00 00 44 00 58 00 BB FF 00 00 BC FF 58 00 BB FF 00 00 95 FF C9 FF B5 FF 00 00 66 00 C9 FF B5 FF 00 00 00 00 61 00 BD FF 00 00 `  
  
`3F 00 C6 FF E7 FF 00 00 36 00 CA FF F9 FF 00 00 36 00 26 00 09 00 00 00 3F 00 2D 00 F9 FF 00 00 BF FF C6 FF E7 FF 00 00 C9 FF CA FF F9 FF 00 00 C1 FF 2D 00 F9 FF `  
  
`00 00 CA FF 26 00 09 00 00 00 00 00 E2 FF 60 FF 00 00 64 00 3D 00 BA FF 00 00 9C FF 3D 00 BA FF 00 00 36 00 FE FF 6E FF 00 00 CA FF FE FF 6E FF 00 00 B1 FF 16 00 `  
  
`81 FF 00 00 4F 00 16 00 81 FF 00 00 17 09 07 00 7F 7F 7F E0 7F 7F 7F 9A 7F 7F 7F A6 02 07 0C 00 7F 7F 7F 4A 7F 7F 7F A6 7F 7F 7F 79 06 0C 09 00 7F 7F 7F 7F 7F 7F `  
  
`7F 79 7F 7F 7F 9A 09 17 06 00 7F 7F 7F 9A 7F 7F 7F E0 7F 7F 7F 7F 0A 15 04 00 7F 7F 7F D0 7F 7F 7F 6B 7F 7F 7F BE 0C 03 08 00 7F 7F 7F 79 7F 7F 7F 70 7F 7F 7F 55 `  
  
`0C 07 09 00 7F 7F 7F 79 7F 7F 7F A6 7F 7F 7F 9A 02 0C 08 00 7F 7F 7F 4A 7F 7F 7F 79 7F 7F 7F 55 15 0B 00 00 7F 7F 7F 6B 7F 7F 7F 1C 7F 7F 7F 32 15 0A 0B 00 7F 7F `  
  
`7F 6B 7F 7F 7F D0 7F 7F 7F 1C 03 16 08 00 7F 7F 7F 70 7F 7F 7F 0F 7F 7F 7F 55 06 17 1A 00 7F 7F 7F 7F 7F 7F 7F E0 7F 7F 7F C7 15 19 04 00 7F 7F 7F 6B 7F 7F 7F 97 `  
  
`7F 7F 7F BE 18 15 00 00 7F 7F 7F 58 7F 7F 7F 6B 7F 7F 7F 32 19 1A 04 00 7F 7F 7F 97 7F 7F 7F C7 7F 7F 7F BE 03 18 1B 00 7F 7F 7F 70 7F 7F 7F 58 7F 7F 7F 2A 1A 19 `  
  
`06 00 7F 7F 7F C7 7F 7F 7F 97 7F 7F 7F 7F 1B 18 00 00 7F 7F 7F 2A 7F 7F 7F 58 7F 7F 7F 32 16 02 08 00 7F 7F 7F 0F 7F 7F 7F 4A 7F 7F 7F 55 0B 02 16 00 7F 7F 7F 1C `  
  
`7F 7F 7F 4A 7F 7F 7F 0F 07 0A 17 00 7F 7F 7F A6 7F 7F 7F D0 7F 7F 7F E0 1B 16 03 00 7F 7F 7F 2A 7F 7F 7F 0F 7F 7F 7F 70 03 0C 06 00 00 00 50 70 00 00 50 79 00 00 `  
  
`50 7F 0A 07 05 00 00 00 50 D0 00 00 50 A6 00 00 50 AC 18 19 15 00 00 00 50 58 00 00 50 97 00 00 50 6B 01 02 0B 00 00 00 50 42 00 00 50 4A 00 00 50 1C 0D 10 11 13 `  
  
`7F 6B 23 1B 7F 6B 23 27 7F 6B 23 D4 7F 6B 23 CA 11 13 12 14 7F 6B 23 D4 7F 6B 23 CA 7F 6B 23 AC 7F 6B 23 B2 13 10 14 0F 7F 6B 23 CA 7F 6B 23 27 7F 6B 23 B2 7F 6B `  
  
`23 3C 10 0D 0F 0E 7F 6B 23 27 7F 6B 23 1B 7F 6B 23 3C 7F 6B 23 42 11 12 0D 0E 7F 6B 23 D4 7F 6B 23 AC 7F 6B 23 1B 7F 6B 23 42 0E 12 0F 14 7F 6B 23 42 7F 6B 23 AC `  
  
`7F 6B 23 3C 7F 6B 23 B2 01 05 02 07 7F 7F 7F 42 7F 7F 7F AC 7F 7F 7F 4A 7F 7F 7F A6 06 19 03 18 00 00 50 7F 00 00 50 97 00 00 50 70 00 00 50 58 0A 04 17 1A 00 00 `  
  
`50 D0 00 00 50 BE 00 00 50 E0 00 00 50 C7 0B 16 00 1B 00 00 50 1C 00 00 50 0F 00 00 50 32 00 00 50 2A 0A 05 0B 01 00 00 50 D0 00 00 50 AC 00 00 50 1C 00 00 50 42`

  
  
  
Model 5, skeleton data for 3rd part \[at offset 0x000041CC\]:

  

`00 00 00 00 13 00 12 00 D8 FF 00 00 ED FF 12 00 D8 FF 00 00 ED FF ED FF D8 FF 00 00 13 00 ED FF D8 FF 00 00 13 00 12 00 0E 00 00 00 ED FF 12 00 0E 00 00 00 13 00 `  
  
`ED FF 0E 00 00 00 ED FF ED FF 0E 00 00 00 AC FF A3 FF 3C FF 00 00 F3 FF C7 FF 07 FF 00 00 D2 FF EE FF 02 FF 00 00 B5 FF 32 00 41 FF 00 00 00 00 2F 00 F0 FF 00 00 `  
  
`00 00 50 00 A5 FF 00 00 00 00 A3 FF C4 FF 00 00 00 00 6B FF 6F FF 00 00 00 00 59 00 B8 FF 00 00 DC FF D9 FF D5 FF 00 00 D0 FF 02 00 E1 FF 00 00 A8 FF 92 FF 6A FF `  
  
`00 00 A9 FF 06 00 75 FF 00 00 9A FF DE FF 80 FF 00 00 8A FF F9 FF 40 FF 00 00 BD FF 2E 00 A8 FF 00 00 C7 FF 30 00 CF FF 00 00 AF FF 06 00 A1 FF 00 00 B4 FF 03 00 `  
  
`C2 FF 00 00 B2 FF B1 FF 9E FF 00 00 C2 FF D8 FF B4 FF 00 00 8D FF EB FF 7E FF 00 00 88 FF CF FF A2 FF 00 00 9D FF E9 FF BE FF 00 00 00 00 59 00 41 FF 00 00 06 00 `  
  
`37 00 DD FE 00 00 63 00 E9 FF BE FF 00 00 78 00 CF FF A2 FF 00 00 73 00 EB FF 7E FF 00 00 3D 00 D8 FF B3 FF 00 00 4E 00 B1 FF 9E FF 00 00 4A 00 03 00 C1 FF 00 00 `  
  
`51 00 06 00 A1 FF 00 00 39 00 30 00 CF FF 00 00 43 00 2E 00 A8 FF 00 00 6B 00 07 00 47 FF 00 00 66 00 DE FF 80 FF 00 00 57 00 06 00 75 FF 00 00 57 00 92 FF 69 FF `  
  
`00 00 2D 00 02 00 DF FF 00 00 22 00 D9 FF D3 FF 00 00 4B 00 32 00 41 FF 00 00 37 00 3E 00 17 FF 00 00 21 00 13 00 02 FF 00 00 2E 00 BA FF 0C FF 00 00 75 00 6A 00 `  
  
`50 FF 00 00 54 00 2F 00 F7 FF 00 00 CD FF 90 00 D3 FE 00 00 B0 FF 04 00 07 FF 00 00 BA FF 2F 00 DC FE 00 00 6C 00 74 FF 7E FF 00 00 58 00 45 FF 42 FF 00 00 12 00 `  
  
`59 FF 7D FF 00 00 00 00 99 FF 23 FF 00 00 60 00 47 00 2A FF 00 00 52 00 58 00 5B FF 00 00 A6 00 D7 FF 6D FF 00 00 67 00 F3 FF F9 FF 00 00 00 00 55 00 65 FF 00 00 `  
  
`48 00 30 00 65 FF 00 00 B8 FF 30 00 65 FF 00 00 7C FF 90 00 57 FF 00 00 2B 00 8E FF F6 FE 00 00 B4 FF 5B 00 6D FF 00 00 75 FF 28 00 75 FF 00 00 9B FF 26 00 A9 FF `  
  
`00 00 8E FF 5D 00 1E FF 00 00 31 00 9C 00 F1 FE 00 00 43 2A 42 0D FF FF FF 61 FF FF FF 18 FF FF FF 79 FF 33 34 85 03 04 05 06 44 42 17 0D FF FF FF D6 FF FF FF 79 `  
  
`FF FF FF D6 FF 20 33 85 08 09 0A 0B 18 10 0C 00 FF FF FF C0 FF FF FF 79 FF FF FF 6A 00 01 02 34 10 29 0C 00 FF FF FF 79 FF FF FF 2C FF FF FF 6A 01 07 02 34 41 31 `  
  
`2B 00 FF 00 00 5B FF 00 00 31 FF 00 00 02 2B 2D 41 00 FF 00 00 02 FF 00 00 22 FF 00 00 5B 44 14 0B 00 FF 00 00 D6 FF 00 00 E2 FF 00 00 79 31 36 43 00 FF 00 00 31 `  
  
`FF 00 00 8D FF 00 00 61 31 41 36 00 FF 00 00 31 FF 00 00 5B FF 00 00 8D 08 38 16 00 92 53 14 C1 92 53 14 D2 92 53 14 E9 3B 3C 3A 00 92 53 14 36 92 53 14 C4 92 53 `  
  
`14 1D 21 33 32 00 92 53 14 48 92 53 14 48 92 53 14 23 13 16 15 00 92 53 14 D0 92 53 14 E9 92 53 14 E9 15 16 14 00 92 53 14 E9 92 53 14 E9 92 53 14 E2 15 14 19 00 `  
  
`92 53 14 E9 92 53 14 E2 92 53 14 E0 13 0F 08 00 92 53 14 D0 92 53 14 68 92 53 14 C1 0B 14 48 00 92 53 14 79 92 53 14 E2 92 53 14 DB 26 2C 2E 00 92 53 14 28 92 53 `  
  
`14 06 92 53 14 30 2B 31 32 00 92 53 14 02 92 53 14 31 92 53 14 23 2E 2B 34 00 92 53 14 30 92 53 14 02 92 53 14 25 2D 2C 28 00 92 53 14 22 92 53 14 06 92 53 14 0F `  
  
`3E 4B 21 00 92 53 14 37 92 53 14 3B 92 53 14 48 16 13 08 00 92 53 14 E9 92 53 14 D0 92 53 14 C1 2E 2C 2B 00 92 53 14 30 92 53 14 06 92 53 14 02 15 1B 13 00 92 53 `  
  
`14 E9 92 53 14 C6 92 53 14 D0 21 37 39 00 92 53 14 48 92 53 14 A9 92 53 14 D2 21 0A 33 00 92 53 14 48 92 53 14 8C 92 53 14 48 39 38 0A 00 92 53 14 D2 92 53 14 D2 `  
  
`92 53 14 8C 08 0F 3D 00 92 53 14 C1 92 53 14 68 92 53 14 B9 0E 30 26 00 92 53 14 72 92 53 14 40 92 53 14 28 1B 11 0E 00 92 53 14 C6 92 53 14 AE 92 53 14 72 0E 11 `  
  
`30 00 92 53 14 72 92 53 14 AE 92 53 14 40 3D 46 09 00 92 53 14 B9 92 53 14 6B 92 53 14 87 32 20 21 00 92 53 14 23 92 53 14 89 92 53 14 48 20 0B 37 00 92 53 14 89 `  
  
`92 53 14 79 92 53 14 A9 31 20 32 00 92 53 14 31 92 53 14 89 92 53 14 23 3E 40 35 00 92 53 14 37 92 53 14 49 92 53 14 18 3E 3F 40 00 92 53 14 37 92 53 14 B6 92 53 `  
  
`14 49 3F 35 40 00 92 53 14 B6 92 53 14 18 92 53 14 49 2B 2C 2D 00 92 53 14 02 92 53 14 06 92 53 14 22 38 0B 4A 00 92 53 14 D2 92 53 14 79 92 53 14 95 45 47 49 00 `  
  
`92 53 14 B0 92 53 14 0C 92 53 14 5B 47 48 49 00 92 53 14 0C 92 53 14 DB 92 53 14 5B 48 45 49 00 92 53 14 DB 92 53 14 B0 92 53 14 5B 46 34 09 00 92 53 14 6B 92 53 `  
  
`14 25 92 53 14 87 48 14 16 00 92 53 14 DB 92 53 14 E2 92 53 14 E9 0B 48 47 00 92 53 14 79 92 53 14 DB 92 53 14 0C 08 3D 09 00 92 53 14 C1 92 53 14 B9 92 53 14 87 `  
  
`4A 47 45 00 92 53 14 95 92 53 14 0C 92 53 14 B0 4A 16 38 00 92 53 14 95 92 53 14 E9 92 53 14 D2 21 39 0A 00 92 53 14 48 92 53 14 D2 92 53 14 8C 4B 20 37 00 92 53 `  
  
`14 3B 92 53 14 89 92 53 14 A9 21 4B 37 00 92 53 14 48 92 53 14 3B 92 53 14 A9 4B 3E 35 00 92 53 14 3B 92 53 14 37 92 53 14 18 4A 0B 47 00 92 53 14 95 92 53 14 79 `  
  
`92 53 14 0C 2F 12 0C 00 FF CC 99 47 FF CC 99 AA FF CC 99 6A 10 17 0D 00 FF CC 99 79 FF CC 99 D6 FF CC 99 85 10 18 17 00 FF CC 99 79 FF CC 99 C0 FF CC 99 D6 12 18 `  
  
`0C 00 FF CC 99 AA FF CC 99 C0 FF CC 99 6A 18 12 1A 00 FF CC 99 C0 FF CC 99 AA FF CC 99 D3 1D 1E 15 00 FF CC 99 C7 FF CC 99 D0 FF CC 99 E9 15 19 1D 00 FF CC 99 E9 `  
  
`FF CC 99 E0 FF CC 99 C7 1D 1F 1E 00 FF CC 99 C7 FF CC 99 B6 FF CC 99 D0 1C 1F 1A 00 FF CC 99 C4 FF CC 99 B6 FF CC 99 D3 1E 1F 1C 00 FF CC 99 D0 FF CC 99 B6 FF CC `  
  
`99 C4 15 1E 1C 00 FF CC 99 E9 FF CC 99 D0 FF CC 99 C4 23 2C 25 00 FF CC 99 1C FF CC 99 06 FF CC 99 29 22 23 25 00 FF CC 99 39 FF CC 99 1C FF CC 99 29 22 25 27 00 `  
  
`FF CC 99 39 FF CC 99 29 FF CC 99 1D 22 24 23 00 FF CC 99 39 FF CC 99 2A FF CC 99 1C 28 2C 24 00 FF CC 99 0F FF CC 99 06 FF CC 99 2A 23 24 2C 00 FF CC 99 1C FF CC `  
  
`99 2A FF CC 99 06 2F 29 27 00 FF CC 99 47 FF CC 99 2C FF CC 99 1D 29 2F 0C 00 FF CC 99 2C FF CC 99 47 FF CC 99 6A 29 10 2A 00 FF CC 99 2C FF CC 99 79 FF CC 99 18 `  
  
`2A 10 0D 00 FF CC 99 18 FF CC 99 79 FF CC 99 85 18 10 0C 00 FF CC 99 C0 FF CC 99 79 FF CC 99 6A 10 29 0C 00 FF CC 99 79 FF CC 99 2C FF CC 99 6A 36 41 43 2D FF 00 `  
  
`00 8D FF 00 00 5B FF 00 00 61 FF 00 00 22 31 43 20 42 FF 00 00 31 FF 00 00 61 FF 00 00 89 FF 00 00 79 0B 20 44 42 FF 00 00 79 FF 00 00 89 FF 00 00 D6 FF 00 00 79 `  
  
`0F 13 0E 1B 92 53 14 68 92 53 14 D0 92 53 14 72 92 53 14 C6 1B 15 11 1C 92 53 14 C6 92 53 14 E9 92 53 14 AE 92 53 14 C4 2B 32 34 33 92 53 14 02 92 53 14 23 92 53 `  
  
`14 25 92 53 14 48 26 30 2C 25 92 53 14 28 92 53 14 40 92 53 14 06 92 53 14 29 0F 0E 2E 26 92 53 14 68 92 53 14 72 92 53 14 30 92 53 14 28 33 0A 34 09 92 53 14 48 `  
  
`92 53 14 8C 92 53 14 25 92 53 14 87 4B 35 20 3F 92 53 14 3B 92 53 14 18 92 53 14 89 92 53 14 B6 0B 38 37 39 92 53 14 79 92 53 14 D2 92 53 14 A9 92 53 14 D2 3A 34 `  
  
`3B 46 92 53 14 1D 92 53 14 25 92 53 14 36 92 53 14 6B 2E 34 0F 3D 92 53 14 30 92 53 14 25 92 53 14 68 92 53 14 B9 3A 3C 34 3D 92 53 14 1D 92 53 14 C4 92 53 14 25 `  
  
`92 53 14 B9 21 20 3E 3F 92 53 14 48 92 53 14 89 92 53 14 37 92 53 14 B6 45 48 4A 16 92 53 14 B0 92 53 14 DB 92 53 14 95 92 53 14 E9 3B 46 3C 3D 92 53 14 36 92 53 `  
  
`14 6B 92 53 14 C4 92 53 14 B9 08 09 38 0A 92 53 14 C1 92 53 14 87 92 53 14 D2 92 53 14 8C 03 00 02 01 FF CC 99 2F FF CC 99 2B FF CC 99 C1 FF CC 99 C5 06 07 04 05 `  
  
`FF CC 99 28 FF CC 99 C6 FF CC 99 2C FF CC 99 C0 2F 30 12 11 FF CC 99 47 FF CC 99 40 FF CC 99 AA FF CC 99 AE 18 1A 17 19 FF CC 99 C0 FF CC 99 D3 FF CC 99 D6 FF CC `  
  
`99 E0 1A 12 1C 11 FF CC 99 D3 FF CC 99 AA FF CC 99 C4 FF CC 99 AE 1D 19 1F 1A FF CC 99 C7 FF CC 99 E0 FF CC 99 B6 FF CC 99 D3 24 22 28 27 FF CC 99 2A FF CC 99 39 `  
  
`FF CC 99 0F FF CC 99 1D 27 25 2F 30 FF CC 99 1D FF CC 99 29 FF CC 99 47 FF CC 99 40 29 2A 27 28 FF CC 99 2C FF CC 99 18 FF CC 99 1D FF CC 99 0F 44 17 14 19 FF CC `  
  
`99 D6 FF CC 99 D6 FF CC 99 E2 FF CC 99 E0 43 2D 2A 28 FF CC 99 61 FF CC 99 22 FF CC 99 18 FF CC 99 0F 04 05 00 01 00 00 7E 2C 00 00 7E C0 00 00 7E 2B 00 00 7E C5 `  
  
`04 00 06 03 00 00 7E 2C 00 00 7E 2B 00 00 7E 28 00 00 7E 2F 02 01 07 05 00 00 7E C1 00 00 7E C5 00 00 7E C6 00 00 7E C0 06 03 07 02 00 00 7E 28 00 00 7E 2F 00 00 `  
  
`7E C6 00 00 7E C1 43 2A 42 0D FF CC 99 61 FF CC 99 18 FF CC 99 79 FF CC 99 85 44 42 17 0D FF CC 99 D6 FF CC 99 79 FF CC 99 D6 FF CC 99 85 00 1C 14 78 00 1C 14 78 `  
  
`01 1C 14 78 00 A9 0F A2 0F B5 20 05 22 1E 3F 05 3F 1D 1F A9 00 05 1F 05 02 1E 1F 1D 01 00 02 02`

  
  
  
Model 5, skeleton data for 4th part \[at offset 0x00004C0C\]:

  

`00 00 00 00 0C 00 F4 FF A3 FF 00 00 F4 FF F4 FF A3 FF 00 00 0C 00 0C 00 A3 FF 00 00 F4 FF F4 FF C9 FF 00 00 F4 FF 0C 00 C9 FF 00 00 0C 00 0C 00 C6 FF 00 00 0C 00 `  
  
`F4 FF C6 FF 00 00 31 00 DD FF E3 FF 00 00 31 00 23 00 E3 FF 00 00 19 00 13 00 1D 00 00 00 19 00 EC FF 1D 00 00 00 F4 FF 0C 00 A3 FF 00 00 E7 FF EC FF 1D 00 00 00 `  
  
`E7 FF 13 00 1D 00 00 00 D7 FF 23 00 EC FF 00 00 D7 FF DD FF EC FF 00 00 0F 03 0E 04 00 00 50 C2 00 00 50 B9 00 00 50 D1 00 00 50 C5 0E 0D 0F 0C 00 00 50 D1 00 00 `  
  
`50 B2 00 00 50 C2 00 00 50 9E 0E 04 08 05 00 00 50 D1 00 00 50 C5 00 00 50 1E 00 00 50 43 0F 07 03 06 00 00 50 C2 00 00 50 1A 00 00 50 B9 00 00 50 37 02 0B 00 01 `  
  
`00 00 50 2B 00 00 50 C5 00 00 50 2F 00 00 50 C1 07 08 06 05 00 00 50 1A 00 00 50 1E 00 00 50 37 00 00 50 43 04 0B 05 02 00 00 50 C5 00 00 50 C5 00 00 50 43 00 00 `  
  
`50 2B 01 0B 03 04 00 00 50 C1 00 00 50 C5 00 00 50 B9 00 00 50 C5 02 00 05 06 00 00 50 2B 00 00 50 2F 00 00 50 43 00 00 50 37 01 03 00 06 00 00 50 C1 00 00 50 B9 `  
  
`00 00 50 2F 00 00 50 37 07 0A 08 09 7F 7F 7F 1A 7F 7F 7F 51 7F 7F 7F 1E 7F 7F 7F 52 0C 0D 0A 09 7F 7F 7F 9E 7F 7F 7F B2 7F 7F 7F 51 7F 7F 7F 52 08 09 0E 0D 7F 7F `  
  
`7F 1E 7F 7F 7F 52 7F 7F 7F D1 7F 7F 7F B2 07 0F 0A 0C 7F 7F 7F 1A 7F 7F 7F C2 7F 7F 7F 51 7F 7F 7F 9E`

  
  
  
Model 5, skeleton data for 5th part \[at offset 0x00004DA8\]:

  

`00 00 00 00 D9 FF 28 00 BB FF 00 00 28 00 28 00 BB FF 00 00 D9 FF D8 FF BB FF 00 00 28 00 D8 FF BB FF 00 00 0C 00 0C 00 00 00 00 00 0C 00 0C 00 E4 FF 00 00 0C 00 `  
  
`F4 FF E4 FF 00 00 0C 00 F4 FF 00 00 00 00 F4 FF 0C 00 00 00 00 00 F4 FF 0C 00 E4 FF 00 00 F4 FF F4 FF 00 00 00 00 F4 FF F4 FF E4 FF 00 00 D9 FF 28 00 7A FF 00 00 `  
  
`D9 FF D8 FF 7A FF 00 00 28 00 D8 FF 7A FF 00 00 28 00 28 00 7A FF 00 00 01 0F 03 0E 71 38 00 18 71 38 00 2B 71 38 00 26 71 38 00 2F 0E 0D 03 02 71 38 00 2F 71 38 `  
  
`00 C1 71 38 00 26 71 38 00 C9 02 0D 00 0C 71 38 00 C9 71 38 00 C1 71 38 00 D6 71 38 00 C5 0F 01 0C 00 71 38 00 2B 71 38 00 18 71 38 00 C5 71 38 00 D6 01 03 05 06 `  
  
`19 19 19 18 19 19 19 26 19 19 19 34 19 19 19 26 01 05 00 09 19 19 19 18 19 19 19 34 19 19 19 D6 19 19 19 C0 00 09 02 0B 19 19 19 D6 19 19 19 C0 19 19 19 C9 19 19 `  
  
`19 C9 03 02 06 0B 19 19 19 26 19 19 19 C9 19 19 19 26 19 19 19 C9 0F 0C 0E 0D 19 19 19 2B 19 19 19 C5 19 19 19 2F 19 19 19 C1 0A 07 0B 06 FF CC 99 C6 FF CC 99 28 `  
  
`FF CC 99 C9 FF CC 99 26 07 04 06 05 FF CC 99 28 FF CC 99 2C FF CC 99 26 FF CC 99 34 09 05 08 04 FF CC 99 C0 FF CC 99 34 FF CC 99 C0 FF CC 99 2C 0A 0B 08 09 FF CC `  
  
`99 C6 FF CC 99 C9 FF CC 99 C0 FF CC 99 C0 0A 08 07 04 FF CC 99 C6 FF CC 99 C0 FF CC 99 28 FF CC 99 2C`

  
  
  
Model 5, skeleton data for 6th part \[at offset 0x00004F44\]:

  

`00 00 00 00 21 00 E0 FF C2 FF 00 00 27 00 DA FF 00 00 00 00 27 00 26 00 00 00 00 00 21 00 20 00 C2 FF 00 00 E1 FF E0 FF C2 FF 00 00 DB FF DA FF 00 00 00 00 E1 FF `  
  
`20 00 C2 FF 00 00 DB FF 26 00 00 00 00 00 02 01 07 05 19 19 19 2C 19 19 19 28 19 19 19 C0 19 19 19 C6 02 07 03 06 19 19 19 2C 19 19 19 C0 19 19 19 43 19 19 19 AD `  
  
`01 00 05 04 19 19 19 28 19 19 19 2F 19 19 19 C6 19 19 19 C1 01 02 00 03 19 19 19 28 19 19 19 2C 19 19 19 2F 19 19 19 43 05 04 07 06 FF CC 99 C6 FF CC 99 C1 FF CC `  
  
`99 C0 FF CC 99 AD 03 06 00 04 FF CC 99 43 FF CC 99 AD FF CC 99 2F FF CC 99 C1`

  
  
  
Model 5, skeleton data for 7th part \[at offset 0x00005000\]:

  

`00 00 00 00 29 00 DD FF EC FF 00 00 29 00 23 00 EC FF 00 00 19 00 13 00 1D 00 00 00 19 00 EC FF 1D 00 00 00 0C 00 0C 00 A3 FF 00 00 E7 FF EC FF 1D 00 00 00 E7 FF `  
  
`13 00 1D 00 00 00 CF FF 23 00 E3 FF 00 00 CF FF DD FF E3 FF 00 00 F4 FF F4 FF C6 FF 00 00 F4 FF 0C 00 C6 FF 00 00 0C 00 0C 00 C9 FF 00 00 0C 00 F4 FF C9 FF 00 00 `  
  
`F4 FF 0C 00 A3 FF 00 00 0C 00 F4 FF A3 FF 00 00 F4 FF F4 FF A3 FF 00 00 00 0C 08 09 00 00 50 2E 00 00 50 37 00 00 50 D7 00 00 50 B9 00 01 0C 0B 00 00 50 2E 00 00 `  
  
`50 1E 00 00 50 37 00 00 50 2B 0E 0C 04 0B 00 00 50 2F 00 00 50 37 00 00 50 2B 00 00 50 2B 0E 0F 0C 09 00 00 50 2F 00 00 50 C1 00 00 50 37 00 00 50 B9 0B 0A 04 0D `  
  
`00 00 50 2B 00 00 50 AD 00 00 50 2B 00 00 50 C5 0D 0A 0F 09 00 00 50 C5 00 00 50 AD 00 00 50 C1 00 00 50 B9 08 09 07 0A 00 00 50 D7 00 00 50 B9 00 00 50 D1 00 00 `  
  
`50 AD 01 07 0B 0A 00 00 50 1E 00 00 50 D1 00 00 50 2B 00 00 50 AD 04 0D 0E 0F 00 00 50 2B 00 00 50 C5 00 00 50 2F 00 00 50 C1 00 03 01 02 00 00 50 2E 00 00 50 51 `  
  
`00 00 50 1E 00 00 50 3C 08 05 00 03 7F 7F 7F D7 7F 7F 7F 9E 7F 7F 7F 2E 7F 7F 7F 51 07 01 06 02 7F 7F 7F D1 7F 7F 7F 1E 7F 7F 7F 9C 7F 7F 7F 3C 05 06 03 02 7F 7F `  
  
`7F 9E 7F 7F 7F 9C 7F 7F 7F 51 7F 7F 7F 3C 07 06 08 05 7F 7F 7F D1 7F 7F 7F 9C 7F 7F 7F D7 7F 7F 7F 9E`

  
  
  
Model 5, skeleton data for 8th part \[at offset 0x0000519C\]:

  

`00 00 00 00 D8 FF 28 00 7A FF 00 00 D8 FF D8 FF 7A FF 00 00 27 00 D8 FF 7A FF 00 00 27 00 28 00 7A FF 00 00 0C 00 F4 FF E4 FF 00 00 0C 00 F4 FF 00 00 00 00 0C 00 `  
  
`0C 00 E4 FF 00 00 0C 00 0C 00 00 00 00 00 F4 FF F4 FF 00 00 00 00 F4 FF F4 FF E4 FF 00 00 F4 FF 0C 00 E4 FF 00 00 F4 FF 0C 00 00 00 00 00 D8 FF D8 FF BB FF 00 00 `  
  
`27 00 D8 FF BB FF 00 00 D8 FF 28 00 BB FF 00 00 27 00 28 00 BB FF 00 00 03 0F 00 0E 71 38 00 2B 71 38 00 18 71 38 00 C5 71 38 00 D6 03 02 0F 0D 71 38 00 2B 71 38 `  
  
`00 2F 71 38 00 18 71 38 00 26 0C 0D 01 02 71 38 00 C9 71 38 00 26 71 38 00 C1 71 38 00 2F 01 00 0C 0E 71 38 00 C1 71 38 00 C5 71 38 00 C9 71 38 00 D6 00 01 03 02 `  
  
`19 19 19 C5 19 19 19 C1 19 19 19 2B 19 19 19 2F 0D 0C 04 09 19 19 19 26 19 19 19 C9 19 19 19 26 19 19 19 C9 0F 0D 06 04 19 19 19 18 19 19 19 26 19 19 19 2C 19 19 `  
  
`19 26 0E 0F 0A 06 19 19 19 D6 19 19 19 18 19 19 19 B8 19 19 19 2C 0E 0A 0C 09 19 19 19 D6 19 19 19 B8 19 19 19 C9 19 19 19 C9 08 05 09 04 FF CC 99 C6 FF CC 99 28 `  
  
`FF CC 99 C9 FF CC 99 26 0B 08 0A 09 FF CC 99 C0 FF CC 99 C6 FF CC 99 B8 FF CC 99 C9 07 06 05 04 FF CC 99 2C FF CC 99 2C FF CC 99 28 FF CC 99 26 0A 06 0B 07 FF CC `  
  
`99 B8 FF CC 99 2C FF CC 99 C0 FF CC 99 2C 07 05 0B 08 FF CC 99 2C FF CC 99 28 FF CC 99 C0 FF CC 99 C6`

  
  
  
Model 5, skeleton data for 9th part \[at offset 0x00005338\]:

  

`00 00 00 00 26 00 26 00 00 00 00 00 20 00 20 00 C2 FF 00 00 26 00 DA FF 00 00 00 00 1F 00 E0 FF C2 FF 00 00 DF FF 20 00 C2 FF 00 00 D9 FF 26 00 00 00 00 00 D9 FF `  
  
`DA FF 00 00 00 00 DF FF E0 FF C2 FF 00 00 06 07 05 04 19 19 19 C6 19 19 19 C1 19 19 19 C0 19 19 19 AD 06 02 07 03 19 19 19 C6 19 19 19 28 19 19 19 C1 19 19 19 2F `  
  
`05 04 00 01 19 19 19 C0 19 19 19 AD 19 19 19 2C 19 19 19 43 05 00 06 02 19 19 19 C0 19 19 19 2C 19 19 19 C6 19 19 19 28 01 04 03 07 FF CC 99 43 FF CC 99 AD FF CC `  
  
`99 2F FF CC 99 C1 02 00 03 01 FF CC 99 28 FF CC 99 2C FF CC 99 2F FF CC 99 43`

  
  
  
Model 5, skeleton data for 10th part \[at offset 0x000053F4\]:

  

`00 00 00 00 00 00 D3 FF 65 FF 00 00 00 00 D9 FF 11 00 00 00 29 00 02 00 11 00 00 00 4A 00 17 00 65 FF 00 00 CE FF 17 00 65 FF 00 00 E5 FF 02 00 11 00 00 00 00 00 `  
  
`61 00 65 FF 00 00 00 00 2F 00 11 00 00 00 02 01 07 05 7F 6B 23 20 7F 6B 23 98 7F 6B 23 77 7F 6B 23 CC 03 06 00 04 7F 6B 23 08 7F 6B 23 80 7F 6B 23 8B 7F 6B 23 E6 `  
  
`03 02 06 07 7F 6B 23 08 7F 6B 23 20 7F 6B 23 80 7F 6B 23 77 03 00 02 01 7F 6B 23 08 7F 6B 23 8B 7F 6B 23 20 7F 6B 23 98 04 06 05 07 7F 6B 23 E6 7F 6B 23 80 7F 6B `  
  
`23 CC 7F 6B 23 77 04 05 00 01 7F 6B 23 E6 7F 6B 23 CC 7F 6B 23 8B 7F 6B 23 98`

  
  
  
Model 5, skeleton data for 11th part \[at offset 0x000054B0\]:

  

`00 00 00 00 00 00 D2 FF CB FF 00 00 00 00 D3 FF 07 00 00 00 4A 00 17 00 07 00 00 00 54 00 1E 00 CB FF 00 00 CE FF 17 00 07 00 00 00 C5 FF 1E 00 CB FF 00 00 00 00 `  
  
`61 00 07 00 00 00 00 00 74 00 CB FF 00 00 20 00 00 00 CB FF 00 00 01 00 E0 FF CB FF 00 00 E1 FF 00 00 CB FF 00 00 01 00 1F 00 CB FF 00 00 01 00 1F 00 97 FF 00 00 `  
  
`E1 FF 00 00 97 FF 00 00 01 00 E0 FF 97 FF 00 00 20 00 00 00 97 FF 00 00 2E 00 00 00 54 FF 00 00 2E 00 00 00 97 FF 00 00 01 00 2D 00 97 FF 00 00 01 00 2D 00 54 FF `  
  
`00 00 D3 FF 00 00 54 FF 00 00 D3 FF 00 00 97 FF 00 00 01 00 D3 FF 97 FF 00 00 01 00 D3 FF 54 FF 00 00 03 00 02 01 7F 6B 23 08 7F 6B 23 8B 7F 6B 23 20 7F 6B 23 98 `  
  
`07 03 06 02 7F 6B 23 80 7F 6B 23 08 7F 6B 23 77 7F 6B 23 20 05 07 04 06 7F 6B 23 E6 7F 6B 23 80 7F 6B 23 CC 7F 6B 23 77 03 07 00 05 7F 6B 23 08 7F 6B 23 80 7F 6B `  
  
`23 8B 7F 6B 23 E6 02 01 06 04 7F 6B 23 20 7F 6B 23 98 7F 6B 23 77 7F 6B 23 CC 05 04 00 01 7F 6B 23 E6 7F 6B 23 CC 7F 6B 23 8B 7F 6B 23 98 08 0F 09 0E FF CC 99 0A `  
  
`FF CC 99 08 FF CC 99 6F FF CC 99 65 0A 09 0D 0E FF CC 99 E7 FF CC 99 6F FF CC 99 E6 FF CC 99 65 0B 0C 08 0F FF CC 99 77 FF CC 99 6E FF CC 99 0A FF CC 99 08 0D 0C `  
  
`0A 0B FF CC 99 E6 FF CC 99 6E FF CC 99 E7 FF CC 99 77 0A 0B 09 08 FF CC 99 E7 FF CC 99 77 FF CC 99 6F FF CC 99 0A 0D 0E 0C 0F FF CC 99 E6 FF CC 99 65 FF CC 99 6E `  
  
`FF CC 99 08 12 15 13 14 33 33 33 77 33 33 33 E7 33 33 33 6E 33 33 33 E6 15 12 16 11 33 33 33 E7 33 33 33 77 33 33 33 6F 33 33 33 0A 16 17 15 14 33 33 33 6F 33 33 `  
  
`33 65 33 33 33 E7 33 33 33 E6 17 16 10 11 33 33 33 65 33 33 33 6F 33 33 33 08 33 33 33 0A 14 17 13 10 33 33 33 E6 33 33 33 65 33 33 33 6E 33 33 33 08 13 10 12 11 `  
  
`33 33 33 6E 33 33 33 08 33 33 33 77 33 33 33 0A`

  
  
  
Model 5, skeleton data for 12th part \[at offset 0x000056DC\]:

  

`00 00 00 00 FE FF 49 00 2C 00 00 00 FE FF 0C 00 38 00 00 00 33 00 BB FF 87 FF 00 00 CF FF BA FF 87 FF 00 00 CF FF FB FF 02 00 00 00 33 00 FB FF 02 00 00 00 C7 FF `  
  
`35 00 EF FF 00 00 3B 00 35 00 EF FF 00 00 C1 FF F9 FF 35 FF 00 00 3E 00 F9 FF 35 FF 00 00 05 04 01 00 24 12 00 28 24 12 00 CD 24 12 00 7C 06 07 00 00 24 12 00 D6 `  
  
`24 12 00 18 24 12 00 77 03 04 02 05 24 12 00 BD 24 12 00 CD 24 12 00 30 24 12 00 28 08 06 03 04 24 12 00 CB 24 12 00 D6 24 12 00 BD 24 12 00 CD 09 02 07 05 24 12 `  
  
`00 25 24 12 00 30 24 12 00 18 24 12 00 28 08 03 09 02 24 12 00 CB 24 12 00 BD 24 12 00 25 24 12 00 30 00 01 06 04 24 12 00 77 24 12 00 7C 24 12 00 D6 24 12 00 CD `  
  
`08 09 06 07 24 12 00 CB 24 12 00 25 24 12 00 D6 24 12 00 18 07 05 00 01 24 12 00 18 24 12 00 28 24 12 00 77 24 12 00 7C`

  
  
  
Model 5, skeleton data for 13th part \[at offset 0x000057DC\]:

  

`00 00 00 00 00 00 2F 00 11 00 00 00 00 00 61 00 65 FF 00 00 1B 00 02 00 11 00 00 00 32 00 17 00 65 FF 00 00 B6 FF 17 00 65 FF 00 00 D7 FF 02 00 11 00 00 00 00 00 `  
  
`D9 FF 11 00 00 00 00 00 D3 FF 65 FF 00 00 05 00 06 02 7F 6B 23 CC 7F 6B 23 77 7F 6B 23 57 7F 6B 23 20 04 07 01 03 7F 6B 23 E6 7F 6B 23 65 7F 6B 23 6E 7F 6B 23 08 `  
  
`04 01 05 00 7F 6B 23 E6 7F 6B 23 6E 7F 6B 23 CC 7F 6B 23 77 04 05 07 06 7F 6B 23 E6 7F 6B 23 CC 7F 6B 23 65 7F 6B 23 57 03 02 01 00 7F 6B 23 08 7F 6B 23 20 7F 6B `  
  
`23 6E 7F 6B 23 77 03 07 02 06 7F 6B 23 08 7F 6B 23 65 7F 6B 23 20 7F 6B 23 57`

  
  
  
Model 5, skeleton data for 14th part \[at offset 0x00005898\]:

  

`00 00 00 00 FF FF D3 FF 54 FF 00 00 FF FF D3 FF 97 FF 00 00 2D 00 00 00 97 FF 00 00 2D 00 00 00 54 FF 00 00 FF FF 2D 00 54 FF 00 00 FF FF 2D 00 97 FF 00 00 D2 FF `  
  
`00 00 97 FF 00 00 D2 FF 00 00 54 FF 00 00 E0 FF 00 00 97 FF 00 00 FF FF E0 FF 97 FF 00 00 1F 00 00 00 97 FF 00 00 FF FF 1F 00 97 FF 00 00 FF FF 1F 00 CB FF 00 00 `  
  
`1F 00 00 00 CB FF 00 00 FF FF E0 FF CB FF 00 00 E0 FF 00 00 CB FF 00 00 00 00 74 00 CB FF 00 00 00 00 61 00 07 00 00 00 3B 00 1E 00 CB FF 00 00 32 00 17 00 07 00 `  
  
`00 00 AC FF 1E 00 CB FF 00 00 B6 FF 17 00 07 00 00 00 00 00 D3 FF 07 00 00 00 00 00 D2 FF CB FF 00 00 0E 0D 09 0A FF CC 99 81 FF CC 99 0A FF CC 99 8B FF CC 99 08 `  
  
`09 08 0E 0F FF CC 99 8B FF CC 99 E6 FF CC 99 81 FF CC 99 E7 0D 0E 0C 0F FF CC 99 0A FF CC 99 81 FF CC 99 77 FF CC 99 E7 0B 0A 0C 0D FF CC 99 80 FF CC 99 08 FF CC `  
  
`99 77 FF CC 99 0A 0B 0C 08 0F FF CC 99 80 FF CC 99 77 FF CC 99 E6 FF CC 99 E7 0A 0B 09 08 FF CC 99 08 FF CC 99 80 FF CC 99 8B FF CC 99 E6 14 15 17 16 7F 6B 23 E6 `  
  
`7F 6B 23 CC 7F 6B 23 65 7F 6B 23 57 12 17 13 16 7F 6B 23 08 7F 6B 23 65 7F 6B 23 20 7F 6B 23 57 12 13 10 11 7F 6B 23 08 7F 6B 23 20 7F 6B 23 6E 7F 6B 23 77 10 11 `  
  
`14 15 7F 6B 23 6E 7F 6B 23 77 7F 6B 23 E6 7F 6B 23 CC 15 11 16 13 7F 6B 23 CC 7F 6B 23 77 7F 6B 23 57 7F 6B 23 20 14 17 10 12 7F 6B 23 E6 7F 6B 23 65 7F 6B 23 6E `  
  
`7F 6B 23 08 01 00 06 07 33 33 33 81 33 33 33 8B 33 33 33 E7 33 33 33 E6 00 01 03 02 33 33 33 8B 33 33 33 81 33 33 33 08 33 33 33 0A 02 01 05 06 33 33 33 0A 33 33 `  
  
`33 81 33 33 33 77 33 33 33 E7 05 04 02 03 33 33 33 77 33 33 33 80 33 33 33 0A 33 33 33 08 05 06 04 07 33 33 33 77 33 33 33 E7 33 33 33 80 33 33 33 E6 03 04 00 07 `  
  
`33 33 33 08 33 33 33 80 33 33 33 8B 33 33 33 E6`

  
  
  
Model 5, skeleton data for 15th part \[at offset 0x00005AC4\]:

  

`00 00 00 00 C2 FF F9 FF 35 FF 00 00 3F 00 F9 FF 35 FF 00 00 C5 FF 35 00 EF FF 00 00 39 00 35 00 EF FF 00 00 CD FF FB FF 02 00 00 00 31 00 FB FF 02 00 00 00 31 00 `  
  
`BA FF 87 FF 00 00 CD FF BB FF 87 FF 00 00 02 00 0C 00 38 00 00 00 02 00 49 00 2C 00 00 00 05 04 08 00 24 12 00 22 24 12 00 C6 24 12 00 73 02 03 09 00 24 12 00 D6 `  
  
`24 12 00 18 24 12 00 77 06 07 05 04 24 12 00 30 24 12 00 BD 24 12 00 22 24 12 00 C6 01 06 03 05 24 12 00 25 24 12 00 30 24 12 00 18 24 12 00 22 00 02 07 04 24 12 `  
  
`00 CB 24 12 00 D6 24 12 00 BD 24 12 00 C6 01 00 06 07 24 12 00 25 24 12 00 CB 24 12 00 30 24 12 00 BD 09 03 08 05 24 12 00 77 24 12 00 18 24 12 00 73 24 12 00 22 `  
  
`00 01 02 03 24 12 00 CB 24 12 00 25 24 12 00 D6 24 12 00 18 02 09 04 08 24 12 00 D6 24 12 00 77 24 12 00 C6 24 12 00 73`

  
  
  
Model 6, skeleton data for 1st part \[at offset 0x00005BC4\]:

  

`00 00 00 00 B8 00 5D FF D5 FF 00 00 09 00 6D FF 1F 00 00 00 F7 FF 93 00 1F 00 00 00 5C FF 48 FF D5 FF 00 00 4B FF 6D 00 D5 FF 00 00 A7 00 82 00 D5 FF 00 00 5D FF `  
  
`6F 00 BA FF 00 00 6D FF 59 FF BA FF 00 00 A5 00 6B FF BA FF 00 00 95 00 82 00 BA FF 00 00 56 00 AF 00 BA FF 00 00 96 FF A4 00 BA FF 00 00 96 FF B1 00 D5 FF 00 00 `  
  
`55 00 BC 00 D5 FF 00 00 02 0C 0D 00 00 00 50 8D 00 00 50 9A 00 00 50 55 05 02 0D 00 00 00 50 07 00 00 50 8D 00 00 50 55 02 04 0C 00 00 00 50 8D 00 00 50 E8 00 00 `  
  
`50 9A 03 01 00 00 00 00 50 D0 00 00 50 73 00 00 50 1C 01 03 02 04 00 00 50 73 00 00 50 D0 00 00 50 8D 00 00 50 E8 02 05 01 00 00 00 50 8D 00 00 50 07 00 00 50 73 `  
  
`00 00 50 1C 04 06 0C 0B 43 0F 00 E8 43 0F 00 AF 43 0F 00 9A 43 0F 00 95 05 0D 09 0A 43 0F 00 07 43 0F 00 55 43 0F 00 41 43 0F 00 5A 00 05 08 09 43 0F 00 1C 43 0F `  
  
`00 07 43 0F 00 3D 43 0F 00 41 03 00 07 08 43 0F 00 D0 43 0F 00 1C 43 0F 00 9D 43 0F 00 3D 03 07 04 06 43 0F 00 D0 43 0F 00 9D 43 0F 00 E8 43 0F 00 AF 06 07 09 08 `  
  
`43 0F 00 AF 43 0F 00 9D 43 0F 00 41 43 0F 00 3D 09 0A 06 0B 43 0F 00 41 43 0F 00 5A 43 0F 00 AF 43 0F 00 95 0B 0A 0C 0D CC CC CC 95 CC CC CC 5A CC CC CC 9A CC CC `  
  
`CC 55`

  
  
  
  
Model 6, skeleton data for 2nd part \[at offset 0x00005D40\]:

  

`00 00 00 00 70 FF 9F FF 20 FF 00 00 91 00 9F FF 20 FF 00 00 38 00 58 00 3C FF 00 00 C8 FF 58 00 3C FF 00 00 9C 00 63 FF F0 FF 00 00 64 FF 63 FF F0 FF 00 00 68 FF `  
  
`49 00 53 FF 00 00 60 00 A9 00 11 00 00 00 A0 FF A9 00 11 00 00 00 49 FF 5A 00 BC FF 00 00 58 00 A7 00 A6 FF 00 00 A8 FF A7 00 A6 FF 00 00 B7 00 5A 00 BC FF 00 00 `  
  
`98 00 49 00 53 FF 00 00 46 00 D6 FF 19 FF 00 00 BB FF D6 FF 19 FF 00 00 9C 00 78 00 0C 00 00 00 64 FF 78 00 0C 00 00 00 1A 00 9F FF 20 FF 00 00 DF FF 63 FF F0 FF `  
  
`00 00 02 0D 0A 00 43 0F 00 5A 43 0F 00 2B 43 0F 00 5C 09 11 05 00 43 0F 00 E5 43 0F 00 BC 43 0F 00 B4 11 13 05 00 43 0F 00 BC 43 0F 00 81 43 0F 00 B4 01 0E 12 00 `  
  
`43 0F 00 32 43 0F 00 6C 43 0F 00 63 02 0A 0B 00 43 0F 00 5A 43 0F 00 5C 43 0F 00 92 0B 0A 08 00 43 0F 00 92 43 0F 00 5C 43 0F 00 A2 09 00 06 00 FF FF 99 E5 FF FF `  
  
`99 BE FF FF 99 C5 0C 01 04 00 FF FF 99 0B FF FF 99 32 FF FF 99 38 10 0C 04 00 FF FF 99 33 FF FF 99 0B FF FF 99 38 07 08 0A 00 FF FF 99 4D FF FF 99 A2 FF FF 99 5C `  
  
`0A 0D 0C 00 FF FF 99 5C FF FF 99 2B FF FF 99 0B 05 12 00 00 FF FF 99 B4 FF FF 99 63 FF FF 99 BE 01 13 04 00 FF FF 99 32 FF FF 99 81 FF FF 99 38 00 09 05 00 FF FF `  
  
`99 BE FF FF 99 E5 FF FF 99 B4 01 0C 0D 00 FF FF 99 32 FF FF 99 0B FF FF 99 2B 03 02 0B 00 FF FF 99 95 FF FF 99 5A FF FF 99 92 09 06 0B 00 99 4C 00 E5 99 4C 00 C5 `  
  
`99 4C 00 92 0B 06 03 00 99 4C 00 92 99 4C 00 C5 99 4C 00 95 0D 02 01 0E 43 0F 00 2B 43 0F 00 5A 43 0F 00 32 43 0F 00 6C 0B 08 09 11 43 0F 00 92 43 0F 00 A2 43 0F `  
  
`00 E5 43 0F 00 BC 13 01 05 12 43 0F 00 81 43 0F 00 32 43 0F 00 B4 43 0F 00 63 0E 02 0F 03 FF CC 99 6C FF CC 99 5A FF CC 99 83 FF CC 99 95 0A 0C 07 10 FF FF 99 5C `  
  
`FF FF 99 0B FF FF 99 4D FF FF 99 33 10 11 07 08 FF FF 99 33 FF FF 99 BC FF FF 99 4D FF FF 99 A2 00 12 0F 0E FF FF 99 BE FF FF 99 63 FF FF 99 83 FF FF 99 6C 11 10 `  
  
`13 04 FF FF 99 BC FF FF 99 33 FF FF 99 81 FF FF 99 38 06 00 03 0F 99 4C 00 C5 99 4C 00 BE 99 4C 00 95 99 4C 00 83`

  
  
  
  
Model 6, skeleton data for 3rd part \[at offset 0x00005FB8\]:

  

`00 00 00 00 58 00 6B 00 D9 FF 00 00 78 00 36 00 7E FF 00 00 8D 00 E3 FF AE FF 00 00 A5 00 D1 FF 95 FF 00 00 78 00 E8 FF B1 FF 00 00 70 00 18 00 BA FF 00 00 4D 00 `  
  
`9B FF BD FF 00 00 83 00 E9 FF 7B FF 00 00 46 00 4B 00 09 00 00 00 3F 00 B5 FF F7 FF 00 00 9D 00 F6 FF 71 FF 00 00 02 00 76 FF 78 FF 00 00 59 00 70 00 80 FF 00 00 `  
  
`56 00 9A FF 7A FF 00 00 56 00 9B FF 51 FF 00 00 83 00 EA FF 53 FF 00 00 76 00 37 00 56 FF 00 00 56 00 72 00 58 FF 00 00 02 00 77 FF 50 FF 00 00 2D 00 AF FF 0C FF `  
  
`00 00 57 00 F5 FF 0F FF 00 00 39 00 5F 00 15 FF 00 00 02 00 84 FF 2B FF 00 00 02 00 05 00 F9 FE 00 00 02 00 7A FF AE FF 00 00 CE FF 5F 00 15 FF 00 00 AE FF F5 FF `  
  
`0F FF 00 00 D8 FF AF FF 0C FF 00 00 AA FF 72 00 58 FF 00 00 8D FF 37 00 56 FF 00 00 83 FF EA FF 53 FF 00 00 AF FF 9B FF 51 FF 00 00 8A FF 36 00 7E FF 00 00 AE FF `  
  
`9A FF 7A FF 00 00 A7 FF 70 00 80 FF 00 00 67 FF F6 FF 71 FF 00 00 C5 FF B5 FF F7 FF 00 00 BE FF 4B 00 09 00 00 00 82 FF E9 FF 7B FF 00 00 BE FF 9B FF BD FF 00 00 `  
  
`95 FF 18 00 BA FF 00 00 8D FF E8 FF B1 FF 00 00 60 FF D1 FF 95 FF 00 00 78 FF E3 FF AE FF 00 00 A5 FF 6B 00 D9 FF 00 00 00 00 71 00 07 00 00 00 7B 00 02 00 F2 FF `  
  
`00 00 8A FF 02 00 F2 FF 00 00 F3 FF 7C FF 78 FF 00 00 11 00 7C FF 78 FF 00 00 F6 FF 25 FF B2 FF 00 00 F6 FF 35 FF 70 FF 00 00 DA FF 61 FF C0 FF 00 00 0F 00 25 FF `  
  
`B2 FF 00 00 2B 00 61 FF C0 FF 00 00 0F 00 35 FF 70 FF 00 00 7A 00 1A 00 88 FF 00 00 8A FF 19 00 88 FF 00 00 00 00 8B 00 C6 FF 00 00 90 FF 3D 00 8E FF 00 00 67 FF `  
  
`49 00 85 FF 00 00 93 FF 46 00 84 FF 00 00 75 FF 68 00 C6 FF 00 00 99 FF 52 00 83 FF 00 00 8A FF 74 00 62 FF 00 00 99 FF A8 00 7F FF 00 00 80 FF A7 00 BB FF 00 00 `  
  
`8F FF 7B 00 9A FF 00 00 9D FF 5C 00 87 FF 00 00 76 00 2E 00 8E FF 00 00 00 00 98 00 DA FF 00 00 00 00 8E 00 82 FF 00 00 00 00 8F 00 59 FF 00 00 00 08 46 2D FF FF `  
  
`FF 18 FF FF FF 4A FF FF FF 79 FF 01 42 76 00 01 02 03 00 3A 0C 47 FF FF FF 18 FF FF FF 69 FF FF FF 31 FF 00 00 79 04 05 06 07 2C 22 3A 47 FF FF FF D6 FF FF FF BF `  
  
`FF FF FF 69 FF 00 00 79 08 09 0A 0B 2C 46 25 2D FF FF FF D6 FF FF FF 79 FF FF FF A6 FF 00 00 76 0C 02 0D 03 36 37 35 00 B4 00 00 3C B4 00 00 65 B4 00 00 98 33 34 `  
  
`32 00 B4 00 00 8B B4 00 00 B2 B4 00 00 57 0B 36 35 00 B4 00 00 7C B4 00 00 3C B4 00 00 98 34 0B 32 00 B4 00 00 B2 B4 00 00 7C B4 00 00 57 30 0B 34 00 B4 00 00 D0 `  
  
`B4 00 00 7C B4 00 00 B2 36 0B 31 00 B4 00 00 3C B4 00 00 7C B4 00 00 1C 12 0E 16 00 B4 00 00 7B B4 00 00 2E B4 00 00 65 0E 13 16 00 B4 00 00 2E B4 00 00 53 B4 00 `  
  
`00 65 1B 16 13 00 B4 00 00 9D B4 00 00 65 B4 00 00 53 12 16 1F 00 B4 00 00 7B B4 00 00 65 B4 00 00 C2 1F 16 1B 00 B4 00 00 C2 B4 00 00 65 B4 00 00 9D 10 14 0F 00 `  
  
`B4 00 00 0B B4 00 00 25 B4 00 00 06 14 10 15 00 B4 00 00 25 B4 00 00 0B B4 00 00 50 17 14 15 00 B4 00 00 83 B4 00 00 25 B4 00 00 50 13 14 17 00 B4 00 00 53 B4 00 `  
  
`00 25 B4 00 00 83 1B 17 1A 00 B4 00 00 9D B4 00 00 11 B4 00 00 CB 17 15 19 00 B4 00 00 83 B4 00 00 50 B4 00 00 9F 15 10 11 00 B4 00 00 50 B4 00 00 0B B4 00 00 27 `  
  
`11 48 15 00 B4 00 00 27 B4 00 00 85 B4 00 00 50 1D 19 1C 00 B4 00 00 D9 B4 00 00 9F B4 00 00 CA 19 1D 1A 00 B4 00 00 9F B4 00 00 D9 B4 00 00 CB 1A 1D 1E 00 B4 00 `  
  
`00 CB B4 00 00 D9 B4 00 00 E9 15 48 19 00 B4 00 00 50 B4 00 00 85 B4 00 00 9F 19 48 1C 00 B4 00 00 9F B4 00 00 85 B4 00 00 CA 03 04 02 00 FF CC 99 1C FF CC 99 22 `  
  
`FF CC 99 40 08 00 2E 00 FF CC 99 4A FF CC 99 18 FF CC 99 16 2E 05 04 00 FF CC 99 16 FF CC 99 07 FF CC 99 22 02 04 05 00 FF CC 99 40 FF CC 99 22 FF CC 99 07 38 07 `  
  
`0A 00 FF CC 99 07 FF CC 99 1B FF CC 99 2A 02 05 0A 00 FF CC 99 40 FF CC 99 07 FF CC 99 2A 07 03 0A 00 FF CC 99 1B FF CC 99 1C FF CC 99 2A 04 03 07 00 FF CC 99 22 `  
  
`FF CC 99 1C FF CC 99 1B 02 0A 03 00 FF CC 99 40 FF CC 99 2A FF CC 99 1C 0A 05 38 00 FF CC 99 2A FF CC 99 07 FF CC 99 07 01 00 0C 00 FF CC 99 07 FF CC 99 18 FF CC `  
  
`99 31 3A 00 46 00 FF CC 99 69 FF CC 99 18 FF CC 99 79 2D 08 25 00 FF CC 99 76 FF CC 99 4A FF CC 99 A6 23 2B 2A 00 FF CC 99 C7 FF CC 99 AE FF CC 99 D0 2A 29 26 00 `  
  
`FF CC 99 D0 FF CC 99 CD FF CC 99 D4 2A 26 23 00 FF CC 99 D0 FF CC 99 D4 FF CC 99 C7 28 2B 23 00 FF CC 99 EA FF CC 99 AE FF CC 99 C7 29 2B 28 00 FF CC 99 CD FF CC `  
  
`99 AE FF CC 99 EA 24 2F 25 00 FF CC 99 9E FF CC 99 DA FF CC 99 A6 2C 2F 28 00 FF CC 99 D6 FF CC 99 DA FF CC 99 EA 29 2A 2B 00 FF CC 99 CD FF CC 99 D0 FF CC 99 AE `  
  
`26 39 23 00 FF CC 99 D4 FF CC 99 E8 FF CC 99 C7 2E 09 08 00 FF CC 99 16 FF CC 99 51 FF CC 99 4A 28 2F 29 00 FF CC 99 EA FF CC 99 DA FF CC 99 CD 2E 00 05 00 FF CC `  
  
`99 16 FF CC 99 18 FF CC 99 07 2F 2C 25 00 FF CC 99 DA FF CC 99 D6 FF CC 99 A6 38 05 45 00 FF CC 99 07 FF CC 99 07 FF CC 99 04 39 28 23 00 FF CC 99 E8 FF CC 99 EA `  
  
`FF CC 99 C7 24 29 2F 00 FF CC 99 9E FF CC 99 CD FF CC 99 DA 04 09 2E 00 FF CC 99 22 FF CC 99 51 FF CC 99 16 3A 46 2C 00 FF CC 99 69 FF CC 99 79 FF CC 99 D6 09 04 `  
  
`06 00 19 19 19 51 19 19 19 22 19 19 19 26 09 06 18 00 19 19 19 51 19 19 19 26 19 19 19 86 09 18 24 00 19 19 19 51 19 19 19 86 19 19 19 9E 18 31 0B 00 19 19 19 86 `  
  
`19 19 19 1C 19 19 19 7C 30 18 0B 00 19 19 19 D0 19 19 19 86 19 19 19 7C 27 24 18 00 19 19 19 C9 19 19 19 9E 19 19 19 86 29 24 27 00 19 19 19 CD 19 19 19 9E 19 19 `  
  
`19 C9 20 3D 3C 00 19 19 19 EE 19 19 19 D1 19 19 19 E6 3D 3E 3C 00 19 19 19 D1 19 19 19 8D 19 19 19 E6 3D 3B 3E 00 19 19 19 D1 19 19 19 DA 19 19 19 8D 3D 44 3B 00 `  
  
`19 19 19 D1 19 19 19 DF 19 19 19 DA 44 3D 43 00 19 19 19 DF 19 19 19 D1 19 19 19 94 44 3F 22 00 19 19 19 DF 19 19 19 9F 19 19 19 BF 43 3D 40 00 19 19 19 94 19 19 `  
  
`19 D1 19 19 19 91 43 40 42 00 19 19 19 94 19 19 19 91 19 19 19 8D 41 42 40 00 19 19 19 4B 19 19 19 8D 19 19 19 91 40 3F 41 00 19 19 19 91 19 19 19 9F 19 19 19 4B `  
  
`43 3F 44 00 19 19 19 94 19 19 19 9F 19 19 19 DF 3D 3F 40 00 19 19 19 D1 19 19 19 9F 19 19 19 91 0E 12 0D 31 B4 00 00 2E B4 00 00 7B B4 00 00 30 B4 00 00 1C 1F 21 `  
  
`12 30 B4 00 00 C2 B4 00 00 D0 B4 00 00 7B B4 00 00 D0 32 0B 33 12 B4 00 00 57 B4 00 00 7C B4 00 00 8B B4 00 00 7B 35 37 0B 12 B4 00 00 98 B4 00 00 65 B4 00 00 7C `  
  
`B4 00 00 7B 33 12 34 30 B4 00 00 8B B4 00 00 7B B4 00 00 B2 B4 00 00 D0 37 36 12 31 B4 00 00 65 B4 00 00 3C B4 00 00 7B B4 00 00 1C 0E 0F 13 14 B4 00 00 2E B4 00 `  
  
`00 06 B4 00 00 53 B4 00 00 25 0E 0D 0F 07 B4 00 00 2E B4 00 00 30 B4 00 00 06 B4 00 00 1B 0F 07 10 01 B4 00 00 06 B4 00 00 1B B4 00 00 0B B4 00 00 07 13 17 1B 17 `  
  
`B4 00 00 53 B4 00 00 83 B4 00 00 9D B4 00 00 11 1A 17 19 17 B4 00 00 CB B4 00 00 11 B4 00 00 9F B4 00 00 83 11 10 0C 01 B4 00 00 27 B4 00 00 0B B4 00 00 31 B4 00 `  
  
`00 07 47 48 0C 11 B4 00 00 79 B4 00 00 85 B4 00 00 31 B4 00 00 27 22 20 1C 1D B4 00 00 BF B4 00 00 EE B4 00 00 CA B4 00 00 D9 1E 1D 26 20 B4 00 00 E9 B4 00 00 D9 `  
  
`B4 00 00 D4 B4 00 00 EE 1F 1B 1E 1A B4 00 00 C2 B4 00 00 9D B4 00 00 E9 B4 00 00 CB 21 1F 26 1E B4 00 00 D0 B4 00 00 C2 B4 00 00 D4 B4 00 00 E9 22 1C 47 48 B4 00 `  
  
`00 BF B4 00 00 CA B4 00 00 79 B4 00 00 85 00 01 05 45 FF CC 99 18 FF CC 99 07 FF CC 99 07 FF CC 99 04 08 09 25 24 FF CC 99 4A FF CC 99 51 FF CC 99 A6 FF CC 99 9E `  
  
`2C 3B 22 44 FF CC 99 D6 FF CC 99 DA FF CC 99 BF FF CC 99 DF 2C 28 3B 39 FF CC 99 D6 FF CC 99 EA FF CC 99 DA FF CC 99 E8 01 07 45 38 19 19 19 07 19 19 19 1B 19 19 `  
  
`19 04 19 19 19 07 0D 06 07 04 19 19 19 30 19 19 19 26 19 19 19 1B 19 19 19 22 06 0D 18 31 19 19 19 26 19 19 19 30 19 19 19 86 19 19 19 1C 27 18 21 30 19 19 19 C9 `  
  
`19 19 19 86 19 19 19 D0 19 19 19 D0 21 26 27 29 19 19 19 D0 19 19 19 D4 19 19 19 C9 19 19 19 CD 20 3B 26 39 19 19 19 EE 19 19 19 DA 19 19 19 D4 19 19 19 E8 20 22 `  
  
`3D 3F 19 19 19 EE 19 19 19 BF 19 19 19 D1 19 19 19 9F 3E 3B 3C 20 19 19 19 8D 19 19 19 DA 19 19 19 E6 19 19 19 EE 41 3F 42 43 19 19 19 4B 19 19 19 9F 19 19 19 8D `  
  
`19 19 19 94 00 08 46 2D FF CC 99 18 FF CC 99 4A FF CC 99 79 FF CC 99 76 2C 46 25 2D FF CC 99 D6 FF CC 99 79 FF CC 99 A6 FF CC 99 76 2C 22 3A 47 FF CC 99 D6 FF CC `  
  
`99 BF FF CC 99 69 FF CC 99 79 00 3A 0C 47 FF CC 99 18 FF CC 99 69 FF CC 99 31 FF CC 99 79 01 1C 14 78 00 1C 14 78 00 1C 14 78 1F A0 1C B9 10 A4 10 BA 20 1D 3F 18 `  
  
`20 00 3F 00 00 1D 00 00 1F 18 1F 00 00 A0 04 B9 00 02 01 00`

  
  
  
  
Model 6, skeleton data for 4th part \[at offset 0x000069EC\]:

  

`00 00 00 00 12 00 12 00 C3 FF 00 00 EE FF 12 00 C3 FF 00 00 EE FF EE FF C3 FF 00 00 12 00 EE FF C3 FF 00 00 12 00 12 00 B1 FF 00 00 EE FF 12 00 B1 FF 00 00 EE FF `  
  
`EE FF B1 FF 00 00 12 00 EE FF B1 FF 00 00 C5 FF 4B 00 EE FF 00 00 4F 00 4B 00 EE FF 00 00 3A 00 29 00 42 00 00 00 D0 FF 29 00 42 00 00 00 4F 00 B0 FF EE FF 00 00 `  
  
`C5 FF B0 FF EE FF 00 00 D0 FF D7 FF 42 00 00 00 3A 00 D7 FF 42 00 00 00 0C 0D 0F 0E 66 66 66 2E 66 66 66 C2 66 66 66 40 66 66 66 C4 0B 0A 0E 0F 66 66 66 BC 66 66 `  
  
`66 3C 66 66 66 C4 66 66 66 40 0C 0F 09 0A 66 66 66 2E 66 66 66 40 66 66 66 27 66 66 66 3C 09 0A 08 0B 66 66 66 27 66 66 66 3C 66 66 66 CA 66 66 66 BC 0D 08 0E 0B `  
  
`FF FF 99 C2 FF FF 99 CA FF FF 99 C4 FF FF 99 BC 0D 0C 02 03 FF FF 99 C2 FF FF 99 2E FF FF 99 C1 FF FF 99 2F 0C 09 03 00 FF FF 99 2E FF FF 99 27 FF FF 99 2F FF FF `  
  
`99 43 08 01 09 00 FF FF 99 CA FF FF 99 C5 FF FF 99 27 FF FF 99 43 0D 02 08 01 FF FF 99 C2 FF FF 99 C1 FF FF 99 CA FF FF 99 C5 03 07 02 06 FF CC 99 2F FF CC 99 2F `  
  
`FF CC 99 C1 FF CC 99 C1 07 03 04 00 FF CC 99 2F FF CC 99 2F FF CC 99 2B FF CC 99 43 01 05 00 04 FF CC 99 C5 FF CC 99 C5 FF CC 99 43 FF CC 99 2B 06 05 02 01 FF CC `  
  
`99 C1 FF CC 99 C5 FF CC 99 C1 FF CC 99 C5 05 06 04 07 FF CC 99 C5 FF CC 99 C1 FF CC 99 2B FF CC 99 2F`

  
  
  
  
Model 6, skeleton data for 5th part \[at offset 0x00006B88\]:

  

`00 00 00 00 3B 00 C5 FF 6A FF 00 00 C6 FF C5 FF 6A FF 00 00 C6 FF C5 FF AA FF 00 00 3B 00 C5 FF AA FF 00 00 C6 FF 3B 00 6A FF 00 00 3B 00 3B 00 6A FF 00 00 3B 00 `  
  
`3B 00 AA FF 00 00 C6 FF 3B 00 AA FF 00 00 12 00 EE FF 00 00 00 00 EE FF EE FF 00 00 00 00 EE FF 12 00 00 00 00 00 12 00 12 00 00 00 00 00 12 00 EE FF D9 FF 00 00 `  
  
`EE FF EE FF D9 FF 00 00 EE FF 12 00 D9 FF 00 00 12 00 12 00 D9 FF 00 00 0C 0D 08 09 00 00 50 28 00 00 50 C6 00 00 50 28 00 00 50 C6 0F 0C 0B 08 00 00 50 2C 00 00 `  
  
`50 28 00 00 50 2C 00 00 50 28 0E 0F 0A 0B 00 00 50 C0 00 00 50 2C 00 00 50 C0 00 00 50 2C 0A 09 0E 0D 00 00 50 C0 00 00 50 C6 00 00 50 C0 00 00 50 C6 08 09 0B 0A `  
  
`00 00 50 28 00 00 50 C6 00 00 50 2C 00 00 50 C0 01 02 00 03 FF CC 99 C1 FF CC 99 C9 FF CC 99 2F FF CC 99 26 05 06 04 07 FF CC 99 2B FF CC 99 18 FF CC 99 C5 FF CC `  
  
`99 D6 05 04 00 01 FF CC 99 2B FF CC 99 C5 FF CC 99 2F FF CC 99 C1 00 03 05 06 FF CC 99 2F FF CC 99 26 FF CC 99 2B FF CC 99 18 02 01 07 04 FF CC 99 C9 FF CC 99 C1 `  
  
`FF CC 99 D6 FF CC 99 C5 03 02 0C 0D FF CC 99 26 FF CC 99 C9 FF CC 99 28 FF CC 99 C6 07 0E 02 0D FF CC 99 D6 FF CC 99 C0 FF CC 99 C9 FF CC 99 C6 07 06 0E 0F FF CC `  
  
`99 D6 FF CC 99 18 FF CC 99 C0 FF CC 99 2C 06 03 0F 0C FF CC 99 18 FF CC 99 26 FF CC 99 2C FF CC 99 28`

  
  
  
  
Model 6, skeleton data for 6th part \[at offset 0x00006D24\]:

  

`00 00 00 00 3B 00 C5 FF 00 00 00 00 C6 FF C5 FF 00 00 00 00 C6 FF 3B 00 00 00 00 00 3B 00 3B 00 00 00 00 00 32 00 31 00 BA FF 00 00 CF FF 31 00 BA FF 00 00 CF FF `  
  
`CF FF BA FF 00 00 32 00 CF FF BA FF 00 00 03 04 00 07 FF CC 99 2C FF CC 99 43 FF CC 99 28 FF CC 99 2F 01 00 06 07 FF CC 99 C6 FF CC 99 28 FF CC 99 C1 FF CC 99 2F `  
  
`01 06 02 05 FF CC 99 C6 FF CC 99 C1 FF CC 99 C0 FF CC 99 AD 02 05 03 04 FF CC 99 C0 FF CC 99 AD FF CC 99 2C FF CC 99 43 04 05 07 06 FF CC 99 43 FF CC 99 AD FF CC `  
  
`99 2F FF CC 99 C1 03 00 02 01 FF CC 99 2C FF CC 99 28 FF CC 99 C0 FF CC 99 C6`

  
  
  
  
Model 6, skeleton data for 7th part \[at offset 0x00006DE0\]:

  

`00 00 00 00 C6 FF D7 FF 42 00 00 00 30 00 D7 FF 42 00 00 00 3B 00 B0 FF EE FF 00 00 B1 FF B0 FF EE FF 00 00 30 00 29 00 42 00 00 00 C6 FF 29 00 42 00 00 00 B1 FF `  
  
`4B 00 EE FF 00 00 3B 00 4B 00 EE FF 00 00 EE FF EE FF B1 FF 00 00 12 00 EE FF B1 FF 00 00 12 00 12 00 B1 FF 00 00 EE FF 12 00 B1 FF 00 00 EE FF EE FF C3 FF 00 00 `  
  
`12 00 EE FF C3 FF 00 00 12 00 12 00 C3 FF 00 00 EE FF 12 00 C3 FF 00 00 03 00 02 01 66 66 66 C2 66 66 66 AE 66 66 66 2E 66 66 66 29 04 01 05 00 66 66 66 33 66 66 `  
  
`66 29 66 66 66 B2 66 66 66 AE 03 06 00 05 66 66 66 C2 66 66 66 CA 66 66 66 AE 66 66 66 B2 06 07 05 04 66 66 66 CA 66 66 66 27 66 66 66 B2 66 66 66 33 02 01 07 04 `  
  
`FF FF 99 2E FF FF 99 29 FF FF 99 27 FF FF 99 33 02 0D 03 0C FF FF 99 2E FF FF 99 2F FF FF 99 C2 FF FF 99 C1 03 0C 06 0F FF FF 99 C2 FF FF 99 C1 FF FF 99 CA FF FF `  
  
`99 AD 07 06 0E 0F FF FF 99 27 FF FF 99 CA FF FF 99 2B FF FF 99 AD 02 07 0D 0E FF FF 99 2E FF FF 99 27 FF FF 99 2F FF FF 99 2B 0C 0D 08 09 FF CC 99 C1 FF CC 99 2F `  
  
`FF CC 99 C1 FF CC 99 2F 0C 08 0F 0B FF CC 99 C1 FF CC 99 C1 FF CC 99 AD FF CC 99 C5 0F 0B 0E 0A FF CC 99 AD FF CC 99 C5 FF CC 99 2B FF CC 99 2B 09 0D 0A 0E FF CC `  
  
`99 2F FF CC 99 2F FF CC 99 2B FF CC 99 2B 0A 0B 09 08 FF CC 99 2B FF CC 99 C5 FF CC 99 2F FF CC 99 C1`

  
  
  
  
Model 6, skeleton data for 8th part \[at offset 0x00006F7C\]:

  

`00 00 00 00 EE FF 12 00 D9 FF 00 00 12 00 12 00 D9 FF 00 00 12 00 EE FF D9 FF 00 00 EE FF EE FF D9 FF 00 00 EE FF 12 00 00 00 00 00 12 00 12 00 00 00 00 00 12 00 `  
  
`EE FF 00 00 00 00 EE FF EE FF 00 00 00 00 3A 00 3B 00 AA FF 00 00 C5 FF 3B 00 AA FF 00 00 C5 FF 3B 00 6A FF 00 00 3A 00 3B 00 6A FF 00 00 C5 FF C5 FF AA FF 00 00 `  
  
`3A 00 C5 FF AA FF 00 00 3A 00 C5 FF 6A FF 00 00 C5 FF C5 FF 6A FF 00 00 02 03 06 07 00 00 50 28 00 00 50 C6 00 00 50 28 00 00 50 C6 00 04 03 07 00 00 50 C0 00 00 `  
  
`50 C0 00 00 50 C6 00 00 50 C6 05 04 01 00 00 00 50 2C 00 00 50 C0 00 00 50 2C 00 00 50 C0 06 05 02 01 00 00 50 28 00 00 50 2C 00 00 50 28 00 00 50 2C 07 04 06 05 `  
  
`00 00 50 C6 00 00 50 C0 00 00 50 28 00 00 50 2C 0C 0D 0F 0E FF CC 99 C9 FF CC 99 26 FF CC 99 C1 FF CC 99 2F 09 0A 08 0B FF CC 99 D6 FF CC 99 C5 FF CC 99 18 FF CC `  
  
`99 2B 0B 0A 0E 0F FF CC 99 2B FF CC 99 C5 FF CC 99 2F FF CC 99 C1 0A 09 0F 0C FF CC 99 C5 FF CC 99 D6 FF CC 99 C1 FF CC 99 C9 08 0B 0D 0E FF CC 99 18 FF CC 99 2B `  
  
`FF CC 99 26 FF CC 99 2F 0C 03 0D 02 FF CC 99 C9 FF CC 99 C6 FF CC 99 26 FF CC 99 28 08 0D 01 02 FF CC 99 18 FF CC 99 26 FF CC 99 2C FF CC 99 28 08 01 09 00 FF CC `  
  
`99 18 FF CC 99 2C FF CC 99 D6 FF CC 99 C0 09 00 0C 03 FF CC 99 D6 FF CC 99 C0 FF CC 99 C9 FF CC 99 C6`

  
  
  
  
Model 6, skeleton data for 9th part \[at offset 0x00007118\]:

  

`00 00 00 00 CE FF CF FF BA FF 00 00 31 00 CF FF BA FF 00 00 31 00 31 00 BA FF 00 00 CE FF 31 00 BA FF 00 00 C5 FF 3B 00 00 00 00 00 3A 00 3B 00 00 00 00 00 3A 00 `  
  
`C5 FF 00 00 00 00 C5 FF C5 FF 00 00 00 00 07 00 04 03 FF CC 99 C6 FF CC 99 C1 FF CC 99 C0 FF CC 99 AD 07 06 00 01 FF CC 99 C6 FF CC 99 28 FF CC 99 C1 FF CC 99 2F `  
  
`05 02 06 01 FF CC 99 2C FF CC 99 43 FF CC 99 28 FF CC 99 2F 04 03 05 02 FF CC 99 C0 FF CC 99 AD FF CC 99 2C FF CC 99 43 03 00 02 01 FF CC 99 AD FF CC 99 C1 FF CC `  
  
`99 43 FF CC 99 2F 05 06 04 07 FF CC 99 2C FF CC 99 28 FF CC 99 C0 FF CC 99 C6`

  
  
  
  
Model 6, skeleton data for 10th part \[at offset 0x000071D4\]:

  

`00 00 00 00 39 00 47 00 53 FF 00 00 C4 FF 40 00 53 FF 00 00 3F 00 D6 FF 53 FF 00 00 04 00 C0 FF 53 FF 00 00 CB FF BC FF 53 FF 00 00 D0 FF 6A FF 8D FF 00 00 C0 FF `  
  
`85 00 8D FF 00 00 72 00 92 FF 8D FF 00 00 09 00 6D FF 8D FF 00 00 D0 FF 6A FF 2B 00 00 00 BF FF 98 00 2B 00 00 00 7C 00 93 FF 2B 00 00 00 09 00 6D FF 2B 00 00 00 `  
  
`6C 00 A2 00 2B 00 00 00 63 00 8F 00 8D FF 00 00 03 02 04 00 00 00 50 6B 00 00 50 48 00 00 50 BE 09 0B 0C 00 00 00 50 AC 00 00 50 28 00 00 50 72 07 0E 02 00 00 00 `  
  
`50 1B 00 00 50 27 00 00 50 48 00 00 50 44 0A 0D 09 0B 00 00 50 C0 00 00 50 34 00 00 50 AC 00 00 50 28 0D 0E 0B 07 00 00 50 34 00 00 50 27 00 00 50 28 00 00 50 1B `  
  
`05 09 08 0C 00 00 50 BA 00 00 50 AC 00 00 50 64 00 00 50 72 0B 07 0C 08 00 00 50 28 00 00 50 1B 00 00 50 72 00 00 50 64 0D 0A 0E 06 00 00 50 34 00 00 50 C0 00 00 `  
  
`50 27 00 00 50 CA 0A 09 06 05 00 00 50 C0 00 00 50 AC 00 00 50 CA 00 00 50 BA 03 04 08 05 00 00 50 6B 00 00 50 BE 00 00 50 64 00 00 50 BA 07 02 08 03 00 00 50 1B `  
  
`00 00 50 48 00 00 50 64 00 00 50 6B 05 04 06 01 00 00 50 BA 00 00 50 BE 00 00 50 CA 00 00 50 C7 0E 06 00 01 00 00 50 27 00 00 50 CA 00 00 50 44 00 00 50 C7 01 04 `  
  
`00 02 00 00 50 C7 00 00 50 BE 00 00 50 44 00 00 50 48`

  
  
  
  
Model 6, skeleton data for 11th part \[at offset 0x00007360\]:

  

`00 00 00 00 00 00 D0 FF CB FF 00 00 00 00 D0 FF 10 00 00 00 30 00 00 00 10 00 00 00 30 00 00 00 CB FF 00 00 D0 FF 00 00 10 00 00 00 00 00 30 00 10 00 00 00 00 00 `  
  
`30 00 CB FF 00 00 D0 FF 00 00 CB FF 00 00 1F 00 00 00 B6 FF 00 00 1F 00 00 00 CB FF 00 00 00 00 1F 00 CB FF 00 00 00 00 1F 00 B6 FF 00 00 E1 FF 00 00 CB FF 00 00 `  
  
`E1 FF 00 00 B6 FF 00 00 00 00 E1 FF B6 FF 00 00 00 00 E1 FF CB FF 00 00 3A 00 00 00 7D FF 00 00 3A 00 00 00 B6 FF 00 00 00 00 3A 00 B6 FF 00 00 00 00 3A 00 7D FF `  
  
`00 00 C6 FF 00 00 7D FF 00 00 00 00 C6 FF 7D FF 00 00 C6 FF 00 00 B6 FF 00 00 00 00 C6 FF B6 FF 00 00 16 17 14 15 43 0F 00 E7 43 0F 00 6F 43 0F 00 E6 43 0F 00 8B `  
  
`11 10 17 15 43 0F 00 0A 43 0F 00 08 43 0F 00 6F 43 0F 00 8B 16 14 12 13 43 0F 00 E7 43 0F 00 E6 43 0F 00 77 43 0F 00 80 10 11 13 12 43 0F 00 08 43 0F 00 0A 43 0F `  
  
`00 80 43 0F 00 77 17 16 11 12 43 0F 00 6F 43 0F 00 E7 43 0F 00 0A 43 0F 00 77 15 10 14 13 43 0F 00 8B 43 0F 00 08 43 0F 00 E6 43 0F 00 80 0F 09 0E 08 FF CC 99 6F `  
  
`FF CC 99 0A FF CC 99 8B FF CC 99 08 0A 0B 09 08 FF CC 99 77 FF CC 99 80 FF CC 99 0A FF CC 99 08 0A 0C 0B 0D FF CC 99 77 FF CC 99 E7 FF CC 99 80 FF CC 99 E6 0A 09 `  
  
`0C 0F FF CC 99 77 FF CC 99 0A FF CC 99 E7 FF CC 99 6F 0E 0D 0F 0C FF CC 99 8B FF CC 99 E6 FF CC 99 6F FF CC 99 E7 0E 08 0D 0B FF CC 99 8B FF CC 99 08 FF CC 99 E6 `  
  
`FF CC 99 80 01 02 00 03 00 00 50 6F 00 00 50 0A 00 00 50 8B 00 00 50 08 00 07 01 04 00 00 50 8B 00 00 50 E6 00 00 50 6F 00 00 50 E7 06 07 03 00 00 00 50 80 00 00 `  
  
`50 E6 00 00 50 08 00 00 50 8B 06 03 05 02 00 00 50 80 00 00 50 08 00 00 50 77 00 00 50 0A 07 06 04 05 00 00 50 E6 00 00 50 80 00 00 50 E7 00 00 50 77 05 02 04 01 `  
  
`00 00 50 77 00 00 50 0A 00 00 50 E7 00 00 50 6F`

  
  
  
  
Model 6, skeleton data for 12th part \[at offset 0x0000758C\]:

  

`00 00 00 00 3A 00 E2 FF 05 00 00 00 49 00 9E FF 65 FF 00 00 BB FF 9E FF 65 FF 00 00 C6 FF E2 FF 05 00 00 00 49 00 00 00 33 FF 00 00 3A 00 22 00 FA FF 00 00 BB FF `  
  
`00 00 33 FF 00 00 C6 FF 22 00 FA FF 00 00 00 00 2E 00 42 00 00 00 00 00 EE FF 4D 00 00 00 07 05 08 00 43 0F 00 C3 43 0F 00 2D 43 0F 00 77 00 03 09 00 43 0F 00 22 `  
  
`43 0F 00 CD 43 0F 00 7C 06 04 07 05 43 0F 00 C7 43 0F 00 2A 43 0F 00 C3 43 0F 00 2D 02 01 06 04 43 0F 00 C2 43 0F 00 2E 43 0F 00 C7 43 0F 00 2A 00 09 05 08 43 0F `  
  
`00 22 43 0F 00 7C 43 0F 00 2D 43 0F 00 77 07 08 03 09 43 0F 00 C3 43 0F 00 77 43 0F 00 CD 43 0F 00 7C 06 07 02 03 43 0F 00 C7 43 0F 00 C3 43 0F 00 C2 43 0F 00 CD `  
  
`04 01 05 00 43 0F 00 2A 43 0F 00 2E 43 0F 00 2D 43 0F 00 22 02 03 01 00 43 0F 00 C2 43 0F 00 CD 43 0F 00 2E 43 0F 00 22`

  
  
  
  
Model 6, skeleton data for 13th part \[at offset 0x0000768C\]:

  

`00 00 00 00 9D FF 8F 00 8D FF 00 00 94 FF A2 00 2B 00 00 00 F7 FF 6D FF 2B 00 00 00 84 FF 93 FF 2B 00 00 00 41 00 98 00 2B 00 00 00 30 00 6A FF 2B 00 00 00 F7 FF `  
  
`6D FF 8D FF 00 00 8E FF 92 FF 8D FF 00 00 40 00 85 00 8D FF 00 00 30 00 6A FF 8D FF 00 00 35 00 BC FF 53 FF 00 00 FC FF C0 FF 53 FF 00 00 C1 FF D6 FF 53 FF 00 00 `  
  
`3C 00 40 00 53 FF 00 00 C7 FF 47 00 53 FF 00 00 03 05 02 00 00 00 50 C6 00 00 50 42 00 00 50 7E 0C 0B 0A 00 00 00 50 A7 00 00 50 87 00 00 50 32 0A 0D 0C 0E 00 00 `  
  
`50 32 00 00 50 2A 00 00 50 A7 00 00 50 AB 00 0E 08 0D 00 00 50 CA 00 00 50 AB 00 00 50 27 00 00 50 2A 09 08 0A 0D 00 00 50 36 00 00 50 27 00 00 50 32 00 00 50 2A `  
  
`07 06 0C 0B 00 00 50 D4 00 00 50 8A 00 00 50 A7 00 00 50 87 0B 06 0A 09 00 00 50 87 00 00 50 8A 00 00 50 32 00 00 50 36 04 08 05 09 00 00 50 2C 00 00 50 27 00 00 `  
  
`50 42 00 00 50 36 04 01 08 00 00 00 50 2C 00 00 50 B8 00 00 50 27 00 00 50 CA 03 02 07 06 00 00 50 C6 00 00 50 7E 00 00 50 D4 00 00 50 8A 05 09 02 06 00 00 50 42 `  
  
`00 00 50 36 00 00 50 7E 00 00 50 8A 03 07 01 00 00 00 50 C6 00 00 50 D4 00 00 50 B8 00 00 50 CA 05 03 04 01 00 00 50 42 00 00 50 C6 00 00 50 2C 00 00 50 B8 00 07 `  
  
`0E 0C 00 00 50 CA 00 00 50 D4 00 00 50 AB 00 00 50 A7`

  
  
  
  
Model 6, skeleton data for 14th part \[at offset 0x00007818\]:

  

`00 00 00 00 00 00 C6 FF B6 FF 00 00 3A 00 00 00 B6 FF 00 00 00 00 C6 FF 7D FF 00 00 3A 00 00 00 7D FF 00 00 00 00 3A 00 7D FF 00 00 00 00 3A 00 B6 FF 00 00 C6 FF `  
  
`00 00 B6 FF 00 00 C6 FF 00 00 7D FF 00 00 00 00 E1 FF CB FF 00 00 00 00 E1 FF B6 FF 00 00 1F 00 00 00 B6 FF 00 00 1F 00 00 00 CB FF 00 00 00 00 1F 00 B6 FF 00 00 `  
  
`00 00 1F 00 CB FF 00 00 E1 FF 00 00 CB FF 00 00 E1 FF 00 00 B6 FF 00 00 30 00 00 00 CB FF 00 00 00 00 30 00 CB FF 00 00 00 00 30 00 10 00 00 00 30 00 00 00 10 00 `  
  
`00 00 D0 FF 00 00 CB FF 00 00 D0 FF 00 00 10 00 00 00 00 00 D0 FF 10 00 00 00 00 00 D0 FF CB FF 00 00 00 02 06 07 43 0F 00 6F 43 0F 00 65 43 0F 00 E7 43 0F 00 E6 `  
  
`00 01 02 03 43 0F 00 6F 43 0F 00 0A 43 0F 00 65 43 0F 00 08 00 06 01 05 43 0F 00 6F 43 0F 00 E7 43 0F 00 0A 43 0F 00 77 05 04 01 03 43 0F 00 77 43 0F 00 80 43 0F `  
  
`00 0A 43 0F 00 08 04 05 07 06 43 0F 00 80 43 0F 00 77 43 0F 00 E6 43 0F 00 E7 02 03 07 04 43 0F 00 65 43 0F 00 08 43 0F 00 E6 43 0F 00 80 0D 0E 0C 0F FF CC 99 77 `  
  
`FF CC 99 E7 FF CC 99 80 FF CC 99 E6 0D 0C 0B 0A FF CC 99 77 FF CC 99 80 FF CC 99 0A FF CC 99 08 09 08 0A 0B FF CC 99 65 FF CC 99 6F FF CC 99 08 FF CC 99 0A 08 09 `  
  
`0E 0F FF CC 99 6F FF CC 99 65 FF CC 99 E7 FF CC 99 E6 0D 0B 0E 08 FF CC 99 77 FF CC 99 0A FF CC 99 E7 FF CC 99 6F 09 0A 0F 0C FF CC 99 65 FF CC 99 08 FF CC 99 E6 `  
  
`FF CC 99 80 15 16 14 17 00 00 50 E7 00 00 50 6F 00 00 50 E6 00 00 50 65 16 13 17 10 00 00 50 6F 00 00 50 0A 00 00 50 65 00 00 50 08 11 10 12 13 00 00 50 80 00 00 `  
  
`50 08 00 00 50 77 00 00 50 0A 15 14 12 11 00 00 50 E7 00 00 50 E6 00 00 50 77 00 00 50 80 11 14 10 17 00 00 50 80 00 00 50 E6 00 00 50 08 00 00 50 65 12 13 15 16 `  
  
`00 00 50 77 00 00 50 0A 00 00 50 E7 00 00 50 6F`

  
  
  
  
Model 6, skeleton data for 15th part \[at offset 0x00007A44\]:

  

`00 00 00 00 00 00 EE FF 4D 00 00 00 00 00 2E 00 42 00 00 00 3A 00 22 00 FA FF 00 00 46 00 00 00 33 FF 00 00 C6 FF 22 00 FA FF 00 00 B7 FF 00 00 33 FF 00 00 3A 00 `  
  
`E2 FF 05 00 00 00 46 00 9E FF 65 FF 00 00 B7 FF 9E FF 65 FF 00 00 C6 FF E2 FF 05 00 00 00 06 09 00 00 43 0F 00 22 43 0F 00 CD 43 0F 00 7C 04 02 01 00 43 0F 00 C3 `  
  
`43 0F 00 2D 43 0F 00 77 07 08 06 09 43 0F 00 2E 43 0F 00 C2 43 0F 00 22 43 0F 00 CD 05 04 08 09 43 0F 00 C7 43 0F 00 C3 43 0F 00 C2 43 0F 00 CD 03 07 02 06 43 0F `  
  
`00 2A 43 0F 00 2E 43 0F 00 2D 43 0F 00 22 06 00 02 01 43 0F 00 22 43 0F 00 7C 43 0F 00 2D 43 0F 00 77 09 04 00 01 43 0F 00 CD 43 0F 00 C3 43 0F 00 7C 43 0F 00 77 `  
  
`08 07 05 03 43 0F 00 C2 43 0F 00 2E 43 0F 00 C7 43 0F 00 2A 03 02 05 04 43 0F 00 2A 43 0F 00 2D 43 0F 00 C7 43 0F 00 C3`

  
  
  
  
Model 7, Model 8, and Model 9 skeleton data for 1st part \[at offset
0x00007B44\]:

  

`00 00 00 00 5E 00 3C 00 B1 FF 00 00 54 00 0C FF 91 00 00 00 73 00 25 00 A0 FF 00 00 68 00 F5 FE 80 00 00 00 4D 00 25 00 9F FF 00 00 42 00 F5 FE 7F 00 00 00 B2 FF `  
  
`1F 00 C4 FF 00 00 00 00 BF FF C4 FF 00 00 B1 FF E0 FF C4 FF 00 00 4F 00 E0 FF C4 FF 00 00 4F 00 20 00 C4 FF 00 00 79 00 DE FF FB FF 00 00 88 FF DC FF FB FF 00 00 `  
  
`87 FF 26 00 FB FF 00 00 78 00 28 00 FB FF 00 00 01 00 9F FF F3 FF 00 00 C7 FF 50 00 04 00 00 00 37 00 51 00 04 00 00 00 AF FF 72 FF E4 00 00 00 56 00 6A FF E4 00 `  
  
`00 00 44 FF EE FF E3 00 00 00 7B FF 5F 00 E4 00 00 00 83 00 62 00 E4 00 00 00 BD 00 F1 FF E3 00 00 00 A7 FF E1 FF 04 00 00 00 5A 00 DD FF 04 00 00 00 2A 00 33 00 `  
  
`C4 FF 00 00 D5 FF 32 00 C4 FF 00 00 E5 FF 44 00 18 00 00 00 D5 FF E5 FF 19 00 00 00 2C 00 E1 FF 19 00 00 00 1A 00 44 00 18 00 00 00 77 00 60 00 BC 00 00 00 B1 00 `  
  
`F2 FF BD 00 00 00 51 00 74 FF BB 00 00 00 B2 FF 7A FF BB 00 00 00 51 FF EF FF BD 00 00 00 87 FF 5D 00 BC 00 00 00 01 03 05 00 6F 68 66 82 6F 68 66 26 6F 68 66 C9 `  
  
`00 04 02 00 6F 68 66 79 6F 68 66 AF 6F 68 66 2A 18 12 14 00 0F 0F 12 10 0F 0F 12 35 0F 0F 12 90 18 25 10 00 0F 0F 12 10 0F 0F 12 17 0F 0F 12 85 19 11 20 00 0F 0F `  
  
`12 DC 0F 0F 12 66 0F 0F 12 61 19 17 13 00 0F 0F 12 DC 0F 0F 12 5E 0F 0F 12 BB 15 18 14 00 0F 0F 12 16 0F 0F 12 10 0F 0F 12 90 25 18 15 00 0F 0F 12 17 0F 0F 12 10 `  
  
`0F 0F 12 16 19 16 17 00 0F 0F 12 DC 0F 0F 12 DB 0F 0F 12 5E 19 20 16 00 0F 0F 12 DC 0F 0F 12 61 0F 0F 12 DB 1D 10 1C 00 1F 1E 25 94 1F 1E 25 89 1F 1E 25 8D 11 1E `  
  
`1F 00 1F 1E 25 4E 1F 1E 25 5B 1F 1E 25 62 1E 11 19 00 1F 1E 25 5B 1F 1E 25 4E 1F 1E 25 CC 10 1D 18 00 1F 1E 25 89 1F 1E 25 94 1F 1E 25 24 09 0F 0B 00 5E 0C 12 2F `  
  
`5E 0C 12 7B 5E 0C 12 1B 0F 08 0C 00 5E 0C 12 7B 5E 0C 12 B3 5E 0C 12 D4 0F 09 07 00 5E 0C 12 7B 5E 0C 12 2F 5E 0C 12 65 08 0F 07 00 5E 0C 12 B3 5E 0C 12 7B 5E 0C `  
  
`12 65 0E 20 11 00 5E 0C 12 23 5E 0C 12 1E 5E 0C 12 3B 21 0E 0B 00 5E 0C 12 03 5E 0C 12 23 5E 0C 12 1B 22 21 0B 00 5E 0C 12 4F 5E 0C 12 03 5E 0C 12 1B 22 0B 0F 00 `  
  
`5E 0C 12 4F 5E 0C 12 1B 5E 0C 12 7B 23 22 0F 00 5E 0C 12 A1 5E 0C 12 4F 5E 0C 12 7B 23 0F 0C 00 5E 0C 12 A1 5E 0C 12 7B 5E 0C 12 D4 24 23 0C 00 5E 0C 12 EF 5E 0C `  
  
`12 A1 5E 0C 12 D4 24 0C 0D 00 5E 0C 12 EF 5E 0C 12 D4 5E 0C 12 D9 25 0D 10 00 5E 0C 12 9A 5E 0C 12 D9 5E 0C 12 B5 21 20 0E 00 5E 0C 12 03 5E 0C 12 1E 5E 0C 12 23 `  
  
`25 24 0D 00 5E 0C 12 9A 5E 0C 12 EF 5E 0C 12 D9 07 1A 1B 00 5E 0C 12 6B 5E 0C 12 6C 5E 0C 12 6C 01 05 00 04 6F 68 66 76 6F 68 66 E3 6F 68 66 76 6F 68 66 E3 05 03 `  
  
`04 02 6F 68 66 E3 6F 68 66 0D 6F 68 66 E3 6F 68 66 0D 01 00 03 02 6F 68 66 76 6F 68 66 76 6F 68 66 0D 6F 68 66 0D 19 13 18 12 0F 0F 12 DC 0F 0F 12 BB 0F 0F 12 10 `  
  
`0F 0F 12 35 1E 1D 1F 1C 1F 1E 25 5B 1F 1E 25 94 1F 1E 25 62 1F 1E 25 8D 11 1F 10 1C 1F 1E 25 4E 1F 1E 25 62 1F 1E 25 89 1F 1E 25 8D 10 1B 11 1A 1F 1E 25 89 1F 1E `  
  
`25 95 1F 1E 25 4E 1F 1E 25 7D 07 09 1A 0A 5E 0C 12 6B 5E 0C 12 3D 5E 0C 12 6C 5E 0C 12 41 0D 0C 06 08 5E 0C 12 D9 5E 0C 12 D4 5E 0C 12 C5 5E 0C 12 B3 0B 0E 09 0A `  
  
`5E 0C 12 1B 5E 0C 12 23 5E 0C 12 2F 5E 0C 12 2B 11 1A 0E 0A 5E 0C 12 3B 5E 0C 12 5A 5E 0C 12 23 5E 0C 12 2B 10 0D 1B 06 5E 0C 12 B5 5E 0C 12 D9 5E 0C 12 7D 5E 0C `  
  
`12 C5 07 1B 08 06 5E 0C 12 6B 5E 0C 12 6C 5E 0C 12 6C 5E 0C 12 AF 13 17 22 21 29 21 4F 73 29 21 4F 08 29 21 4F 4F 29 21 4F 03 13 22 12 23 29 21 4F 73 29 21 4F 4F `  
  
`29 21 4F 7C 29 21 4F A1 16 20 17 21 29 21 4F DA 29 21 4F 1E 29 21 4F 08 29 21 4F 03 15 14 25 24 29 21 4F E5 29 21 4F E6 29 21 4F 9A 29 21 4F EF 12 23 14 24 29 21 `  
  
`4F 7C 29 21 4F A1 29 21 4F E6 29 21 4F EF`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 2nd part \[at offset
0x00007FC0\]:

  

`00 00 00 00 B2 FF 21 00 E3 FF 00 00 B3 FF E2 FF E0 FF 00 00 4E 00 E3 FF E0 FF 00 00 4D 00 21 00 E3 FF 00 00 00 00 3E 00 E5 FF 00 00 00 00 C2 FF DE FF 00 00 00 00 `  
  
`8B FF 8B FF 00 00 00 00 6D 00 C1 FF 00 00 41 00 D7 FF 55 FF 00 00 00 00 BA FF 5C FF 00 00 BF FF D7 FF 55 FF 00 00 C4 FF 1F 00 63 FF 00 00 3C 00 1F 00 63 FF 00 00 `  
  
`94 00 22 00 A7 FF 00 00 6C FF 22 00 A7 FF 00 00 7A FF 90 FF 9F FF 00 00 86 00 90 FF 9F FF 00 00 D1 FF CB FF 34 FF 00 00 2F 00 CB FF 34 FF 00 00 4D 00 E0 FF FE FF `  
  
`00 00 00 00 C0 FF FD FF 00 00 B2 FF E1 FF FE FF 00 00 B3 FF 20 00 02 00 00 00 00 00 3C 00 03 00 00 00 4E 00 1F 00 02 00 00 00 97 00 E4 FF 6D FF 00 00 69 FF E4 FF `  
  
`6D FF 00 00 27 00 2B 00 47 FF 00 00 D9 FF 2B 00 47 FF 00 00 0A 00 46 00 58 FF 00 00 F6 FF 46 00 58 FF 00 00 19 00 3E 00 77 FF 00 00 E7 FF 3E 00 77 FF 00 00 09 08 `  
  
`12 00 29 21 4F 7B 29 21 4F 53 29 21 4F 36 11 09 12 00 29 21 4F BA 29 21 4F 7B 29 21 4F 36 0A 09 11 00 29 21 4F D7 29 21 4F 7B 29 21 4F BA 0E 0F 1A 00 5E 0C 12 E0 `  
  
`5E 0C 12 C4 5E 0C 12 CB 10 0D 19 00 5E 0C 12 29 5E 0C 12 0F 5E 0C 12 2A 0D 02 03 00 5E 0C 12 0F 5E 0C 12 51 5E 0C 12 2C 0E 00 01 00 5E 0C 12 E0 5E 0C 12 B2 5E 0C `  
  
`12 C6 06 02 10 00 5E 0C 12 72 5E 0C 12 51 5E 0C 12 29 01 06 0F 00 5E 0C 12 C6 5E 0C 12 72 5E 0C 12 C4 07 0E 20 00 5E 0C 12 79 5E 0C 12 E0 5E 0C 12 92 03 07 0D 00 `  
  
`5E 0C 12 2C 5E 0C 12 79 5E 0C 12 0F 00 0E 07 00 5E 0C 12 B2 5E 0C 12 E0 5E 0C 12 79 1F 0D 07 00 5E 0C 12 5C 5E 0C 12 0F 5E 0C 12 79 06 05 02 00 5E 0C 12 72 5E 0C `  
  
`12 6F 5E 0C 12 51 04 07 03 00 5E 0C 12 76 5E 0C 12 79 5E 0C 12 2C 06 01 05 00 5E 0C 12 72 5E 0C 12 C6 5E 0C 12 6F 00 07 04 00 5E 0C 12 B2 5E 0C 12 79 5E 0C 12 76 `  
  
`0C 08 19 00 5E 0C 12 50 5E 0C 12 58 5E 0C 12 2A 0B 1A 0A 00 5E 0C 12 9F 5E 0C 12 CB 5E 0C 12 9D 0D 1F 0C 00 5E 0C 12 0F 5E 0C 12 5C 5E 0C 12 50 1F 07 20 00 5E 0C `  
  
`12 5C 5E 0C 12 79 5E 0C 12 92 0E 0B 20 00 5E 0C 12 E0 5E 0C 12 9F 5E 0C 12 92 19 0D 0C 00 5E 0C 12 2A 5E 0C 12 0F 5E 0C 12 50 1A 0B 0E 00 5E 0C 12 CB 5E 0C 12 9F `  
  
`5E 0C 12 E0 02 0D 10 00 5E 0C 12 51 5E 0C 12 0F 5E 0C 12 29 0E 01 0F 00 5E 0C 12 E0 5E 0C 12 C6 5E 0C 12 C4 08 06 10 00 55 50 45 63 55 50 45 7A 55 50 45 1C 08 09 `  
  
`06 00 55 50 45 63 55 50 45 65 55 50 45 7A 09 0A 06 00 55 50 45 65 55 50 45 A3 55 50 45 7A 06 0A 0F 00 55 50 45 7A 55 50 45 A3 55 50 45 D0 1A 0F 0A 00 55 50 45 9D `  
  
`55 50 45 D0 55 50 45 A3 19 08 10 00 55 50 45 25 55 50 45 63 55 50 45 1C 0C 1F 1B 1D 29 21 4F 43 29 21 4F 5C 29 21 4F 23 29 21 4F 31 1B 12 0C 08 29 21 4F 23 29 21 `  
  
`4F 36 29 21 4F 43 29 21 4F 53 0B 1C 20 1E 29 21 4F AD 29 21 4F 9F 29 21 4F 92 29 21 4F 92 1C 0B 11 0A 29 21 4F 9F 29 21 4F AD 29 21 4F BA 29 21 4F D7 17 18 14 13 `  
  
`18 18 18 82 18 18 18 2C 18 18 18 82 18 18 18 22 14 15 17 16 18 18 18 82 18 18 18 CD 18 18 18 82 18 18 18 C0 04 17 00 16 18 18 18 78 18 18 18 76 18 18 18 C0 18 18 `  
  
`18 E0 00 16 01 15 18 18 18 C0 18 18 18 E0 18 18 18 E1 18 18 18 E1 05 01 14 15 18 18 18 68 18 18 18 E1 18 18 18 7E 18 18 18 E1 14 13 05 02 18 18 18 7E 18 18 18 0E `  
  
`18 18 18 68 18 18 18 28 18 03 13 02 18 18 18 13 18 18 18 13 18 18 18 0E 18 18 18 28 17 04 18 03 18 18 18 76 18 18 18 78 18 18 18 13 18 18 18 13 20 1E 1F 1D 5E 0C `  
  
`12 92 5E 0C 12 80 5E 0C 12 5C 5E 0C 12 5C 11 12 1C 1B 56 3A 2F A3 56 3A 2F 4C 56 3A 2F 7D 56 3A 2F 50 1C 1B 1E 1D 56 3A 2F 7D 56 3A 2F 50 56 3A 2F 80 56 3A 2F 5C`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 3rd part \[at offset
0x000083F8\]:

  

`00 00 00 00 00 00 15 00 12 00 00 00 00 00 15 00 E4 FF 00 00 15 00 00 00 E4 FF 00 00 15 00 00 00 12 00 00 00 00 00 EB FF 12 00 00 00 00 00 EB FF E4 FF 00 00 EB FF `  
  
`00 00 E4 FF 00 00 EB FF 00 00 12 00 00 00 00 00 7E 00 82 FF 00 00 00 00 72 00 E0 FF 00 00 5C 00 3F 00 82 FF 00 00 40 00 3A 00 E0 FF 00 00 39 00 B4 FF 82 FF 00 00 `  
  
`C7 FF B4 FF 82 FF 00 00 A4 FF 3F 00 82 FF 00 00 C0 FF 3A 00 E0 FF 00 00 00 00 52 00 04 00 00 00 00 00 72 00 B8 FF 00 00 D9 FF CB FF E0 FF 00 00 27 00 CB FF E0 FF `  
  
`00 00 00 00 03 00 F4 FF 00 00 00 00 AF 00 F9 FE 00 00 8F 00 3A 00 06 FF 00 00 87 00 20 00 E7 FF 00 00 74 00 A0 FF 09 FF 00 00 6E 00 9B FF E7 FF 00 00 00 00 35 00 `  
  
`C9 FE 00 00 00 00 93 00 3A FF 00 00 6D 00 1C 00 7A FF 00 00 59 00 BB FF 7A FF 00 00 00 00 C5 00 83 FF 00 00 67 00 4E 00 83 FF 00 00 99 FF 4E 00 83 FF 00 00 A7 FF `  
  
`BB FF 7A FF 00 00 93 FF 1C 00 7A FF 00 00 92 FF 9B FF E7 FF 00 00 8C FF A0 FF 09 FF 00 00 79 FF 20 00 E7 FF 00 00 71 FF 3A 00 06 FF 00 00 00 00 5F FF FF FE 00 00 `  
  
`00 00 8A FF 7A FF 00 00 00 00 5D FF E7 FF 00 00 00 00 C6 FF D2 FE 00 00 00 00 DB FF 83 FF 00 00 0F 09 10 00 FF FF FF DC FF FF FF 78 FF FF FF 6A 00 01 02 01 09 0B `  
  
`10 00 FF FF FF 78 FF FF FF 10 FF FF FF 6A 01 03 02 01 11 0E 08 00 FF FF FF 79 FF FF FF D6 FF FF FF 79 04 05 06 70 0B 11 0A 00 FF FF FF 10 FF FF FF 79 FF FF FF 18 `  
  
`07 08 09 00 0A 11 08 00 FF FF FF 18 FF FF FF 79 FF FF FF 79 09 08 0A 03 0E 11 0F 00 FF FF FF D6 FF FF FF 79 FF FF FF DC 05 04 0B 02 11 0B 09 00 F8 A7 87 79 F8 A7 `  
  
`87 10 F8 A7 87 78 0F 11 09 00 F8 A7 87 DC F8 A7 87 79 F8 A7 87 78 0B 13 14 00 F8 A7 87 10 F8 A7 87 42 F8 A7 87 6D 13 12 14 00 F8 A7 87 42 F8 A7 87 AC F8 A7 87 6D `  
  
`12 0F 14 00 F8 A7 87 AC F8 A7 87 DC F8 A7 87 6D 0F 10 14 00 F8 A7 87 DC F8 A7 87 6A F8 A7 87 6D 10 0B 14 00 F8 A7 87 6A F8 A7 87 10 F8 A7 87 6D 15 26 1A 00 5E 0C `  
  
`12 80 5E 0C 12 D9 5E 0C 12 83 16 15 1A 00 5E 0C 12 14 5E 0C 12 80 5E 0C 12 83 27 2A 24 00 5E 0C 12 7B 5E 0C 12 87 5E 0C 12 D7 27 18 2A 00 5E 0C 12 7B 5E 0C 12 1A `  
  
`5E 0C 12 87 1B 1F 1E 00 57 45 2B 80 57 45 2B 14 57 45 2B 80 1F 1B 1C 00 57 45 2B 14 57 45 2B 80 57 45 2B 02 20 25 22 00 57 45 2B D9 57 45 2B B8 57 45 2B E6 1B 20 `  
  
`22 00 57 45 2B 80 57 45 2B D9 57 45 2B E6 20 1B 1E 00 57 45 2B D9 57 45 2B 80 57 45 2B 80 17 1F 1C 00 57 45 2B 00 57 45 2B 14 57 45 2B 02 20 2B 25 00 33 33 32 BF `  
  
`33 33 32 76 33 33 32 33 23 19 29 00 33 33 32 B6 33 33 32 39 33 33 32 68 19 2B 17 00 33 33 32 39 33 33 32 76 33 33 32 C8 2B 23 25 00 33 33 32 76 33 33 32 B6 33 33 `  
  
`32 33 2B 19 23 00 33 33 32 76 33 33 32 39 33 33 32 B6 2B 1F 17 00 33 33 32 76 33 33 32 31 33 33 32 34 11 0E 08 00 F8 A7 87 79 F8 A7 87 D6 F8 A7 87 79 0E 11 0F 00 `  
  
`F8 A7 87 D6 F8 A7 87 79 F8 A7 87 DC 0B 11 0A 00 F8 A7 87 10 F8 A7 87 79 F8 A7 87 18 0A 11 08 00 F8 A7 87 18 F8 A7 87 79 F8 A7 87 79 0F 09 10 00 F8 A7 87 DC F8 A7 `  
  
`87 78 F8 A7 87 6A 09 0B 10 00 F8 A7 87 78 F8 A7 87 10 F8 A7 87 6A 06 01 07 00 56 3A 2F E6 56 3A 2F 79 56 3A 2F EC 56 3A 2F 79 04 03 05 02 56 3A 2F 7A 56 3A 2F 03 `  
  
`56 3A 2F 7A 56 3A 2F 08 05 06 04 07 56 3A 2F 7A 56 3A 2F E6 56 3A 2F 7A 56 3A 2F EC 03 00 02 01 56 3A 2F 03 56 3A 2F 79 56 3A 2F 08 56 3A 2F 79 0A 0C 0B 13 F8 A7 `  
  
`87 18 F8 A7 87 26 F8 A7 87 10 F8 A7 87 42 0E 0F 0D 12 F8 A7 87 D6 F8 A7 87 DC F8 A7 87 BA F8 A7 87 AC 16 1A 18 2A 5E 0C 12 14 5E 0C 12 83 5E 0C 12 1A 5E 0C 12 87 `  
  
`26 24 1A 2A 5E 0C 12 D9 5E 0C 12 D7 5E 0C 12 83 5E 0C 12 87 27 28 18 1D 5E 0C 12 7B 5E 0C 12 7A 5E 0C 12 1A 5E 0C 12 22 16 18 1C 1D 5E 0C 12 14 5E 0C 12 1A 5E 0C `  
  
`12 0C 5E 0C 12 22 27 24 28 21 5E 0C 12 7B 5E 0C 12 D7 5E 0C 12 7A 5E 0C 12 CD 26 22 24 21 5E 0C 12 D9 5E 0C 12 EE 5E 0C 12 D7 5E 0C 12 CD 16 1C 15 1B 5E 0C 12 14 `  
  
`5E 0C 12 0C 5E 0C 12 80 5E 0C 12 78 26 15 22 1B 5E 0C 12 D9 5E 0C 12 80 5E 0C 12 EE 5E 0C 12 78 19 17 1D 1C 57 45 2B 1A 57 45 2B 00 57 45 2B 12 57 45 2B 02 29 19 `  
  
`28 1D 57 45 2B 7B 57 45 2B 1A 57 45 2B 7B 57 45 2B 12 23 21 25 22 57 45 2B D7 57 45 2B DE 57 45 2B B8 57 45 2B E6 29 28 23 21 57 45 2B 7B 57 45 2B 7B 57 45 2B D7 `  
  
`57 45 2B DE 1E 1F 20 2B 33 33 32 79 33 33 32 31 33 33 32 BF 33 33 32 76 00 1C 14 78 00 1C 14 78 01 1C 14 78 00 A0 0F A7 0F BE 1F A0 1F 13 00 00 1F 00 29 1E 3F 13 `  
  
`20 00 3F 00 09 1E 02 02 00 01 01 00 22 08`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 4th part \[at offset
0x0000894C\]:

  

`00 00 00 00 20 00 DA FF 3E 00 00 00 D4 FF DA FF 3E 00 00 00 D4 FF 26 00 3E 00 00 00 20 00 26 00 3E 00 00 00 4A 00 DE FF F2 FF 00 00 CB FF B6 FF 01 00 00 00 4A 00 `  
  
`22 00 F2 FF 00 00 CB FF 4E 00 F5 FF 00 00 E8 FF 18 00 BC FF 00 00 E8 FF E8 FF BC FF 00 00 18 00 18 00 BC FF 00 00 18 00 E8 FF BC FF 00 00 E8 FF E8 FF 9C FF 00 00 `  
  
`18 00 E8 FF 9C FF 00 00 18 00 18 00 9C FF 00 00 E8 FF 18 00 9C FF 00 00 0A 00 4E 00 F5 FF 00 00 0A 00 B6 FF 01 00 00 00 09 11 0B 00 5E 0C 12 D4 5E 0C 12 60 5E 0C `  
  
`12 37 0A 06 10 00 5E 0C 12 2B 5E 0C 12 0B 5E 0C 12 69 03 10 06 00 5E 0C 12 3C 5E 0C 12 69 5E 0C 12 0B 04 11 00 00 5E 0C 12 0E 5E 0C 12 60 5E 0C 12 51 0A 10 08 00 `  
  
`5E 0C 12 2B 5E 0C 12 69 5E 0C 12 CE 11 09 05 00 5E 0C 12 60 5E 0C 12 D4 5E 0C 12 BD 08 10 07 00 5E 0C 12 CE 5E 0C 12 69 5E 0C 12 D1 0B 11 04 00 5E 0C 12 37 5E 0C `  
  
`12 60 5E 0C 12 0E 04 06 0B 0A 5E 0C 12 0E 5E 0C 12 0B 5E 0C 12 37 5E 0C 12 2B 05 09 07 08 5E 0C 12 BD 5E 0C 12 D4 5E 0C 12 D1 5E 0C 12 CE 03 06 00 04 5E 0C 12 3C `  
  
`5E 0C 12 0B 5E 0C 12 51 5E 0C 12 0E 0D 0E 0C 0F 29 21 4F 2F 29 21 4F 2B 29 21 4F C1 29 21 4F C5 0A 08 0E 0F 29 21 4F 2B 29 21 4F CE 29 21 4F 31 29 21 4F BF 0E 0D `  
  
`0A 0B 29 21 4F 31 29 21 4F 30 29 21 4F 2B 29 21 4F 37 0C 09 0D 0B 29 21 4F BD 29 21 4F D4 29 21 4F 30 29 21 4F 37 09 0C 08 0F 29 21 4F D4 29 21 4F BD 29 21 4F CE `  
  
`29 21 4F BF 00 11 01 05 55 50 45 51 55 50 45 60 55 50 45 C4 55 50 45 BD 00 01 03 02 55 50 45 51 55 50 45 C4 55 50 45 3C 55 50 45 BC 02 07 03 10 55 50 45 BC 55 50 `  
  
`45 D1 55 50 45 3C 55 50 45 69 07 02 05 01 55 50 45 D1 55 50 45 BC 55 50 45 BD 55 50 45 C4`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 5th part \[at offset
0x00008B50\]:

  

`00 00 00 00 37 00 37 00 C5 FF 00 00 C9 FF 37 00 C5 FF 00 00 37 00 C9 FF C5 FF 00 00 C9 FF C9 FF C5 FF 00 00 DF FF 21 00 00 00 00 00 DF FF DF FF 00 00 00 00 21 00 `  
  
`DF FF 00 00 00 00 21 00 21 00 00 00 00 00 D3 FF D3 FF 86 FF 00 00 2D 00 D3 FF 86 FF 00 00 2D 00 2D 00 86 FF 00 00 D3 FF 2D 00 86 FF 00 00 06 05 07 04 5E 0C 12 51 `  
  
`5E 0C 12 9E 5E 0C 12 3C 5E 0C 12 B2 03 01 05 04 5E 0C 12 D0 5E 0C 12 C3 5E 0C 12 9E 5E 0C 12 B2 02 03 06 05 5E 0C 12 1C 5E 0C 12 D0 5E 0C 12 51 5E 0C 12 9E 02 06 `  
  
`00 07 5E 0C 12 1C 5E 0C 12 51 5E 0C 12 2D 5E 0C 12 3C 00 07 01 04 5E 0C 12 2D 5E 0C 12 3C 5E 0C 12 C3 5E 0C 12 B2 03 08 01 0B 55 50 45 D0 55 50 45 C1 55 50 45 C3 `  
  
`55 50 45 AD 02 09 03 08 55 50 45 1C 55 50 45 2F 55 50 45 D0 55 50 45 C1 02 00 09 0A 55 50 45 1C 55 50 45 2D 55 50 45 2F 55 50 45 43 00 01 0A 0B 55 50 45 2D 55 50 `  
  
`45 C3 55 50 45 43 55 50 45 AD 09 0A 08 0B 55 50 45 2F 55 50 45 43 55 50 45 C1 55 50 45 AD`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 6th part \[at offset
0x00008C7C\]:

  

`00 00 00 00 24 00 24 00 C8 FF 00 00 DC FF 24 00 C8 FF 00 00 DC FF DC FF C8 FF 00 00 24 00 DC FF C8 FF 00 00 D3 FF D3 FF 00 00 00 00 2D 00 D3 FF 00 00 00 00 2D 00 `  
  
`2D 00 00 00 00 00 D3 FF 2D 00 00 00 00 00 02 03 01 00 55 50 45 C1 55 50 45 2F 55 50 45 AD 55 50 45 43 06 07 00 01 55 50 45 2C 55 50 45 C0 55 50 45 43 55 50 45 AD `  
  
`05 06 03 00 55 50 45 28 55 50 45 2C 55 50 45 2F 55 50 45 43 05 03 04 02 55 50 45 28 55 50 45 2F 55 50 45 C6 55 50 45 C1 04 02 07 01 55 50 45 C6 55 50 45 C1 55 50 `  
  
`45 C0 55 50 45 AD 05 04 06 07 55 50 45 28 55 50 45 C6 55 50 45 2C 55 50 45 C0`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 7th part \[at offset
0x00008D38\]:

  

`00 00 00 00 F6 FF B6 FF 01 00 00 00 F6 FF 4E 00 F5 FF 00 00 18 00 18 00 9C FF 00 00 E8 FF 18 00 9C FF 00 00 E8 FF E8 FF 9C FF 00 00 18 00 E8 FF 9C FF 00 00 E8 FF `  
  
`E8 FF BC FF 00 00 E8 FF 18 00 BC FF 00 00 18 00 E8 FF BC FF 00 00 18 00 18 00 BC FF 00 00 35 00 4E 00 F5 FF 00 00 B6 FF 22 00 F2 FF 00 00 35 00 B6 FF 01 00 00 00 `  
  
`B6 FF DE FF F2 FF 00 00 E0 FF 26 00 3E 00 00 00 2C 00 26 00 3E 00 00 00 2C 00 DA FF 3E 00 00 00 E0 FF DA FF 3E 00 00 00 00 08 06 00 5E 0C 12 8F 5E 0C 12 1B 5E 0C `  
  
`12 B9 0B 07 01 00 5E 0C 12 E5 5E 0C 12 C5 5E 0C 12 85 01 0E 0B 00 5E 0C 12 85 5E 0C 12 B2 5E 0C 12 E5 00 0D 11 00 5E 0C 12 8F 5E 0C 12 E1 5E 0C 12 9E 01 07 09 00 `  
  
`5E 0C 12 85 5E 0C 12 C5 5E 0C 12 23 08 00 0C 00 5E 0C 12 1B 5E 0C 12 8F 5E 0C 12 30 01 09 0A 00 5E 0C 12 85 5E 0C 12 23 5E 0C 12 1E 00 06 0D 00 5E 0C 12 8F 5E 0C `  
  
`12 B9 5E 0C 12 E1 0D 06 0B 07 5E 0C 12 E1 5E 0C 12 B9 5E 0C 12 E5 5E 0C 12 C5 0C 0A 08 09 5E 0C 12 30 5E 0C 12 1E 5E 0C 12 1B 5E 0C 12 23 0E 11 0B 0D 5E 0C 12 B2 `  
  
`5E 0C 12 9E 5E 0C 12 E5 5E 0C 12 E1 04 05 03 02 29 21 4F C1 29 21 4F 83 29 21 4F C5 29 21 4F 2B 09 07 02 03 29 21 4F 23 29 21 4F C5 29 21 4F 31 29 21 4F BF 04 03 `  
  
`06 07 29 21 4F BD 29 21 4F BF 29 21 4F B9 29 21 4F C5 04 06 05 08 29 21 4F BD 29 21 4F B9 29 21 4F 2F 29 21 4F 1B 09 02 08 05 29 21 4F 23 29 21 4F 31 29 21 4F 1B `  
  
`29 21 4F 2F 11 10 00 0C 55 50 45 9E 55 50 45 29 55 50 45 8F 55 50 45 30 0E 0F 11 10 55 50 45 B2 55 50 45 33 55 50 45 9E 55 50 45 29 0F 0E 0A 01 55 50 45 33 55 50 `  
  
`45 B2 55 50 45 1E 55 50 45 85 0A 0C 0F 10 55 50 45 1E 55 50 45 30 55 50 45 33 55 50 45 29`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 8th part \[at offset
0x00008F3C\]:

  

`00 00 00 00 DF FF 21 00 00 00 00 00 DF FF DF FF 00 00 00 00 21 00 DF FF 00 00 00 00 21 00 21 00 00 00 00 00 37 00 C9 FF C5 FF 00 00 C9 FF C9 FF C5 FF 00 00 37 00 `  
  
`37 00 C5 FF 00 00 C9 FF 37 00 C5 FF 00 00 2D 00 2D 00 86 FF 00 00 D3 FF 2D 00 86 FF 00 00 D3 FF D3 FF 86 FF 00 00 2D 00 D3 FF 86 FF 00 00 01 00 02 03 5E 0C 12 9E `  
  
`5E 0C 12 B2 5E 0C 12 51 5E 0C 12 3C 04 02 06 03 5E 0C 12 1C 5E 0C 12 51 5E 0C 12 2D 5E 0C 12 3C 05 01 04 02 5E 0C 12 D0 5E 0C 12 9E 5E 0C 12 1C 5E 0C 12 51 05 07 `  
  
`01 00 5E 0C 12 D0 5E 0C 12 C3 5E 0C 12 9E 5E 0C 12 B2 07 06 00 03 5E 0C 12 C3 5E 0C 12 2D 5E 0C 12 B2 5E 0C 12 3C 04 06 0B 08 55 50 45 1C 55 50 45 2D 55 50 45 2F `  
  
`55 50 45 43 07 09 06 08 55 50 45 C3 55 50 45 AD 55 50 45 2D 55 50 45 43 05 0A 07 09 55 50 45 D0 55 50 45 C1 55 50 45 C3 55 50 45 AD 05 04 0A 0B 55 50 45 D0 55 50 `  
  
`45 1C 55 50 45 C1 55 50 45 2F 0A 0B 09 08 55 50 45 C1 55 50 45 2F 55 50 45 AD 55 50 45 43`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 9th part \[at offset
0x00009068\]:

  

`00 00 00 00 DC FF DC FF C8 FF 00 00 24 00 DC FF C8 FF 00 00 24 00 24 00 C8 FF 00 00 DC FF 24 00 C8 FF 00 00 2D 00 2D 00 00 00 00 00 D3 FF 2D 00 00 00 00 00 D3 FF `  
  
`D3 FF 00 00 00 00 2D 00 D3 FF 00 00 00 00 01 02 00 03 55 50 45 2F 55 50 45 43 55 50 45 C1 55 50 45 AD 05 03 04 02 55 50 45 C0 55 50 45 AD 55 50 45 2C 55 50 45 43 `  
  
`06 00 05 03 55 50 45 C6 55 50 45 C1 55 50 45 C0 55 50 45 AD 06 07 00 01 55 50 45 C6 55 50 45 28 55 50 45 C1 55 50 45 2F 07 04 01 02 55 50 45 28 55 50 45 2C 55 50 `  
  
`45 2F 55 50 45 43 06 05 07 04 55 50 45 C6 55 50 45 C0 55 50 45 28 55 50 45 2C`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 10th part \[at offset
0x00009124\]:

  

`00 00 00 00 00 00 29 00 00 00 00 00 D7 FF 00 00 00 00 00 00 00 00 D7 FF 00 00 00 00 29 00 00 00 00 00 00 00 4C 00 01 00 62 FF 00 00 FF FF 56 00 62 FF 00 00 B4 FF `  
  
`FF FF 62 FF 00 00 01 00 AA FF 62 FF 00 00 28 00 00 00 2A FF 00 00 00 00 2D 00 2A FF 00 00 D8 FF 00 00 2A FF 00 00 00 00 D3 FF 2A FF 00 00 02 03 04 00 1F 1E 25 72 `  
  
`1F 1E 25 24 1F 1E 25 03 01 02 06 00 1F 1E 25 C8 1F 1E 25 72 1F 1E 25 EF 00 01 06 00 1F 1E 25 77 1F 1E 25 C8 1F 1E 25 EF 03 00 04 00 1F 1E 25 24 1F 1E 25 77 1F 1E `  
  
`25 03 02 04 07 00 1F 1E 25 72 1F 1E 25 03 1F 1E 25 7A 06 02 07 00 1F 1E 25 EF 1F 1E 25 72 1F 1E 25 7A 00 06 05 00 1F 1E 25 77 1F 1E 25 EF 1F 1E 25 85 04 00 05 00 `  
  
`1F 1E 25 03 1F 1E 25 77 1F 1E 25 85 04 08 07 0B 1F 1E 25 03 1F 1E 25 25 1F 1E 25 7A 1F 1E 25 63 06 07 0A 0B 1F 1E 25 EF 1F 1E 25 7A 1F 1E 25 CB 1F 1E 25 63 06 0A `  
  
`05 09 1F 1E 25 EF 1F 1E 25 CB 1F 1E 25 85 1F 1E 25 7F 05 09 04 08 1F 1E 25 85 1F 1E 25 7F 1F 1E 25 03 1F 1E 25 25 08 09 0B 0A 1F 1E 25 25 1F 1E 25 7F 1F 1E 25 63 `  
  
`1F 1E 25 CB 03 02 00 01 1F 1E 25 24 1F 1E 25 72 1F 1E 25 77 1F 1E 25 C8`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 11th part \[at offset
0x00009280\]:

  

`00 00 00 00 00 00 2D 00 C8 FF 00 00 D8 FF 00 00 C8 FF 00 00 00 00 D3 FF C8 FF 00 00 28 00 00 00 C8 FF 00 00 23 00 00 00 31 FF 00 00 00 00 28 00 31 FF 00 00 DD FF `  
  
`00 00 31 FF 00 00 00 00 D8 FF 31 FF 00 00 4C 00 00 00 00 00 00 00 00 00 AA FF 00 00 00 00 B4 FF 00 00 00 00 00 00 00 00 56 00 00 00 00 00 00 00 00 00 26 00 00 00 `  
  
`08 09 0C 00 1F 1E 25 00 1F 1E 25 68 1F 1E 25 82 0B 08 0C 00 1F 1E 25 79 1F 1E 25 00 1F 1E 25 82 0A 0B 0C 00 1F 1E 25 EC 1F 1E 25 79 1F 1E 25 82 09 0A 0C 00 1F 1E `  
  
`25 68 1F 1E 25 EC 1F 1E 25 82 06 07 05 04 CC CC CC E6 CC CC CC 65 CC CC CC 70 CC CC CC 08 03 00 04 05 38 17 0D 08 38 17 0D 6E 38 17 0D 03 38 17 0D 85 00 01 05 06 `  
  
`38 17 0D 6E 38 17 0D E6 38 17 0D 85 38 17 0D EF 02 07 01 06 38 17 0D 7B 38 17 0D 7A 38 17 0D E6 38 17 0D EF 03 04 02 07 38 17 0D 08 38 17 0D 03 38 17 0D 7B 38 17 `  
  
`0D 7A 0A 09 01 02 1F 1E 25 EC 1F 1E 25 68 1F 1E 25 E6 1F 1E 25 7B 0B 0A 00 01 1F 1E 25 79 1F 1E 25 EC 1F 1E 25 6E 1F 1E 25 E6 0B 00 08 03 1F 1E 25 79 1F 1E 25 6E `  
  
`1F 1E 25 00 1F 1E 25 08`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 12th part \[at offset
0x000093CC\]:

  

`00 00 00 00 D0 FF E7 FF 1E FF 00 00 30 00 E7 FF 1E FF 00 00 22 00 32 00 3D 00 00 00 DE FF 32 00 3D 00 00 00 B8 FF 13 00 C7 FF 00 00 48 00 13 00 C7 FF 00 00 DF FF `  
  
`C6 FF DB FF 00 00 21 00 C6 FF DB FF 00 00 12 00 DF FF 3A 00 00 00 EE FF DF FF 3A 00 00 00 E4 FF BC FF 39 FF 00 00 1C 00 BC FF 39 FF 00 00 08 05 07 00 38 1B 12 42 `  
  
`38 1B 12 09 38 1B 12 3F 09 06 04 00 38 1B 12 AC 38 1B 12 B1 38 1B 12 E4 09 04 03 00 38 1B 12 AC 38 1B 12 E4 38 1B 12 B6 05 08 02 00 38 1B 12 09 38 1B 12 42 38 1B `  
  
`12 39 02 08 03 09 38 1B 12 39 38 1B 12 42 38 1B 12 B6 38 1B 12 AC 00 0A 01 0B 38 1B 12 B9 38 1B 12 BA 38 1B 12 37 38 1B 12 36 05 01 07 0B 38 1B 12 09 38 1B 12 37 `  
  
`38 1B 12 3F 38 1B 12 36 04 06 00 0A 38 1B 12 E4 38 1B 12 B1 38 1B 12 B9 38 1B 12 BA 07 0B 06 0A 38 1B 12 3F 38 1B 12 36 38 1B 12 B1 38 1B 12 BA 06 09 07 08 38 1B `  
  
`12 B1 38 1B 12 AC 38 1B 12 3F 38 1B 12 42 05 04 01 00 50 3A 28 07 50 3A 28 E8 50 3A 28 25 50 3A 28 CB 05 02 04 03 50 3A 28 07 50 3A 28 33 50 3A 28 E8 50 3A 28 BC`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 13th part \[at offset
0x00009510\]:

  

`00 00 00 00 00 00 D3 FF 2A FF 00 00 28 00 00 00 2A FF 00 00 00 00 2D 00 2A FF 00 00 D8 FF 00 00 2A FF 00 00 FF FF AA FF 62 FF 00 00 4C 00 FF FF 62 FF 00 00 01 00 `  
  
`56 00 62 FF 00 00 B4 FF 01 00 62 FF 00 00 D7 FF 00 00 00 00 00 00 00 00 D7 FF 00 00 00 00 29 00 00 00 00 00 00 00 00 00 29 00 00 00 00 00 08 09 07 00 1F 1E 25 C8 `  
  
`1F 1E 25 7E 1F 1E 25 EF 09 0A 05 00 1F 1E 25 7E 1F 1E 25 24 1F 1E 25 03 0A 0B 05 00 1F 1E 25 24 1F 1E 25 77 1F 1E 25 03 0B 08 07 00 1F 1E 25 77 1F 1E 25 C8 1F 1E `  
  
`25 EF 0B 07 06 00 1F 1E 25 77 1F 1E 25 EF 1F 1E 25 69 05 0B 06 00 1F 1E 25 03 1F 1E 25 77 1F 1E 25 69 09 05 04 00 1F 1E 25 7E 1F 1E 25 03 1F 1E 25 7A 07 09 04 00 `  
  
`1F 1E 25 EF 1F 1E 25 7E 1F 1E 25 7A 04 00 07 03 1F 1E 25 7A 1F 1E 25 8C 1F 1E 25 EF 1F 1E 25 CB 04 05 00 01 1F 1E 25 7A 1F 1E 25 03 1F 1E 25 8C 1F 1E 25 25 06 02 `  
  
`05 01 1F 1E 25 69 1F 1E 25 70 1F 1E 25 03 1F 1E 25 25 06 07 02 03 1F 1E 25 69 1F 1E 25 EF 1F 1E 25 70 1F 1E 25 CB 03 00 02 01 1F 1E 25 CB 1F 1E 25 8C 1F 1E 25 70 `  
  
`1F 1E 25 25 0B 0A 08 09 1F 1E 25 77 1F 1E 25 24 1F 1E 25 C8 1F 1E 25 7E`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 14th part \[at offset
0x0000966C\]:

  

`00 00 00 00 00 00 D8 FF 31 FF 00 00 23 00 00 00 31 FF 00 00 00 00 28 00 31 FF 00 00 DD FF 00 00 31 FF 00 00 D8 FF 00 00 C8 FF 00 00 00 00 D3 FF C8 FF 00 00 28 00 `  
  
`00 00 C8 FF 00 00 00 00 2D 00 C8 FF 00 00 00 00 AA FF 00 00 00 00 B4 FF 00 00 00 00 00 00 00 00 56 00 00 00 00 00 4C 00 00 00 00 00 00 00 00 00 00 00 26 00 00 00 `  
  
`08 09 0C 00 1F 1E 25 86 1F 1E 25 EC 1F 1E 25 6D 0B 08 0C 00 1F 1E 25 00 1F 1E 25 86 1F 1E 25 6D 0A 0B 0C 00 1F 1E 25 79 1F 1E 25 00 1F 1E 25 6D 09 0A 0C 00 1F 1E `  
  
`25 EC 1F 1E 25 79 1F 1E 25 6D 02 03 01 00 CC CC CC 7F CC CC CC 83 CC CC CC 08 CC CC CC 8B 04 03 07 02 38 17 0D E6 38 17 0D E6 38 17 0D 80 38 17 0D 69 07 02 06 01 `  
  
`38 17 0D 80 38 17 0D 69 38 17 0D 08 38 17 0D 03 05 06 00 01 38 17 0D 7B 38 17 0D 08 38 17 0D 7A 38 17 0D 03 04 05 03 00 38 17 0D E6 38 17 0D 7B 38 17 0D E6 38 17 `  
  
`0D 7A 0A 09 07 04 1F 1E 25 79 1F 1E 25 EC 1F 1E 25 80 1F 1E 25 E6 0B 0A 06 07 1F 1E 25 00 1F 1E 25 79 1F 1E 25 08 1F 1E 25 80 0B 06 08 05 1F 1E 25 00 1F 1E 25 08 `  
  
`1F 1E 25 86 1F 1E 25 7B`

  
  
  
  
Model 7, Model 8, and Model 9, skeleton data for 15th part \[at offset
0x000097B8\]:

  

`00 00 00 00 E4 FF BC FF 39 FF 00 00 1C 00 BC FF 39 FF 00 00 12 00 DF FF 3A 00 00 00 EE FF DF FF 3A 00 00 00 DF FF C6 FF DB FF 00 00 21 00 C6 FF DB FF 00 00 B8 FF `  
  
`13 00 C7 FF 00 00 48 00 13 00 C7 FF 00 00 22 00 32 00 3D 00 00 00 DE FF 32 00 3D 00 00 00 D0 FF E7 FF 1E FF 00 00 30 00 E7 FF 1E FF 00 00 06 03 04 00 38 1B 12 E8 `  
  
`38 1B 12 AC 38 1B 12 B1 05 02 07 00 38 1B 12 3F 38 1B 12 42 38 1B 12 07 03 06 09 00 38 1B 12 AC 38 1B 12 E8 38 1B 12 BC 07 02 08 00 38 1B 12 07 38 1B 12 42 38 1B `  
  
`12 33 08 02 09 03 38 1B 12 33 38 1B 12 42 38 1B 12 BC 38 1B 12 AC 0B 0A 01 00 38 1B 12 37 38 1B 12 CB 38 1B 12 36 38 1B 12 BA 06 04 0A 00 38 1B 12 E8 38 1B 12 B1 `  
  
`38 1B 12 CB 38 1B 12 BA 07 0B 05 01 38 1B 12 07 38 1B 12 37 38 1B 12 3F 38 1B 12 36 05 01 04 00 38 1B 12 3F 38 1B 12 36 38 1B 12 B1 38 1B 12 BA 04 03 05 02 38 1B `  
  
`12 B1 38 1B 12 AC 38 1B 12 3F 38 1B 12 42 06 0A 07 0B 50 3A 28 69 50 3A 28 69 50 3A 28 69 50 3A 28 25 07 08 06 09 50 3A 28 69 50 3A 28 69 50 3A 28 69 50 3A 28 69`

  
  
  
  
  
Note: 'Skeleton Data Section' runs until 'Animation Data Section'.

  
  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
**'Animation Data Section**' \[at offset 0x000098FC\]:

  
Note: Offset to 'Animation Data Section' contained in 'Models Section',
Individual Bones/Parts/Animations Data.

Note2: Number of animations contained in 'Models Section', Individual
Model Data.

  
  
Model 0 (Cloud) 1st animation data \[at offset 0x000098FC\]:

  

`00 00 00 00 77 00 01 02 00 01 02 00 07 03 04 05 FF FF FF 00 07 06 07 08 FF FF FF 00 07 09 0A 0B FF FF FF 00 07 0C 0D 0E FF FF FF 00 07 0F 10 11 FF `  
  
`FF FF 00 07 12 13 14 FF FF FF 00 07 15 16 17 FF FF FF 00 01 18 00 00 FF FF FF 00 07 19 1A 1B FF FF FF 00 07 1C 1D 1E FF FF FF 00 07 1F 20 21 FF FF `  
  
`FF 00 02 00 22 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 00 B3 80 FF FF FF 00 07 23 24 25 FF FF FF 00 07 26 27 28 FF FF FF 00 07 29 2A 2B FF FF FF `  
  
`00 00 00 4D 80 FF FF FF 00 07 2C 2D 2E FF FF FF 00 07 2F 30 31 FF FF FF 00 07 32 33 34 FF FF FF 00 69 F8 B7 F8 06 F9 54 F9 A3 F9 F3 F9 3B FA 62 FA `  
  
`6C FA 70 FA 64 FA 52 FA 49 FA 4A FA 57 FA 74 FA A2 FA DB FA 16 FB 5E FB BF FB 2E FC 95 FC EB FC 46 FD AB FD 03 FE 47 FE 87 FE C1 FE F6 FE 27 FF 54 `  
  
`FF 7E FF A6 FF CD FF F3 FF 0D 00 0F 00 08 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 74 F7 75 `  
  
`F7 77 F7 79 F7 7C F7 81 F7 92 F7 AA F7 B7 F7 B5 F7 AB F7 A3 F7 A3 F7 A3 F7 A3 F7 9D F7 93 F7 8E F7 93 F7 A1 F7 BA F7 EC F7 38 F8 9B F8 0F F9 8E F9 `  
  
`09 FA 7B FA ED FA 5F FB D0 FB 3E FC AB FC 14 FD 7C FD E1 FD 44 FE 93 FE CB FE F2 FE 08 FF 12 FF 19 FF 1D FF 1F FF 20 FF 1F FF 1D FF 1A FF 17 FF 14 `  
  
`FF 11 FF 0F FF 0D FF 0C FF 0C FF 0C FF 0C FF 0C FF 0D FF 0E FF 11 FF 13 FF 16 FF 18 FF 1A FF 1A FF 1A FF 17 FF 13 FF 0C FF 02 FF F4 FE E2 FE CF FE `  
  
`B9 FE A3 FE 8D FE 78 FE 64 FE B2 FE AE FE AA FE A8 FE AB FE B4 FE D3 FE 03 FF 28 FF 2F FF 25 FF 19 FF 17 FF 18 FF 1C FF 1C FF 1C FF 25 FF 3E FF 75 `  
  
`FF C2 FF 0C 00 3B 00 41 00 32 00 1F 00 15 00 12 00 10 00 0E 00 0C 00 0A 00 08 00 07 00 05 00 04 00 03 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 `  
  
`02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 `  
  
`00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 02 00 39 38 37 37 37 39 3E 36 2C 23 1A 11 08 FF F7 EF E8 E1 DA D1 C7 C2 C9 D5 E6 F4 `  
  
`FC FF 02 03 04 04 03 03 02 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 92 93 94 95 94 92 64 24 22 22 24 24 22 1F 1D 1B 19 16 13 12 18 85 A7 BB C6 D0 D7 DC E1 E5 EA EE F2 F5 F9 FC FF 01 01 01 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 F4 F6 F7 F8 F7 F4 C5 86 84 84 82 81 80 `  
  
`81 82 84 86 89 8D 8F 89 19 F7 E6 E3 E7 EB EF F2 F5 F7 F9 FB FC FE FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D4 D4 D4 D4 D4 D4 D4 D5 D5 D5 D5 D5 D3 D1 CF CD `  
  
`CB C9 C6 C4 C2 C1 C0 C1 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 25 2C 34 3A 40 3C 3C 40 39 30 24 19 0F 05 FD F6 EF EA E6 E3 E1 E2 E4 EC F7 02 08 09 09 08 07 05 03 01 FF FE `  
  
`FF 02 0A 13 1A 1C 1D 1D 1E 1E 1E 1D 1D 1D 1C 1C 1B 1B 1B 1B 1B 1B 1B 1B 1B 1C 1C 1D 1D 1D 1D 1D 1D 1C 1B 19 16 13 0F 0B 06 02 FE FA 00 00 01 01 19 `  
  
`7E 7E 13 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 01 19 7E 7E 13 01 01 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 DF DA D4 CF CA C6 C3 C1 C0 C1 C1 C1 C2 C2 C2 C1 C0 C2 C2 C0 C3 C4 C2 C7 D5 E1 EA EF F3 F8 FC 01 05 09 0C 0F 13 15 17 19 1A `  
  
`1A 1B 1B 1C 1D 1E 1F 1F 1F 1F 1F 1E 1C 1A 12 03 F5 ED EA E8 E7 E6 E6 E7 E7 E8 E9 EA EB ED EE F0 F3 F6 F9 FC 00 03 06 00 00 00 00 00 00 00 00 80 80 `  
  
`80 80 80 80 80 80 00 00 00 0E 79 7C 80 F6 F9 FD 00 03 04 06 07 07 06 05 04 02 01 FF FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 00 00 00 F2 87 85 80 0A 0A 0E 10 10 `  
  
`10 0F 0E 0D 0B 08 06 03 01 FF FF FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 1C 20 24 26 27 28 28 27 26 22 1B 12 0A 02 FC F6 F1 EC E9 E7 E6 E6 E8 EE F7 00 05 06 06 05 04 02 00 FF FE FD FD 00 06 0E 13 15 15 16 16 16 `  
  
`16 16 16 15 15 14 14 14 14 14 14 14 14 14 14 14 15 15 16 16 16 16 15 15 14 12 10 0D 0A 07 04 00 FD FA DF DA D3 CB C4 BE BE C4 CD D7 E0 E4 E6 E7 E7 `  
  
`E6 E5 E3 E2 E1 E0 E0 E1 E4 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E6 E4 E3 E3 E3 E3 E3 E3 E3 E3 E3 E3 E3 E4 E4 E4 E4 E4 E4 E4 E4 E4 E3 E3 E3 `  
  
`E3 E3 E3 E3 E3 E3 E4 E4 E5 E6 E6 E7 E7 E7 E7 E7 1B 13 0A 00 F7 F0 F0 F7 02 0F 1C 25 2B 31 35 3A 3E 42 45 47 48 48 46 40 39 33 2F 2F 2F 2F 30 31 32 `  
  
`33 34 35 35 33 2E 28 24 23 22 21 21 21 21 21 22 22 22 23 23 23 23 23 23 23 23 23 23 23 22 22 22 21 21 21 22 22 23 25 27 29 2B 2E 30 32 35 37 F6 F6 `  
  
`F6 F6 F6 F6 F5 F4 F3 F2 F0 F0 F1 F2 F1 ED E8 E2 E0 E0 E3 E5 E5 E0 DD DE E0 E0 E1 E3 E5 E9 EC F0 F4 F7 F9 F9 F3 EB E5 E4 E3 E2 E2 E2 E2 E2 E3 E3 E3 `  
  
`E4 E4 E4 E4 E4 E4 E4 E4 E4 E4 E5 E5 E5 E5 E5 E5 E5 E5 E5 E4 E4 E3 E2 E1 DF DE DD DC DC CF CF CF CF CF CF CE CB C9 C5 C1 BD B9 B6 B2 AE A9 A3 9E 9B `  
  
`9A 9B 9E A8 BA CD D9 E0 E7 ED F2 F5 F8 FA FB FC FD FF 03 06 06 05 05 05 05 05 05 05 05 05 05 05 06 06 06 06 06 06 06 06 06 06 06 07 07 07 07 07 07 `  
  
`06 06 04 03 01 FE FB F8 F5 F1 EE 28 27 27 27 27 28 2A 2E 32 37 3D 43 49 4E 52 55 58 5C 5F 62 64 63 61 58 46 33 27 1D 14 0B 04 FD F8 F5 F2 F1 F0 F2 `  
  
`F7 FF 06 08 09 0A 0B 0B 0B 0A 0A 09 08 08 07 07 07 07 07 07 07 07 07 07 07 06 06 06 06 06 06 07 07 07 08 09 0B 0C 0E 11 13 16 07 07 08 08 08 07 06 `  
  
`03 01 FE FC FA F9 F9 F9 F8 F6 F3 F0 ED EA E7 E5 E4 E5 E5 E5 E3 E1 DF DD DB D9 D7 D6 D5 D5 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 `  
  
`D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 D4 E0 E0 E0 E0 E0 E0 E1 E2 E3 E4 E4 E5 E6 E6 E7 E8 E9 EB EF F3 F8 FE 01 03 03 `  
  
`02 01 01 01 01 01 02 03 05 08 0A 0D 0F 0F 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E `  
  
`0E 0E 0E 0E 0E 0E 87 87 87 87 87 87 86 83 81 7E 7B 77 73 70 6C 68 65 61 5E 5B 59 57 56 56 57 57 56 54 52 4F 4C 49 45 40 3B 36 32 2F 2F 30 30 30 30 `  
  
`30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 ED ED ED ED ED ED ED ED ED EA E6 E2 `  
  
`DF DD D9 D4 CD C8 C4 C4 C6 C9 CA CA C9 C9 CA CF D6 DE E6 EE F5 FA FE 00 00 FB E7 CC CF D4 D8 DA DB DB DB DA D9 D7 D6 D4 D3 D2 D2 D2 D2 D2 D2 D2 D3 `  
  
`D4 D5 D6 D7 D8 D9 D8 D7 D5 D2 CD C6 C3 CC D7 E1 EC F6 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 04 0A 15 13 08 02 00 FD F9 F8 00 09 0F 13 `  
  
`16 19 1D 21 24 27 28 26 20 30 7C 83 85 87 87 88 87 87 86 85 84 83 81 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FD F6 EC ED F8 FE 00 03 07 08 00 F7 F3 F2 F2 F4 F7 FA FD FF 00 FA EB D1 84 7D 7B 7B 7A 7A 7A 7A `  
  
`7B 7C 7D 7E 7F 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 E4 E4 E4 E4 E4 E4 E4 E4 E4 E2 E0 DE DD DB DA DA DB `  
  
`DB DC DB D9 D8 DA E1 EB F5 FB FD FF 00 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 1B 20 24 26 27 27 27 27 26 22 1A 12 0A 02 FB F6 F0 EC E9 E7 E6 E6 E8 EE F7 00 04 05 05 05 03 02 00 FF FD `  
  
`FD FD FF 06 0E 13 14 15 16 16 16 16 16 15 15 15 14 14 14 14 14 14 14 14 14 14 14 15 15 15 16 16 16 15 15 14 12 10 0D 0A 07 03 00 FC F9 21 26 2D 35 `  
  
`3C 42 42 3C 33 29 21 1C 1A 19 19 1A 1B 1C 1E 1F 20 20 1E 1C 19 19 19 19 19 19 19 19 19 19 19 19 19 19 19 1A 1C 1D 1D 1D 1E 1E 1E 1E 1D 1D 1D 1D 1D `  
  
`1D 1C 1C 1C 1C 1C 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1C 1C 1B 1A 1A 19 19 19 19 19 E6 ED F6 00 09 10 10 09 FE F1 E4 DC D5 D0 CB C7 C3 BF BC BA B8 B8 `  
  
`BB C0 C8 CE D1 D2 D2 D1 D0 CF CE CD CC CC CC CE D2 D8 DC DE DF DF DF DF DF DF DF DE DE DE DD DD DD DD DD DD DD DD DD DE DE DE DF DF DF DF DF DE DD `  
  
`DC DA D8 D5 D3 D0 CE CC C9 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 03 03 04 06 06 04 FD F2 E8 E3 E2 E1 E2 E3 E5 E7 E9 EB ED EF F0 EE EE `  
  
`F1 F3 F4 F4 F5 F5 F5 F4 F4 F3 F3 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F3 F3 F3 F3 F3 F3 F3 F3 F2 F0 EF ED EA E8 E5 E2 DF DC FF FF FF FF FF FF FF FF FF `  
  
`FF FF FF FF FF FF FF FF FF FF FF FE FE FF 02 06 0B 0D 0C 09 06 02 FE FA F8 F7 F8 FA 05 1F 3C 4F 54 57 58 59 59 59 58 57 56 55 54 53 52 52 52 52 52 `  
  
`52 52 52 53 54 55 56 57 57 56 56 54 52 4E 49 43 3B 33 2B 23 1A 12 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F2 F2 F3 F3 F2 F0 EE `  
  
`EF F0 F2 F3 F5 F6 F6 F6 F6 F5 F5 F1 E7 DE DB DA D9 D8 D8 D8 D9 D9 DA DB DB DC DC DD DD DD DD DD DC DC DC DC DC DC DB DB DB DC DC DD DD DE E0 E1 E2 `  
  
`E4 E6 E8 EA 13 13 13 13 13 13 13 13 13 13 13 13 13 13 13 14 16 16 17 18 19 1A 1B 1C 1D 1D 1B 15 0C 02 F9 F3 F0 F2 F5 F9 FC FB F8 F7 FB FC FD FE FE `  
  
`FE FE FE FD FD FC FC FC FB FB FB FB FB FB FB FC FC FD FD FD FD FE FD FD FC FB F9 F6 F2 EC E6 DF D8 D2 D0 08 08 08 08 08 08 08 08 08 08 08 08 08 08 `  
  
`08 0A 0D 10 11 11 10 0E 0D 0B 09 08 0D 13 17 18 14 0E 05 FF FA F9 F9 FA FE 05 0A 0B 0B 0B 0C 0C 0B 0B 0B 0B 0B 0B 0B 0A 0A 0A 0A 0A 0A 0A 0A 09 09 `  
  
`09 08 08 08 08 08 09 0A 0C 0E 10 11 11 0F 09 FE ED 52 52 52 52 52 52 52 52 52 52 52 52 51 51 52 54 57 5B 5C 5C 59 56 54 51 4D 4C 54 61 6F 7D 8C 9F `  
  
`B2 C4 D4 E1 EA E6 CC AB 94 8E 8A 88 87 87 87 88 89 8B 8D 8E 90 90 91 91 91 91 91 91 90 90 8F 8E 8D 8D 8D 8D 8E 8F 91 94 98 9C A1 A6 AD B5 C2 D4 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF FF FF FF 00 00 00 01 01 00 FE FB F8 F5 F2 EE EB E9 E7 E6 E8 F0 F9 FF 01 02 03 03 03 03 03 02 02 `  
  
`01 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 F3 F3 F4 F4 F4 F2 EE E5 DF DA D7 D4 D1 CD CB CB CB CB CB `  
  
`CB CB CB CB CB CB CB CB CB CB CA C9 C9 C8 C8 C9 CB CE D5 E5 F7 04 08 0A 0B 0C 0C 0C 0B 0B 0A 09 08 07 06 06 06 06 06 06 06 07 08 09 0A 0B 0C 0C 0C `  
  
`0B 09 06 02 FC F5 EC E4 DA D2 CA C6 AA AA AA AA AA AA AB AD B0 B0 AF AD AB A9 A7 A6 A7 A8 A8 A8 A7 A7 A7 A6 A5 A5 A7 A9 AA AC AF B1 B5 B8 BB BE C0 `  
  
`C1 C0 C0 C0 C0 BF BF BF BF BF BF BF BF C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 BF BF BF BF BF BF BF BF BF BF C0 C0 C0 C1 C2 C3 C6 CA D7 00 89 89 88 88 89 89 `  
  
`89 88 85 85 86 88 8A 8C 8E 8E 8E 8D 8D 8D 8D 8E 8E 8E 8E 8F 8E 8D 8C 8B 8A 89 87 84 82 80 7F 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 7F 7E 7B 77 6A 40 32 32 33 33 33 32 2F 2B 26 22 1E 19 16 12 0E 0A 06 03 00 FF FF 00 00 00 `  
  
`00 00 00 00 FF FD FC FB FA F9 FA FC FF 07 1A 2D 32 31 2F 2E 2D 2D 2E 2E 2F 2F 30 31 31 31 32 32 32 32 32 31 31 31 30 30 2F 2F 2F 2F 2F 30 32 32 32 `  
  
`2E 28 21 18 10 08 00 10 10 11 11 11 10 0D 0A 08 07 05 05 04 03 03 02 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 02 01 00 FD F5 E0 B7 AA `  
  
`A5 A1 A0 9F A0 A1 A3 A6 A8 AB AE B0 B1 B1 B1 B1 B1 B0 AE AC A9 A7 A5 A4 A3 A4 A6 AA B1 BD CE DF EA F1 F6 FA FD 00 10 10 11 11 11 10 0D 0B 09 08 07 `  
  
`06 06 06 06 05 05 04 04 04 05 05 05 06 06 06 05 04 02 00 FE FC FA F8 F6 F5 F3 F2 EE DE B8 AC A6 A3 A2 A1 A2 A3 A5 A7 AA AD AF B1 B1 B1 B1 B1 B1 B1 `  
  
`AF AD AB A8 A7 A5 A5 A5 A7 AB B1 BD CE DD E6 EC F0 F1 F2 F3 E7 E8 E8 E8 E8 E7 E3 E0 DF E0 E2 E3 E5 E7 E7 E4 E0 DB D9 D8 D8 D8 D8 D8 D7 D7 D8 D9 DC `  
  
`DE E1 E4 E6 E9 EA EB EB E6 D9 CC CB CD CE CF CF D0 CF CF CE CE CD CC CC CC CC CC CC CC CC CC CC CC CD CE CE CE CE CE CE CD CC CA C7 C6 C7 CB CF D4 `  
  
`D8 DD A3 A2 A0 A0 A0 A3 AF C4 D7 DF E1 E4 E7 EA ED F1 F6 FD 03 05 05 04 04 04 05 05 04 02 FF FD FB F9 F8 F6 F5 F3 F2 F0 F0 FE 24 2D 30 32 32 33 32 `  
  
`32 31 2F 2E 2C 2B 29 29 29 29 29 29 29 2A 2A 2B 2C 2C 2D 2D 2D 2C 2B 29 24 1A 04 E9 DA D4 D1 D0 CF 5A 5B 5C 5C 5C 59 51 41 35 30 2E 2C 2A 28 26 24 `  
  
`20 1B 17 14 14 15 15 15 14 14 15 17 1A 1C 1E 1F 20 21 21 22 22 22 1E 09 DD D3 CE CC CB CB CB CC CD CF D1 D4 D6 D7 D8 D8 D8 D8 D8 D7 D7 D6 D5 D4 D4 `  
  
`D3 D3 D3 D4 D5 D8 DD E7 FE 1A 2A 31 35 38 39 EE EE EE EE EE EE EE EF EE EC E9 E7 E5 E3 E0 DD D9 D5 D2 D1 D2 D2 D3 D3 D4 D4 D3 D2 D0 CF CD CB CA C8 `  
  
`C7 C7 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 39 39 39 `  
  
`39 39 39 39 39 39 39 39 38 38 38 37 36 35 33 31 31 31 32 32 32 32 32 32 31 30 2E 2B 28 23 1D 16 0C 03 FD FD FE 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 83 83 83 83 83 83 83 83 83 83 84 84 85 85 86 87 89 8B 8D 8E 8E `  
  
`8D 8D 8C 8C 8C 8D 8E 8F 91 94 97 9C A2 AA B3 BD C3 C3 C2 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 `  
  
`C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 2D 2D 2D 2D 2D 2D 2D 2D 2D 2F 31 32 33 32 31 31 31 31 32 31 31 31 31 31 31 31 31 32 32 32 33 32 32 32 31 30 2F 2E 2C `  
  
`2A 29 29 29 28 28 28 28 28 28 29 29 29 29 29 29 29 29 29 29 29 28 27 26 25 24 23 23 23 24 26 29 2D 31 32 2F 27 1D 13 09 00 61 61 61 61 61 61 62 62 `  
  
`61 5C 53 49 3E 34 2E 2C 2D 2F 30 30 2F 2E 2E 2D 2C 2C 2E 31 35 3A 3F 45 4A 50 54 59 5D 60 64 67 68 69 69 6A 6A 6A 6A 6A 69 69 69 69 69 69 69 69 69 `  
  
`69 69 69 6A 6B 6C 6D 6E 6F 6F 6F 6E 6C 69 62 54 3B 23 14 0C 07 03 00 5F 5F 5F 5F 5F 5F 5F 60 5F 5A 52 48 3E 34 2F 2E 2E 30 31 31 30 2F 2F 2E 2D 2D `  
  
`2F 32 36 3A 3F 45 4A 4F 53 57 5B 5E 61 64 65 66 66 66 66 66 66 66 66 66 66 66 66 65 65 65 65 65 65 66 66 67 68 69 6A 6B 6B 6B 6A 68 65 60 53 3B 24 `  
  
`18 12 0F 0E 0D E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E1 E1 E1 E1 E1 E2 E2 E2 E3 E3 E2 E0 DD DA D7 D3 D0 CD CB CA C9 CA D2 DA E1 E3 E4 E5 `  
  
`E5 E5 E5 E5 E4 E4 E3 E3 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 31 31 31 31 31 31 31 31 31 31 31 31 31 `  
  
`31 31 31 31 31 31 31 31 31 31 31 31 31 31 30 30 2E 2D 2B 29 26 22 1E 1B 20 2A 2F 31 31 31 32 32 32 32 32 31 31 31 31 31 31 31 31 31 31 31 31 31 31 `  
  
`31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 31 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C8 C7 C7 C7 C7 C7 C7 C7 C7 C8 C8 C9 CA `  
  
`CC CE D1 D5 D9 DB D6 CD C9 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7`

  
  
Model 1 (Barret) 1st animation data \[at offset 0x0000AC20\]:

  

`00 00 00 00 20 00 00 00 FF 00 FF 00 06 C2 00 01 FF FF FF 00 07 02 03 04 FF FF FF 00 07 05 06 07 FF FF FF 00 07 08 09 0A FF FF FF 00 00 D3 D9 69 FF `  
  
`FF FF 00 07 0B 0C 0D FF FF FF 00 07 0E 0F 10 FF FF FF 00 00 00 00 00 FF FF FF 00 07 11 12 13 FF FF FF 00 07 14 15 16 FF FF FF 00 07 17 18 19 FF FF `  
  
`FF 00 07 1A 1B 1C FF FF FF 00 00 00 00 00 FF FF FF 00 07 1D 1E 1F FF FF FF 00 07 20 21 22 FF FF FF 00 01 23 00 00 FF FF FF 00 07 24 25 26 FF FF FF `  
  
`00 07 27 28 29 FF FF FF 00 07 2A 2B 2C FF FF FF 00 01 2D 00 00 FF FF FF 00 03 2E 2F FC FF FF FF 00 52 FE 44 FE 44 FE 44 FE 44 FE 43 FE 42 FE 44 FE `  
  
`4D FE 52 FE 53 FE 53 FE 53 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 `  
  
`FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 52 FE 00 00 00 00 00 FF FF 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 46 FF FE FE 00 08 14 21 38 46 49 49 48 47 46 46 `  
  
`46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 46 FB FB FB FB FB FB FB FB FB FB FB FB FB FB FB FB `  
  
`F9 FA FC FE FF 00 00 00 FF FF FE FC FC FC FC FC FC FC FC FC FB FB FB FB FB FB FB FB FB FB FB FB FB 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 `  
  
`03 02 00 FD FA F9 F9 F9 FA FB FD 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 18 0D 1C 29 33 38 3A 36 24 18 15 15 16 17 18 18 `  
  
`19 17 15 12 0F 0E 0D 0D 0D 0E 10 14 15 15 15 15 15 15 16 16 17 17 18 18 18 18 18 18 18 18 18 18 18 0C 04 03 02 01 FE FB F8 F3 F1 F1 F1 F1 F1 F1 F1 `  
  
`F1 F2 F2 F2 F2 F1 F1 F2 F2 F2 F2 F3 F3 F3 F3 F3 F3 F2 F2 F2 F2 F2 F2 F1 F4 F7 FA FD 00 03 06 09 0C 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF `  
  
`FC FC FF 03 06 07 07 06 04 03 02 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF FE FE FE FE FF FF 00 0B 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`01 02 03 05 06 07 07 07 08 08 08 09 09 09 09 09 08 07 06 05 04 02 01 00 01 03 04 05 06 08 09 0A 0B 01 FD 02 05 07 08 08 08 04 00 00 FF 00 00 01 00 `  
  
`FF FF 00 01 02 02 01 01 01 01 01 01 00 00 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 F3 F1 F3 F6 F9 FA FB FA F5 F3 F2 F2 F2 F2 F2 F3 `  
  
`F5 F5 F2 EE EB EA EA EB EB ED EE F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 48 3D 4B 57 61 67 68 64 52 47 45 45 45 47 48 48 `  
  
`49 47 44 40 3E 3C 3C 3C 3C 3D 3F 43 44 44 44 44 44 45 45 46 46 47 47 48 48 48 48 48 48 48 48 48 48 0C 15 15 15 14 12 0F 0C 0C 0C 0C 0C 0C 0C 0C 0C `  
  
`0C 0D 11 15 18 19 19 17 17 18 1F 2D 32 33 32 30 2D 29 25 20 1B 16 11 0C 0C 0C 0C 0C 0C 0C 0C 0C 0C 24 25 25 25 24 24 24 24 24 24 24 24 24 24 24 24 `  
  
`24 24 24 24 25 25 25 25 25 25 24 26 28 29 28 27 26 25 24 24 23 23 24 24 24 24 24 24 24 24 24 24 24 01 02 02 02 02 02 02 01 01 01 01 01 01 01 01 01 `  
  
`01 02 02 02 02 02 02 02 01 02 02 03 04 04 04 04 03 03 03 02 02 02 02 01 01 01 01 01 01 01 01 01 01 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 `  
  
`D2 D0 CB C6 C1 C1 C1 C0 C0 C0 C2 C6 C7 C8 C8 C7 C5 C2 C1 C4 C7 CB CE D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A `  
  
`0A 0A 0A 0A 0A 8A 8A 8A 0A 0A 8A 8A 8A 8A 8A 8A 8A 8A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 0A 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 80 80 80 00 00 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 F0 F4 F0 ED EC EC EC EC EE F1 F1 F1 F1 F1 F1 F0 `  
  
`EF F0 F2 F5 F7 F8 F8 F8 F8 F7 F6 F3 F2 F2 F3 F3 F3 F2 F2 F2 F1 F1 F1 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 0B 0D 0A 06 02 00 FF 01 08 0B 0C 0C 0B 0B 0B 0B `  
  
`0E 0E 0C 09 06 05 05 06 07 08 09 0B 0C 0C 0C 0C 0C 0C 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B E7 DC EB F9 03 0A 0B 07 F3 E6 E4 E4 E4 E6 E7 E7 `  
  
`E7 E5 E4 E1 DF DE DD DD DD DE E0 E3 E4 E4 E4 E3 E4 E4 E5 E5 E6 E6 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 `  
  
`D6 D2 CB C3 C3 C6 C5 C4 C3 C4 C4 C4 C4 C4 C4 C4 C4 C6 C8 CA CD CF D2 D5 D5 D5 D5 D5 D5 D5 D5 D5 D5 26 26 26 26 26 26 26 26 26 26 26 26 26 26 26 26 `  
  
`26 26 25 20 AC A6 A0 93 76 5C 56 58 5A 5F 62 5B 4B 3D 34 2F 2C 29 28 26 26 26 26 26 26 26 26 26 26 97 97 97 97 97 97 97 97 97 97 97 97 97 97 97 97 `  
  
`97 97 99 9E 11 17 1D 2A 48 63 68 66 64 5F 5C 63 74 82 8A 90 93 95 96 97 97 97 97 97 97 97 97 97 97 1B 15 17 19 1B 1B 1B 1B 1B 1B 1B 1B 1B 1B 1B 1B `  
  
`1B 1B 1E 20 1E 13 02 EE DB CD C7 CB CE CD CC CC CE CC C5 C8 DC F3 0A 1B 1B 1B 1B 1B 1B 1B 1B 1B 1B DB DB DB DB DB DB DB DB DB DB DB DB DB DB DB DB `  
  
`DA DC DD E0 E5 EB ED EB E6 D8 BC 6C 65 67 6A 68 66 67 6A F1 F3 F3 ED DB DB DB DB DB DB DB DB DB DB FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE `  
  
`FE FE FF 00 04 08 07 05 03 08 22 72 74 71 6E 73 7D 86 8F 13 17 17 10 FE FE FE FE FE FE FE FE FE FE DB D1 D0 D0 D1 D4 D8 DB DB DB DB DB DB DB DB DB `  
  
`DA DC DE E0 E4 EB F6 03 0D 0F F5 C6 D7 D9 D6 D0 CC C8 C2 C3 C9 CF D5 DB DB DB DB DB DB DB DB DB DB F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 `  
  
`F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 76 76 76 76 76 76 76 76 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 F6 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 02 00 00 00 00 00 01 02 02 02 02 02 02 02 02 02 `  
  
`02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 02 05 BF BE BE C0 C8 D3 E1 F8 06 09 09 08 07 05 05 `  
  
`05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 05 80 7E 7E 7E 7E 7E 7E 7F 80 80 80 80 80 80 80 80 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 D2 CA CA CA CA CC CF D2 D3 D2 D2 D2 D2 D2 D2 D2 `  
  
`D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 F2 19 1B 1C 17 07 F8 F1 F1 F2 F2 F2 F2 F2 F2 F2 `  
  
`F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 F2 66 41 3F 3F 44 53 61 67 67 66 66 66 66 66 66 66 `  
  
`66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 66 20 00 FF FF 01 04 09 0F 1A 20 22 22 21 21 20 20 `  
  
`20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 20 EC FE FE FE FE FF 00 FD F2 EB EA EA EA EB EC EC `  
  
`EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC EC 08 0B 0B 0B 0B 0B 0B 0B 0A 08 07 07 07 08 08 08 `  
  
`08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 08 F7 08 09 09 07 01 FA F4 F5 F7 F8 F8 F8 F7 F7 F7 `  
  
`F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 FE 00 00 00 00 00 FF FE FE FE FE FE FE FE FE FE `  
  
`FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE FE 85 3F 3E 3E 40 48 53 61 78 86 89 89 88 87 85 85 `  
  
`85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 85 80 82 82 82 82 82 82 81 80 80 80 80 80 80 80 80 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 CE CA CA CA CA CA CA CA CC CE CF CF CE CE CE CE `  
  
`CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE CE D2 EA EA EA EA EB ED E8 D9 D2 D1 D1 D1 D2 D2 D2 `  
  
`D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 D2 CA B3 B3 B3 B3 B1 B0 B4 C3 CA CB CB CB CA CA CA `  
  
`CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA CA 1D FF FD FD 01 0F 21 2C 24 1C 1B 1B 1B 1C 1C 1D `  
  
`1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D EF 01 01 01 01 02 02 00 F5 EF EE ED EE EF EF EF `  
  
`EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF F7 F5 F5 F5 F5 F5 F5 F5 F6 F7 F7 F7 F7 F7 F7 F7 `  
  
`F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 F7 00 00`  

  
  
Model 2, Model 3, Model 4, Model 5, and Model 6 1st animation data \[at
offset 0x0000B668\]:

  

`00 00 00 00 00 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 00 FA 00 00 FF FF FF 00 00 06 00 00 FF FF FF 00 00 FA E7 37 FF FF FF 00 00 DC EE 16 FF `  
  
`FF FF 00 00 D4 0E 30 FF FF FF 00 00 00 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 F9 19 C9 FF FF FF 00 00 DC 12 EA FF FF FF 00 00 D0 ED D4 FF FF `  
  
`FF 00 00 00 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 00 B3 80 FF FF FF 00 00 C6 00 40 FF FF FF 00 00 00 00 F3 FF FF FF 00 00 DD CF 39 FF FF FF `  
  
`00 00 00 4D 80 FF FF FF 00 00 C6 00 C0 FF FF FF 00 00 00 00 0D FF FF FF 00 00 E2 31 C7 FF FF FF 00 64 FE 02 00`

  
  
Model 2, Model 3, Model 4, Model 5, Model 6, Model 7, Model 8, and Model
9 2nd animation data \[at offset 0x0000B720\]:

  

`00 00 00 00 20 00 00 00 FF 00 00 00 00 C0 00 00 FF FF FF 00 00 FA 00 00 FF FF FF 00 00 06 00 00 FF FF FF 00 00 FA E7 37 FF FF FF 00 07 00 01 02 FF `  
  
`FF FF 00 07 03 04 05 FF FF FF 00 01 06 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 F9 19 C9 FF FF FF 00 07 07 08 09 FF FF FF 00 07 0A 0B 0C FF FF `  
  
`FF 00 01 0D 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 00 B3 80 FF FF FF 00 07 0E 0F 10 FF FF FF 00 01 11 00 00 FF FF FF 00 07 12 13 14 FF FF FF `  
  
`00 00 00 4D 80 FF FF FF 00 07 15 16 17 FF FF FF 00 01 18 00 00 FF FF FF 00 07 19 1A 1B FF FF FF 00 77 FE 71 FE 6C FE 68 FE 64 FE 61 FE 60 FE 61 FE `  
  
`64 FE 68 FE 6C FE 71 FE 76 FE 7B FE 7D FE 7A FE 73 FE 6D FE 68 FE 64 FE 61 FE 60 FE 61 FE 64 FE 68 FE 6C FE 70 FE 74 FE 79 FE 7D FE 02 00 D7 D7 D7 `  
  
`D8 D8 D7 D7 D7 D8 D8 D9 D9 D9 D9 D9 D8 D8 D8 D8 D8 D8 D9 D9 DA DA DA D9 D8 D7 D6 E8 E9 E9 E9 E9 E9 E9 E9 E9 EA EA EB EB EB EA EA EA E9 E9 E9 EA EB `  
  
`EB EC EC EC EB EA E9 E7 1B 1A 1A 19 1A 1A 1A 1A 19 19 18 18 18 18 18 19 19 1A 1A 19 19 18 18 18 17 17 18 19 1A 1B E6 E5 E4 E3 E0 DE DB D9 D7 D6 D4 `  
  
`D3 D3 D3 D4 D5 D4 D4 D3 D3 D5 D7 DA DD E0 E3 E4 E5 E6 E7 29 28 27 26 24 22 1F 1C 18 13 0E 06 FB F2 ED ED F0 F5 FB 05 0F 17 1D 21 24 26 27 28 29 29 `  
  
`0F 10 11 13 15 18 1C 20 25 2A 31 39 45 50 55 56 52 4D 45 3B 2F 25 1F 1A 16 13 11 10 0F 0E F7 F5 F3 F0 ED EA E7 E6 E6 E6 E7 E9 ED F0 F2 F3 F2 F1 EF `  
  
`ED EA E7 E6 E5 E6 E7 EA EF F4 F9 D8 D8 D8 D9 D9 D8 D8 D9 D9 D9 D9 D9 D9 D9 D8 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D8 D8 16 16 16 16 16 16 16 16 `  
  
`15 15 15 15 15 15 16 16 15 15 15 15 15 16 15 15 15 15 15 16 16 16 E7 E7 E7 E7 E7 E7 E7 E7 E8 E8 E8 E8 E8 E8 E7 E7 E8 E8 E8 E8 E8 E8 E8 E8 E8 E8 E8 `  
  
`E8 E7 E7 D2 CF CE CE CF D0 D1 D3 D6 DA DD E0 E2 E3 E4 E5 E4 E3 E1 DE D9 D5 D3 D2 D2 D1 CF CE D1 D5 1B 12 07 FC F4 ED E8 E2 DC D8 D6 D4 D3 D2 D2 D2 `  
  
`D2 D2 D3 D5 D9 DE E2 E3 E5 E9 F3 05 17 22 A3 AD B9 C4 CD D4 DA E1 E7 EC EF F1 F3 F4 F4 F4 F4 F4 F2 EF EB E5 E1 DF DD D9 CD BA A8 9B F3 EF EC EA E9 `  
  
`EA EB EB EB EA EB ED F0 F4 F6 F5 F3 F0 EE ED EC EC EB E9 E8 E7 E9 ED F2 F6 D4 D2 CF CD C9 C6 C3 C2 C4 C6 C8 CB CF D3 D5 D4 D1 CD C9 C3 C4 CA CF D2 `  
  
`D4 D5 D6 D7 D7 D7 B6 B7 B7 B8 BB C0 D1 06 1E 25 29 2C 2E 2F 2F 2F 2E 2D 2A 1B C3 BA B8 B7 B6 B6 B6 B6 B6 B6 7D 7C 7C 7A 78 73 62 2D 15 0D 09 06 04 `  
  
`03 03 03 04 05 08 18 6F 79 7B 7C 7D 7D 7D 7D 7D 7D 09 09 09 08 06 03 01 00 02 05 07 08 07 06 08 10 1A 25 2C 31 33 34 33 2F 29 23 1D 16 0F 08 C4 C7 `  
  
`CA CC CC CB C9 C6 C3 C3 C7 C9 CA CB CB CB CB CB CB CD CE CF CD CA C6 C3 C2 C1 C1 C1 F2 FA FD FD FD FD FC F9 E9 97 8B 89 88 88 88 87 88 88 87 87 86 `  
  
`86 87 88 8D 9B B5 BF BD C0 10 08 06 05 05 06 07 0A 1A 6B 77 79 7A 7A 7A 7B 7B 7A 7B 7B 7C 7C 7B 7A 75 67 4E 43 45 43 D3 D0 CD C9 C3 C4 CB CF D2 D4 `  
  
`D5 D6 D7 D7 D7 D5 D3 D0 CE CA C6 C3 C0 C3 C5 C7 CB CE D2 D6 CE CE CE CE D0 4C 4D 4D 4D 4D 4D 4D 4D 4D 4D 4D 4D 4D 4D 4D 4C 4B E2 D0 CF CF CE CE CE `  
  
`CE 00 00 FF FF FD 82 81 80 80 80 80 80 80 80 80 80 80 80 81 81 81 83 EC FD FF FF FF 00 00 00 11 1C 25 2B 30 34 35 34 2F 29 22 1C 14 0C 08 07 09 0C `  
  
`0C 09 05 02 02 03 06 07 08 08 08 08 CB CB CA CB CC CE CE CD CA C6 C2 C1 C1 C0 C0 C3 C5 C8 C9 CA C9 C8 C6 C2 C2 C6 C8 C9 CA CB 7E 7E 7E 7E 7F 7F 7F `  
  
`7F 7E 7E 7D 79 75 72 0C 01 00 00 FF FF FF 00 00 01 7C 7E 7E 7E 7E 7E 80 80 81 80 80 80 80 80 81 81 82 86 8A 8D F3 FE FF FF FF FF FF FF FF FE 83 81 `  
  
`81 81 81 80 00 00`

  
  
Model 2, Model 3, Model 4, Model 5, Model 6, Model 7, Model 8, and Model
9 3rd animation data \[at offset 0x0000BB5C\]:

  

`00 00 00 00 20 00 00 00 FF 00 00 00 00 C0 00 00 FF FF FF 00 01 00 00 00 FF FF FF 00 01 01 00 00 FF FF FF 00 07 02 03 04 FF FF FF 00 00 D6 E6 1C FF FF FF 00 07 05 `  
  
`06 07 FF FF FF 00 00 C9 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 07 08 09 0A FF FF FF 00 00 D8 16 E7 FF FF FF 00 07 0B 0C 0D FF FF FF 00 00 CD 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 B3 80 FF FF FF 00 07 0E 0F 10 FF FF FF 00 07 11 12 13 FF FF FF 00 07 14 15 16 FF FF FF 00 00 00 4D 80 FF FF FF 00 07 17 18 19 FF FF `  
  
`FF 00 07 1A 1B 1C FF FF FF 00 07 1D 1E 1F FF FF FF 00 6F FE 91 FE 91 FE 6F FE 52 FE 4A FE 4C FE 5D FE 82 FE 97 FE 82 FE 5D FE 4C FE 4A FE 52 FE 02 00 21 22 22 23 `  
  
`23 23 23 23 22 22 23 23 23 22 21 E0 DF DF DF E0 E0 E0 E0 E0 DF DF DF E0 E0 E0 19 19 1A 1A 1A 1A 1A 1A 1A 19 1A 1A 1A 19 19 E1 E1 E0 E0 E0 E0 E0 E0 E0 E1 E0 E0 E0 `  
  
`E1 E1 1E 1E 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1D 1E 1E DF DC E0 E7 EF FA 02 02 FA EF E7 E1 DC DF E3 E6 04 1A 26 2E 37 3E 3E 37 2E 26 1C 07 E7 DA 50 39 2A 22 1E 1D 1B `  
  
`1B 1D 1E 21 29 37 4F 5A 18 19 19 19 1A 1A 1A 19 19 19 19 1A 19 19 18 1F 20 20 20 20 20 20 20 20 20 20 20 20 1F 1F E2 E3 E3 E3 E4 E4 E4 E3 E3 E3 E3 E4 E3 E3 E2 FE `  
  
`F0 E4 DD D7 DC EA EA DC D7 DC E5 F0 FE 04 C5 CD D4 DB EE 1C 34 35 1C F0 DB D4 CD C5 C1 E9 E7 E6 E1 D2 B0 9B 9A AF D1 E1 E6 E8 E9 EB D0 C3 CA D7 E0 E1 DD D8 D3 CB `  
  
`C2 CE D6 DA D8 2E 19 BA B6 B5 B5 B5 B6 B7 B9 08 2D 2F 30 2F 04 1A 79 7D 7E 7E 7E 7D 7C 7A 2B 05 03 02 03 3F 39 30 24 24 3C 13 08 19 27 20 15 17 26 35 FE 80 80 80 `  
  
`80 00 00 00 00 00 00 00 00 00 00 FE 80 80 80 80 00 00 00 00 00 00 00 00 00 00 CF CE C9 C2 C6 C4 C2 C2 CD D5 D2 CA C3 C7 CD FF FE FC C9 8C 93 E3 A0 87 85 85 88 9B `  
  
`FA FE 04 04 06 39 76 70 1F 63 7B 7D 7D 7A 67 09 05 D5 CF C6 C7 D1 D8 DB D6 CA C3 D0 DC E0 DE DA 4D 4D 4C CF CE CE CE CE CE 4B 4D 4D 4D 4D 4D 80 80 81 FF 00 00 00 `  
  
`00 FF 83 80 80 80 80 80 0E 23 27 1B 13 1D 2D 39 3E 36 2A 22 32 25 07 00 00 00 00 00 00 00 00 81 80 80 80 80 00 00 00 00 00 00 00 00 00 00 81 80 80 80 80 00 00 C8 `  
  
`D4 D5 CD C4 C4 CB CE CD CB C5 C2 C4 C0 C1 7F 7F 7F 7F 7E 00 FF FF FF FF 00 7D 7E 6E 03 80 80 80 80 81 FF 00 00 00 00 FF 81 81 91 FC`

  
  
  
Model 4 and Model 6 4th animation data \[at offset 0x0000BE10\]:

  

`00 00 00 00 61 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 01 01 00 00 FF FF FF 00 07 02 03 04 FF FF FF 00 07 05 06 07 FF FF FF 00 07 08 09 0A FF FF FF 00 07 0B `  
  
`0C 0D FF FF FF 00 07 0E 0F 10 FF FF FF 00 00 00 00 00 FF FF FF 00 07 11 12 13 FF FF FF 00 07 14 15 16 FF FF FF 00 07 17 18 19 FF FF FF 00 07 1A 1B 1C FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 07 1D 1E 1F FF FF FF 00 07 20 21 22 FF FF FF 00 07 23 24 25 FF FF FF 00 00 00 51 80 FF FF FF 00 07 26 27 28 FF FF `  
  
`FF 00 07 29 2A 2B FF FF FF 00 07 2C 2D 2E FF FF FF 00 65 F6 62 F6 60 F6 5F F6 63 F6 6C F6 7B F6 8E F6 A3 F6 B6 F6 C6 F6 D6 F6 E8 F6 F3 F6 F0 F6 D3 F6 8F F6 46 F6 `  
  
`1B F6 2B F6 6B F6 BD F6 20 F7 93 F7 16 F8 A9 F8 4B F9 19 FA 1E FB 3F FC 5F FD 5A FE ED FE 1B FF 28 FF 31 FF 37 FF 3B FF 3C FF 3C FF 39 FF 35 FF 30 FF 2A FF 23 FF `  
  
`1B FF 12 FF 05 FF F4 FE E2 FE CE FE BA FE A5 FE 91 FE 7F FE EB 0B 91 0B 36 0B DB 0A 80 0A 22 0A BF 09 5B 09 F8 08 9C 08 4A 08 12 08 EF 07 CB 07 8E 07 21 07 8E 06 `  
  
`E7 05 3D 05 A1 04 0E 04 76 03 DE 02 4C 02 C2 01 47 01 DF 00 97 00 73 00 64 00 5E 00 52 00 4E 00 53 00 53 00 54 00 55 00 56 00 57 00 58 00 59 00 59 00 59 00 58 00 `  
  
`56 00 53 00 4E 00 47 00 3F 00 35 00 2B 00 20 00 16 00 0C 00 02 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF FF 02 05 0A 0E 11 12 13 13 13 13 12 11 0E 09 04 FF FB `  
  
`FD 00 00 00 01 01 01 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 12 12 12 12 12 12 12 12 12 12 12 13 14 14 13 10 0A 02 FC F9 F8 F8 F9 FA FC FF 01 04 09 0D 12 `  
  
`15 14 12 12 12 13 13 13 14 14 14 14 14 13 12 11 0F 0C 09 06 03 00 FD FA FE FE FE FE FE FE FE FE FE FE FE FD FC FC FD 01 09 12 1A 20 22 23 23 23 22 21 20 1E 1C 19 `  
  
`16 13 08 FE FD FC FC FC FC FC FC FC FC FD FD FE FF 00 01 02 03 04 05 06 06 FD FD FD FD FD FD FD FD FD FD FD FD FD FD FD FE FF 00 00 00 00 00 00 00 00 00 00 01 03 `  
  
`04 03 00 F9 FD FF 00 00 01 01 00 00 FF FF FE FE FD FD FD FC FC FD FD FE FF 00 06 06 06 06 06 06 06 06 06 06 06 06 07 07 07 06 04 02 01 00 00 FF FF 00 00 00 00 02 `  
  
`05 07 06 00 E4 CD CA C8 C6 C5 C4 C4 C5 C6 C7 C9 CB CD D0 D4 D9 DF E6 ED F3 FA 00 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0F 0F 0E 0C 06 00 FA F7 F6 F6 F7 F9 FB FD FF `  
  
`01 05 09 0D 10 0F 0E 0E 0E 0E 0E 0F 0F 0F 0F 0F 0F 0E 0E 0C 0B 08 06 03 00 FE FB F8 EA EA EA EA EA EA EA EA EA EA EA EA EA EA EA EA EB EB EB EB EB EB EB EB EB EB `  
  
`EB EB EB EB EA E9 EA EA EA EA EA EA EA EA EA EA EA EA EA EA EA EB EB EB EB EB EB EB EB 27 27 27 27 27 27 27 27 27 27 27 27 26 26 27 28 2C 2F 32 34 34 34 34 33 32 `  
  
`31 30 2E 2C 2A 28 26 26 27 27 27 27 27 26 26 26 26 26 26 27 27 28 29 2A 2C 2D 2F 30 32 33 DA DA DA DA DA DA DA DA DA DA DA DA DA DA DA DA DA DB DB DB DC DD DE DF `  
  
`E0 E2 E3 E6 EB EF F2 F2 E6 DA D9 D8 D8 D8 D8 D8 D8 D9 D9 DA DA DA DA DA DA DA DA DA DA DA DA E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E7 E7 E7 E7 E8 E9 EA EB `  
  
`EC EE EF F0 F3 F5 F8 FA FA F2 E6 E4 E3 E2 E2 E2 E3 E4 E4 E5 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 E6 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1D 1D 1C 1B `  
  
`1A 19 19 18 17 15 14 13 12 12 16 1E 20 21 21 22 21 21 20 20 1F 1F 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E 1E DA D2 CA C2 C7 D1 DF ED FB 05 09 05 F8 E8 D9 CD C4 CD D4 D6 DC `  
  
`F0 09 22 36 3A 30 28 16 08 0A 0A D8 DB E1 E5 E8 E9 EA E9 E7 E5 E2 E0 DD DB D8 D5 D0 CC C7 C5 C8 CD D1 C0 C0 C0 C0 40 40 40 40 40 40 40 40 40 40 40 41 77 A2 AC C3 `  
  
`EC 12 31 4D 67 FB 0A 1D 26 2A 2F 34 3B C0 BF BE BE BE BE BE BE BE BF BF BF C0 C1 C2 C5 CA D8 FE 1E 29 2D 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 FE C5 97 8C `  
  
`7C 62 53 4E 4E 51 D7 E1 FA 07 01 FA FD 01 80 81 81 81 81 81 81 81 81 81 81 80 80 7F 7E 7B 76 69 42 21 16 11 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C6 C3 C0 C1 C3 CB D5 `  
  
`DF E5 E9 EC ED EF F0 F0 F1 F2 F1 F0 F0 F1 F9 00 01 02 02 02 03 03 02 02 02 01 01 00 FF FE FC FB F9 F7 F5 F3 F1 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0E 0F 0F 0E `  
  
`0C 06 00 FA F7 F6 F7 F7 F9 FB FD FF 01 05 09 0D 10 0F 0E 0E 0E 0E 0E 0F 0F 0F 0F 0F 0F 0E 0E 0C 0B 08 06 03 00 FE FB F9 16 16 16 16 16 16 16 16 16 16 16 16 16 16 `  
  
`16 16 15 15 15 15 15 15 15 15 15 15 15 15 15 15 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 15 15 15 15 15 15 15 15 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 DA `  
  
`DA D9 D7 D4 D1 CE CC CB CB CC CD CE CF D0 D2 D4 D6 D8 DA DA D9 D9 D9 D9 D9 D9 DA DA DA DA DA D9 D9 D8 D7 D6 D4 D3 D1 D0 CE CD DA DA DA DA DA DA DA DA DA DA DA DA `  
  
`DA DA DA DA DA DA DA DA DB DC DD DF E0 E2 E4 E6 EA EE F0 F0 E5 DA D9 D8 D8 D8 D8 D8 D9 D9 D9 DA DA DA DA DA DA DA DA DA DA DA DA 1A 1A 1A 1A 1A 1A 1A 1A 1A 1A 1A `  
  
`1A 1A 1A 1A 1A 1A 1A 1A 19 18 17 15 14 12 11 0F 0D 0B 09 07 07 0E 1A 1B 1D 1D 1E 1D 1D 1C 1C 1B 1A 1A 1A 1A 1A 1A 1A 1A 1A 1A 1A 1A E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 `  
  
`E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E3 E4 E5 E6 E7 E8 E9 EB EC ED EE EE EA E2 E1 DF DF DF DF DF E0 E0 E1 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 E2 11 05 F8 EC E1 D6 CA C2 CC `  
  
`D4 D9 D8 D0 C7 C0 C0 C5 CC D0 CB C3 D7 ED 04 18 24 27 27 26 22 19 0C E5 C1 C4 C7 C9 CA CA C9 C7 C6 C4 C2 C0 C1 C2 C3 C5 C7 C9 CB CD CF D1 C0 C0 C0 C0 C0 C0 C0 40 `  
  
`40 40 40 40 40 40 3E A1 47 45 44 42 DD CB CB CE D5 E4 F4 F9 F3 E8 DD D5 CC C0 4C 4C 4C 4C 4C 4C 4C 4D 4E 51 66 C0 C8 CB CD CD CE CE CE CF CF 00 00 00 00 00 00 00 `  
  
`80 80 80 80 80 80 80 82 1F 79 7B 7C 7E E3 F7 FB 01 0D 1F 31 37 30 22 13 07 F9 00 74 75 75 75 75 74 74 73 72 6F 5A 00 F8 F5 F3 F3 F3 F2 F2 F2 F2 D4 D4 D4 D4 D4 D4 `  
  
`D4 D5 D5 D5 D4 D5 D5 D6 D6 D2 D1 D7 E1 E8 EB EC EC EB E9 E8 E8 E9 EB EC EC E8 D4 D5 D6 D8 D9 DA DB DB DA DA D9 D7 D6 D5 D3 D2 D2 D4 D8 DE E4 EB F1 C6 C6 C6 C6 C6 `  
  
`C6 C7 C7 C7 C7 C6 C2 BC B7 B7 BF D8 F1 FC 00 01 02 02 01 01 00 00 01 02 02 02 00 E9 B9 B4 B2 B0 AF AF AE AF AF B1 B2 B5 B9 BE C8 D5 E3 ED F5 FA FD 00 39 39 39 39 `  
  
`39 39 38 38 38 38 39 3D 45 4A 4B 41 26 0D 03 00 FF FF FF FF 00 00 00 00 FF FF FF 00 15 49 4D 51 53 55 55 55 55 54 52 50 4D 49 42 37 29 1B 10 09 04 01 00 C9 C4 D0 `  
  
`DB E4 E9 EB EA E8 E7 E7 EB F2 F7 F7 EF DD C9 CD D8 DB DC DA D7 D3 CF CD CB CA C8 C7 C6 C6 C9 CA CB CB CB CB CB CB CB CB CA CA C9 C9 C8 C7 C6 C6 C5 C5 C5 C6 2F AF `  
  
`AF AF AF AF AF AF AF AF AF AF AF AF AF B0 B2 C0 1E 24 25 25 24 23 21 1F 1B 18 12 0B 00 EF C3 AF AE AD AC AB AB AB AB AC AC AD AE AF B1 B3 B7 BD C5 D0 DC E7 EF 00 `  
  
`80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 7E 6F 10 09 08 08 09 0A 0C 0F 13 17 1C 24 2F 40 6C 80 81 83 83 84 84 84 84 83 83 82 81 80 7E 7C 78 72 6A 5F 54 49 40 `  
  
`2B 21 18 12 11 19 2C 3B 20 0B 01 0A 21 3C 32 32 3F 2A 15 09 05 04 04 06 09 0B 0C 0B 09 07 07 0C 28 3E 3B 38 36 35 34 34 34 35 37 39 3B 3E 3E 38 31 2A 21 19 10 08 `  
  
`00 80 80 80 80 80 80 80 00 00 00 00 00 00 00 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 `  
  
`00 00 80 80 80 80 80 80 80 00 00 00 00 00 00 00 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 `  
  
`00 00 00 C5 C5 C5 C5 C5 C5 C6 C7 C7 C7 C5 C1 C9 D1 D5 D1 CF DA E8 F0 F3 F5 F5 F4 F3 F2 F0 EF EE EC E8 E1 DC F3 F7 FA FC FD FE FE FD FC FA F8 F6 F3 F0 EB E6 E0 DC `  
  
`D9 DA DD E1 00 00 00 00 00 00 00 00 00 00 00 48 73 76 7C 8D BA DE ED F3 F5 F6 F7 F7 F6 F5 F3 EF EA E3 DB D0 9C 80 7D 7B 7A 79 79 79 79 7A 7B 7C 7E 80 83 87 8C 94 `  
  
`9F AD BC C8 D0 00 00 00 00 00 00 00 00 00 00 00 B8 8B 87 83 77 52 35 29 23 21 20 20 20 21 22 23 24 26 28 2D 38 6C 80 81 81 81 81 81 81 81 81 81 81 80 80 7F 7D 7A `  
  
`74 6A 5C 4E 41 38 E3 DF DB D7 D1 CB C0 CC D6 DD DD CE CC E8 FA F7 E3 C7 D5 E5 EA EC EC E9 E6 E2 DE DA D5 CF C8 C8 E3 FB FF 01 03 05 05 05 05 04 02 00 FE FB F8 F3 `  
  
`ED E6 DE D6 CF C8 C5 51 51 51 51 51 51 51 D1 D1 D1 D1 D1 52 51 51 50 4F 3F DA D8 D7 D7 D7 D7 D8 D8 D9 DA DC E1 F3 34 4E 51 51 51 52 52 52 52 52 52 52 51 51 51 51 `  
  
`50 4F 4F 4D 4B 46 39 11 80 80 80 80 80 80 80 00 00 00 00 00 7F 80 80 80 81 92 F8 FC FD FD FD FD FC FB FA F9 F6 F1 DE 9D 82 80 80 80 80 80 80 80 80 80 80 80 80 80 `  
  
`80 80 81 81 83 85 8A 97 C0 0E 1A 25 2F 38 3F 3D 3A 38 35 32 2A 20 17 16 21 38 2B 11 00 F9 F7 F7 F9 FC FF 00 FE FB F8 F9 00 26 36 31 2E 2B 2A 29 29 2A 2B 2D 30 33 `  
  
`36 3B 3F 38 2F 26 1C 12 09 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 `  
  
`80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 `  
  
`80 80 80 80 00 00 00 00 00 00 00 00 C0 CB D5 DE E3 E5 E2 DD D6 CF CB CA CC CE CD C8 D1 E1 EE F5 F7 F6 F3 F0 EC E8 E5 E5 E7 E9 E9 E5 D1 C7 C9 CB CC CC CD CC CC CB `  
  
`CA C9 C8 C7 C7 C7 C9 CC D0 D4 D9 DD E1 80 80 80 80 80 80 80 80 80 80 80 85 8B 8E 87 65 2A 15 0A 07 07 0A 0E 12 17 1C 20 21 20 1F 1F 20 2F 80 8B 92 95 97 98 98 97 `  
  
`95 92 8E 88 80 73 61 51 45 3E 39 35 33 31 80 80 80 80 80 80 80 80 80 80 80 7C 77 76 7A 97 C8 D5 DB DE DF DE DC D9 D7 D4 D3 D2 D3 D3 D4 D3 C8 80 76 71 6E 6C 6B 6B `  
  
`6C 6D 70 73 79 80 8C 9D AC B7 BD C1 C4 C6 C7 00 00 00`

  
  
  
Model 4 5th animation data \[at offset 0x0000C9BC\]:

  

`00 00 00 00 73 00 01 00 00 01 02 00 00 C0 00 00 FF FF FF 00 07 02 03 04 FF FF FF 00 07 05 06 07 FF FF FF 00 07 08 09 0A FF FF FF 00 07 0B 0C 0D FF FF FF 00 07 0E `  
  
`0F 10 FF FF FF 00 07 11 12 13 FF FF FF 00 01 14 00 00 FF FF FF 00 07 15 16 17 FF FF FF 00 07 18 19 1A FF FF FF 00 07 1B 1C 1D FF FF FF 00 07 1E 1F 20 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 07 21 22 23 FF FF FF 00 07 24 25 26 FF FF FF 00 07 27 28 29 FF FF FF 00 00 00 51 80 FF FF FF 00 07 2A 2B 2C FF FF `  
  
`FF 00 07 2D 2E 2F FF FF FF 00 07 30 31 32 FF FF FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 00 02 00 03 00 02 00 00 00 FA FF F1 FF E9 FF E4 FF `  
  
`E3 FF E2 FF E2 FF E3 FF E4 FF E5 FF E6 FF E7 FF E8 FF E9 FF EA FF EB FF EC FF ED FF EE FF EE FF EE FF EE FF ED FF ED FF ED FF ED FF ED FF EE FF EE FF F0 FF F1 FF `  
  
`F3 FF F4 FF F6 FF F7 FF F9 FF FA FF FC FF FD FF FF FF 00 00 85 FE 8B FE 92 FE 99 FE 9F FE A5 FE AA FE AE FE B0 FE B1 FE B0 FE AF FE AE FE AE FE AE FE AE FE AE FE `  
  
`AE FE AE FE AE FE AE FE AF FE AF FE AE FE AE FE AD FE AD FE AD FE AE FE B0 FE B3 FE B6 FE B9 FE BB FE BC FE BD FE BE FE BE FE BD FE BC FE BB FE B9 FE B6 FE B1 FE `  
  
`AB FE A5 FE 9F FE 9A FE 95 FE 91 FE 8D FE 89 FE 85 FE 82 FE 7F FE F7 FF EB FF DF FF D3 FF C8 FF BE FF B5 FF AE FF A9 FF A6 FF A5 FF A7 FF A9 FF AE FF B6 FF C4 FF `  
  
`D1 FF D9 FF DA FF D9 FF D7 FF D4 FF D2 FF D3 FF D7 FF E0 FF EC FF FB FF 0A 00 19 00 27 00 32 00 3A 00 3F 00 41 00 42 00 42 00 41 00 40 00 3E 00 3C 00 3A 00 38 00 `  
  
`34 00 2F 00 2A 00 25 00 20 00 1B 00 16 00 12 00 0D 00 08 00 03 00 FE FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF FF FF 00 01 03 05 07 09 `  
  
`0B 0C 0E 0E 0F 0F 0F 0F 0F 0E 0E 0E 0D 0C 0B 0A 09 07 06 05 04 03 02 01 00 00 00 00 00 00 00 00 00 01 04 06 08 06 00 F0 D7 BD AB A1 99 92 8D 89 86 83 81 80 80 80 `  
  
`81 82 83 83 83 83 83 83 83 83 83 83 83 83 83 82 82 82 81 81 80 80 80 7F 7F 7F 0D 0D 0D 0D 0D 0D 0D 0D 0D 0D 0E 0E 0D 0D 09 02 F8 F2 F0 EF ED EB EA E9 EB EF F6 00 `  
  
`0A 14 1D 25 2B 2E 31 32 33 33 33 32 31 30 2E 2A 26 21 1D 18 14 10 0B 07 03 FE FA 00 00 00 00 00 00 00 00 00 FE FD FD FE 00 07 0E 12 12 0F 0B 07 04 02 00 00 FF FF `  
  
`00 00 01 02 04 05 06 07 08 09 09 09 08 08 07 06 05 04 03 02 02 01 01 01 01 00 00 00 00 00 00 00 00 00 00 00 FF FE FD FC FD 00 07 11 19 1B 1A 16 12 0D 09 05 03 01 `  
  
`01 00 00 01 02 04 05 06 07 08 08 09 08 08 07 06 05 04 03 02 01 01 01 00 00 00 00 00 00 F4 F4 F4 F4 F4 F4 F4 F4 F3 F3 F2 F1 F2 F4 FA 04 0F 15 18 1B 1C 1E 1F 20 21 `  
  
`22 23 24 25 25 25 23 20 1B 14 0C 02 F8 EF E6 DF DA D8 D8 DB DF E3 E7 EB EF F3 F8 FD 01 06 00 00 00 00 00 00 00 00 00 01 02 02 02 00 FC F9 FA FE 01 03 04 05 05 04 `  
  
`04 05 06 07 09 09 09 07 04 FF FA F6 F3 F0 ED EB E9 E7 E7 EA EE F1 F4 F6 F8 F9 FB FC FD FF 00 00 00 00 00 00 00 00 00 00 FE FD FD FE 00 06 0F 17 1C 1D 1C 1A 18 15 `  
  
`13 11 11 12 13 14 15 15 13 11 0E 0B 09 09 0A 0B 0E 11 14 14 11 0D 09 06 04 02 01 00 00 FF 00 00 09 09 09 09 09 09 09 09 09 08 08 08 08 09 0A 07 02 FE FB F9 F6 F2 `  
  
`EF EC ED F0 F6 FD 06 0F 18 1F 23 26 27 28 29 29 29 28 27 27 25 22 1F 1B 17 13 0F 0C 08 04 00 FC F8 EB EB EB EB EB EB EB EB EA E9 E9 E8 E9 EB F1 FA 00 00 FD F8 F3 `  
  
`EE EB E8 E8 E9 EA EB EB EA E9 E6 E3 E0 DD DC DB DB DB DC DD DF E0 E3 E5 E8 E9 EA EB EB EC EC EC EB EB 2A 2A 2A 2A 2A 2A 2A 2A 2A 28 27 27 27 2A 32 3F 4A 4F 4E 4C `  
  
`49 46 44 41 3E 3A 36 31 2C 27 22 1D 18 14 11 0F 0E 0D 0E 0F 11 12 14 18 1C 1F 22 25 27 29 2B 2D 2F 31 33 DA DA DA DA DA DA DA DA DA D8 D7 D6 D7 DA E6 FB 10 1D 20 `  
  
`21 1F 1B 18 16 13 10 0A 00 F3 E6 DB D8 DB DE E0 E1 E1 E0 DE DD DC DB DA D9 D8 D7 D7 D6 D6 D7 D7 D8 D8 D9 DA E6 E6 E6 E6 E6 E6 E6 E6 E8 EB EF F0 EE E6 D8 CB C0 B7 `  
  
`B0 AA A7 A7 A9 AD B1 B6 BC C1 C6 CE DB EF FC 01 04 04 04 03 01 FF FD FC FB FA F8 F6 F4 F1 EF ED EB E9 E8 E7 E6 1E 1E 1E 1E 1E 1E 1E 1E 1D 1A 17 16 18 1E 29 2E 2D `  
  
`26 1E 14 0C 07 03 02 04 08 0F 13 14 0F 02 ED DE D7 D3 D2 D2 D4 D6 D9 DB DE E0 E4 E9 EF F5 FB 01 06 0B 11 15 1A 1E EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF F0 `  
  
`F2 F3 F3 F4 F4 F4 F4 F4 F3 F1 EF ED EA E7 E5 E2 E1 E0 E0 E1 E1 E2 E2 E2 E2 E1 DF DC D9 D5 D1 CE CB C9 C8 C9 CB CE D1 C8 C8 C8 C8 C8 C8 C8 C8 C8 C7 C7 C6 C7 C8 CD `  
  
`D4 DA DE E0 E1 E1 E1 E0 DF DE DD DB D9 D6 D4 D1 CF CD CC CB CB CB CB CC CC CD CD CE CF D0 D3 D7 DC E4 F1 03 14 20 28 2D 7D 7D 7D 7D 7D 7D 7D 7D 7D 7D 7D 7D 7D 7D `  
  
`7B 78 76 74 74 74 74 74 74 75 74 74 74 74 74 74 75 76 77 77 78 78 78 78 78 78 77 77 76 74 72 6F 6B 65 5C 4F 3D 2C 1F 17 11 E0 E0 E0 E0 E0 E0 E0 E0 E0 E0 E1 E1 E1 `  
  
`E0 DE DC DA D9 D5 D0 CB C5 C3 C5 C6 C5 C5 C9 CF D6 DC E1 E4 E6 E7 E8 E8 E8 E7 E6 E5 E4 E2 E0 DE DC DB DC DD DF E2 E5 E9 ED F1 00 00 00 00 00 00 00 00 00 FF FE FE `  
  
`FE 00 05 0F 19 1F 20 1F 1C 10 DB B6 A9 94 6E 56 4C 47 44 43 42 42 42 43 43 43 44 44 43 42 41 3D 38 32 2A 22 1B 15 10 0B 07 03 00 00 00 00 00 00 00 00 00 00 01 01 `  
  
`01 01 00 FC F4 EB E5 E3 E3 E5 F0 25 4A 57 6C 92 AA B3 B8 BA BC BC BC BC BB BB BA BA BA BB BC BF C4 CA D2 DB E3 EA F0 F5 F9 FC FF 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 01 01 00 FE FC F9 F7 F4 F2 F0 F0 EF EF EF F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F1 F2 F3 F5 F6 F7 F9 FA FB FC FE FF 00 09 09 09 09 09 09 09 09 09 `  
  
`0A 0B 0B 0B 09 02 F7 EB E5 E4 E4 E5 E5 E6 E7 EA EE F5 FD 06 0F 16 1C 20 22 23 24 24 25 24 24 23 23 22 20 1D 19 16 12 0F 0B 08 04 00 FC F9 15 15 15 15 15 15 15 15 `  
  
`15 14 13 13 13 15 1A 20 24 24 23 21 1E 1C 1A 19 18 16 15 14 15 17 1B 1F 23 26 28 2A 2B 2B 2B 2A 29 27 25 23 1F 1D 1A 19 18 17 16 15 15 15 15 D6 D6 D6 D6 D6 D6 D6 `  
  
`D6 D5 D5 D4 D3 D4 D6 DB E0 E2 E2 DF DB D5 D0 CB C7 C6 C8 CB CF D4 DA E1 E8 ED F1 F4 F6 F7 F8 F7 F6 F4 F3 F0 EC E8 E4 E0 DD DA D8 D5 D3 D1 CF CD 04 04 04 04 04 04 `  
  
`04 04 05 06 08 08 07 04 F9 E7 D7 D1 D0 D0 D0 D0 D0 D0 D1 D3 D7 DD E5 ED F5 FB FF 01 03 03 04 03 02 01 00 FF FD FB F8 F4 F1 EE EB E8 E5 E2 E0 DD DA 39 39 39 39 39 `  
  
`39 39 39 39 3A 3A 3B 3A 39 38 3B 49 5E 6A 71 74 73 6E 67 5E 53 47 3E 38 35 34 34 35 35 36 36 36 36 36 35 35 35 34 32 31 2F 2D 2B 29 27 25 23 20 1D 1A D3 D3 D3 D3 `  
  
`D3 D3 D3 D3 D3 D4 D5 D6 D5 D3 CD C5 B7 A5 9A 94 91 93 96 9D A5 AF BA C2 C8 CD D0 D4 D6 D7 D8 D9 D8 D8 D7 D7 D6 D6 D6 D6 D6 D6 D6 D7 D8 D9 DA DB DD DF E2 FF FF FF `  
  
`FF FF FF FF FF FF FF FF FF FF FF FE FC FB F9 F7 F6 F6 F7 F9 FA F9 F7 F8 FF 0B 13 13 10 0E 0E 0F 0F 10 10 10 10 11 11 0F 03 EA D0 D8 E8 EE ED E8 E0 D8 D2 D1 0F 0F `  
  
`0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0F 0E 0B 05 FF FC FB 01 0E 25 46 6C 93 BD E5 04 19 26 2F 36 3A 3A 37 30 26 18 FE DA B7 85 38 23 1A 12 0B 02 F6 E3 CF 83 `  
  
`83 83 83 83 83 83 83 82 82 82 81 82 83 85 8A 8F 91 91 8F 8B 87 84 81 7F 7A 72 6A 68 6E 75 77 76 75 75 76 77 79 7A 7A 79 75 6D 61 5D 76 B3 BF C3 C7 CA CF D7 E4 F2 `  
  
`F1 F1 F1 F1 F1 F1 F1 F1 F2 F5 F8 F9 F7 F1 E0 C5 D6 E7 ED F2 F4 F4 F2 F0 EB E4 DA D2 D3 DE EB F6 FD 01 02 01 FE FA F7 F3 F0 EE ED ED ED EE EE EE EF EF EF F0 F0 F1 `  
  
`F1 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF F7 82 80 7D 79 74 6F 6B 67 64 61 5A 46 22 0E 07 03 01 00 FF FF FF FF 00 00 01 01 01 01 01 01 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 09 7E 80 81 83 84 85 87 8B 8F 96 A1 B9 E0 F5 FD FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 C6 C6 C7 C7 C8 C8 C9 C9 CA CB CC CC CC C9 C5 CD D8 DF E2 E3 E3 E2 E1 E0 DF DF DF DF DF DF DF DF DF DF E0 E0 E0 E1 E1 E0 E0 DF DE DC DA D7 D4 D2 D0 CD CB `  
  
`C9 C7 C6 C6 F5 FC 02 07 0B 0F 11 13 15 18 19 1A 18 13 EC BF B6 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B4 B5 B5 B6 B7 B9 BA BC BF `  
  
`C3 C9 D1 DF EF 3A 33 2D 28 24 20 1E 1C 1A 17 15 14 16 1C 43 71 7A 7C 7D 7D 7D 7D 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7B 7A 79 78 76 74 `  
  
`71 6D 67 5E 51 40 03 06 0A 0D 10 13 16 18 18 18 17 16 16 18 1D 26 2F 34 35 35 34 33 32 32 32 32 32 32 32 32 32 32 32 32 32 32 33 33 33 33 33 32 30 2D 2A 26 21 1D `  
  
`19 14 10 0C 08 04 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF 00 03 07 0B 0E 12 15 17 19 1A 1A 19 19 18 18 17 17 18 18 19 19 1A 19 19 17 15 13 11 0F 0D `  
  
`0C 0B 0A 08 07 05 03 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 02 04 06 08 08 09 0A 0A 0B 0B 0B 0A 0A 0A 0A 0A 0B 0B 0C 0D 0D 0D 0C 0A 07 03 00 FD `  
  
`FC FB FA FA FA FB FC FE 00 DD D9 D6 D4 D3 D3 D4 D5 D7 D7 D7 D7 D6 D5 D4 D1 CE CC CC CC CC CD CE CF D0 D1 D2 D3 D4 D5 D6 D7 D8 D8 D9 D9 D9 D9 D9 D8 D8 D8 D8 D7 D7 `  
  
`D8 D8 D9 D9 DA DB DD DE DF E1 CD C8 C0 B7 AC A2 99 93 90 8F 90 91 92 93 94 96 99 9C A0 A5 A9 AB AC AC AB A9 A6 A2 9F 9B 99 97 95 95 94 93 92 92 92 93 94 95 98 9D `  
  
`A2 A8 AE B4 B8 BD C1 C5 C9 CD D0 3C 42 4A 53 5E 67 6F 75 77 78 78 77 76 75 74 73 70 6C 67 61 5B 56 52 51 50 52 54 57 5B 5E 60 62 64 64 65 66 66 66 66 66 65 64 61 `  
  
`5E 5A 55 51 4C 49 45 42 3F 3C 3A 38 C6 C9 CD D1 D5 D8 DB DE E0 E1 E2 E2 E1 DE D7 CE CB CF D0 D0 CE CD CB C9 C9 CA CB CC CD CE CF CF CE CD CB C8 C5 C2 C2 C5 C7 C9 `  
  
`CA CA CA C9 C8 C7 C7 C6 C6 C5 C5 C5 C5 2B 39 40 44 46 48 49 49 4A 4B 4C 4C 4B 49 42 2C 01 EA E3 DD D9 D4 CF CA C5 C2 C1 C0 C1 C1 C2 C3 C3 C3 C4 C5 C8 D9 2C 37 3A `  
  
`3B 3C 3C 3C 3B 39 37 35 31 2D 26 1F 18 11 A6 97 90 8C 89 88 87 86 85 85 84 84 85 86 8B 9D C6 DA E1 E5 E9 ED F1 F7 FB FE FF FF FF FE FE FD FD FD FC FB F7 E7 94 88 `  
  
`86 85 85 86 88 8A 8D 91 94 99 9F A6 AF B8 C0 03 06 09 0C 0E 11 13 15 16 16 16 16 15 15 15 14 14 15 16 17 18 19 1A 1A 1B 1B 1B 1B 1B 1A 1A 19 1A 1D 24 2F 3B 3A 33 `  
  
`30 2F 2F 2F 2C 2A 2A 2E 34 3C 39 2D 1F 12 07 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FF FE FE FE FE FE FF 00 02 02 02 01 FE F9 F4 EF E6 7E `  
  
`7D 7F 82 84 84 82 7E 7A 75 72 73 E7 E9 EB EF F6 00 00 00 00 00 00 00 00 00 00 01 01 01 01 00 FE FA F7 F4 F4 F3 F2 F2 F2 F3 F3 F4 F4 F4 F5 F6 F7 FA FE 03 07 09 01 `  
  
`96 8E 89 86 85 84 85 87 8B 90 94 9B 12 15 14 11 0A 00 DF DD DA D8 D7 D5 D4 D3 D2 D2 D3 D3 D3 D3 D2 D4 D7 DA DC DE DF E0 E0 E0 DD DA D5 D3 D5 DB E2 E8 ED F0 F2 F3 `  
  
`F3 F2 F1 F0 EE ED EC E9 E6 E4 E1 DF DE DD DD DD DE DF E1 30 2F 2D 2B 29 26 24 21 1F 1E 1D 1E 1F 21 28 31 37 3A 3C 3E 40 42 44 44 44 40 38 28 16 09 03 00 FE FD FD `  
  
`FC FC FC FC FD FD FE FF 02 04 08 0C 11 15 1A 1F 24 29 2D 31 C9 CB CD D0 D2 D5 D8 DB DD DF E1 E0 DF DB D1 C3 B6 B0 AD AA A7 A6 A5 A6 A8 AF BA CD E2 F1 F8 FC FE FF `  
  
`FF FF FF FF FF FF FE FE FD FB F9 F6 F2 ED E8 E3 DD D7 D2 CC C7 00`

  
  
  
Model 5 4th animation data \[at offset 0x0000D6B0\]:

  

`00 00 00 00 77 00 01 02 00 01 02 00 00 C0 00 00 FF FF FF 00 07 03 04 05 FF FF FF 00 07 06 07 08 FF FF FF 00 07 09 0A 0B FF FF FF 00 07 0C 0D 0E FF FF FF 00 07 0F `  
  
`10 11 FF FF FF 00 07 12 13 14 FF FF FF 00 00 00 00 00 FF FF FF 00 07 15 16 17 FF FF FF 00 07 18 19 1A FF FF FF 00 07 1B 1C 1D FF FF FF 00 07 1E 1F 20 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 07 21 22 23 FF FF FF 00 07 24 25 26 FF FF FF 00 07 27 28 29 FF FF FF 00 00 00 51 80 FF FF FF 00 00 C5 11 C0 FF FF `  
  
`FF 00 02 00 2A 00 FF FF FF 00 07 2B 2C 2D FF FF FF 00 FE FF FB FF F8 FF F6 FF F3 FF F2 FF F1 FF F1 FF F2 FF F2 FF F2 FF F2 FF ED FF E8 FF E6 FF E7 FF E9 FF EB FF `  
  
`EE FF F0 FF F4 FF F7 FF FA FF FD FF 00 00 7F FE 80 FE 81 FE 83 FE 84 FE 85 FE 86 FE 86 FE 85 FE 85 FE 85 FE 85 FE 89 FE 90 FE 93 FE 91 FE 8F FE 8C FE 89 FE 86 FE `  
  
`83 FE 81 FE 80 FE 7F FE 7F FE 0F 00 1C 00 29 00 35 00 3F 00 47 00 4A 00 49 00 47 00 44 00 43 00 47 00 58 00 70 00 7A 00 74 00 6B 00 61 00 55 00 48 00 3A 00 2B 00 `  
  
`1D 00 0F 00 02 00 FF FE FE FE FF 00 01 01 01 00 00 00 00 01 00 FF FD FC FC FC FC FC FD FF 00 0A 14 1F 28 31 36 3A 3A 3A 38 37 36 37 38 37 32 2E 28 23 1D 17 11 0B `  
  
`06 00 FF FE FC FB F9 F8 F8 F8 F8 F9 F9 F8 F6 F4 F3 F3 F5 F6 F8 FA FC FD FF FF 00 FD FF 02 05 06 08 08 07 07 06 06 08 0B 07 01 00 FF FF 00 00 FF FF FD FC FA 01 01 `  
  
`00 FF FD FC FA FA F9 F9 FA FC 03 10 15 14 12 10 0E 0B 08 06 03 01 00 FB F5 EF EA E6 E3 E0 DE DC DC DE E3 F5 0F 1C 1D 1C 1A 17 14 0F 0B 07 03 00 07 08 08 08 07 07 `  
  
`06 06 06 06 06 07 03 F4 EB EE F3 F9 FF 05 09 0C 0B 09 06 FE FB F9 F6 F4 F2 F2 F2 F3 F4 F4 F2 EA E3 E2 E1 E1 E2 E4 E8 ED F3 F8 FD 00 FB F6 F1 EC E8 E5 E5 E6 E8 EA `  
  
`E9 E5 D4 BF B6 B8 BC C1 C8 D0 D9 E4 EE F8 00 F8 F8 F8 F8 F8 F8 F8 F6 F5 F5 F6 F8 02 0B 0C 0B 0A 0A 09 07 05 02 FF FB F8 EC ED EE EE EE EE ED ED EE EE EE EE F0 FB `  
  
`03 02 00 FE FB F7 F4 F1 EF ED EB 2D 27 21 1B 16 13 10 0E 0D 0D 0F 13 22 3A 49 4B 4A 48 45 42 3E 3B 37 35 33 DD E1 E5 E8 EB EE EF F1 F1 F1 F0 EE E6 DB D6 D5 D5 D5 `  
  
`D5 D6 D7 D8 D9 DA DA EB EE F2 F4 F6 F7 F8 F9 F9 F9 F9 F7 F2 E8 DE DC DB DB DC DE E0 E2 E4 E5 E6 1B 18 16 14 13 13 13 12 12 12 12 13 15 1D 25 27 28 28 26 25 23 22 `  
  
`20 1F 1E D0 D0 D0 D1 D2 D4 D5 D5 D6 D6 D5 D4 D0 CE D0 D1 D2 D2 D2 D2 D2 D2 D1 D1 D1 35 3F 49 51 57 5B 5E 5F 5F 5E 5D 5B 53 40 34 32 30 2F 2E 2E 2E 2E 2E 2E 2D 0A `  
  
`01 F8 F0 EB E7 E5 E3 E3 E3 E4 E7 F3 0C 1B 1D 1D 1D 1C 1A 18 16 14 13 11 E8 DF D8 D5 D7 D9 DB DC DB DB DA D9 DA DA D9 D7 D6 D5 D7 D9 DD E2 E7 EC F1 05 0E 1B 2C 3B `  
  
`44 47 48 48 46 44 44 45 46 44 3E 35 2B 21 18 11 0B 06 03 00 FD F6 E9 D6 C6 BB B7 B6 B6 B8 BA BB BA B9 BB C3 CC D7 E2 EC F3 F9 FC FF 00 FD 02 08 0C 10 12 14 14 14 `  
  
`14 13 12 0C FD F2 F1 F0 F1 F3 F4 F6 F7 F8 F9 F9 16 15 14 13 10 0F 0D 0B 0A 0A 0B 0F 19 22 24 23 21 20 1E 1D 1B 19 18 16 15 C9 C6 C2 BF BC B9 B7 B4 B2 B2 B4 B9 CB `  
  
`E0 EA EA EA E8 E5 E1 DD D9 D4 D0 CD D8 D6 D4 D3 D2 D1 D1 D1 D1 D1 D1 D1 D1 D1 D1 D2 D2 D3 D4 D5 D6 D7 D8 D9 DA 1D 21 27 2C 31 35 38 38 38 37 36 35 36 37 35 32 2F `  
  
`2C 29 26 23 20 1E 1B 1A DF DB D7 D2 CD CA C8 C7 C8 C8 C9 CA C9 C9 CA CD CF D2 D5 D8 DA DD DF E0 E2 D3 D5 D7 D9 DB DC DD DC DC DB DB DC E4 F5 FF FD FA F6 F1 EB E5 `  
  
`DE D9 D4 D1 D1 D3 D5 D6 D7 D8 D7 D5 D3 D1 D3 D8 EA FA FF FF FD FB F8 F5 F1 EC E5 DB CF F1 EF EE ED ED EC ED EF F1 F2 F1 ED DF D6 D4 D4 D3 D3 D4 D5 D7 DA DF E8 F2 `  
  
`E8 DF D5 CD C5 C0 C3 C4 C4 C3 C1 C0 C1 C3 C6 CA CE D2 D7 DB DF E4 E8 ED F1 00 00 00 00 00 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 D0 DC E7 F1 FA 00 03 04 03 01 00 00 03 08 08 03 FE F7 F1 EA E3 DB D4 CD C6 DE D1 C5 BB B3 AE AA A6 `  
  
`A4 A4 A7 AE C7 ED 03 05 05 04 01 FD F8 F4 F0 EE EF 46 47 48 4A 4B 4C 4D 4D 4D 4D 4C 4C 4C 4C 4B 4A 49 48 48 47 46 46 45 44 40 11 22 34 3B 2D 23 1D 18 16 17 1B 23 `  
  
`3E 1A 02 FC F9 F7 F7 F8 FA FC FE 00 00 00 00 01 7D 7F 7F 7F 7F 7F 7F 7F 7F 7D 00 FF FF FF FF 00 00 00 00 00 00 00 00 00 01 7D 7F 7F 80 80 80 80 80 7F 7D 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 DA D3 CC C6 C3 C6 C8 C8 C8 C7 C6 C6 C8 CD CE CC C9 C7 C8 CA CE D3 D8 DC E1 D0 CF CB BF 8B 6D 69 6A 6D 71 73 6D 52 40 39 32 28 15 FC E9 `  
  
`DE D8 D4 D2 D0 39 3B 3F 4C 80 9E A2 A1 9E 9A 98 9E B9 CB D2 D9 E3 F5 0E 21 2B 31 34 36 38 FE FC FA F8 F6 F5 F4 F4 F4 F4 F4 F5 F4 F4 F5 F5 F6 F8 F9 FA FB FC FE FF `  
  
`00 DF DC DA D7 D5 D4 D3 D3 D3 D3 D4 D4 D3 D2 D2 D4 D5 D6 D8 D9 DB DC DE E0 E1 34 36 39 3C 3D 3F 3F 3F 3F 3F 3F 3F 40 43 43 42 41 3F 3D 3B 39 37 35 33 31 C8 C9 CA `  
  
`CB CB CC CC CD CC CC CC CC CC CD CC CC CB CB CA CA C9 C9 C8 C8 C7`

  
  
  
  
Model 7, Model 8 and Model 9 1st animation data \[at offset
0x0000DC78\]:

  

`00 00 00 00 00 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 00 FA 00 00 FF FF FF 00 00 06 00 00 FF FF FF 00 00 FA E7 37 FF FF FF 00 00 DC EE 16 FF FF FF 00 00 D4 `  
  
`0E 30 FF FF FF 00 00 00 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 F9 19 C9 FF FF FF 00 00 DC 12 EA FF FF FF 00 00 D0 ED D4 FF FF FF 00 00 00 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 B3 80 FF FF FF 00 00 C6 F3 40 FF FF FF 00 00 00 00 00 FF FF FF 00 00 DD CF 39 FF FF FF 00 00 00 4D 80 FF FF FF 00 00 C6 0E C0 FF FF `  
  
`FF 00 00 00 00 00 FF FF FF 00 00 E2 31 C7 FF FF FF 00 64 FE 02 00`

  
  
  
  
Model 7, Model 8, and Model 9 4th animation data \[at offset
0x0000DD30\]:

  

`00 00 00 00 00 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 00 C1 02 FE FF FF FF 00 00 08 00 1D FF FF FF 00 00 D5 BE 72 FF FF FF 00 00 DA E6 1E FF FF FF 00 00 F9 `  
  
`10 10 FF FF FF 00 00 D6 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 00 D5 42 8E FF FF FF 00 00 DA 1A E2 FF FF FF 00 00 00 FC 01 FF FF FF 00 00 E3 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 00 11 B6 83 FF FF FF 00 00 17 00 00 FF FF FF 00 00 E8 E6 2A FF FF FF 00 00 00 51 80 FF FF FF 00 00 27 48 79 FF FF `  
  
`FF 00 00 39 00 00 FF FF FF 00 00 F3 0A DD FF FF FF 00 FD FF 03 00`

  
  
  
  
Model 7, Model 8, and Model 9 5th animation data \[at offset
0x0000DDE8\]:

  

`00 00 00 00 00 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 07 00 01 02 FF FF FF 00 07 03 04 05 FF FF FF 00 07 06 07 08 FF FF FF 00 00 DA E6 1E FF FF FF 00 07 09 `  
  
`0A 0B FF FF FF 00 01 0C 00 00 FF FF FF 00 00 00 00 00 FF FF FF 00 07 0D 0E 0F FF FF FF 00 00 DA 1A E2 FF FF FF 00 07 10 11 12 FF FF FF 00 01 13 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 00 C6 EF 40 FF FF FF 00 00 00 00 00 FF FF FF 00 00 E1 D0 38 FF FF FF 00 00 00 51 80 FF FF FF 00 00 C5 11 C0 FF FF `  
  
`FF 00 00 00 00 00 FF FF FF 00 00 E1 31 C7 FF FF FF 00 7F FE 02 00 FA F9 F9 F9 F8 F8 F8 F7 F7 F7 F7 F6 F6 F6 F5 F5 F5 F5 F5 F4 F4 F4 F4 F4 F4 F4 F4 F4 F4 F4 00 00 `  
  
`00 00 00 00 00 01 01 01 01 01 01 02 02 02 02 03 03 03 03 03 03 03 03 03 03 03 03 03 FF FE FD FC FB FA F9 F8 F7 F6 F5 F4 F3 F1 F1 F0 EF EE ED EC EB EB EB EA EB EB `  
  
`EB EB EB EB 06 07 08 08 09 09 0A 0B 0B 0C 0D 0D 0E 0E 0F 0F 10 10 10 11 11 11 11 11 11 11 11 11 11 11 00 00 01 01 01 01 01 01 01 01 00 00 00 FF FF FF FE FE FD FD `  
  
`FC FC FC FC FC FC FC FC FC FC FF FD FB FA F8 F7 F5 F3 F2 F0 EF ED EB EA E8 E7 E5 E4 E3 E1 E0 DF DF DF DF DF DF E0 E0 E0 F8 F7 F6 F5 F5 F4 F3 F2 F1 F1 F0 EF EE EE `  
  
`ED EC EC EB EB EA EA E9 E9 E9 E9 E9 E9 EA EA EA EB EB EB EB EB EB EB EC EC EC EC EC ED ED ED EE EE EE EF EF EF F0 F0 F0 F0 F0 F0 F0 F0 EF 33 32 31 30 30 2F 2E 2D `  
  
`2D 2C 2B 2A 29 29 28 27 26 25 25 24 23 23 23 23 23 23 23 23 23 23 D3 D4 D6 D7 D9 DB DC DE DF E1 E3 E4 E6 E7 E9 EA EB ED EE EF F0 F1 F2 F2 F2 F1 F1 F1 F0 F0 2E 30 `  
  
`31 32 33 33 34 34 35 35 36 36 36 37 37 37 37 37 38 38 38 38 38 38 38 38 38 38 38 38 10 0F 0D 0C 0B 0A 09 09 08 07 07 06 06 05 05 05 04 04 04 03 03 03 03 03 03 03 `  
  
`03 03 03 03 F0 EE ED EB EA E8 E7 E5 E4 E2 E1 DF DE DC DB DA D8 D7 D6 D5 D4 D3 D3 D3 D3 D3 D3 D3 D4 D4 F9 F9 F9 F9 FA FA FA FA FA FB FB FB FB FC FC FC FC FD FD FD `  
  
`FD FD FD FD FD FD FD FD FD FD 15 15 15 15 15 15 15 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 16 CC CB CA C8 C7 C6 C5 C4 C3 C2 C1 C0 BF BE `  
  
`BD BC BB BA BA B9 B8 B8 B7 B7 B7 B7 B8 B8 B8 B8 D2 D3 D4 D5 D6 D7 D9 DA DB DC DD DE DF E0 E1 E2 E3 E4 E5 E6 E7 E7 E7 E7 E7 E7 E7 E7 E7 E7 D0 D1 D2 D3 D3 D4 D5 D6 `  
  
`D6 D7 D8 D8 D9 D9 DA DA DB DB DB DC DC DC DC DC DC DC DC DC DC DC F2 F1 F0 F0 EF EF EE EE EE EE ED ED ED ED ED ED ED ED EE EE EE EE EE EE EE EE EE EE EE EE EF ED `  
  
`EB E9 E7 E5 E3 E1 DF DD DB D9 D7 D5 D3 D2 D0 CE CD CB CA C9 C8 C8 C8 C8 C9 C9 CA CA`

  
  
  
Model 7, Model 8, and Model 9 6th animation data \[at offset
0x0000E0F8\]:

  

`00 00 00 00 60 00 00 00 FF 00 01 00 00 C0 00 00 FF FF FF 00 07 00 01 02 FF FF FF 00 07 03 04 05 FF FF FF 00 07 06 07 08 FF FF FF 00 00 DA E6 1E FF FF FF 00 07 09 `  
  
`0A 0B FF FF FF 00 07 0C 0D 0E FF FF FF 00 00 00 00 00 FF FF FF 00 07 0F 10 11 FF FF FF 00 00 DA 1A E2 FF FF FF 00 07 12 13 14 FF FF FF 00 01 15 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 07 16 17 18 FF FF FF 00 01 19 00 00 FF FF FF 00 07 1A 1B 1C FF FF FF 00 00 00 51 80 FF FF FF 00 07 1D 1E 1F FF FF `  
  
`FF 00 01 20 00 00 FF FF FF 00 07 21 22 23 FF FF FF 00 4E FE 14 FE D8 FD A0 FD 74 FD 5C FD 5F FD 76 FD 96 FD BF FD EE FD 23 FE 5D FE 9A FE DA FE 1C FF 5D FF 9E FF `  
  
`DD FF A0 FF 45 FF F3 FE D1 FE FA FE 54 FF B7 FF FD FF 10 00 06 00 FD FF 8E 00 20 01 B3 01 43 02 CB 02 48 03 B3 03 0F 04 63 04 B0 04 F8 04 3B 05 7D 05 BF 05 02 06 `  
  
`47 06 92 06 E2 06 3B 07 77 07 C4 07 1E 08 7C 08 E9 08 65 09 DA 09 31 0A 52 0A 4D 0A 47 0A FC FE 00 02 04 05 06 07 07 07 07 07 07 07 07 06 06 06 06 05 04 02 FE F8 `  
  
`EF E6 DC D4 CB C1 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 02 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 FE 0A 0F 13 18 1C 1F 21 22 23 23 24 24 23 23 23 22 22 21 21 1A 10 06 FE F8 F3 F0 F0 F5 FF 08 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 01 01 00 FD FC 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FF FE FD 00 08 12 1D FA FC FE FF 01 02 `  
  
`03 03 04 04 04 04 04 04 03 03 03 03 03 02 01 00 FC F6 EF E7 E0 DA D6 D5 EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB E9 E6 E1 DA CE BE `  
  
`32 31 30 2F 2F 2E 2D 2D 2D 2D 2D 2D 2D 2D 2D 2D 2D 2D 2D 2E 2E 2F 31 34 39 3F 47 51 60 72 DA E4 ED F6 FD 03 07 0A 0D 0E 10 11 12 12 13 14 15 16 17 17 16 14 10 0A `  
  
`01 F8 F2 F1 F5 F9 2F 2F 2E 2D 2B 29 28 26 25 25 24 24 24 24 24 24 24 23 23 23 24 24 26 28 2A 29 26 20 18 10 0E 0B 08 05 02 FE FB F9 F7 F5 F4 F3 F2 F2 F1 F1 F0 EF `  
  
`EE EF F0 F1 F4 FA 00 05 0A 0E 0F 10 F2 F2 F3 F4 F4 F3 F1 EE EB E7 E4 DF DB D7 D2 CD C8 C3 C2 C3 C3 C2 C2 C3 C4 C4 C2 C4 CD D6 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 00 00 00 FA FC FE FF 01 02 `  
  
`03 03 04 04 04 04 04 04 04 03 03 03 03 02 01 00 FC F6 EF E7 E0 DA D6 D5 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 17 1A 1F 27 33 42 `  
  
`CE CF D0 D0 D1 D2 D2 D3 D3 D3 D3 D3 D3 D3 D3 D3 D3 D3 D2 D2 D2 D1 CF CB C7 C1 B9 AF A0 8E D8 DF E6 ED F3 F8 FC FF 01 03 05 07 08 0A 0B 0C 0E 10 12 0E 0A 05 01 00 `  
  
`00 00 00 00 00 00 D0 D1 D2 D3 D5 D6 D7 D8 D8 D8 D9 D9 D9 D9 D9 D9 D9 D9 D9 D8 D6 D5 D7 DC E5 ED F4 F8 FA FC F3 F4 F5 F7 F9 FB FD FF 01 02 04 05 06 07 07 08 09 0A `  
  
`0C 09 06 03 01 00 00 01 01 01 01 01 F1 F2 F2 F2 F2 F2 F1 F0 F0 EF EE ED EB EA E9 E8 E6 E5 E3 E3 E3 E3 E3 E3 E3 E3 E3 E3 E3 E3 CB D4 DE E8 F1 F8 FD 00 03 04 05 05 `  
  
`05 05 05 05 05 05 06 09 0D 12 15 17 19 1B 1B 19 15 11 C6 BC B8 B6 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B5 B6 B6 B6 B6 B6 B7 B6 B6 B6 6A 75 7A 7C 7E 7F `  
  
`80 80 80 81 81 81 81 81 81 81 81 81 81 81 82 83 83 84 84 85 85 84 83 83 00 00 00 00 00 00 00 00 01 01 01 02 02 03 03 04 05 05 06 09 0F 14 17 18 18 18 17 17 17 17 `  
  
`E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E0 E0 E1 E2 E5 E8 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 D0 CF `  
  
`CE CE D0 D6 DE E6 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 38 39 39 38 34 2E 2A CF DF EF FE 0C 17 1E 22 25 26 27 26 25 24 22 21 1F 1E `  
  
`1E 20 22 25 28 2C 30 34 36 33 2D 27 43 49 4B 4C 4C 4B 4A 49 49 48 48 48 48 49 49 49 4A 4A 4A 4A 49 49 48 46 43 3E 3B 40 45 48 8D 86 82 80 7E 7D 7B 7A 79 79 79 79 `  
  
`79 7A 7A 7B 7B 7B 7B 7B 7A 79 78 76 73 6E 6B 70 75 79 05 0A 10 15 19 1D 20 21 22 22 22 22 22 21 21 20 20 20 20 22 24 27 29 29 29 28 29 2D 33 39 E1 E1 E1 E1 E1 E1 `  
  
`E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E0 E0 E1 E4 EB F3 34 37 3A 3E 40 43 44 45 45 46 46 46 45 45 45 45 44 44 44 44 44 44 44 46 49 4A 44 33 1D 0A `  
  
`C5 C3 C1 BF BD BB BA B9 B9 B9 B9 B9 B9 B9 B9 BA BA BA BA BA BA BA BA B9 B6 B6 BA C5 D3 DD`

  
  
  
Model 7, Model 8, and Model 9 7th animation data \[at offset
0x0000E65C\]:

  

`00 00 00 00 00 F1 7D 7D 00 01 02 00 00 C0 00 00 FF FF FF 00 00 30 00 00 FF FF FF 00 00 0D 00 00 FF FF FF 00 00 25 DB 0F FF FF FF 00 00 DA E6 1E FF FF FF 00 00 02 `  
  
`04 EF FF FF FF 00 00 C9 80 80 FF FF FF 00 00 00 00 00 FF FF FF 00 00 25 25 F1 FF FF FF 00 00 DA 1A E2 FF FF FF 00 00 07 0B 69 FF FF FF 00 00 0B 00 00 FF FF FF 00 `  
  
`00 00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 00 E1 B8 7A FF FF FF 00 00 2B 00 00 FF FF FF 00 00 F0 F3 23 FF FF FF 00 00 00 51 80 FF FF FF 00 00 CD 3F 91 FF FF `  
  
`FF 00 00 F8 00 00 FF FF FF 00 00 F8 04 DF FF FF FF 00 EA FF 7D FF C5 FF 00 00 00`

  
  
  
  
Model 7, Model 8, and Model 9 8th animation data \[at offset
0x0000E718\]:

  

`00 00 00 77 00 01 02 00 01 02 00 00 C0 00 00 FF FF FF 00 01 03 00 00 FF FF FF 00 01 04 00 00 FF FF FF 00 07 05 06 07 FF FF FF 00 00 DA E6 1E FF FF FF 00 07 08 09 `  
  
`0A FF FF FF 00 07 0B 0C 0D FF FF FF 00 00 00 00 00 FF FF FF 00 07 0E 0F 10 FF FF FF 00 00 DA 1A E2 FF FF FF 00 07 11 12 13 FF FF FF 00 01 14 00 00 FF FF FF 00 00 `  
  
`00 00 00 FF FF FF 00 00 00 AF 80 FF FF FF 00 07 15 16 17 FF FF FF 00 01 18 00 00 FF FF FF 00 07 19 1A 1B FF FF FF 00 00 00 51 80 FF FF FF 00 07 1C 1D 1E FF FF FF `  
  
`00 01 1F 00 00 FF FF FF 00 07 20 21 22 FF FF FF 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 00 E7 FF 00 00 00 00 00 00 00 00 01 00 03 00 03 00 00 00 F7 FF EB FF DF FF D9 FF D8 FF D7 FF D6 FF D5 FF D5 FF D5 FF D5 FF D5 FF D5 FF D6 `  
  
`FF D6 FF D7 FF D7 FF D8 FF D8 FF D9 FF D9 FF D9 FF D9 FF 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 7F FE 48 FE 17 FE EE FD CB FD AE FD 98 FD 87 `  
  
`FD 7B FD 74 FD 71 FD 9E FD E6 FD DA FD F1 FD 52 FE CA FE 26 FF 55 FF 66 FF 62 FF 5C FF 65 FF 79 FF 8F FF 9A FF 9C FF 9D FF 9F FF 9F FF A0 FF A0 FF A0 FF A0 FF 9F `  
  
`FF 9F FF 9E FF 9E FF 9D FF 9C FF 9B FF 9B FF 9A FF 9A FF 9A FF 02 00 02 00 03 00 03 00 03 00 03 00 03 00 03 00 03 00 03 00 02 00 CD FF 9B FF 6D FF 42 FF 19 FF F4 `  
  
`FE D2 FE B1 FE 93 FE 76 FE B9 FD 25 FD BA FC 59 FC FA FB A5 FB 66 FB 3F FB 2A FB 1C FB 0C FB F4 FA D9 FA C2 FA B6 FA B3 FA B0 FA AE FA AD FA AC FA AC FA AC FA AC `  
  
`FA AD FA AE FA AF FA B0 FA B1 FA B3 FA B4 FA B5 FA B6 FA B6 FA B6 FA 00 00 00 00 00 00 00 00 00 00 00 06 0B 11 16 1C 22 27 2D 32 38 3E 39 28 30 29 22 1A 12 09 00 `  
  
`FA F6 F3 F2 F1 F1 F1 F0 F0 F0 F0 F0 F0 F0 F0 F1 F1 F1 F1 F1 F1 F1 F1 F1 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 54 80 80 80 80 80 80 `  
  
`80 80 7F 7E 7D 7D 7D 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7D 7D 7D 7D 7D 7D 7D 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 54 80 80 80 80 80 `  
  
`80 80 80 7F 7E 7D 7D 7D 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7C 7D 7D 7D 7D 7D 7D 7D FB FB FC FD FD FE FF FF 00 01 01 03 06 08 0A 0C 0E 11 13 15 17 17 17 1B 20 28 31 37 `  
  
`39 39 38 37 36 34 31 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 05 04 03 02 01 00 00 FF FE FD FC 00 03 07 0B 0F 12 16 1A 1D 21 21 21 1F 21 29 33 `  
  
`3B 3E 3F 3F 3B 31 22 14 0D 0B 0A 09 08 08 08 08 08 08 09 09 0A 0B 0B 0C 0C 0D 0D 0D F9 FA FA FB FB FC FC FD FE FE FF 01 03 04 06 08 0A 0C 0E 10 11 11 11 15 19 20 `  
  
`25 29 29 29 29 29 28 27 26 25 25 25 25 24 24 24 24 24 24 24 25 25 25 25 25 25 25 25 25 EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EB EA EA EA E9 E9 E9 E8 E6 `  
  
`E1 DA D3 D0 D0 D1 D3 D5 D8 DA DB DB DB DC DC DC DC DC DC DC DC DB DB DB DB DB DB DB DB DB 33 33 32 32 32 31 31 31 30 30 30 2F 2E 2D 2B 2A 29 28 27 26 25 25 25 22 `  
  
`1E 18 0E 05 02 02 03 05 07 0B 0D 0F 0F 0F 10 10 10 10 10 10 10 10 10 0F 0F 0F 0F 0F 0F 0F 0F D3 D5 D7 D9 DB DD DF E1 E3 E5 E7 EB EF F4 F8 FC 01 05 09 0D 11 11 11 `  
  
`11 11 11 11 11 11 11 11 11 0F 0B 05 02 01 00 00 FF FF FF FF FF FF 00 00 00 01 01 01 01 02 02 02 2F 30 32 33 33 34 35 35 36 36 37 37 38 38 38 38 38 38 38 38 38 38 `  
  
`38 38 38 38 38 38 39 3B 3C 38 2B 1A 0B 04 02 00 FF FF FE FE FE FE FF FF 00 00 01 02 02 03 03 04 04 0F 0E 0C 0B 0A 09 08 07 07 06 06 04 03 02 02 01 00 FF FE FD FD `  
  
`FD FD FD FD FD FD FD FD FE FE FD F8 F2 F0 EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF EF ED EA E8 E6 E4 E1 DF DD DB D9 D9 D9 D9 D9 D9 D9 D9 D9 D9 `  
  
`D9 D9 D9 D4 CE C6 C3 C9 CB CA C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 C9 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 `  
  
`00 00 00 00 00 00 00 00 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 80 F9 FA FA FB FB FC FD FD FE FE FF 01 03 05 06 08 0A `  
  
`0C 0E 10 11 11 11 15 19 20 26 29 29 2A 29 29 28 27 26 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 25 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 15 `  
  
`15 16 16 16 17 17 17 18 1A 1E 26 2D 30 30 2F 2D 2B 28 26 25 25 25 24 24 24 24 24 24 24 24 24 24 25 25 25 25 25 25 25 CD CD CE CE CE CF CF CF D0 D0 D0 D1 D2 D3 D4 `  
  
`D6 D7 D8 D9 DA DB DB DB DE E2 E8 F2 FB FE FE FD FB F9 F5 F2 F1 F1 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F1 F1 F1 F1 F1 F1 F1 CC C8 C6 C7 CB CF D3 D8 DD E2 E6 EB F0 F6 `  
  
`FB 00 05 0A 0E 13 18 18 18 00 F3 FB 05 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 07 D4 E0 F9 18 28 2F 33 36 37 38 39 39 3A `  
  
`3A 3A 3A 3A 3A 3A 3A 39 39 39 2F 22 1A 12 0B 09 09 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B ED E1 C7 A8 97 90 8B 89 87 85 84 83 `  
  
`82 82 81 80 7F 7F 7E 7D 7C 7C 7C 80 8C 87 77 69 66 66 68 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 69 EF EE EC EA E8 E7 E5 E3 E1 E0 DE `  
  
`E3 E7 EC F0 F5 FA FE 02 07 0B 0B 0B FC F1 F7 03 0B 0D 0D 0C 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B 0B C6 C6 C6 C6 C6 C6 C6 C6 C6 C6 `  
  
`C6 C6 C6 C6 C7 C7 C8 C8 C9 C9 CA CA CA CB CA C7 C6 C8 C8 C8 C7 C8 CD D5 DD E1 E2 E3 E4 E4 E5 E5 E5 E5 E4 E4 E4 E3 E3 E3 E2 E2 E2 E1 E1 EF EF EF EF EF EF EF EF EF `  
  
`EF EF F5 FA FF 04 08 0C 0F 11 13 15 15 15 17 15 06 E5 D3 D2 D6 DA D3 C4 BC B9 B8 B8 B7 B7 B7 B7 B7 B7 B7 B7 B7 B7 B7 B7 B8 B8 B8 B8 B8 B8 40 40 40 40 40 40 40 40 `  
  
`40 40 40 3A 35 30 2B 27 23 20 1D 1B 19 19 19 18 19 29 4A 5C 5E 59 55 5C 6C 75 79 7A 7A 7B 7B 7B 7B 7B 7B 7B 7B 7B 7B 7B 7A 7A 7A 7A 7A 7A 7A 00 00 00 00 00 00 00 `  
  
`00 00 00 00 02 04 05 07 09 0B 0D 0E 10 12 12 12 14 19 1F 26 2B 2D 2D 2C 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B 2B E1 E1 E1 E1 E1 E1 `  
  
`E1 E1 E1 E1 E1 E2 E4 E5 E7 E8 EA EB ED EE F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 F0 D0 D0 D0 D0 D0 `  
  
`D0 D0 D0 D0 D0 D0 D4 D8 DC E0 E3 E7 EA ED F0 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 F3 38 38 38 38 `  
  
`38 38 38 38 38 38 38 35 32 30 2E 2C 2A 28 27 25 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 23 C5 C5 C5 `  
  
`C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C5 C6 C8 CB CD CD CD CE CE CE CE CE CE CE CE CD CD CD CD CD CD CD CD CD 11 11 `  
  
`11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 11 0F 0B 0B 11 23 34 3D 3F 40 40 41 41 41 41 41 41 41 41 41 40 40 40 40 40 40 3F 3F C0 `  
  
`C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C0 C2 C6 C6 C0 AE 9C 94 91 90 90 8F 8F 8F 8F 8F 8F 8F 8F 90 90 90 90 90 90 91 91 91 `  
  
`00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 FD FA F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 `  
  
`F8 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E1 E3 E6 E8 EB ED F0 F2 F4 F6 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 F8 `  
  
`F8 F8 31 31 31 31 31 31 31 31 31 31 31 2B 26 20 1C 17 13 0F 0B 07 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 04 `  
  
`04 04 04 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 C7 CB CE D0 D3 D5 D7 D9 DB DD DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF DF `  
  
`DF DF DF DF 00`

  
  
  
Note: Animation Data Section runs directly into Models Section.

  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
  
**'Models Section**' \[at offset 0x0000F09C\]

  
***'Models Section', Header***

  

`9C F0 00 80 0A 00 00 00 80 16 00 00 E0 37 03 00`

  
Breakdown:

9C F0 00 80 - Possibly memory address to load section to in PSX
(little-endian, so 0x8000F09C) \[contiguous with other data loaded from
this file? F09C is also

the block offset for this data...\]

0A 00 00 00 - Number of models (little-endian, so 0x0A; 10 models)

80 16 00 00 - "Pointer to texture data" (little-endian, so 0x00001680)

E0 37 03 00 - "Pointer to something. We copy enviroment settings for
models to where it points."

  
  
Note: 'Models Section', Header runs until 'Models Section', Individual
Model Data.

  
  
  
***'Models Section', Individual Model Data***

  
  
  
Model 0 (Cloud) Model Data - \[at offset 0x0000F0AC\]

  

`00 01 00 02 E0 01 00 00 57 54 55 00 AD FF CE F7 CD 0D FF FF 93 90 91 00 00 06 75 F6 A2 F4 FF FF 6C 67 67 00 76 F4 49 FA 67 F6 03 03 4D 4D 4D 01`

  
Breakdown:

00 01 - Model ID (Cloud) \[actually, 01 is the body, and 00 is the
face\]

00 02 - "Scale; 12 bit fixed point"

E0 01 00 00 - Relative offset to skeleton of model \[parts, bones, and
animations\] (little endian, so 0x000001E0)

57 54 55 - RGB for something, respectively \[R==57; G==54; B==55\]

00 AD FF CE F7 CD 0D - Unknown

FF - "Start index of bones"

FF - Unknown

93 90 91 - RGB1 for something, respectively \[R1==93; G1==90; B1==91\]

00 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\] (Cloud has no extra bones in this
field)

00 06 75 F6 A2 F4 - Unknown

FF - "Start index of parts"

FF - Unknown

6C 67 67 - RGB2 for something, respectively \[R2==6C; G2==67; B2==67\]

00 - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\] (Cloud has no extra parts in this
field)

76 F4 49 FA 67 F6 - Unknown

03 - "Start index of animations"

03 - Unknown

4D 4D 4D - RGB3 for something, respectively \[R3==4D; G3==4D; B3==4D\]

01 - Additional number of animations \[not counting anything in BCX, if
applicable\] (Cloud has one extra animation in this field)

  
  
  
Model 1 (Barret) model data - \[at offset 0x0000F0DC\]

  

`02 03 00 02 C0 01 00 00 57 54 55 00 AD FF CE F7 CD 0D FF FF 93 90 91 00 00 06 75 F6 A2 F4 FF FF 6C 67 67 00 76 F4 49 FA 67 F6 03 03 4D 4D 4D 01`

  
  
Breakdown:

02 03 - Model ID (Barret) \[actually, 03 is the body, and 02 is the
face\]

00 02 - "Scale; 12 bit fixed point"

C0 01 00 00 - Relative offset to skeleton of model \[parts, bones, and
animations\] (little endian, so 0x000001C0)

57 54 55 - RGB for something, respectively \[R==57; G==54; B==55\]

00 AD FF CE F7 CD 0D - Unknown

FF - "Start index of bones"

FF - Unknown

93 90 91 - RGB1 for something, respectively \[R1==93; G1==90; B1==91\]

00 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\] (Barret has no extra bones in this
field)

00 06 75 F6 A2 F4 - Unknown

FF - "Start index of parts"

FF - Unknown

6C 67 67 - RGB2 for something, respectively \[R2==6C; G2==67; B2==67\]

00 - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\] (Barret has no extra parts in this
field)

76 F4 49 FA 67 F6 - Unknown

03 - "Start index of animations"

03 - Unknown

4D 4D 4D - RGB3 for something, respectively \[R3==4D; G3==4D; B3==4D\]

01 - Additional number of animations \[not counting anything in BCX, if
applicable\] (Barret has one extra animation in this field)

  
  
  
Model 2 model data \[at offset 0x0000F10C\]

  

`11 00 00 02 A0 01 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 02 4D 4D 4D 03`

  
Breakdown:

11 00 - Model ID (little-endian, so 0x0011) \[actually, 00 is the body,
and 11 is the face\]

00 02 - "Scale; 12 bit fixed point"

A0 01 00 00 - Relative offset to skeleton of model \[parts, bones, and
animations\] (little endian, so 0x000001A0)

57 54 55 - RGB for something, respectively \[R==57; G==54; B==55\]

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively \[R1==93; G1==90; B1==91\]

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\] (Model ID 2 has 0x16, or 22 bones in
this field)

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively \[R2==6C; G2==67; B2==67\]

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\] (Model ID 2 has 0x0F, or 15 parts in
this field)

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

02 - Unknown

4D 4D 4D - RGB3 for something, respectively \[R3==4D; G3==4D; B3==4D\]

03 - Additional number of animations \[not counting anything in BCX, if
applicable\] (Model 2 has 3 animation in this field)

  
  
  
Model 3 model data \[at offset 0x0000F13C\]

  

`11 00 00 02 D8 03 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 02 4D 4D 4D 03`

  
  
Breakdown:

11 00 - Model ID (little-endian, so 0x0011)

00 02 - "Scale; 12 bit fixed point"

D8 03 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little-endian, so 0x000003D8)

57 54 55 - RGB for something, respectively \[R==57; G==54; B==55\]

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

02 - Unknown

4D 4D 4D - RGB3 for something, respectively

03 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
Model 4 model data \[at offset 0x0000F16C\]

  

`0D 00 00 02 10 06 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 04 4D 4D 4D 05`

  
  
Breakdown:

0D 00 - Model ID (little-endian, so 0x000D)

00 02 - "Scale; 12 bit fixed point"

10 06 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00000610)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

04 - Unknown

4D 4D 4D - RGB3 for something, respectively

05 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
  
Model 5 model data \[at offset 0x0000F19C\]

  

`0C 00 00 02 68 08 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 03 4D 4D 4D 04`

  
  
Breakdown:

0C 00 - Model ID (little-endian, so 0x000C)

00 02 - "Scale; 12 bit fixed point"

68 08 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00000868)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

03 - Unknown

4D 4D 4D - RGB3 for something, respectively

04 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
Model 6 model data \[at offset 0x0000F1CC\]

  

`12 00 00 02 B0 0A 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 03 4D 4D 4D 04`

  
  
Breakdown:

12 00 - Model ID (little-endian, so 0x0012)

00 02 - "Scale; 12 bit fixed point"

B0 0A 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00000AB0)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

03 - Unknown

4D 4D 4D - RGB3 for something, respectively

04 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
  
Model 7 model data \[at offset 0x0000F1FC\]

  

`1D 00 00 02 F8 0C 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 07 4D 4D 4D 08`

  
  
  
Breakdown:

1D 00 - Model ID (little-endian, so 0x001D)

00 02 - "Scale; 12 bit fixed point"

F8 0C 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00000CF8)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

07 - Unknown

4D 4D 4D - RGB3 for something, respectively

08 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
Model 8 model data \[at offset 0x0000F2CC\]

  

`1D 00 00 02 80 0F 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 07 4D 4D 4D 08`

  
  
  
Breakdown:

1D 00 - Model ID (little-endian, so 0x001D)

00 02 - "Scale; 12 bit fixed point"

80 0F 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00000F80)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

07 - Unknown

4D 4D 4D - RGB3 for something, respectively

08 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
Model 9 model data \[at offset 0x0000F25C\]

  

`1D 00 00 02 08 12 00 00 57 54 55 00 AD FF CE F7 CD 0D 00 15 93 90 91 16 00 06 75 F6 A2 F4 00 0E 6C 67 67 0F 76 F4 49 FA 67 F6 00 07 4D 4D 4D 08`

  
  
  
Breakdown:

1D 00 - Model ID (little-endian, so 0x001D)

00 02 - "Scale; 12 bit fixed point"

08 12 00 00 - Relative offset to skeleton of model
\[parts/bones/animations\] (little endian, so 0x00001208)

57 54 55 - RGB for something, respectively

00 AD FF CE F7 CD 0D - Unknown

00 - "Start index of bones"

15 - Unknown

93 90 91 - RGB1 for something, respectively

16 - Additional number of bones in the model's skeleton \[not counting
anything in BCX, if applicable\]

00 06 75 F6 A2 F4 - Unknown

00 - "Start index of parts"

0E - Unknown

6C 67 67 - RGB2 for something, respectively

0F - Additional number of parts in the model's skeleton \[not counting
anything in BCX, if applicable\]

76 F4 49 FA 67 F6 - Unknown

00 - "Start index of animations"

07 - Unknown

4D 4D 4D - RGB3 for something, respectively

08 - Additional number of animations \[not counting anything in BCX, if
applicable\]

  
  
  
  
  
***Individual Bones/Parts/Animations Data*** \[at offset 0x0000F28C\]

  
  
Model 0 (Cloud) animation data (no parts/bones data for Cloud) - \[at
offset 0x0000F28C\]

  

`50 00 16 03 00 35 B4 00 94 02 94 02 FC 98 00 80`

  
Breakdown:

50 00 - Number of frames (little-endian, so 0x0050)

16 - Number of bones

03 - Number of translation frames

00 - Number of static translation frames

35 - Number of rotation frames

B4 00 - Relative offset to translation frames (little-endian, so 0x00B4)

94 02 - Relative offset to static translation frames (little-endian, so
0x0294)

94 02 - Relative offset to rotation frames (little-endian, so 0x0294)

FC 98 00 80 - Offset to animation data section (little-endian, so
0x800098FC)

  
  
Model 1 (Barret) animation data (no parts/bones data for Barret) - \[at
offset 0x0000F29C\]:

  

`31 00 16 01 00 30 B4 00 16 01 16 01 20 AC 00 80`

  
Breakdown:

31 00 - Number of frames (little-endian, so 0x0031)

16 - Number of bones

01 - Number of translation frames

00 - Number of static translation frames

30 - Number of rotation frames

B4 00 - Relative offset to translation frames (little-endian, so 0x00B4)

16 01 - Relative offset to static translation frames (little-endian, so
0x0116)

16 01 - Relative offset to rotation frames (little-endian, so 0x0116)

20 AC 00 80 - Offset to animation data section (little-endian, so
0x8000AC20)

  
  
Model 2 bones data \[at offset 0x0000F2AC\] (22 bones):

`00 00 FF 00`  
`00 00 00 01`  
`9C FF 01 01`  
`5A FF 02 01`  
`9C FF 01 00`  
`73 FF 04 00`  
`97 FF 05 01`  
`A3 FF 06 01`  
`83 FF 07 01`  
`9C FF 01 00 `  
`73 FF 09 00`  
`97 FF 0A 01`  
`A3 FF 0B 01`  
`83 FF 0C 01`  
`00 00 00 00`  
`C3 FF 0E 01`  
`14 FF 0F 01`  
`A4 FF 10 01`  
`00 00 00 00`  
`C3 FF 12 01`  
`14 FF 13 01`  
`A4 FF 14 01`

  
No breakdown at the moment; all bone data above is unknown.

  
  
Model 2 parts data \[at offset 0x0000F304\] (15 parts):

  

`01 01 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 08 00 00 80 00 00 00 00`  
`01 02 25 00 00 00 00 00 00 00 0A 1E 00 00 2C 01 24 04 24 04 24 04 50 05 4C 01 00 80 00 00 00 00`  
`01 03 4B 04 00 02 00 00 00 00 24 37 01 02 5C 02 14 09 10 09 1C 09 FC 0B 70 05 00 80 00 00 00 00`  
`01 06 10 00 00 00 00 00 00 00 0A 09 00 00 84 00 D8 01 D8 01 D8 01 5C 02 90 0E 00 80 00 00 00 00`  
`01 07 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 68 10 00 80 00 00 00 00`  
`01 08 09 00 00 00 00 00 00 00 04 05 00 00 4C 00 F0 00 F0 00 F0 00 24 01 94 11 00 80 00 00 00 00`  
`01 0B 10 00 00 00 00 00 00 00 0A 09 00 00 84 00 D8 01 D8 01 D8 01 5C 02 84 12 00 80 00 00 00 00`  
`01 0C 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 5C 14 00 80 00 00 00 00`  
`01 0D 09 00 00 00 00 00 00 00 04 05 00 00 4C 00 F0 00 F0 00 F0 00 24 01 88 15 00 80 00 00 00 00`  
`01 0F 0C 00 00 00 00 00 00 00 0A 05 00 00 64 00 68 01 68 01 68 01 CC 01 78 16 00 80 00 00 00 00`  
`01 10 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 E0 17 00 80 00 00 00 00`  
`01 11 0E 00 00 00 00 00 00 00 0A 07 00 00 74 00 A0 01 A0 01 A0 01 14 02 9C 18 00 80 00 00 00 00`  
`01 13 0C 00 00 00 00 00 00 00 0A 05 00 00 64 00 68 01 68 01 68 01 CC 01 3C 1A 00 80 00 00 00 00`  
`01 14 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 A4 1B 00 80 00 00 00 00`  
`01 15 0E 00 00 00 00 00 00 00 0A 07 00 00 74 00 A0 01 A0 01 A0 01 14 02 60 1C 00 80 00 00 00 00`

  
Breakdown of first line of Model 2's parts above:

01 - Unknown; "0 - not calculate stage lighting and color. 1 -
calculate."

01 - Bone to which this part is attached to

0C - Number of vertices

00 - Number of Texture coord

00 - number of textured quads (Gourad Shading)

00 - number of textured triangles (Gourad Shading)

00 - number of textured quads (Flat Shading)

00 - number of textured triangles (Flat Shading)

00 - number of monochrome triangles

00 - number of monochrome quads

04 - number of gradated triangles

08 - number of gradated quads

00 00 - number of data in block 4 (flags)

64 00 - Relative offset to ?

44 01 - Relative offset to ?

44 01 - Relative offset to texture settings. Indexed by 5th block data
(control)

44 01 - Relative offset to one byte stream for every packet with texture

90 01 - Relative offset to ?

08 00 00 80 - Offset to skeleton data section

00 00 00 00 - Offset to ?

  
  
  
Model 2 animation data \[at offset 0x0000F4E4\] (3 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 68 B6 00 80`  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80`  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80`

  
  
Breakdown of 1st animation (first line) at top of group of animations
above:

01 00 - Number of frames (little-endian, so 0x0001)

16 - Number of bones

00 - Number of translation frames

02 - Number of static translation frames

00 - Number of rotation frames

B4 00 - Relative offset to translation frames (little-endian, so 0x00B4)

B4 00 - Relative offset to static translation frames (little-endian, so
0x00B4)

B8 00 - Relative offset to rotation frames (little-endian, so 0x00B8)

68 B6 00 80 - Offset to animation data section (little-endian, so
0x8000B668)

  
  
  
  
Model 3 bones data \[at offset 0x0000F514\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`9C FF 01 01 `  
`5A FF 02 01 `  
`9C FF 01 00 `  
`73 FF 04 00 `  
`97 FF 05 01 `  
`A3 FF 06 01 `  
`83 FF 07 01 `  
`9C FF 01 00 `  
`73 FF 09 00 `  
`97 FF 0A 01 `  
`A3 FF 0B 01 `  
`83 FF 0C 01 `  
`00 00 00 00 `  
`C3 FF 0E 01 `  
`14 FF 0F 01 `  
`A4 FF 10 01 `  
`00 00 00 00 `  
`C3 FF 12 01 `  
`14 FF 13 01 `  
`A4 FF 14 01 `

  
  
  
Model 3 parts data \[at offset 0x0000F56C\] (15 parts):

Note: In this case, Model 3 shares skeleton data with Model 2 (see
offsets below).

  

`01 01 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 08 00 00 80 00 00 00 00 `  
`01 02 25 00 00 00 00 00 00 00 0A 1E 00 00 2C 01 24 04 24 04 24 04 50 05 4C 01 00 80 00 00 00 00 `  
`01 03 4B 04 00 02 00 00 00 00 24 37 01 02 5C 02 14 09 10 09 1C 09 FC 0B 70 05 00 80 00 00 00 00 `  
`01 06 10 00 00 00 00 00 00 00 0A 09 00 00 84 00 D8 01 D8 01 D8 01 5C 02 90 0E 00 80 00 00 00 00 `  
`01 07 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 68 10 00 80 00 00 00 00 `  
`01 08 09 00 00 00 00 00 00 00 04 05 00 00 4C 00 F0 00 F0 00 F0 00 24 01 94 11 00 80 00 00 00 00 `  
`01 0B 10 00 00 00 00 00 00 00 0A 09 00 00 84 00 D8 01 D8 01 D8 01 5C 02 84 12 00 80 00 00 00 00 `  
`01 0C 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 5C 14 00 80 00 00 00 00 `  
`01 0D 09 00 00 00 00 00 00 00 04 05 00 00 4C 00 F0 00 F0 00 F0 00 24 01 88 15 00 80 00 00 00 00 `  
`01 0F 0C 00 00 00 00 00 00 00 0A 05 00 00 64 00 68 01 68 01 68 01 CC 01 78 16 00 80 00 00 00 00 `  
`01 10 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 E0 17 00 80 00 00 00 00 `  
`01 11 0E 00 00 00 00 00 00 00 0A 07 00 00 74 00 A0 01 A0 01 A0 01 14 02 9C 18 00 80 00 00 00 00 `  
`01 13 0C 00 00 00 00 00 00 00 0A 05 00 00 64 00 68 01 68 01 68 01 CC 01 3C 1A 00 80 00 00 00 00 `  
`01 14 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 A4 1B 00 80 00 00 00 00 `  
`01 15 0E 00 00 00 00 00 00 00 0A 07 00 00 74 00 A0 01 A0 01 A0 01 14 02 60 1C 00 80 00 00 00 00`

  
  
  
  
Model 3 animations data \[at offset 0x0000F74C\] (3 animations):

Note: In this case, Model 3 shares animation data with Model 2 (see
offsets below).

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 68 B6 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80`

  
  
  
  
Model 4 bones data \[at offset 0x0000F77C\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`CA FF 01 01 `  
`51 FF 02 01 `  
`CA FF 01 00 `  
`6D FF 04 00 `  
`BA FF 05 01 `  
`A9 FF 06 01 `  
`7E FF 07 01 `  
`CA FF 01 00 `  
`6D FF 09 00 `  
`BA FF 0A 01 `  
`A9 FF 0B 01 `  
`7E FF 0C 01 `  
`00 00 00 00 `  
`D0 FF 0E 01 `  
`5E FF 0F 01 `  
`44 FF 10 01 `  
`00 00 00 00 `  
`D0 FF 12 01 `  
`5E FF 13 01 `  
`44 FF 14 01`

  
  
  
Model 4 parts data \[at offset 0x0000F7D4\] (15 parts):

  

`01 01 0E 00 00 00 00 00 00 00 04 0A 00 00 74 00 7C 01 7C 01 7C 01 D8 01 00 1E 00 80 00 00 00 00 `  
`01 02 1A 00 00 00 00 00 00 00 06 15 00 00 D4 00 D8 02 D8 02 D8 02 9C 03 7C 1F 00 80 00 00 00 00 `  
`01 03 46 0C 02 02 00 00 00 00 4E 18 03 04 34 02 58 09 4C 09 70 09 A0 0C 54 22 00 80 00 00 00 00 `  
`01 06 12 00 00 00 00 00 00 00 0B 0A 00 00 94 00 0C 02 0C 02 0C 02 9C 02 C8 2B 00 80 00 00 00 00 `  
`01 07 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 D4 2D 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 70 2F 00 80 00 00 00 00 `  
`01 0B 12 00 00 00 00 00 00 00 0B 0A 00 00 94 00 0C 02 0C 02 0C 02 9C 02 2C 30 00 80 00 00 00 00 `  
`01 0C 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 38 32 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 D4 33 00 80 00 00 00 00 `  
`01 0F 08 00 00 00 00 00 00 00 04 04 00 00 44 00 D4 00 D4 00 D4 00 00 01 90 34 00 80 00 00 00 00 `  
`01 10 15 00 00 00 00 00 00 00 07 0B 00 00 AC 00 F8 01 F8 01 F8 01 50 02 64 35 00 80 00 00 00 00 `  
`01 11 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 5C 37 00 80 00 00 00 00 `  
`01 13 08 00 00 00 00 00 00 00 04 04 00 00 44 00 D4 00 D4 00 D4 00 00 01 5C 38 00 80 00 00 00 00 `  
`01 14 15 00 00 00 00 00 00 00 07 0B 00 00 AC 00 F8 01 F8 01 F8 01 50 02 30 39 00 80 00 00 00 00 `  
`01 15 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 28 3B 00 80 00 00 00 00`

  
  
  
  
Model 4 animations data \[at offset 0x0000F9B4\] (5 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 68 B6 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`37 00 16 02 00 2F B4 00 90 01 90 01 10 BE 00 80 `  
`37 00 16 03 00 33 B4 00 FE 01 FE 01 BC C9 00 80`

  
  
  
  
  
Model 5 bones data \[at offset 0x0000FA04\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`AE FF 01 01 `  
`70 FF 02 01 `  
`AE FF 01 00 `  
`7C FF 04 00 `  
`CA FF 05 01 `  
`A3 FF 06 01 `  
`7A FF 07 01 `  
`AE FF 01 00 `  
`7C FF 09 00 `  
`CA FF 0A 01 `  
`A3 FF 0B 01 `  
`7A FF 0C 01 `  
`00 00 00 00 `  
`E0 FF 0E 01 `  
`5E FF 0F 01 `  
`58 FF 10 01 `  
`00 00 00 00 `  
`E0 FF 12 01 `  
`5E FF 13 01 `  
`58 FF 14 01`

  
  
  
  
Model 5 parts data \[at offset 0x0000FA5C\] (15 parts):

  

`01 01 17 00 00 00 00 00 00 00 02 12 00 00 BC 00 44 02 44 02 44 02 C0 02 28 3C 00 80 00 00 00 00 `  
`01 02 1C 00 00 00 00 00 00 00 1A 0B 00 00 E4 00 60 03 60 03 60 03 64 04 6C 3E 00 80 00 00 00 00 `  
`01 03 4C 0C 02 02 00 00 00 00 4A 23 03 04 64 02 24 0A 18 0A 3C 0A BC 0D CC 41 00 80 00 00 00 00 `  
`01 06 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 0C 4C 00 80 00 00 00 00 `  
`01 07 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 A8 4D 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 44 4F 00 80 00 00 00 00 `  
`01 0B 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 00 50 00 Start index of bones80 00 00 00 00 `  
`01 0C 10 00/cpp 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 9C 51 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 38 53 00 80 00 00 00 00 `  
`01 0F 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 F4 53 00 80 00 00 00 00 `  
`01 10 18 00 00 00 00 00 00 00 00 12 00 00 C4 00 2C 02 2C 02 2C 02 88 02 B0 54 00 80 00 00 00 00 `  
`01 11 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 DC 56 00 80 00 00 00 00 `  
`01 13 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 DC 57 00 80 00 00 00 00 `  
`01 14 18 00 00 00 00 00 00 00 00 12 00 00 C4 00 2C 02 2C 02 2C 02 88 02 98 58 00 80 00 00 00 00 `  
`01 15 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 C4 5A 00 80 00 00 00 00`

  
  
  
  
Model 5 animations data \[at offset 0x0000FC3C\] (4 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 68 B6 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`19 00 16 03 00 2E B4 00 4A 01 4A 01 B0 D6 00 80`

  
  
  
  
  
  
Model 6 bones data \[at offset 0x0000FC7C\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`BA FF 01 01 `  
`2B FF 02 01 `  
`BA FF 01 00 `  
`2C FF 04 00 `  
`B3 FF 05 01 `  
`B0 FF 06 01 `  
`6A FF 07 01 `  
`BA FF 01 00 `  
`2C FF 09 00 `  
`B3 FF 0A 01 `  
`B0 FF 0B 01 `  
`6A FF 0C 01 `  
`00 00 00 00 `  
`C7 FF 0E 01 `  
`6A FF 0F 01 `  
`5E FF 10 01 `  
`00 00 00 00 `  
`C7 FF 12 01 `  
`6A FF 13 01 `  
`5E FF 14 01`

  
  
  
  
Model 6 parts data \[at offset 0x0000FCD4\] (15 parts):

  

`01 01 0E 00 00 00 00 00 00 00 04 0A 00 00 74 00 7C 01 7C 01 7C 01 D8 01 C4 5B 00 80 00 00 00 00 `  
`01 02 14 00 00 00 00 00 00 00 12 09 00 00 A4 00 78 02 78 02 78 02 3C 03 40 5D 00 80 00 00 00 00 `  
`01 03 49 0E 04 00 00 00 00 00 4A 23 03 04 4C 02 14 0A 08 0A 30 0A D4 0D B8 5F 00 80 00 00 00 00 `  
`01 06 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 EC 69 00 80 00 00 00 00 `  
`01 07 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 88 6B 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 24 6D 00 80 00 00 00 00 `  
`01 0B 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 E0 6D 00 80 00 00 00 00 `  
`01 0C 10 00 00 00 00 00 00 00 00 0E 00 00 84 00 9C 01 9C 01 9C 01 F8 01 7C 6F 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 18 71 00 80 00 00 00 00 `  
`01 0F 0F 00 00 00 00 00 00 00 02 0C 00 00 7C 00 8C 01 8C 01 8C 01 E8 01 D4 71 00 80 00 00 00 00 `  
`01 10 18 00 00 00 00 00 00 00 00 12 00 00 C4 00 2C 02 2C 02 2C 02 88 02 60 73 00 80 00 00 00 00 `  
`01 11 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 8C 75 00 80 00 00 00 00 `  
`01 13 0F 00 00 00 00 00 00 00 02 0C 00 00 7C 00 8C 01 8C 01 8C 01 E8 01 8C 76 00 80 00 00 00 00 `  
`01 14 18 00 00 00 00 00 00 00 00 12 00 00 C4 00 2C 02 2C 02 2C 02 88 02 18 78 00 80 00 00 00 00 `  
`01 15 0A 00 00 00 00 00 00 00 02 07 00 00 54 00 00 01 00 01 00 01 34 01 44 7A 00 80 00 00 00 00`

  
  
  
  
Model 6 animations data \[at offset 0x0000FEB4\] (4 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 68 B6 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`37 00 16 02 00 2F B4 00 90 01 90 01 10 BE 00 80`

  
  
  
  
  
  
Model 7 bones data \[at offset 0x0000FEF4\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`C4 FF 01 01 `  
`48 FF 02 01 `  
`C4 FF 01 00 `  
`80 FF 04 00 `  
`A1 FF 05 01 `  
`9C FF 06 01 `  
`86 FF 07 01 `  
`C4 FF 01 00 `  
`80 FF 09 00 `  
`A1 FF 0A 01 `  
`9C FF 0B 01 `  
`86 FF 0C 01 `  
`00 00 00 00 `  
`CA FF 0E 01 `  
`62 FF 0F 01 `  
`40 FF 10 01 `  
`00 00 00 00 `  
`CA FF 12 01 `  
`62 FF 13 01 `  
`40 FF 14 01`

  
  
  
  
Model 7 parts data \[at offset 0x0000FF4C\] (15 parts):

  

`01 01 26 00 00 00 00 00 00 00 1E 12 00 00 34 01 7C 04 7C 04 7C 04 D0 05 44 7B 00 80 00 00 00 00 `  
`01 02 21 00 00 00 00 00 00 00 20 0F 00 00 0C 01 38 04 38 04 38 04 9C 05 C0 7F 00 80 00 00 00 00 `  
`01 03 2C 0C 00 06 00 00 00 00 1D 13 03 06 64 01 34 05 28 05 4C 05 C8 06 F8 83 00 80 00 00 00 00 `  
`01 06 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 4C 89 00 80 00 00 00 00 `  
`01 07 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 50 8B 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 7C 8C 00 80 00 00 00 00 `  
`01 0B 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 38 8D 00 80 00 00 00 00 `  
`01 0C 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 3C 8F 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 68 90 00 80 00 00 00 00 `  
`01 0F 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 24 91 00 80 00 00 00 00 `  
`01 10 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 80 92 00 80 00 00 00 00 `  
`01 11 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 CC 93 00 80 00 00 00 00 `  
`01 13 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 10 95 00 80 00 00 00 00 `  
`01 14 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 6C 96 00 80 00 00 00 00 `  
`01 15 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 B8 97 00 80 00 00 00 00`

  
  
  
  
Model 7 animations data \[at offset 0x0001012C\] (8 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 78 DC 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`01 00 16 00 02 00 B4 00 B4 00 B8 00 30 DD 00 80 `  
`1E 00 16 00 02 14 B4 00 B4 00 B8 00 E8 DD 00 80 `  
`1E 00 16 02 00 24 B4 00 2C 01 2C 01 F8 E0 00 80 `  
`01 00 16 00 03 00 B4 00 B4 00 BA 00 5C E6 00 80 `  
`37 00 16 03 00 23 B4 00 FE 01 FE 01 18 E7 00 80`

  
  
  
  
  
Model 8 bones data \[at offset 0x000101AC\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`C4 FF 01 01 `  
`48 FF 02 01 `  
`C4 FF 01 00 `  
`80 FF 04 00 `  
`A1 FF 05 01 `  
`9C FF 06 01 `  
`86 FF 07 01 `  
`C4 FF 01 00 `  
`80 FF 09 00 `  
`A1 FF 0A 01 `  
`9C FF 0B 01 `  
`86 FF 0C 01 `  
`00 00 00 00 `  
`CA FF 0E 01 `  
`62 FF 0F 01 `  
`40 FF 10 01 `  
`00 00 00 00 `  
`CA FF 12 01 `  
`62 FF 13 01 `  
`40 FF 14 01`

  
  
  
  
Model 8 parts data \[at offset 0x00010204 (15 parts):

  

`01 01 26 00 00 00 00 00 00 00 1E 12 00 00 34 01 7C 04 7C 04 7C 04 D0 05 44 7B 00 80 00 00 00 00 `  
`01 02 21 00 00 00 00 00 00 00 20 0F 00 00 0C 01 38 04 38 04 38 04 9C 05 C0 7F 00 80 00 00 00 00 `  
`01 03 2C 0C 00 06 00 00 00 00 1D 13 03 06 64 01 34 05 28 05 4C 05 C8 06 F8 83 00 80 00 00 00 00 `  
`01 06 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 4C 89 00 80 00 00 00 00 `  
`01 07 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 50 8B 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 7C 8C 00 80 00 00 00 00 `  
`01 0B 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 38 8D 00 80 00 00 00 00 `  
`01 0C 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 3C 8F 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 68 90 00 80 00 00 00 00 `  
`01 0F 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 24 91 00 80 00 00 00 00 `  
`01 10 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 80 92 00 80 00 00 00 00 `  
`01 11 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 CC 93 00 80 00 00 00 00 `  
`01 13 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 10 95 00 80 00 00 00 00 `  
`01 14 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 6C 96 00 80 00 00 00 00 `  
`01 15 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 B8 97 00 80 00 00 00 00`

  
  
  
  
Model 8 animations data \[at offset 0x000103E4\] (8 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 78 DC 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`01 00 16 00 02 00 B4 00 B4 00 B8 00 30 DD 00 80 `  
`1E 00 16 00 02 14 B4 00 B4 00 B8 00 E8 DD 00 80 `  
`1E 00 16 02 00 24 B4 00 2C 01 2C 01 F8 E0 00 80 `  
`01 00 16 00 03 00 B4 00 B4 00 BA 00 5C E6 00 80 `  
`37 00 16 03 00 23 B4 00 FE 01 FE 01 18 E7 00 80`

  
  
  
  
  
Model 9 bones data \[at offset 0x00010464\] (22 bones):

  

`00 00 FF 00 `  
`00 00 00 01 `  
`C4 FF 01 01 `  
`48 FF 02 01 `  
`C4 FF 01 00 `  
`80 FF 04 00 `  
`A1 FF 05 01 `  
`9C FF 06 01 `  
`86 FF 07 01 `  
`C4 FF 01 00 `  
`80 FF 09 00 `  
`A1 FF 0A 01 `  
`9C FF 0B 01 `  
`86 FF 0C 01 `  
`00 00 00 00 `  
`CA FF 0E 01 `  
`62 FF 0F 01 `  
`40 FF 10 01 `  
`00 00 00 00 `  
`CA FF 12 01 `  
`62 FF 13 01 `  
`40 FF 14 01`

  
  
  
  
Model 9 parts data \[at offset 0x000104BC\] (15 parts):

  

`01 01 26 00 00 00 00 00 00 00 1E 12 00 00 34 01 7C 04 7C 04 7C 04 D0 05 44 7B 00 80 00 00 00 00 `  
`01 02 21 00 00 00 00 00 00 00 20 0F 00 00 0C 01 38 04 38 04 38 04 9C 05 C0 7F 00 80 00 00 00 00 `  
`01 03 2C 0C 00 06 00 00 00 00 1D 13 03 06 64 01 34 05 28 05 4C 05 C8 06 F8 83 00 80 00 00 00 00 `  
`01 06 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 4C 89 00 80 00 00 00 00 `  
`01 07 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 50 8B 00 80 00 00 00 00 `  
`01 08 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 7C 8C 00 80 00 00 00 00 `  
`01 0B 12 00 00 00 00 00 00 00 08 0C 00 00 94 00 04 02 04 02 04 02 90 02 38 8D 00 80 00 00 00 00 `  
`01 0C 0C 00 00 00 00 00 00 00 00 0A 00 00 64 00 2C 01 2C 01 2C 01 68 01 3C 8F 00 80 00 00 00 00 `  
`01 0D 08 00 00 00 00 00 00 00 00 06 00 00 44 00 BC 00 BC 00 BC 00 D8 00 68 90 00 80 00 00 00 00 `  
`01 0F 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 24 91 00 80 00 00 00 00 `  
`01 10 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 80 92 00 80 00 00 00 00 `  
`01 11 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 CC 93 00 80 00 00 00 00 `  
`01 13 0C 00 00 00 00 00 00 00 08 06 00 00 64 00 5C 01 5C 01 5C 01 B8 01 10 95 00 80 00 00 00 00 `  
`01 14 0D 00 00 00 00 00 00 00 04 08 00 00 6C 00 4C 01 4C 01 4C 01 90 01 6C 96 00 80 00 00 00 00 `  
`01 15 0C 00 00 00 00 00 00 00 04 08 00 00 64 00 44 01 44 01 44 01 90 01 B8 97 00 80 00 00 00 00`

  
  
  
  
Model 9 animations data \[at offset 0x0001069C\] (8 animations):

  

`01 00 16 00 02 00 B4 00 B4 00 B8 00 78 DC 00 80 `  
`1E 00 16 01 01 1C B4 00 F0 00 F2 00 20 B7 00 80 `  
`0F 00 16 01 01 20 B4 00 D2 00 D4 00 5C BB 00 80 `  
`01 00 16 00 02 00 B4 00 B4 00 B8 00 30 DD 00 80 `  
`1E 00 16 00 02 14 B4 00 B4 00 B8 00 E8 DD 00 80 `  
`1E 00 16 02 00 24 B4 00 2C 01 2C 01 F8 E0 00 80 `  
`01 00 16 00 03 00 B4 00 B4 00 BA 00 5C E6 00 80 `  
`37 00 16 03 00 23 B4 00 FE 01 FE 01 18 E7 00 80`

  
  
  
  
  
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

  
The rest of the file (20 bytes) is unknown:

  

`14 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 - Unknown`

Note: This small final section of BSX files does not exist in BCX files.
This may provide some idea as to what this section is for.

  [Micky's tool]: http://web.archive.org/web/20170521085448/http://forums.qhimm.com/index.php?topic=8969.msg122920#msg122920
