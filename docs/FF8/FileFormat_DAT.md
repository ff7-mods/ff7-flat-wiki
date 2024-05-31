---
title: FileFormat_DAT
---

By Mirex, JWP, random\_npc and myst6re. Edit: We now know the animation and skeleton- see <https://github.com/MaKiPL/OpenVIII/blob/4ac151daad7cd1475eb0694dd0715bc35d7a4b39/FF8/debug_battleDat.cs>

## Header

DAT file is divided into 11 sections (except for c0m127.dat, which contains only 2 sections : 7th and 8th).

| Offset              | Length                | Description                                            |
|---------------------|-----------------------|--------------------------------------------------------|
| 0                   | 4 bytes               | Number of sections (always =11, except for c0m127.dat) |
| 4                   | nbSections \* 4 bytes | Section Positions                                      |
| 4 + nbSections \* 4 | 4 bytes               | File size                                              |

## Section 1: Skeleton

| Offset | Length                      | Description     |
|--------|-----------------------------|-----------------|
| 0      | 2 bytes                     | Number of bones |
| 2      | 6 bytes                     | Unknown         |
| 8      | s16f (divide by 4096f)      | scaleX          |
| 10     | s16f (divide by 4096f)      | scale -Z        |
| 12     | s16f (divide by 4096f)      | scale Y         |
| 14     | 2 bytes                     | Unknown         |
| 16     | Number of bones \* 48 bytes | Bones           |

### Bone struct

| Offset | Length                 | Description                 |
|--------|------------------------|-----------------------------|
| 0      | 2 bytes                | Parent id                   |
| 2      | s16f (divide by 4096f) | Bone size (?)               |
| 4      | s16f (divide by 4096f) | unknown, multiplied by 360f |
| 6      | s16f (divide by 4096f) | unknown, multiplied by 360f |
| 8      | s16f (divide by 4096f) | unknown, multiplied by 360f |
| 10     | s16f (divide by 4096f) | unknown                     |
| 12     | s16f (divide by 4096f) | unknown                     |
| 14     | s16f (divide by 4096f) | unknown                     |
| 16     | 28 bytes               | Unknown (often empty)       |

## Section 2: Model geometry

### Header (data sub table)

| Offset             | Length               | Description             |
|--------------------|----------------------|-------------------------|
| 0                  | 4 bytes              | Number of objects       |
| 4                  | nbObjects \* 4 bytes | Object Positions        |
| 4 + nbObjects \* 4 | Varies               | Object Data (see below) |
| Varies             | 4 bytes              | Total count of vertices |

### Object Data

| Offset | Length                     | Description               |
|--------|----------------------------|---------------------------|
| 0      | 2 bytes                    | Number of Vertices Data   |
| 2      | Varies \* NbVerticesData   | Vertices Data (see below) |
| Varies | 4 - (absolutePosition % 4) | Padding (0x00)            |
| Varies | 2 bytes                    | Num triangles             |
| Varies | 2 bytes                    | Num quads                 |
| Varies | 8 bytes                    | Always empty              |
| Varies | numTriangles \* 16 bytes   | Triangles                 |
| Varies | numQuads \* 20 bytes       | Quads                     |

#### Vertice Data

| Offset | Length                | Description                       |
|--------|-----------------------|-----------------------------------|
| 0      | 2 bytes               | Bone id                           |
| 2      | 2 bytes               | Number of vertices                |
| 4      | nbVertices \* 6 bytes | Vertices (nbVertices \* 3 shorts) |

#### Useful structures

`struct vertice {`  
`     sint16    x, y, z;`  
`};`

(sizeof = 6)

`struct triangle {`  
`     uint16    vertex_indexes[3]; // vertex_indexes[0] &= 0xFFF, other bits are unknown`  
`     uint8 texCoords1[2];`  
`     uint8 texCoords2[2];`  
`     uint16    textureID_related;`  
`     uint8 texCoords3[2];`  
`     uint16    u; // textureID_related2`  
`};`

(sizeof = 16)

`struct quad {`  
`     uint16    vertex_indexes[4]; // vertex_indexes[0] &= 0xFFF, other bits are unknown`  
`     uint8 texCoords1[2];`  
`     uint16    textureID_related;`  
`     uint8 texCoords2[2];`  
`     uint16    u; // textureID_related2`  
`     uint8 texCoords3[2];`  
`     uint8 texCoords4[2];`  
`};`

