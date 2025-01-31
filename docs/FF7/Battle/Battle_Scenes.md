---
title: Battle_Scenes
---

## Introduction

FF7 keeps each enemy battle configuration is a file called "scene.bin" This file is located in the following directories.

|      PSX Version       |    PC Version     |
|:----------------------:|:-----------------:|
| /DATA/BATTLE/SCENE.BIN | /BATTLE/SCENE.BIN |
|                        |                   |

This file is exactly the same in both versions. This holds all the battle configurations for all enemies encountered in the game.

## Scene.Bin file format

### Overview

The scene.bin file contains 256 gziped files which give us information for all the FF7 monsters. In order to find these files in scene.bin, you have to know that the file is structured with blocks exactly 0x2000 bytes in length. In the first table (scene.bin block), you will see what contains a block. Blocks are concatenated with each other to form the scene.bin file. So if you want to extract data from scene.bin, you'll need to find the correct blocks and to extract the gziped files from it. After that you simply ungzip those files and you'll find 256 files, with a length is 7808 bytes. Known information about those files can be found in the second table (The Data File specification). Because extracting file manually would be a pain, several tools was developed in order to help you. You can use [Scene Reader](http://spinningcone.com/ff/stormmedia/projects/SceneReader.zip) for example, it's a win32 tool to extract and repack scene.bin archive.

Also note, that in [kernel.bin](FF7/Kernel/Kernel.bin "wikilink") there is a look-up table for scene.bin, which tells how many files there are in each section of scene.bin. You need to update it every time you repack the file and something changes. The table is at offset 0x0F1C of the third section of the kernel.bin file. You can use [SceneFix](http://forums.qhimm.com/index.php?topic=7127.0) program, which'll update the table for you.

We have 1024 possible battle numbers: 0 - 1023. Each group of \*4\* Battle Numbers refers to a particular Scene file: for instance, Battles 0-3 refer to File 0 in Scene.bin, Battles 4-7 refer to File 1 in Scene.bin, and so forth.

#### Japanese format

In the japanese scene.bin, ennemies names and attacks names have a size of 16 bytes, instead of 32 bytes.

### General file format

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Offset</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Length</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><p>0x0000</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Pointer to first data file. You must multiply it by 4 to get actual data file offset. If the pointer is equal to FFFFFFFFh then it means that the end of block has been reached.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0004</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Pointer to second data file. You must multiply it by 4 to get actual data file offset. If the pointer is equal to FFFFFFFFh then it means that the end of block has been reached.</p></td>
</tr>
<tr>
<td colspan="3" style="text-align: center;"><p>...</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x003C</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Last pointer, usually it equal FFFFFFFFh.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0040</p></td>
<td style="text-align: center;"><p>4 * (pointer2 - pointer1) bytes</p></td>
<td style="text-align: center;"><p>First data file in block. It's a gziped file.<br />
<em>Note: Sometimes it may finish by 0xFF bytes, because its size must be multiple of 4.</em></p></td>
</tr>
<tr>
<td style="text-align: center;"><p>pointer2 * 4</p></td>
<td style="text-align: center;"><p>4 * (pointer3 - pointer2) bytes</p></td>
<td style="text-align: center;"><p>Second data file in block. It's a gziped file.<br />
<em>Note: Sometimes it may finish by 0xFF bytes, because its size must be multiple of 4.</em></p></td>
</tr>
<tr>
<td colspan="3" style="text-align: center;"><p>...</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>lastpointer * 4</p></td>
<td style="text-align: center;"><p>4 * (2000h - lastpointer) bytes</p></td>
<td style="text-align: center;"><p>Last data file in block.<br />
''Note: There are about 6 to 12 files in each block. Each block finishes by 0xFF bytes, because its length must be 2000h (8192d) bytes.</p></td>
</tr>
</tbody>
</table>

### Data file format

| Offset | Length | Description |
|:--:|:--:|:--:|
| 0x0000 | 2 bytes | Enemy ID 1 |
| 0x0002 | 2 bytes | Enemy ID 2 |
| 0x0004 | 2 bytes | Enemy ID 3 |
| 0x0006 | 2 bytes | Padding (always FFFFh) |
| 0x0008 | 4 \* 20 bytes | Battle Setup (4 records) ([format explanation](#battle-setup-1-format) |
| 0x0058 | 4 \* 48 bytes | Camera Placement Data (4 records) ([format explanation](#camera-placement-data-format) |
| 0x0118 | 6 \* 16 bytes | Battle Formation 1 (6 records) ([format explanation](#battle-formation-data) |
| 0x0178 | 6 \* 16 bytes | Battle Formation 2 (6 records) |
| 0x01E8 | 6 \* 16 bytes | Battle Formation 3 (6 records) |
| 0x0238 | 6 \* 16 bytes | Battle Formation 4 (6 records) |
| 0x0298 | 184 bytes | Enemy Data 1 ([format explanation](#enemy-data-format) |
| 0x0350 | 184 bytes | Enemy Data 2 |
| 0x0408 | 184 bytes | Enemy Data 3 |
| 0x04C0 | 32 \* 28 bytes | Attack Data (32 records) ([format explanation](../Attack_data) |
| 0x0840 | 32 \* 2 bytes | Attack IDs (32 records) |
| 0x0880 | 32 \* 32 bytes | Attack Names (32 records, [in FF Text format](../FF_Text) |
| 0x0C80 | 2 bytes | Formation 1 AI Script Offset |
| 0x0C82 | 2 bytes | Formation 2 AI Script Offset |
| 0x0C84 | 2 bytes | Formation 3 AI Script Offset |
| 0x0C86 | 2 bytes | Formation 4 AI Script Offset |
| 0x0C88 | 0 - 504 bytes | Beginning of Formation AI Data ([format explanation](#ai-data) |
| 0x0E80 | 2 bytes | Enemy 1 AI Offset |
| 0x0E82 | 2 bytes | Enemy 2 AI Offset |
| 0x0E84 | 2 bytes | Enemy 3 AI Offset |
| 0x0E86 | 0 - 4090 bytes | Beginning of AI Data ([format explanation](#ai-data) |

#### Battle Setup 1 format

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Offset</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Length</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><p>0x0000</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p><strong>Battle location, as follows:</strong></p></td>
</tr>
<tr>
<td colspan="2" rowspan="2" style="text-align: center; background: rgb(204,204,255);"><p> </p></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><p>0000h : Blank<br />
0001h : Bizarro Battle - Center<br />
0002h : Grassland<br />
0003h : Mt Nibel<br />
0004h : Forest<br />
0005h : Beach<br />
0006h : Desert<br />
0007h : Snow<br />
0008h : Swamp<br />
0009h : Sector 1 Train Station<br />
000Ah : Reactor 1<br />
000Bh : Reactor 1 Core<br />
000Ch : Reactor 1 Entrance<br />
000Dh : Sector 4 Subway<br />
000Eh : Nibel Caves or AForest Caves<br />
000Fh : Shinra HQ<br />
0010h : Midgar Raid Subway<br />
0011h : Hojo's Lab<br />
0012h : Shinra Elevators<br />
0013h : Shinra Roof<br />
0014h : Midgar Highway<br />
0015h : Wutai Pagoda<br />
0016h : Church<br />
0017h : Coral Valley<br />
0018h : Midgar Slums<br />
0019h : Sector 4 Corridors or Junon Path<br />
001Ah : Sector 4 Gantries or Midgar Underground<br />
001Bh : Sector 7 Support Pillar Stairway<br />
001Ch : Sector 7 Support Pillar Top<br />
001Dh : Sector 8<br />
001Eh : Sewers<br />
001Fh : Mythril Mines<br />
0020h : Northern Crater - Floating Platforms<br />
0021h : Corel Mountain Path<br />
0022h : Junon Beach<br />
0023h : Junon Cargo Ship<br />
0024h : Corel Prison<br />
0025h : Battle Square<br />
0026h : Da Chao - Rapps Battle<br />
0027h : Cid's Backyard<br />
0028h : Final Descent to Sephiroth<br />
0029h : Reactor 5 Entrance<br />
002Ah : Temple of the Ancients - Escher Room<br />
002Bh : Shinra Mansion<br />
002Ch : Junon Airship Dock<br />
002Dh : Whirlwind Maze<br />
002Eh : Junon Underwater Reactor<br />
002Fh : Gongaga Reactor<br />
0030h : Gelnika<br />
0031h : Train Graveyard<br />
0032h : Great Glacier Ice Caves &amp; Gaea Cliffs - Inside<br />
0033h : Sister Ray<br />
0034h : Sister Ray Base<br />
0035h : Forgotten City Altar<br />
0036h : Northern Crater - Initial Descent<br />
0037h : Northern Crater - Hatchery<br />
0038h : Northern Crater - Water Area<br />
0039h : Safer Battle<br />
003Ah : Kalm Flashback - Dragon Battle<br />
003Bh : Junon Underwater Pipe<br />
003Ch : Blank<br />
003Dh : Corel Railway - Canyon<br />
003Eh : Whirlwind Maze - Crater<br />
003Fh : Corel Railway - Rollercoaster<br />
0040h : Wooden Bridge<br />
0041h : Da Chao<br />
0042h : Fort Condor<br />
0043h : Dirt Wasteland<br />
0044h : Bizarro Battle - Right Side<br />
0045h : Bizarro Battle - Left Side<br />
0046h : Jenova*SYNTHESIS Battle<br />
0047h : Corel Train Battle<br />
0048h : Cosmo Canyon<br />
0049h : Caverns of the Gi<br />
004Ah : Nibelheim Mansion Basement<br />
004Bh : Temple of the Ancients - Demons Gate<br />
004Ch : Temple of the Ancients - Mural Room<br />
004Dh : Temple of the Ancients - Clock Passage<br />
004Eh : Final Battle - Sephiroth<br />
004Fh : Jungle<br />
0050h : Ultimate Weapon - Battle on Highwind<br />
0051h : Corel Reactor<br />
0052h : Unused<br />
0053h : Don Corneo's Mansion<br />
0054h : Emerald Weapon Battle<br />
0055h : Reactor 5<br />
0056h : Shinra HQ - Escape<br />
0057h : Ultimate Weapon - Gongaga Reactor<br />
0058h : Corel Prison - Dyne Battle<br />
0059h : Ultimate Weapon - Forest</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0002</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Upon defeat of all opponents in current formation, begin battle with <a href="Battle_scenes#Formation_ID" title="wikilink">Formation ID</a> without ending battle scene</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0004</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Escape Counter</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0006</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Unused/Align 'FF'</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0008</p></td>
<td style="text-align: center;"><p>4 * 2 bytes</p></td>
<td style="text-align: center;"><p><a href="Battle_scenes#Formation_ID" title="wikilink">Formation ID</a> of candidates for next Battle Arena battle. (default of 03E7h)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0010</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Escapable Flag (Along with other flags)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0012</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Battle layout type (normal, ambush, side). 0-8 types.</p></td>
</tr>
<tr>
<td colspan="2" rowspan="10" style="text-align: center; background: rgb(204,204,255);"><p> </p></td>
<td style="text-align: center;"></td>
</tr>
<tr>
<td style="text-align: center;"><p>00 - Normal fight</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>01 - Preemptive</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>02 - Back attack</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>03 - Side attack</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>04 - Attacked from both sides (pincer attack, reverse side attack)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>05 - Another attack from both sides battle (different maybe?)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>06 - Another side attack</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>07 - A third side attack</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>08 - Normal battle that locks you in the front row, change command is disabled</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0013</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Indexed Pre-Battle Camera position</p></td>
</tr>
</tbody>
</table>

#### Camera Placement Data format

48 bytes per Formation

| Offset | Length | Description |
|:--:|:--:|:--:|
| 0x00 | 12 bytes | Primary Battle Idle Camera Position |
|   |  |  |
|  | 0x0 | Camera X Position |
|  | 0x2 | Camera Y Position |
|  | 0x4 | Camera Z Position |
|  | 0x6 | Camera X Direction |
|  | 0x8 | Camera Y Direction |
|  | 0xA | Camera Z Direction |
| 0x0C | 2 \* 12 bytes | Other Camera Positions in the above format referenced in enemies' animations. |
| 0x24 | 12 bytes | Unused/Align 'FF' |

#### Battle Formation Data

4 Possible battle formations per scene, maximum of 6 enemies per battle. Each enemy entry contains the following data:

| Offset | Length | Description |  |
|:--:|:--:|:--:|:--:|
| 0x00 | 2 bytes | Enemy ID |  |
| 0x02 | 2 bytes | position X |  |
| 0x04 | 2 bytes | position Y |  |
| 0x06 | 2 bytes | position Z |  |
| 0x08 | 2 bytes | Row |  |
| 0x0A | 2 bytes | [Binary "Cover flags"](#binary) |  |
| 0x0C | 4 bytes | Initial condition flags. Only last 5 bits are considered. |  |
|  |  | 0x0001 | Visible |
|  |  | 0x0002 | Indicates initial direction facing if players get a side attack. |
|  |  | 0x0004 | Unknown |
|  |  | 0x0008 | Targetable |
|  |  | 0x0010 | Main Script Active |

#### Enemy data format

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Offset</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Length</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center;"><p>0x0000</p></td>
<td style="text-align: center;"><p>32 bytes</p></td>
<td style="text-align: center;"><p>Enemy's name (completed by FFh bytes)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0020</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's level</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0021</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's speed</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0022</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's luck</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0023</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's evade</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0024</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's strength</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0025</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's defense</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0026</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's magic</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0027</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Enemy's magic defense</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0028</p></td>
<td style="text-align: center;"><p>8 bytes</p></td>
<td style="text-align: center;"><p>Element types (8 records):<br />
00h - Fire<br />
01h - Ice<br />
02h - Bolt<br />
03h - Earth<br />
04h - Bio<br />
05h - Gravity<br />
06h - Water<br />
07h - Wind<br />
08h - Holy<br />
09h - Health<br />
0Ah - Cut<br />
0Bh - Hit<br />
0Ch - Punch<br />
0Dh - Shoot<br />
0Eh - Scream<br />
0Fh - HIDDEN<br />
10h-1Fh - No Effect<br />
20h-3Fh - <a href="Status_Effects" title="wikilink">Statuses</a> (Damage done by actions that inflict these statuses will be modified)<br />
FFh - No element</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0030</p></td>
<td style="text-align: center;"><p>8 bytes</p></td>
<td style="text-align: center;"><p>Element rates for elements above, respectively (8 records):<br />
00h - Death<br />
02h - Double Damage<br />
04h - Half Damage<br />
05h - Nullify Damage<br />
06h - Absorb 100%<br />
07h - Full Cure<br />
FFh - Nothing</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0038</p></td>
<td style="text-align: center;"><p>16 bytes</p></td>
<td style="text-align: center;"><p>Action animation index (1 byte each).</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0048</p></td>
<td style="text-align: center;"><p>32 bytes</p></td>
<td style="text-align: center;"><p>Enemy Attack ID's (2 bytes each).</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0x0068</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>32 bytes</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Enemy Attacks <a href="Camera_Movement_Id_List" title="wikilink">Camera Movement Id</a> for single and multiple targets (2 bytes each). If set this will overwrite camera movement set in attack itself.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0088</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Item drop/steal rates.<br />
These are chances to get items listed in next section. 1 byte per item. If the rate is lower than 80h, for e.g. 08h - then this is a drop item and has 8/63 [63 is max] chance for drop. But if rate is higher than 80h, let's say... A0h, then this is an item for steal, and chances for successful steal is A0h - 80h = 20h = 32/63.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x008C</p></td>
<td style="text-align: center;"><p>8 bytes</p></td>
<td style="text-align: center;"><p>This is a list of Item ID's which are described above. 2 bytes per item. FFFFh means no item.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x0094</p></td>
<td style="text-align: center;"><p>6 bytes</p></td>
<td style="text-align: center;"><p>Indexes of up to three attacks (2 bytes each) that enemy can perform while manipulated or berserked</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0x009A</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>2 bytes</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>Unknown data</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x009C</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Enemy's MP</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x009E</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>AP points you receive when you win the battle</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00A0</p></td>
<td style="text-align: center;"><p>2 bytes</p></td>
<td style="text-align: center;"><p>Enemy can be morphed into this item. FFFFh if it can't be morphed into anything.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00A2</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>Multiplier for back damage. damage = damage * 0xXX / 8.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00A3</p></td>
<td style="text-align: center;"><p>1 byte</p></td>
<td style="text-align: center;"><p>align 0xff.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00A4</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Enemy's HP</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00A8</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Exp points you receive when you win the battle</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00AC</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Gil you receive when you win the battle</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00B0</p></td>
<td style="text-align: center;"><p>4 bytes</p></td>
<td style="text-align: center;"><p>Status immunities</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,204);"><p>0x00B4</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>4 bytes</p></td>
<td style="text-align: center; background: rgb(255,255,204);"><p>Unknown [Always FFFFFFFFh]</p></td>
</tr>
</tbody>
</table>

#### Formation ID

Formation ID is an index to a formation within a given scene. It is the scene index bit shifted 2 to the left plus formation index within the scene.

`0 1 2 3 4 5 6 7 8 9 A B C D E F`  
`[ - - - - - - - - - - - - ] [ ]`  
`        scene index         formation index`

For this reason, the Formation ID will not exceed 03FFh.

example: Formation 028Dh bit shift two to the right to get scene

`028D >> 2 = 00A3 (right-most bits are truncated)`

This is Scene 163 Formation Index is just the ID ANDed with 3.

`028D AND 3 = 01`

Formation 1 So this is Formation 1 in scene 163. (SOLDIER:3rd x2)

#### AI Data

This section contains Battle Script that is executed before or/and during every fight. Every enemy has it's own script, and this script is divided to a number of sections. Each script starts with 32 bytes of header that are divided into 16 parts representing 16 script types. The 2-byte number in any section is an offset relative to the beginning of this 32 byte block that tells the script reader where the script starts for that script type.

| Offset |   Script Type    |
|:------:|:----------------:|
|  0x00  |    Initialize    |
|  0x02  |       Main       |
|  0x04  | General Counter  |
|  0x06  |  Death Counter   |
|  0x08  | Physical Counter |
|  0x0A  | Magical Counter  |
|  0x0C  |    Battle End    |
|  0x0E  | Pre-Action Setup |
|  0x10  |  Custom Event 1  |
|  0x12  |  Custom Event 2  |
|  0x14  |  Custom Event 3  |
|  0x16  |  Custom Event 4  |
|  0x18  |  Custom Event 5  |
|  0x1A  |  Custom Event 6  |
|  0x1C  |  Custom Event 7  |
|  0x1E  |  Custom Event 8  |

Its structure and opcodes are described [here](Battle_Scenes/Battle_Script).

NOTES:

- A monster's total AI size will always be an even number of bytes. If the actual scripts are an odd number, a single NULL (FFh) will be placed before the next monster's AI header (may not be required).
- Battle begins after all characters' Initialize scripts have been run (Players first, then enemies, then formation).
- The only character with "Battle End" is in Cloud's AI. It's meant to lower the character's Love Points with him if he lets them die or he dies with them in the party (not sure which).
- Pre-Action Event occurs on all battle participants prior to any actions performed by any participant regardless of actor or target. This includes all executed 92 commands that have a command index of less than 21h. If any 92 commands are called in this section, the command that caused this script to run has priority.
- The Custom Event sections are not called by any event. They only occur if they are called with the 92 command.

`60 22 <- command index "Run script"`  
`60 0X <- where X is the script section in hex (eg. X = 8 would call Custom Event 1 since it is script id 08`  
`         [not to be confused with offset])`  
`92`

- Custom Event 8 is only used on Mystery Ninja (all), Ultimate Weapons in location other than above Cosmo Canyon, Safer Sephiroth, and the final "showdown" between Cloud and Sephiroth. These characters have scripts on them that do not remove them from battle when they are defeated.
- Custom Events 1-7 may not work. (not thoroughly tested)
- The order of scripts executed:

:\*Beginning of battle

  
  
Pre-Battle (all participants)

#### Binary "Cover Flags"

These flags are used in conjunction with row to determine if a target can be selected as the target of a **short-range attack**. The determination of this is worked out in this way: An enemy exists in row 1 and another in row 2. If the enemy in row 1 shares a cover flag with the enemy in row 2 then the enemy in row 2 cannot be targeted until all enemies in row 1 that share a cover flag with the row 2 enemy is defeated. It works like this. Two active enemies exist, A and B.

`If ((B's row > A's row) and (B's cover flags AND A's cover flags) > 0) then enemy B cannot be targeted by short-range attacks.`

for any enemies A and B.  
Example:  
Consider the Battery Cap x6 battle in the forest between Nibelheim and Rocket Town. Their cover flags (in binary) are:

`Row 1:       00100`  
`Row 2:    00110 01100`  
`Row 3: 00011 00100 11000`

The battery caps in row 2 cannot be targeted by a short-range attack until the one in row 1 has been defeated because they share the 0x4 cover flag. Once row 1 has been cleared:

`Row 2:    00110 01100`  
`Row 3: 00011 00100 11000`

The battery cap on left in row 2 covers the left two in row 3 because it shares flag 0x4 with the one in the middle and flag 0x2 with the one on the far left. As long as it is active these in row 3 cannot be targeted. Similarly, the battery cap on the right in row 2 shares the 0x4 flag with the middle of row 3 and the 0x8 flag with the far right of row 3 so these cannot be targeted until the right side of row 2 is defeated.  
It is also necessary to note that because row 1 does not share any flags with the extreme right and left of row 3, they can be targeted if the corresponding enemy in row 2 is defeated even if the row 1 enemy is still active.  
Also of note is that enemies in the same row that share cover flags are not considered.  
Only the first five bits may be considered even though the value is stored as a word.  

## Useful downloads

There are few programs written that will help you edit scene.bin file:

- [Scene Reader](http://spinningcone.com/ff/stormmedia/projects/SceneReader.zip)
- [SceneEdit](http://www.subfan.pl/mav/SceneEdit.zip)
- [Scenester](http://aaronserv.dyndns.org/hosting/qhimmwiki/ramza_scenester_0.5.zip)
- [Proud Clod](http://forums.qhimm.com/index.php?topic=8481.0)
