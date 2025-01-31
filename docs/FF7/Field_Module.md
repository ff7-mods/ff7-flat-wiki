---
title: Field_Module
---

## Important Files

|  PSX Version  |       PC Version       |
|:-------------:|:----------------------:|
| /FIELD/\*.DAT | /DATA/FIELD/FLEVEL.LGP |
| /FIELD/\*.MIM | /DATA/FIELD/FLEVEL.LGP |
| /FIELD/\*.BSX |                        |
| /FIELD/\*.BCX |  /DATA/FIELD/CHAR.LGP  |

## Field Overview

The field module is the core of the game to which everything else is spawned. It is tied very closely with the kernel and contains many low-level calls to it. The field system also contains a self-contained bytecode language called commonly called "Field Script". The field module is responsible for the following:

- The loading and parsing of the field files
- The display of the 2D background ands related special effects
- The display of 3D elements in the field such as the camera, perspective and and entities
- The running of the Field Script to display events and to get user input
- The on-demand loading of other modules when needed

The Field module loads modular "Field Files". In the PC version, the Field File is a single file with nine sections. In the PSX version, there are three files with the same name but with different extensions that do the same thing. The three files are MIM (Mutiple Image Maps, or the backgrounds), DAT (Field Script Data), and BSX (3D data).

![Snapshot of the PSX&#39;s VRAM demonstrating the background field files in various stages of assembly]({{site.baseurl}}/assets/Field_BackgroundVRAM.jpg)

The backgrounds are actually 16x16 blocks that are loaded into VRAM and then assembled into the video buffer every frame. The system allows for layers to obscure the 3D entities using a simple painter's algorithm.

In this particular field file, there are six cached sections of background data. Also notice the bright green patches that don't show up in in the video buffer. This was to show where a lower layer of 2D data was to be covered by a higher layer. The bright green is for debug purposes. During development, if any bright green showed up, it meant that your upper layer had a "hole" in it that a 3D entity could be seen through.

When the PSX version of FF7 is ran in higher resolutions via emulation with texture filtering on, often the lower layers will "bleed" outside the upper layer and make artifacts. This was also the reason why the field files were not re-rendered for the PC version of the game. It would of required "re-cutting" the layers again in the higher resolution.

Another last thing to note is in the middle of the bottom texture cache there are a sea of eyes. These blink at random times and reflect the random blinking of the characters in the game.

  

## Field Format (PC)

### General PC Field File Format

Field files are always found in FLEVEL.LGP. They are always [LZS](LZS_format) compressed.

The first two bytes of each (decompressed) field file are blank (zero). The next four bytes is an integer indicating how many sections are present in the file. Then a number of 4-byte integers follow, giving the starting offset for each section.

All field files should contain 9 sections; it's what FF7 expects.

### PC Field File Header

<table>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Size</p></th>
<th><p>Description</p></th>
<th><p>Section Data</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x00</p></td>
<td><p>2 bytes</p></td>
<td><p>Blank</p></td>
<td><p>Always 0x00</p></td>
</tr>
<tr>
<td><p>0x02</p></td>
<td><p>4 bytes</p></td>
<td><p>Number of Sections</p></td>
<td><p>Always 0x0009</p></td>
</tr>
<tr>
<td><p>0x06</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 1</p></td>
<td><p><a href="Field/Field_Script" title="wikilink">Field Script &amp; Dialog</a></p></td>
</tr>
<tr>
<td><p>0x0A</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 2</p></td>
<td><p><a href="Field/Camera_Matrix" title="wikilink">Camera Matrix</a></p></td>
</tr>
<tr>
<td><p>0x0E</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 3</p></td>
<td><p><a href="Field/Model_Loader" title="wikilink">Model Loader</a></p></td>
</tr>
<tr>
<td><p>0x12</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 4</p></td>
<td><p><a href="Field/Palette" title="wikilink">Palette</a></p></td>
</tr>
<tr>
<td><p>0x16</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 5</p></td>
<td><p><a href="Field/Walkmesh" title="wikilink">Walkmesh</a></p></td>
</tr>
<tr>
<td><p>0x1A</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 6</p></td>
<td><p><a href="Field_Module/DAT/Tile_Map" title="wikilink">TileMap</a> (Unused)</p></td>
</tr>
<tr>
<td><p>0x1E</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 7</p></td>
<td><p><a href="Field/Encounter" title="wikilink">Encounter</a></p></td>
</tr>
<tr>
<td><p>0x22</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 8</p></td>
<td><p><a href="Field/Triggers" title="wikilink">Triggers</a></p></td>
</tr>
<tr>
<td><p>0x26</p></td>
<td><p>4 bytes</p></td>
<td><p>Pointer to Section 9</p></td>
<td><p><a href="Field/Background" title="wikilink">Background</a></p></td>
</tr>
<tr>
<td><p>0x2A</p></td>
<td><p>4 bytes</p></td>
<td><p>Where Pointer to Section 1 points to</p></td>
<td><p>Length of Section 1</p></td>
</tr>
<tr>
<td><p>0x2E</p></td>
<td><p>Varies</p></td>
<td><p>Start of Section 1 data. Continues for the<br />
number of bytes specified in Section Length</p></td>
<td><p><em>See links above</em></p></td>
</tr>
</tbody>
</table>

Each section generally starts with a four byte integer indicating the length of the section. You could just work this out by comparing offsets (how much space until the next section/end of file, etc) but FF7 stores the length at the start of the section anyway. After that the actual data follows. So the first bit of data for a section is actually 4 bytes after the point given in the section header (since the first four bytes are actually the length marker).

To examine each section, please navigate using the links in the table above. For sections 3 and 8, there is some information on [the forum](http://forums.qhimm.com/index.php?topic=4358.msg58674#msg58674).

## Field Format (PS1)

### PSX DAT Format

The PSX script is contained in the DAT file, it is compressed with [LZS compression](LZS_format). The first 4 bytes of the compressed DAT file is the length of the compressed data starting at address 0x4.

The header for the DAT file (after it is decompressed), is 28 bytes in size (they are used in the PSX, it's a list of 7 long word values which point to locations in PSX RAM). So for each of these sections are addressable by taking the first memory location subtracting it and adding 28.

There are 7 sections each corresponding to the first 7 memory locations at the beginning of the file.

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(0,255,0);"><p>Section Name</p></th>
<th style="text-align: center; background: rgb(0,255,0);"><p>Section Information</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Script" title="wikilink">Script</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Contains conversations, save point interaction etc.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Walkmesh" title="wikilink">Walkmesh</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Contains walkmesh triangles and access info.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field_Module/DAT/Tile_Map" title="wikilink">TileMap</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Contains the information for the background, animation,<br />
and static scene objects.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Camera_Matrix" title="wikilink">Camera_Matrix</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Contains camera info.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Triggers" title="wikilink">Triggers</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Contains triggers, singles, gateways and so on.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Encounter" title="wikilink">Encounter</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Battle Encounter information for location.</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(200,255,200);"><p><a href="Field/Models" title="wikilink">Models</a></p></td>
<td style="text-align: center; background: rgb(200,255,200);"><p>Some info about field models.</p></td>
</tr>
</tbody>
</table>

### PSX MIM Format

Part of the PSX background data is contained in the [MIM file](FF7/Field/MIMfile "wikilink"), it is compressed with [LZS compression](LZS_format). It consists of palettes (256 color ones) and screen blocks. No data for locating the blocks on the screen is in this file. The MIM file is a truncated TIM file and contains the normal clut location height and width information. This information is directly loaded into the PSX video ram to be decoded by the field module.

### PSX BSX Format

The Field models are contained in the [BSX file](FF7/Field/BSX "wikilink"), it is compressed with [LZS compression](FF7/LZS_format "wikilink"). [FIELD.TDB](Field/FIELD.TDB) contains the textures for these models.

### PSX BCX Format

The individual characters' field models are stored in [BCX files](FF7/Field/BCX "wikilink"). Their textures are also in [FIELD.TDB](FF7/Field/FIELD.TDB "wikilink"); they are compressed with [LZS compression](LZS_format).

## Event Scripting

Event scripting is handled via a series of script commands and entities spawned for the event. The exception to this is the battle event scripting. This is actually a little bit different. Please refer to the [Field Script](Field/Script) for more information.

## Script commands

The event scripting language for FF7 has 246 commands that have a wide array of functions. For a complete listing of the commands, opcodes, arguments and descriptions, please refer to the [opcodes](Field/Script/Opcodes) section.

## Movies

Movies in FF7 are actually triggered from the [Field Script](Field/Script). The [F8 PMVIE](FF7/Field/Script/Opcodes/F8_PMVIE "wikilink") opcode is first used to set the movie for which the [F9 MOVIE](FF7/Field/Script/Opcodes/F9_MOVIE "wikilink") opcode is used to play. It is important to remember the MOVIE ID may vary in the PS1 versionn depending on what disc you are on. The PC movies were encoded using the DUCK (goose?) format and are AVI video files.

The PS1 movies were encoded using FMV Motion JPEG video files, for the playstation. These files cannot be decode or read directly from the CD disc media because of the Mode 2 format of the files. The files are encoded using ISO Mode 2 which means the sectors are 2302 bytes in length instead of 2048. The video files have interleaved audio (ADPCM format), between video frames and are 320x224 15fps. Video files that have no audio with it actually has empty sectors of space between video frames to prevent the extremely timing sensitive MDEC decoder in the playstation from locking up.

[Cyberman](../User:Cyberman)

## The 3D Overlay

## Data Organization

## "A" Field Animation Files for PC by [Mirex](User:Mirex "wikilink") (Edits by [Aali](../User:Aali)

Each animation file holds one character animation ( run, walk or some other). Some characters have more animation files. Animation is set of frames, in each frame are stored bone rotations.

-- animation file contents --

| Name   | Size in bytes         |
|--------|-----------------------|
| header | 36                    |
| frames | frames_count \* frame |

-- one frame, size is (bones \* 12 + 12 + 12) --

| Name             | Size                                  |
|------------------|---------------------------------------|
| root rotation    | 12 = 3 floats                         |
| root translation | 12 = 3 floats                         |
| rotations        | bones \* 12 bytes = bones \* 3 floats |

header structure, 36 bytes

`struct {`  
`    unsigned int32 version;`  
`    unsigned int32 frames_count;`  
`    unsigned int32 bones_count;`  
`    unsigned char rotation_order[3];`  
`    unsigned char unused;`  
`    unsigned int32 runtime_data[5];`  
`} anim_head;`

I understand only two values from the header, 'frames_count' which is number of animation frames and 'bones_count' which is suprisingly number of animated bones.

*version should always be 1 or FF7 will not load the file*

*rotation order determines in which order rotations are applied, 0 means alpha rotation, 1 beta rotation and 2 gamma rotation.*

*runtime data has no meaning in the animation file and is discarded on load*

If you want to load all possible animations for the model (even animations of different models) then check if animation file has same number of bones as current model.

Frame starts with the root rotations and root translations, followed by rotations for each bone. Rotations are stored as 3 floats (float is 4byte floating-point number).