(sizeof = 20)

## Section 3: Model animation

### Header (data sub table)

| Offset | Length                  | Description          |
|--------|-------------------------|----------------------|
| 0      | 4 bytes                 | Number of animations |
| 4      | nbAnimations \* 4 bytes | Animations Positions |

### Animation

| Offset | Length | Description      |
|--------|--------|------------------|
| 0      | 1 byte | Number of frames |
| 1      | Varies | Unknown          |

## Section 4: Unknown

Optional section, often empty.

## Section 5: Unknown

Unknown sequences.

### Header

| Offset | Length                 | Description         |
|--------|------------------------|---------------------|
| 0      | 2 bytes                | Number of sequences |
| 2      | nbSequences \* 2 bytes | Sequences Positions |

## Section 6: unknown

Can be empty.

## Section 7: Informations & stats

<table><thead><tr class="header"><th><p>Offset</p></th><th><p>Length</p></th><th><p>Description</p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>24 bytes</p></td><td><p>Monster name</p></td></tr><tr class="even"><td><p>24</p></td><td><p>4 bytes</p></td><td><p>HP values</p></td></tr><tr class="odd"><td><p>28</p></td><td><p>4 bytes</p></td><td><p>Str values</p></td></tr><tr class="even"><td><p>32</p></td><td><p>4 bytes</p></td><td><p>Vit values</p></td></tr><tr class="odd"><td><p>36</p></td><td><p>4 bytes</p></td><td><p>Mag values</p></td></tr><tr class="even"><td><p>40</p></td><td><p>4 bytes</p></td><td><p>Spr values</p></td></tr><tr class="odd"><td><p>44</p></td><td><p>4 bytes</p></td><td><p>Spd values</p></td></tr><tr class="even"><td><p>48</p></td><td><p>4 bytes</p></td><td><p>Eva values</p></td></tr><tr class="odd"><td><p>52</p></td><td><p>16*4 bytes</p></td><td><p>Abilities, low level</p></td></tr><tr class="even"><td><p>116</p></td><td><p>16*4 bytes</p></td><td><p>Abilities, med level</p></td></tr><tr class="odd"><td><p>180</p></td><td><p>16*4 bytes</p></td><td><p>Abilities, high level</p></td></tr><tr class="even"><td><p>244</p></td><td><p>1 byte</p></td><td><p>Med level start</p></td></tr><tr class="odd"><td><p>245</p></td><td><p>1 byte</p></td><td><p>High level start</p></td></tr><tr class="even"><td><p>246</p></td><td><p>1 byte</p></td><td><p>Unknown (flags, 3 bits used)</p></td></tr><tr class="odd"><td><p>247</p></td><td><p>1 byte</p></td><td><p>[LSB] Zombie / Fly / zz1 / LvUP-Down Immunity / HP Hidden / Auto-Reflect / Auto-Shell / Auto-Protect [MSB]</p></td></tr><tr class="even"><td><p>248</p></td><td><p>3 bytes</p></td><td><p>Cards (low/med/high)</p></td></tr><tr class="odd"><td><p>251</p></td><td><p>3 bytes</p></td><td><p>Devour (low/med/high)</p></td></tr><tr class="even"><td><p>254</p></td><td><p>1 byte</p></td><td><p>[LSB] zz1 / zz2 / unused / unused / unused / unused / Diablos missed / Always obtains card [MSB]</p></td></tr><tr class="odd"><td><p>255</p></td><td><p>1 byte</p></td><td><p>Unknown (flags, 4 bits used)</p></td></tr><tr class="even"><td><p>256</p></td><td><p>2 bytes</p></td><td><p>Extra EXP</p></td></tr><tr class="odd"><td><p>258</p></td><td><p>2 bytes</p></td><td><p>EXP</p></td></tr><tr class="even"><td><p>260</p></td><td><p>8 bytes</p></td><td><p>Draw (low)</p></td></tr><tr class="odd"><td><p>268</p></td><td><p>8 bytes</p></td><td><p>Draw (med)</p></td></tr><tr class="even"><td><p>276</p></td><td><p>8 bytes</p></td><td><p>Draw (high)</p></td></tr><tr class="odd"><td><p>284</p></td><td><p>8 bytes</p></td><td><p>Mug (low)</p></td></tr><tr class="even"><td><p>292</p></td><td><p>8 bytes</p></td><td><p>Mug (med)</p></td></tr><tr class="odd"><td><p>300</p></td><td><p>8 bytes</p></td><td><p>Mug (high)</p></td></tr><tr class="even"><td><p>308</p></td><td><p>8 bytes</p></td><td><p>Drop (low)</p></td></tr><tr class="odd"><td><p>316</p></td><td><p>8 bytes</p></td><td><p>Drop (med)</p></td></tr><tr class="even"><td><p>324</p></td><td><p>8 bytes</p></td><td><p>Drop (high)</p></td></tr><tr class="odd"><td><p>332</p></td><td><p>1 byte</p></td><td><p>Mug rate</p></td></tr><tr class="even"><td><p>333</p></td><td><p>1 byte</p></td><td><p>Drop rate</p></td></tr><tr class="odd"><td><p>334</p></td><td><p>1 byte</p></td><td><p>Padding (0x00)</p></td></tr><tr class="even"><td><p>335</p></td><td><p>1 byte</p></td><td><p>APs</p></td></tr><tr class="odd"><td><p>336</p></td><td><p>16 bytes</p></td><td><p>Unknown</p></td></tr><tr class="even"><td><p>352</p></td><td><p>8 bytes</p></td><td><p>Elemental resistance<br />
(Fire, Ice, Thunder, Earth, Poison, Wind, Water, Holy)</p></td></tr><tr class="odd"><td><p>360</p></td><td><p>20 bytes</p></td><td><p>Mental resistance<br />
(Death, Poison, Petrify, Darkness,<br />
Silence, Beserk, Zombie, Sleep,<br />
Haste, Slow, Stop, Regen,<br />
Reflect, Doom, Slow Petrify, Float,<br />
Confuse, Drain, Expulsion, ???)</p></td></tr></tbody></table>

