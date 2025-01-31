---
title: Low_level_libraries
---

## PC to PSX comparison

The files and data formats used in the PSX version of FF7 and it's PC port are conceptually the same thing, and accomplish the same tasks. That being said, they both have wildly different formats, both of which were derived from a third original format that is also somewhat different to the first two.

The original PSX FF7 was created in part using Sony's Psy-Q development library. This library uses common formats that are "native" to the PSX. Often, a toolkit was used to convert common development-based formats, such as a TGA bitmap or a palleted GIF file, to something a little more suited to Psy-Q, which would be a [TIM file](../../PSX/TIM_format).

During the porting process to the PC, some of the original artwork (and artists for that matter) were no longer available. This resulted in the port team having to use the Psy-Q versions of many files, which were ill suited for the PC architecture. In our example, the [TIM file](../../PSX/TIM_format) was converted to a TEX file, which would be manipulated in the PC's video memory a little more efficiently. Sometimes the original artwork was available, such as the pictures of the characters within the menu, or the original MIDI files. Most often times it was not.

To make things a little more confusing, both systems also archive their data files in different ways, making the extraction and rendering of each file a bit of a bear. For the most part the data within each file is the same thing, just a little switched around. Here, we will cover the more generic files first, and then common files used in each module.

## Data Archives

To save space, quicken access time, and to obfuscate the file structure a little, most of the data files are stored in some kind of archive format. The archives remove such useful items as subdirectories and logical data placement. There is no real "native" format these are based on.

### BIN archive data format

The BIN format comes as two different types. They both have the same extension, so one must open the file to see which format is which. They are best described as BIN Types and BIN-GZIP types.

#### BIN Type Archives

These are uncompressed archives. The header is 4 bytes long and gives the length of the file without the header and then the data beyond that.

#### BIN-GZIP Type Archives

Unless otherwise noted, these have a 6 byte header. After this are many gziped sections concatenated together.

| Offset | Length  | Description                                        |
|--------|---------|----------------------------------------------------|
| 0x0000 | 2 bytes | Length of gzipped section 1                        |
| 0x0002 | 2 bytes | Length of ungzipped section 1                      |
| 0x0004 | 2 bytes | File type\*                                        |
| 0x0006 | Varies  | \[0x1F8B080000000000...\] - Gzip header 1 and data |
| Varies | 2 bytes | Length of gzipped section 2                        |
| Varies | 2 bytes | Length of ungzipped section 2                      |
| Varies | 2 bytes | File type\*                                        |
| Varies | Varies  | \[0x1F8B080000000000...\] - Gzip header 2 and data |
| ...    |         |                                                    |

  
*\** This particular value might be ignored by the whatever method is decompressing these archive types. Within archives it declares that the compressed file is a particular type. These values seem to be unique to the particular archive that is being opened and is not consistent between archives.

Example 1: Within the [KERNEL.BIN](Kernel.bin) the first nine files are all different data sets so are numbered sequentially 0-8. All remaining files are text types and get labeled as type 9.  
Example 2: Within the WINDOW.BIN file there are three files. The first two are type "0" and are textures. The third file is type "1" and not a texture.

### LZS Archives

The [LZS format](FF7/LZS_format "wikilink") is used throughout the PSX version of Final Fantasy 7, often ending with the .lzs extension. LZS itself stands for Lempel-Ziv-Shannon-Fano, Statistical plus Arithmetic. It was originally developed by [Professor Haruhiko Okumura](http://oku.edu.mie-u.ac.jp/~okumura/index-e.html) based on the work of [Abraham Lempel](http://www.hpl.hp.com/about/bios/abraham_lempel.html) and [Jacob Ziv](http://www.marconifoundation.org/pages/dynamic/fellows/fellow_details.php?roster_id=23).

### LGP Archives

The LGP file format is only used for the PC port of Final Fantasy 7. These are large "volume" type archives that hold most of the game's data. These archives can hold thousands of files. Unlike the BIN or LZS type files, this archive does reference the data within it by filename. Its file format is explained [here](../LGP_format).

## Textures

A texture is just a picture that is placed into video memory. It is later manipulated by the engine and displayed on the screen. The native format of a texture was the Psy-Q [TIM](../../PSX/TIM_format). This is used as the native format for the PSX version as well, with a few caveats explained below. The file can hold multiple color look up tables. This was one of the reasons why a video card on the PC that could do palleted data at high color depths was needed.

### TIM texture data format for PSX

The [TIM files](PSX/TIM_format "wikilink") are found both on raw format and also within several archives, including [BIN](FF7/Kernel/Low_level_libraries#BIN_archive_data_format "wikilink"), [LZS](FF7/Kernel/Low_level_libraries#LZS_Archives "wikilink"), or even MNU. The format proper has the ability to contain 24 bit bitmaps, but is not used in FF7. The format was created because the PSX does not have direct access to it's VRAM, and must go through the [GPU](PSX/GPU "wikilink") for any graphic access. [A TIM file](../../PSX/TIM_format) is a clean way to load a texture and color look up table into VRAM.

### TEX texture data format for the PC

TEX files are texture files for the PC. The format for these files are located [here](../TEX_format).

## File formats for 3D models

During the development process, 3D models contain a good deal of information needed by the artist every time they save or load the model. When the model is finished, it is often exported and broken up into smaller files with many unneeded attributes stripped from them. When the models for FF7 were created, they were exported into Psy-Q's 3D library formats. These include [resource data (.RSD)](PSX/RSD "wikilink"), polygon data (.PLY), polygon groups (.GRP), materials (.MAT), [textures (.TIM)](PSX/TIM_file "wikilink"), [skeletal hierarchy (.HRC)](../../PSX/HRC).

The models are handled differently between modules. The models in the "battle" modules have a different animation system than the field models. When the models were converted to the PC version, they were taken from the Psy-Q formats to a more PC-friendly one. Some are even the original, uncompiled, Psy-Q files.

### Model formats for PSX

The Playstation models are stored in the following directories, \ENEMY1 \ENEMY2 \ENEMY3 \ENEMY4 \ENEMY5 \ENEMY6 (battle models), \FIELD (field models and field character models), \MAGIC (Summon magic), and \STAGE1 \STAGE2 (battle scenes). Battle model names for special characters and party characters are stored in \ENEMY6, all models of this type end in an .LZS extension. The same goes with summon magic used they are stored with there animations etc. in \MAGIC with a .LZS extension. The only exception to this extension is the FIELD models, which use the extensions BSX and BCX for scene models and character models respectively. The [Playstation battle model format](FF7/Playstation_Battle_Model_Format "wikilink"), is different than the [Playstation field model format](FF7/Field/BSX "wikilink"), also the [FF7/Playstation battle scene format](FF7/Playstation_battle_scene_format "wikilink"), is similiar but not identical to the [Playstation battle model format](FF7/Playstation_Battle_Model_Format "wikilink"). The [Playstation magic model](../Playstation_magic_model) format is a work in progress.

### Model Formats for PC

The PC models are stored in the LGP files in the /DATA directory. The names for the models were obfuscated a little. The data can be found in the [Hierarchy files (.HRC)](PSX/HRC "wikilink"), [Resource data files (.RSD)](PSX/RSD "wikilink"), and [Polygon files (.P)](../P).
