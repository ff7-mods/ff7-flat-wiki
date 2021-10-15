---
title: FileFormat_X
---

By MaKiPL. Thanks for help in research for: shakotay2 (XeNTaX), Halfer, Yagami Light. Complete list of original battle stages by Kaspar01: [List of battle stages](BS_list.md)

## Info

.X file is uncompressed 3D stage model with texture embedeed. The file contains unused info (not used by FF8 engine), camera data, movement, translations and geometry data.

Battle stages **DOES NOT** contain pointers to next sections. All pointers are **HARDCODED** in FF8.EXE. [Click me for battle stage pointer list](BattleStage/Pointers.md)

| Name                      | Usually starting with:                  | Description                                                             |
|---------------------------|-----------------------------------------|-------------------------------------------------------------------------|
| PlayStation MIPS assembly | E8 FF BD 27 01 00 02                    | Used only in PS version; skipped in PC                                  |
| Camera data + movement    | 02 00 08 00 20 00                       | Camera animations, movement (pre-keyed)                                 |
| Model section             | 06 00 00 00 (See geometry section info) | Divides to object (group) and it's sub-objects + vert/triangle grouping |
| Texture                   | 10 00 00 00 09 (Always)                 | Contains one .TIM texture, 8 BPP                                        |

## How is this file handled by the engine?

FF8 loads specific file and reads it from hardcoded (written in FF8 code) position (or reads MIPS PlayStation assembly that contains battle stage load code). This hardcoded position points to camera data (in PC). Camera data has size uint16, which is calculated and relative jump is made. Just after camera, a typical section based file handling is made.

| Offset | Length | Description                |
|--------|--------|----------------------------|
| 0      | uint32 | Number of sections         |
| 4      | uint32 | Objects group \#1          |
| 8      | uint32 | Objects group \#2          |
| 12     | uint32 | Objects group \#3          |
| 16     | uint32 | Objects group \#4          |
| 20     | uint32 | Texture \[unused in code\] |
| 24     | uint32 | Texture                    |
| 28     | uint32 | Relative to EOF            |

#### Objects Group

| Offset | Length | Description                |
|--------|--------|----------------------------|
| 0      | uint32 | Number of sections         |
| 4      | uint32 | Pointer to Settings \#1    |
| 8      | uint32 | Pointer to ObjectsList     |
| 12     | uint32 | Pointer to Settings \#2    |
| 16     | uint32 | Relative to end\_of\_group |

##### Objects List

| Offset          | Length | Description                                                 |
|-----------------|--------|-------------------------------------------------------------|
| 0               | uint32 | Number of objects                                           |
| Num\_of\_obj\*4 | uint32 | Relative pointer to segment (one .obj file) \[01 00 01 00\] |

##### Settings 1

| Offset | Length                       | Description                                                 |
|--------|------------------------------|-------------------------------------------------------------|
| 0      | uint16                       | Unknown, fixed 2?                                           |
| 2      | sint16 (probably, or uint16) | Scale (01 is the smallest)                                  |
| 4      | 4 bytes                      | PADDING                                                     |
| 8      | 4 bytes                      | Nothing?                                                    |
| 12     | 4 bytes                      | Nothing?                                                    |
| 16     | 2 bytes                      | if not FF FF, then model vanishes                           |
| 18     | sint16                       | X or Z Axis rot origin (Translation)                        |
| 20     | 44 bytes                     | Left null for storing some engine data AFTER loaded in-game |
| 64     | 2 bytes                      | if not FF FF or 00 00, then model vanishes                  |
| 66     | 2 bytes                      | Nothing?                                                    |
| 68     | ...up to end                 | Left null for storing some engine data AFTER loaded in-game |

This might look difficult, but it's like multi-pointer file that starts at different location given by executable. See list at the beginning of this wiki to see which stages camera starts at which position (where FF8.exe really starts to read file as BattleStage) \[FF8 stores whole file, even with useless data before camera\] If this still makes trouble, see this video: TODO

## Camera data

Starts at \~0x5d4 (see How the engine handles this file?). \[.text:00509820\]

| Offset | Length   | Description                                                   |
|--------|----------|---------------------------------------------------------------|
| 0      | uInt16   | Pointers count. Fixed (02 00) **\[Unused in code\]**          |
| 2      | uInt16   | Relative jump to CameraSetting. Should be (08 00)             |
| 4      | uInt16   | Relative jump to CameraAnimationCollection. Should be (20 00) |
| 6      | uInt16   | Camera data size (starting from 0) **\[unused in code\]**     |
| 8      | 24 bytes | Camera Settings                                               |
| 32     | ?? bytes | Camera Animation Collection                                   |

