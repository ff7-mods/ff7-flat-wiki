---
title: FF7:CC
---

<small> My first ever wiki entry! Apologies for any inconsistencies etc. </small>

Information confirmed by Quimm forum members (by MrAdults in particular), HUGE props to them for their support.

Last updated: [Koral](User:Koral)

  

## Final Fantasy 7: Crisis Core

**Crisis Core: Final Fantasy VII** is an action role-playing game developed by Square Enix for the PlayStation Portable. The game is a prequel to Final Fantasy VII and is also the sixth installment in the Compilation of Final Fantasy VII. Production was overseen by Yoshinori Kitase, the director of the original Final Fantasy VII, with Hajime Tabata as the game's director and Tetsuya Nomura as the game's character designer.

The game mainly focuses around Zack Fair, a 2nd Class SOLDIER, and the events leading up to his destined demise. He meets many of the Final Fantasy VII characters, including Cloud Strife and Aerith Gainsborough, with whom he develops strong bonds. The game's storyline takes the player from the war with the Wutai to the events at Nibelheim, and right up to the time just before the Final Fantasy VII beginning. Some of the missing events or plot holes from Nibelheim and afterwards are explained in the animated feature, Last Order: Final Fantasy VII.

The game's tagline is "Men cry not for themselves, but for their comrades", a quote from LOVELESS.

  

## Data Retreival and Organisation

