---
title: Menu_sp2
---

by MaKi  
updated by Sebanisu

This file is a mapping file for atlas textures like icons.tex

## Layout of **icon.sp1**:

### Header

**(4 x (PointerCount + 1))** bytes

| Offset | SizeOf                         | Name         | Description                     |
|--------|--------------------------------|--------------|---------------------------------|
| 0      | UInt32                         | PointerCount | Number of entries               |
| 4      | Struct Pointer\[PointerCount\] | Pointers     | Seek locations for entry groups |

### Pointer

**4** bytes

| Offset | SizeOf | Name    | Description                   |
|--------|--------|---------|-------------------------------|
| 0      | UInt16 | Pointer | Seek location for entry group |
| 2      | UInt16 | Count   | Number of entries in group    |

### Entry Group

**(8 x Count)** bytes  
At pointer's location there will be **Struct Entry\[Count\]**. Example of an entry group is the direction pad is in eight pieces. Four of them are unpressed and four are pressed versions. It has four entries for the direction pad depending on the directions it is highlighting.

### Entry

**8** bytes

| Offset | SizeOf    | Name     | Description                             |
|--------|-----------|----------|-----------------------------------------|
| 0      | Byte      | xPos     | Pixel X coordinate in image atlas       |
| 1      | Byte      | yPos     | Pixel Y coordinate in image atlas       |
| 2      | Byte\[2\] | UNK      | Unknown data                            |
| 4      | Byte      | Width    | Width of entry in pixels                |
| 5      | Byte      | Offset X | Offset of X coordinate for when drawing |
| 6      | Byte      | Height   | Height of entry in pixels               |
| 7      | Byte      | Offset Y | Offset of Y coordinate for when drawing |

Invalid Entries will have **X** and **Y** of **zero**. The top **16x16** pixel area is blank. Everything in **icon.tex** is aligned to a **8x8 grid**. Some entry groups leave out connecting pieces I think you are expected to fill in the blank. Some things like the menu border and menu background don't appear to be listed in this file.

### End of file

Everything at and beyond file pointer **4272 {0x10C0}** appears to be garbage.

## Layout of **face.sp2** and **cardanm.sp2**:

Both **face.sp2** and **cardanm.sp2** have the same layout. Main difference is **face.sp2** has **32** valid and **64** total entries. **cardanm.sp2** only has **11** valid entries and **1** invalid, as it has no dims. In each of the card texture files the final slot is the **Triple Triad** card back. If the entry had dims they would be X=**192**,Y=**128**, W=**64**, H=**64**.

### Header

<table><thead><tr class="header"><th><p>Offset</p></th><th><p>SizeOf</p></th><th><p>Name</p></th><th><p>Description</p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>UInt32</p></td><td><p>Count</p></td><td><p>Number of entries Count can be more than the actual images in the texture.<br />
<strong>face.sp2</strong>: There are 8 images per texture in 2 textures, and there are 32/64 valid entries. 1 is blank.<br />
<strong>cardanm.sp2</strong>: There are 11 images pre texture in 10 textures, and there are 11/12 valid entries. The 12th entry is the card back but it's missing dims.</p></td></tr><tr class="even"><td><p>4</p></td><td><p>UInt32[Count]</p></td><td><p>Locations</p></td><td><p>Seek location for each entry</p></td></tr></tbody></table>

### Entry

**16** bytes