#### Camera Setting

| Offset | Length                      | Description                       |
|--------|-----------------------------|-----------------------------------|
| 0      | char (based on disassembly) | CameraAnimMode?                   |
| 1      | byte?                       | StopEnemyBeforeAnim?              |
| 2      | Bitfield? (1B)              | UHM?                              |
| 3      | ???                         | DefaultEndofCameraPosition\_Zoom? |
| 4      | ???                         | ???                               |

#### Camera Animations Collection

| Offset                    | Length             | Description                              |
|---------------------------|--------------------|------------------------------------------|
| 0                         | uint16             | NumOfSets                                |
| 2 \*(Set index)           | uint16             | Relative pointer to camera Animation Set |
| 2 \*(Set index)+ 2        | uint16             | Camera EOF                               |
| CameraAnimationSetPointer | CameraAnimationSet | CameraAnimationSet                       |

##### CameraAnimationSet

Seems to be 8 pointers in each set.

| Offset      | Length                           | Description     |
|-------------|----------------------------------|-----------------|
| 0           | ushort                           | AnimPointer\*2  |
| AnimPointer | Varies 144-146-148 bytes usually | CameraAnimation |

## Camera Animation (WIP)

`All this is based on best effort knowledge from reversing by Maki. I'm just trying to understand it.`

### Control Word

| Offset | Length                 | Description                     |
|--------|------------------------|---------------------------------|
| 0      | uint16\_t (bit varies) | Main controller. If 0xFFFFU END |

#### FOV

`Control Word & 0b0000'0000'1100'0000U`

##### 1 Default

| Offset | Length | Description   |
|--------|--------|---------------|
| None   | None   | Start = 0x200 |
| None   | None   | End = 0x200   |

##### 2 Same

| Offset | Length    | Description |
|--------|-----------|-------------|
| 0      | uint16\_t | Start       |
| 2      | uint16\_t | Padding     |
| None   | None      | End = Start |

##### 2 Different

| Offset | Length    | Description |
|--------|-----------|-------------|
| 0      | uint16\_t | Start       |
| 2      | uint16\_t | Padding     |
| 4      | uint16\_t | End         |

#### ROLL

`Control Word & 0b0000'0011'0000'0000U`

##### 0 Unknown

`TODO`

##### 1 Default

| Offset | Length | Description   |
|--------|--------|---------------|
| None   | None   | Start = 0x000 |
| None   | None   | End = 0x000   |

##### 2 Same

| Offset | Length    | Description |
|--------|-----------|-------------|
| 0      | uint16\_t | Start       |
| None   | None      | End = Start |

##### 2 Different

| Offset | Length    | Description |
|--------|-----------|-------------|
| 0      | uint16\_t | Start       |
| 2      | uint16\_t | End         |

#### LAYOUT

`Control Word & 0b0000'0000'0000'0001U`

##### 0 Default

`You'll loop through the data till the first value is less than 0. pushing back to a variable length container.`

| Offset | Length   | Description                                         |
|--------|----------|-----------------------------------------------------|
| 0      | int16\_t | if &lt; 0 break; could be related to time of frame. |
| 2      | 16 bytes | Animation Frame                                     |

##### 1 Other

`TODO`

### Time

`Time is calculated from number of frames. You basically set starting position World+lookat and ending position, then mark number of frames to interpolate between them. Every frame is one draw call and it costs 16. Starting time needs to be equal or higher for next animation frame to be read; If next frame==0xFFFF then it's all done.`

### Animation Frame

| Offset | Length                    | Description             |
|--------|---------------------------|-------------------------|
| 0      | uint16\_t                 | is frame durations shot |
| 2      | Vertice<uint16_t> (x,y,z) | World                   |
| 8      | uint16\_t                 | is frame ending shot    |
| 10     | Vertice<uint16_t> (x,y,z) | Look At                 |

##### Dependency

`  CAMERA:`  
`  -Camera Settings`  
`  -Camera Animation Collection (even three collections in a0stg006.x and up to 7 in a0stg101.x!)`  
`     |`  
`     |`  
`      -Camera animation Set (Always 8 camera animations, may be empty (0xFFFF); look for example to a0stg127.x collectionId==1; there are 8 animations, but 7 of them are 0xFFFF (pointers increase by 2))`  
`         |`  
`         |`  
`          - Camera animation`