Extracting the Data Files using the [FF7CC Data Extractor](FF7:CC#Tools) results in 8725 .RAW files. This file extension does not represent any specific file format and was used to clarify the "raw" nature of the data.

Every RAW file can be categorised into specific File-Format Types by reading the first 8-bytes of the file.

There are specific character sequences of these bytes which can be used to accuratly categorise the file and determine what kind of data it contains (more details on the various File Format Types can be found in next section).

The RAW files themselves appear to be organised into clusters of same Types, or of similar function:

  

| RAW Files | Type \[bytes within 8-byte header\] | Description |
|----|----|----|
| 00000 - 00005 | ? (various unknown) | Possibly misc system files, or events occuring at game boot-up |
| 00006 - 00062 | **[PSMF](FF7:CC/Video_Formats#PSMF_Format)** | \* PSP format Video files |
| 00063 - 01349 | **[RIFF](FF7:CC/Audio_Formats#RIFF_Format)** | \* Audio files, usually voiced dialogues |
| 01350 - 01417 | **[SSCF](FF7:CC/Audio_Formats#SSCF_Format)** | \* Audio files, usually background music |
| 01418 - 01442 | **IMG**, ? (various unknown) | Possibly Menu and DMW related stuff, IMG are HUD or sprite images |
| 01443 - 01445 | **PNG** | \* standard PNG images |
| 01446 | ? | seems to contain a list of Locations and Mission Titles |
| 01447 | ? | Contains a long list of character names, probably used when talking to NPC's etc |
| 01448 - 01455 | ? | Maybe mesh data |
| 01456 | **MBD** |  |
| 01457 - 02011 | **[GT](FF7:CC/Image_Formats#GT_Format)**, **ATEL** | \* Story progression and Event data, GT are Chapter-End Images, ATEL are events and dialogue script data |
| 02012 - 02161 | **[! (exp TYPE-1)](FF7:CC/Model_Formats#exp_TYPE-1_Models) | \* Static Mesh Models: Location Map Models |
| 02162 - 02457 | **[! (exp TYPE-0)](FF7:CC/Model_Formats#exp_TYPE-0_Models "wikilink")**, **[TEX](FF7:CC/Image_Formats#TEX_Format) | \* Skinned Animated Models: Characters, Monsters, NPCs and Event-Specific Models |
| 02458 - 03352 | ? (various unknown) | Tiny files, no common header, no ascii info visible. No idea. |
| 03353 - 08538 | ? (various unknown) | no common header, fairly small files \<500 kb. Ditto |
| 08539 - 08622 | **MOT**, **SSCF** | Monster / Battle / Boss data: maybe "file-names", Event Scripts, Boss Battle scripts, Monster behaviour or something else. |
| 08623 - 08627 | **zack**, **ATEL** | Possibly Zack's specific battle data |
| 08628 - 08690 | **MAGIC** | Zack's Battle commands, actions and animations |
| 08671 - 08706 | ? (various unknown) | tiny files |
| 08707 - 08725 | **[PSMF](FF7:CC/Video_Formats#PSMF_Format)** | \* more Videos |

  
*\** - These files are understood enough to view and/or extract their contents.

.

## Data File Formats

Overview of the different types of data files and what they contain. List shows the data types currently known.

### [Game Events and Scripts](FF7:CC/Game_Event_Files)

- [ATEL](FF7:CC/File_Types) Files
- [MBD](FF7:CC/File_Types) Files

### [Sprites, Images and Texture Data](FF7:CC/Image_Formats)

- [\[IMG](FF7:CC/Image_Formats#IMG_Format)\] Files
- [\[TEX](FF7:CC/Image_Formats#TEX_Format)\] Files
- [\[GT](FF7:CC/Image_Formats#GT_Format)\] Files

### [Audio Data](FF7:CC/Audio_Formats)

- [RIFF](FF7:CC/Audio_Formats#RIFF_Format) Files
- [SSCF](FF7:CC/Audio_Formats#SSCF_Format) Files

### [Video Data](FF7:CC/Video_Formats)

- [\[PSMF](FF7:CC/Video_Formats#PSMF_Format)\]

### [Models and Mesh Geometry](FF7:CC/Model_Formats)

- [\[!](FF7:CC/Model_Formats#exp_Format) Model\] Files

### [Battles and Monsters](FF7:CC/Battle_and_Monster_Data)

### [Materia](FF7:CC/Materia_Data)

## Differences between Japanese, US and PAL versions

Japanese one has two diffs. First of all, japanese version has more audio files than english one (It was confirmed while making an undub of english one ;P) and has changed Minerva statue model. In japanese version it looked too much like cathlic Maria so in US release they made completly new model for it.

<small>-[Aurenasek116](http://forums.qhimm.com/index.php?action=profile;u=4603)</small>

.

## Miscelenous Findings

Anything interesting or weird worth noting.

### Debug Menu

File "00000.RAW" contains an interesting menu-dialogue where the player is shown a menu listing the names of various FF7CC developers, and a Moogle apparantly narrating the choice, and asking for user input.

Here is a copy of the precise text:

`<TEXT>`  
` Where do you want to go?`  
`<M-CHOICE>`  
` Battle`  
` Ms. Ishibashi`  
` Mr. Oka`  
` Mr. Kitase`  
` Mr. Kunikata`  
` Mr. Shindo`  
` Mr. Terada`  
` Mr. Maeda`  
` Moriya kun`  
`<END>`

Nothing else is known about this menu, as it does not appear during normal gameplay, and currently there is no way to initilise it.

Someone has been able to iniate this menu somehow, screenshots of which were posted [here](http://forums.qhimm.com/index.php?topic=8163.msg100101#msg100101).

  

### Hidden Event-Dialogues Menu and/or Materia

Contained within all ATEL files are the following Menu-Dialogue texts.

- The "Kupo!" suggests a Moogle narrating, possibly related to the Debug-Menu.
- The "Materia has leveled up!" suggests maybe a hidden Materia was used to initiate this Menu.
- "Gondola" and "Elevator" may be references to the side-quest during the mission in Junon.
- It is currently unknown why these texts appear within ALL \[ATEL\] files, the only possibility being that they serve as interfaces to the Debug-Menu, which has now been confirmed to exist.

`<TEXT>`  
` Materia has leveled up!`  
`<END>`  
  
`<TEXT>`  
` Nothing more to do, kupo!`  
`<END>`  
  
`<TEXT>`  
` Load failed.`  
`<END>`  
  
`<TEXT>`  
` Load canceled.`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Open`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Push`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Go up`  
`<END>`  
  
`<TEXT>`  
`<TEXT>`  
` <CHOICE1>: Go down`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Use elevator`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Use gondola`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Rotate`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Read`  
`<END>`  
  
`<TEXT>`  
` <CHOICE1>: Move`  
`<END>`  
  
`<TEXT>`  
`<TEXT>`  
` <CHOICE1>: Examine`  
`<END>`

  

## Tools

### Viewers / Extractors

| Project Name | Description | Author | Version / Status | Links |
|----|----|----|----|----|
| FF7CC Data Extractor | Extracts the Data-Files from the FF7CC PKG and FSE files stored on PSP Media | [G](http://forums.qhimm.com/index.php?action=profile;u=3309) | 1.0 | [Forum](http://forums.qhimm.com/index.php?topic=7053.0), [Binary](http://superg.org.ua/ff7cc_extractor.tar.bz2), [Mirror](http://www.mediafire.com/?nwm24zynjmk) |
| RINOA Model Viewer | Suppors some FF7CC Data-Files, such as Game-Scripts, and Models, also has an OBJ mesh exporter | [Koral](http://forums.qhimm.com/index.php?action=profile;u=5116) | 0.51 | [Forum](http://forums.qhimm.com/index.php?topic=8451.0), [Binary](http://www.mediafire.com/?jzqmgzmoq4m) |
| \[!\]-Model Extractor (aka mesh2rdm) | Powerful file viewer and extractor, exporting out skin-weighted models from !-Models to OBJ or SMD | [MrAdults](http://forums.qhimm.com/index.php?action=profile;u=3607) | v1.81 | [Website](http://www.richwhitehouse.com/index.php?postid=30) |
| MarC's HiMD Renderer | Convert FF7CC \[SSCF\] audio-files to wav, mp3, ogg or pcm <small>( -- [aljnx](http://forums.qhimm.com/index.php?action=profile;u=4675))</small> | MarC | 0.54 | [Website](http://www.marcnetsystem.co.uk/) |
| CC Plugin for Xpert2 | Allows Xpert2 to extract and re-pack the Data-files from and to FF7CC PKG and FSE files stored on PSP Media <small>( -- [Karlislie](http://forums.qhimm.com/index.php?action=profile;u=5343))</small> |  |  | [Download](http://www.mediafire.com/download.php?j5tnduxoemd), [Mirror](http://www.mediafire.com/?hmbmdzdmwki) |