<table><thead><tr class="header"><th><p>Offset</p></th><th><p>SizeOf</p></th><th><p>Name</p></th><th><p>Description</p></th></tr></thead><tbody><tr class="odd"><td><p>0</p></td><td><p>UInt32</p></td><td><p>Count</p></td><td><p>Number of entries at this location Always <strong>1</strong></p></td></tr><tr class="even"><td><p>4</p></td><td><p>byte</p></td><td><p>xPos</p></td><td><p>Pixel X coordinate in image atlas</p></td></tr><tr class="odd"><td><p>5</p></td><td><p>byte</p></td><td><p>yPos</p></td><td><p>Pixel Y coordinate in image atlas <strong>face.sp2</strong>: Invalid entries seem to have <strong>yPos&gt;=Texture.Height</strong>.<br />
Detected switch from <strong>face1.tex</strong> to <strong>face2.tex</strong> when <strong>yPos&lt;previous.yPos</strong>.</p></td></tr><tr class="even"><td><p>6</p></td><td><p>byte[2]</p></td><td><p>UNK</p></td><td><p>Unknown <strong>face.sp2</strong>: <strong>{0x20,0x36}</strong> on the valid entries. <strong>{0x60,0x36}</strong> on invalid entries.<br />
<strong>cardanm.sp2</strong>: <strong>{0x20,0xB6}</strong> on the valid entries. <strong>{0x00,0x00}</strong> on the invalid entry.</p></td></tr><tr class="odd"><td><p>8</p></td><td><p>UInt16</p></td><td><p>Width</p></td><td><p>Width of entry in pixels Possible this is really a <strong>byte</strong> with a <strong>0 x-offset</strong>.</p></td></tr><tr class="even"><td><p>10</p></td><td><p>UInt16</p></td><td><p>Height</p></td><td><p>Height of entry in pixels Possible this is really a <strong>byte</strong> with a <strong>0 y-offset</strong>.</p></td></tr><tr class="odd"><td><p>12</p></td><td><p>byte[4]</p></td><td><p>UNK</p></td><td><p>Unknown <strong>face.sp2</strong>: <strong>{0x00,0x00,0x8E,0x00}</strong> on most. Last one has all <strong>{0x00}</strong><br />
<strong>cardanm.sp2</strong>: <strong>{0x00,0x00,0xAE,0x00}</strong> on most. Last one has all <strong>{0x00}</strong></p></td></tr></tbody></table>

### End of file

**face.sp2**File ends with **byte\[16\]** of **{0x00}**

### Content of **face1.tex** and **face2.tex**

| Name            | File      | X   | Y   | Width | Height |
|-----------------|-----------|-----|-----|-------|--------|
| Squall Leonhart | face1.tex | 0   | 0   | 32    | 48     |
| Zell Dincht     | face1.tex | 32  | 0   | 32    | 48     |
| Irvine Kinneas  | face1.tex | 64  | 0   | 32    | 48     |
| Quistis Trepe   | face1.tex | 96  | 0   | 32    | 48     |
| Rinoa Heartilly | face1.tex | 128 | 0   | 32    | 48     |
| Selphie Tilmitt | face1.tex | 160 | 0   | 32    | 48     |
| Seifer Almasy   | face1.tex | 192 | 0   | 32    | 48     |
| Edea Kramer     | face1.tex | 224 | 0   | 32    | 48     |
| Laguna Loire    | face1.tex | 0   | 48  | 32    | 48     |
| Kiros Seagill   | face1.tex | 32  | 48  | 32    | 48     |
| Ward Zabac      | face1.tex | 64  | 48  | 32    | 48     |
| Lion            | face1.tex | 128 | 48  | 32    | 48     |
| MiniMog         | face1.tex | 160 | 48  | 32    | 48     |
| Boko            | face1.tex | 192 | 48  | 32    | 48     |
| Angelo          | face1.tex | 224 | 48  | 32    | 48     |
| Quezacotl       | face2.tex | 0   | 0   | 32    | 48     |
| Shiva           | face2.tex | 32  | 0   | 32    | 48     |
| Ifrit           | face2.tex | 64  | 0   | 32    | 48     |
| Siren           | face2.tex | 96  | 0   | 32    | 48     |
| Brothers        | face2.tex | 128 | 0   | 32    | 48     |
| Diablos         | face2.tex | 160 | 0   | 32    | 48     |
| Carbuncle       | face2.tex | 192 | 0   | 32    | 48     |
| Leviathan       | face2.tex | 224 | 0   | 32    | 48     |
| Pandemona       | face2.tex | 0   | 48  | 32    | 48     |
| Cerberus        | face2.tex | 32  | 48  | 32    | 48     |
| Alexander       | face2.tex | 64  | 48  | 32    | 48     |
| Doomtrain       | face2.tex | 96  | 48  | 32    | 48     |
| Bahamut         | face2.tex | 128 | 48  | 32    | 48     |
| Cactuar         | face2.tex | 160 | 48  | 32    | 48     |
| Tonberry        | face2.tex | 192 | 48  | 32    | 48     |
| Eden            | face2.tex | 224 | 48  | 32    | 48     |

There is one blank space in **face1.tex**, I skipped that entry.

### Content of **mc00.tex**-**mc09.tex**

Each level on the [fandom wiki page](https://finalfantasy.fandom.com/wiki/Final_Fantasy_VIII_Triple_Triad_cards)is in the same order of the contents of the tex files. The cardback is always the bottom right of each texture.