##### Example

a0stg006.x:  
0x5d8 -&gt; 02 00 08 00 20 00

1.  Get EOF-&gt; \*(0x5d8 + 8) -&gt; 32
2.  Jump to EOF -&gt; 0x5d8 + 32 = 0x5F8 (This is now Camera Animation Collection)
3.  Get pointer to correct anim collection. In this case we will use AnimCollectionID == 0, so: \*(0x5F8 + 0\*2 + 2) -&gt; 0x0c
4.  Jump to Anim collection data: 0x5F8 + 0x0c = 0x604 (This is now Camera Animation Set)
5.  Jump to Camera animation by cameraAnimSetID, let's take for example cameraAnimSetID == 7, so: \*(0x604 + 7\*2) -&gt; 0x25E. Now carefully, jump by multiplying it by 2!
    1.  0x604 + (0x25E \* 2) = 0xAC0

Therefore: a0stg006.x Camera animation 7 in camera collection 0 is at 0xAC0

## Geometry

Geometry contains groups, that contains Triangles and/or quads poligons. Models always stars at 01 00 01 00, and needs to be after camera data, either it's not model itself, but some other data.

#### Group

| Offset                       | Length                       | Description                                                                                                               |
|------------------------------|------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| 0                            | 4 bytes                      | Always 01 00 01 00 / Header of object                                                                                     |
| 4                            | 2 bytes                      | Uint16 / number of vertices.                                                                                              |
| 6                            | Number of vertices \* 6      | Vertex data, short X; short Y; short Z;                                                                                   |
| 6 + (Number of vertices \*6) | (AbsolutePosition MOD 4) + 4 | Padding                                                                                                                   |
| varies (just after above)    | 2 bytes                      | uint16 / number of triangles                                                                                              |
| varies (just after above)    | 2 bytes                      | uint16 / number of quads                                                                                                  |
| varies (just after above)    | 4 bytes                      | padding                                                                                                                   |
| varies (just after above)    | number of triangles \* 20    | Triangle data. If NumOfTriangles = 0, then instead of any triangle data, there's quad data.                               |
| varies (just after above)    | number of quads \* 24        | Triangle data. If NumOfQuads = 0, then instead of any quad data, there's either next header 01 00 01 00, or end of group. |

##### Triangle

| Name                                   | Type                    | Description                                   |
|----------------------------------------|-------------------------|-----------------------------------------------|
| F1 (A)                                 | uint16                  | A of face indice                              |
| F2 (B)                                 | uint16                  | B of face indice                              |
| F3 (C)                                 | uint16                  | C of face indice                              |
| U1                                     | Byte                    | U of first texture coordinate                 |
| V1                                     | Byte                    | V of first texture coordinate                 |
| U2                                     | Byte                    | U of second texture coordinate                |
| V2                                     | Byte                    | V of second texture coordinate                |
| CLUT\_ID                               | UInt16 (BIT operated)\* | Index to CLUT\_ID operated by BIT (see below) |
| U3                                     | Byte                    | U of third texture coordinate                 |
| V3                                     | Byte                    | V of third texture coordinate                 |
| Special (see below / After QUAD table) | 8 Byte                  | See below (after QUAD table)                  |
| Hide                                   | Byte/Bool               | Bool. Hides or shows texture                  |
| Red                                    | Byte                    | Texture colourization (Red)                   |
| Green                                  | Byte                    | Texture colourization (Green)                 |
| Blue                                   | Byte                    | Texture colourization (Blue)                  |
| PSone GPU related                      | Byte                    | PSOne instruction                             |

##### Quad

| Name                | Type                    | Description                                   |
|---------------------|-------------------------|-----------------------------------------------|
| F1 (A)              | uint16                  | A of face indice                              |
| F2 (B)              | uint16                  | B of face indice                              |
| F3 (C)              | uint16                  | C of face indice                              |
| F4 (D)              | uint16                  | D of face indice                              |
| U1                  | Byte                    | U of first texture coordinate                 |
| V1                  | Byte                    | V of first texture coordinate                 |
| CLUT\_ID            | UInt16 (BIT operated)\* | Index to CLUT\_ID operated by BIT (see below) |
| U2                  | Byte                    | U of second texture coordinate                |
| V2                  | Byte                    | V of second texture coordinate                |
| Special (see below) | 8 Byte                  | See below (after table)                       |
| Hide                | Byte/Bool               | Bool. Hides or shows texture                  |
| U3                  | Byte                    | U of third texture coordinate                 |
| V3                  | Byte                    | V of third texture coordinate                 |
| U4                  | Byte                    | U of fourth texture coordinate                |
| V4                  | Byte                    | V of fourth texture coordinate                |
| Red                 | Byte                    | Texture colourization (Red)                   |
| Green               | Byte                    | Texture colourization (Green)                 |
| Blue                | Byte                    | Texture colourization (Blue)                  |
| PSone GPU related   | Byte                    | PSOne instruction                             |