### Abilities

`typedef struct {`  
`    uint8 kernel_id;`  
`    uint8 unknown;`  
`    uint16 ability_id;`  
`}`

kernel\_id is the used table in kernel.bin. May be 0x02 (= magic), 0x04 (= item) or 0x08 (= monster ability). ability\_id is the ability in the selected kernel table.

### Draw/mug/drop

`typedef struct {`  
`    uint8 id_1; // magic_id for draw, item_id for mug & drop`  
`    uint8 qty_1; // quantities are always 0 for draw`  
`    uint8 id_2;`  
`    uint8 qty_2;`  
`    uint8 id_3;`  
`    uint8 qty_3;`  
`    uint8 id_4;`  
`    uint8 qty_4;`  
`}`

## Section 8: Battle scripts/AI

| Offset | Length  | Description                |
|--------|---------|----------------------------|
| 0      | 4 bytes | Number of sub-sections     |
| 4      | 4 bytes | Offset to AI sub-section   |
| 8      | 4 bytes | Offset to text offsets     |
| 12     | 4 bytes | Offset to text sub-section |

### AI

| Offset | Length  | Description                              |
|--------|---------|------------------------------------------|
| 0      | 4 bytes | Offset to init code                      |
| 4      | 4 bytes | Offset to code executed at ennemy's turn |
| 8      | 4 bytes | Offset to counterattack code             |
| 12     | 4 bytes | Offset to death code                     |
| 16     | 4 bytes | Unknown offset                           |

### Texts

Text offsets is a list of text positions (2 bytes each) in the text sub-section.

## Section 9: Sounds

Contains AKAO sequences (can be empty).

| Offset           | Length             | Description      |
|------------------|--------------------|------------------|
| 0                | 2 bytes            | Number of AKAOs  |
| 2                | nbAKAOs \* 2 bytes | AKAOs Positions  |
| 2 + nbAKAOs \* 2 | 2 bytes            | End of section 9 |
| 4 + nbAKAOs \* 2 | Varies \* nbAKAOs  | AKAOs            |

## Section 10: Sounds/Unknown

Contains AKAO sequence + unknown data (can be empty).

## Section 11: Textures

Contains some [TIMs](../PSX/TIM_format.md).

| Offset          | Length            | Description    |
|-----------------|-------------------|----------------|
| 0               | 4 bytes           | Number of TIMs |
| 4               | nbTIMs \* 4 bytes | TIMs Positions |
| 4 + nbTIMs \* 4 | 4 bytes           | End of file    |
| 8 + nbTIMs \* 4 | Varies \* nbTIMs  | TIMs           |