Special Byte: This byte, needs to be divided to two bytes. So, for example, a 0xE5 needs to be treated like two bytes: 0x0E 0x05

| Singular of char    | Example      | Description         |
|---------------------|--------------|---------------------|
| First char/ 4 BIT   | B2 --&gt; 0B | Unknown             |
| Second char / 4 BIT | B2 --&gt; 02 | Texture page number |

#### CLUT ID

The most important bit's are the first two on one byte, and last two on last byte. Example: 00000000 00111100 (00 3C) should be read like this: 00111100 00000000 (3C 00) And the CLUT ID is revealed by watching this four bits: 001111\[00 00\]000000

Same applies to reading CLUT colors (16bits) where they are: 1b-T, 5b-B, 5b-G, 5b-R (Or RGBT if reordered as shown above)

Complete list (without replacing bit order - as is in HEX editor/memory):

| CLUT ID | BIT               | HEX   |
|---------|-------------------|-------|
| \#1     | 00000000 00111100 | 00 3C |
| \#2     | 01000000 00111100 | 40 3C |
| \#3     | 10000000 00111100 | 80 3C |
| \#4     | 11000000 00111100 | C0 3C |
| \#5     | 00000000 00111101 | 00 3D |
| \#6     | 01000000 00111101 | 40 3D |
| \#7     | 10000000 00111101 | 80 3D |
| \#8     | 11000000 00111101 | C0 3D |
| \#9     | 00000000 00111110 | 00 3E |
| \#10    | 01000000 00111110 | 40 3E |
| \#11    | 10000000 00111110 | 80 3E |
| \#12    | 11000000 00111110 | C0 3E |
| \#13    | 00000000 00111111 | 00 3F |
| \#14    | 01000000 00111111 | 40 3F |
| \#15    | 10000000 00111111 | 80 3F |
| \#16    | 11000000 00111111 | C0 3F |

## Texture

Contains one [TIMs](../PSX/TIM_format.md).

### UV calculation algorithm

`Float U = (float)U_Byte / (float)(TIM_Texture_Width * 2) + ((float)Texture_Page/(TIM_Texture_Width * 2));`

### Texture page calculation

`Byte TPage = InputBytes[TexturePage_index] & 0F;`

Bitwise TPage byte AND 0F, to delete first 4 bits

`int TPageINT = TPage * 64;`

For 16 bit TIM's, the texture page is 64 pixels wide

#### Example

For 24-bit TIM:

`0xB2 byte is: 2*48 = 96`

Unsure about this one. It could be 42.667 instead of 48. It takes 1.5x the space of 16 bit. I haven't seen a file that uses 24-bit yet.

For 16-bit TIM:

`0xB2 byte is: 2*64= 128`

For 8-bit TIM:

`0xB2 byte is: 2*128 = 256`

For 4-bit TIM:

`0xB2 byte is: 2*256 = 512`

Each time you half the number of bits you double the amount of data you can store in the same space. So the calculated Texture Page is different.

### Face order / Translation/ triangulation

#### Quad wing order

` ABCD ---> ABDC`  
` example:`  
`  f 1 2 3 4`  
` to:`  
`  f 1 2 4 3`

#### Quad triangulation face order

` ABDC > ABD`  
`        ACD (same for VT)`  
` example:`  
` f 1 2 4 3`  
` to:`  
` f 1 2 4`  
` f 1 3 4`

#### Triangles VT order

` A/T1 > A/T2`  
` B/T2 > B/T3`  
` C/T3 > C/T1`

#### Example

` (Also with quad triangulation face order!)`  
` f 1/1 2/2 7/4 6/3`  
` to:`  
` f 1/1 2/2 7/4`  
` f 1/1 6/3 7/4`  
` where:`  
` A=1 B=2 C=6 D=7`
