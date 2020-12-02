---
title: FF7:CC
---

[Home](/Main%20Page.md) > FF7:CC

<small> My first ever wiki entry! Apologies for any inconsistencies etc.
</small>

Information confirmed by Quimm forum members (by MrAdults in
particular), HUGE props to them for their support.

Last updated: [Koral][] 19:15, 18 May 2009 (EDT)

  

## Final Fantasy 7: Crisis Core

**Crisis Core: Final Fantasy VII** is an action role-playing game
developed by Square Enix for the PlayStation Portable. The game is a
prequel to Final Fantasy VII and is also the sixth installment in the
Compilation of Final Fantasy VII. Production was overseen by Yoshinori
Kitase, the director of the original Final Fantasy VII, with Hajime
Tabata as the game's director and Tetsuya Nomura as the game's character
designer.

The game mainly focuses around Zack Fair, a 2nd Class SOLDIER, and the
events leading up to his destined demise. He meets many of the Final
Fantasy VII characters, including Cloud Strife and Aerith Gainsborough,
with whom he develops strong bonds. The game's storyline takes the
player from the war with the Wutai to the events at Nibelheim, and right
up to the time just before the Final Fantasy VII beginning. Some of the
missing events or plot holes from Nibelheim and afterwards are explained
in the animated feature, Last Order: Final Fantasy VII.

The game's tagline is "Men cry not for themselves, but for their
comrades", a quote from LOVELESS.

  

## Data Retreival and Organisation

Extracting the Data Files using the [FF7CC Data Extractor][] results in
8725 .RAW files. This file extension does not represent any specific
file format and was used to clarify the "raw" nature of the data.

Every RAW file can be categorised into specific File-Format Types by
reading the first 8-bytes of the file.

There are specific character sequences of these bytes which can be used
to accuratly categorise the file and determine what kind of data it
contains (more details on the various File Format Types can be found in
next section).

The RAW files themselves appear to be organised into clusters of same
Types, or of similar function:

  

| RAW Files     | Type \[bytes within 8-byte header\]                              | Description                                                                                                                |
|---------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| 00000 - 00005 | ? (various unknown)                                              | Possibly misc system files, or events occuring at game boot-up                                                             |
| 00006 - 00062 | **[PSMF][]**                                                     | \* PSP format Video files                                                                                                  |
| 00063 - 01349 | **[RIFF][]**                                                     | \* Audio files, usually voiced dialogues                                                                                   |
| 01350 - 01417 | **[SSCF][]**                                                     | \* Audio files, usually background music                                                                                   |
| 01418 - 01442 | **IMG**, ? (various unknown)                                     | Possibly Menu and DMW related stuff, IMG are HUD or sprite images                                                          |
| 01443 - 01445 | **PNG**                                                          | \* standard PNG images                                                                                                     |
| 01446         | ?                                                                | seems to contain a list of Locations and Mission Titles                                                                    |
| 01447         | ?                                                                | Contains a long list of character names, probably used when talking to NPC's etc                                           |
| 01448 - 01455 | ?                                                                | Maybe mesh data                                                                                                            |
| 01456         | **MBD**                                                          |                                                                                                                            |
| 01457 - 02011 | **[GT][]**, **ATEL**                                             | \* Story progression and Event data, GT are Chapter-End Images, ATEL are events and dialogue script data                   |
| 02012 - 02161 | **[! (exp TYPE-1)][]**, **&&** (double-and), ? (various unknown) | \* Static Mesh Models: Location Map Models                                                                                 |
| 02162 - 02457 | **[! (exp TYPE-0)][]**, **[TEX][]** (embedded textures)          | \* Skinned Animated Models: Characters, Monsters, NPCs and Event-Specific Models                                           |
| 02458 - 03352 | ? (various unknown)                                              | Tiny files, no common header, no ascii info visible. No idea.                                                              |
| 03353 - 08538 | ? (various unknown)                                              | no common header, fairly small files &lt;500 kb. Ditto                                                                     |
| 08539 - 08622 | **MOT**, **SSCF**                                                | Monster / Battle / Boss data: maybe "file-names", Event Scripts, Boss Battle scripts, Monster behaviour or something else. |
| 08623 - 08627 | **zack**, **ATEL**                                               | Possibly Zack's specific battle data                                                                                       |
| 08628 - 08690 | **MAGIC**                                                        | Zack's Battle commands, actions and animations                                                                             |
| 08671 - 08706 | ? (various unknown)                                              | tiny files                                                                                                                 |
| 08707 - 08725 | **[PSMF][]**                                                     | \* more Videos                                                                                                             |

  
*\** - These files are understood enough to view and/or extract their
contents.

.

## Data File Formats

Overview of the different types of data files and what they contain.
List shows the data types currently known.

### [Game Events and Scripts][]

-   [ATEL][] Files
-   [MBD][ATEL] Files

### [Sprites, Images and Texture Data][]

-   [\[IMG][1]\] Files
-   [\[TEX][TEX]\] Files
-   [\[GT][GT]\] Files

### [Audio Data][]

-   [RIFF][] Files
-   [SSCF][] Files

### [Video Data][]

-   [\[PSMF][PSMF]\]

### [Models and Mesh Geometry][]

-   [\[!][2] (exp) Model\] Files

### [Battles and Monsters][]

### [Materia][]

## Differences between Japanese, US and PAL versions

Japanese one has two diffs. First of all, japanese version has more
audio files than english one (It was confirmed while making an undub of
english one ;P) and has changed Minerva statue model. In japanese
version it looked too much like cathlic Maria so in US release they made
completly new model for it.

<small>-[Aurenasek116][]</small>

.

## Miscelenous Findings

Anything interesting or weird worth noting.

### Debug Menu

File "00000.RAW" contains an interesting menu-dialogue where the player
is shown a menu listing the names of various FF7CC developers, and a
Moogle apparantly narrating the choice, and asking for user input.

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

Nothing else is known about this menu, as it does not appear during
normal gameplay, and currently there is no way to initilise it.

Someone has been able to iniate this menu somehow, screenshots of which
were posted [here][].

  

### Hidden Event-Dialogues Menu and/or Materia

Contained within all ATEL files are the following Menu-Dialogue texts.

-   The "Kupo!" suggests a Moogle narrating, possibly related to the
    Debug-Menu.
-   The "Materia has leveled up!" suggests maybe a hidden Materia was
    used to initiate this Menu.
-   "Gondola" and "Elevator" may be references to the side-quest during
    the mission in Junon.
-   It is currently unknown why these texts appear within ALL \[ATEL\]
    files, the only possibility being that they serve as interfaces to
    the Debug-Menu, which has now been confirmed to exist.

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

| Project Name                         | Description                                                                                                                                    | Author       | Version / Status | Links                             |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|--------------|------------------|-----------------------------------|
| FF7CC Data Extractor                 | Extracts the Data-Files from the FF7CC PKG and FSE files stored on PSP Media                                                                   | [G][]        | 1.0              | [Forum][], [Binary][], [Mirror][] |
| RINOA Model Viewer                   | Suppors some FF7CC Data-Files, such as Game-Scripts, and Models, also has an OBJ mesh exporter                                                 | [Koral][3]   | 0.51             | [Forum][4], [Binary][5]           |
| \[!\]-Model Extractor (aka mesh2rdm) | Powerful file viewer and extractor, exporting out skin-weighted models from !-Models to OBJ or SMD                                             | [MrAdults][] | v1.81            | [Website][]                       |
| MarC's HiMD Renderer                 | Convert FF7CC \[SSCF\] audio-files to wav, mp3, ogg or pcm <small>( -- [aljnx][])</small>                                                      | MarC         | 0.54             | [Website][6]                      |
| CC Plugin for Xpert2                 | Allows Xpert2 to extract and re-pack the Data-files from and to FF7CC PKG and FSE files stored on PSP Media <small>( -- [Karlislie][])</small> |              |                  | [Download][], [Mirror][7]         |

  [Koral]: /User:Koral.md "wikilink"
  [FF7CC Data Extractor]: /FF7:CC.md#Tools "wikilink"
  [PSMF]: /FF7:CC/Video%20Formats.md#PSMF%20Format "wikilink"
  [RIFF]: /FF7:CC/Audio%20Formats.md#RIFF%20Format "wikilink"
  [SSCF]: /FF7:CC/Audio%20Formats.md#SSCF%20Format "wikilink"
  [GT]: /FF7:CC/Image%20Formats.md#GT%20Format "wikilink"
  [! (exp TYPE-1)]: /FF7:CC/Model%20Formats.md#exp%20TYPE-1%20Models "wikilink"
  [! (exp TYPE-0)]: /FF7:CC/Model%20Formats.md#exp%20TYPE-0%20Models "wikilink"
  [TEX]: /FF7:CC/Image%20Formats.md#TEX%20Format "wikilink"
  [Game Events and Scripts]: /FF7:CC/Game%20Event%20Files.md "wikilink"
  [ATEL]: /FF7:CC/File%20Types.md "wikilink"
  [Sprites, Images and Texture Data]: /FF7:CC/Image%20Formats.md "wikilink"
  [1]: /FF7:CC/Image%20Formats.md#IMG%20Format "wikilink"
  [Audio Data]: /FF7:CC/Audio%20Formats.md "wikilink"
  [Video Data]: /FF7:CC/Video%20Formats.md "wikilink"
  [Models and Mesh Geometry]: /FF7:CC/Model%20Formats.md "wikilink"
  [2]: /FF7:CC/Model%20Formats.md#exp%20Format "wikilink"
  [Battles and Monsters]: /FF7:CC/Battle%20and%20Monster%20Data.md "wikilink"
  [Materia]: /FF7:CC/Materia%20Data.md "wikilink"
  [Aurenasek116]: http://forums.qhimm.com/index.php?action=profile;u=4603
  [here]: http://forums.qhimm.com/index.php?topic=8163.msg100101#msg100101
  [G]: http://forums.qhimm.com/index.php?action=profile;u=3309
  [Forum]: http://forums.qhimm.com/index.php?topic=7053.0
  [Binary]: http://superg.org.ua/ff7cc_extractor.tar.bz2
  [Mirror]: http://www.mediafire.com/?nwm24zynjmk
  [3]: http://forums.qhimm.com/index.php?action=profile;u=5116
  [4]: http://forums.qhimm.com/index.php?topic=8451.0
  [5]: http://www.mediafire.com/?jzqmgzmoq4m
  [MrAdults]: http://forums.qhimm.com/index.php?action=profile;u=3607
  [Website]: http://www.richwhitehouse.com/index.php?postid=30
  [aljnx]: http://forums.qhimm.com/index.php?action=profile;u=4675
  [6]: http://www.marcnetsystem.co.uk/
  [Karlislie]: http://forums.qhimm.com/index.php?action=profile;u=5343
  [Download]: http://www.mediafire.com/download.php?j5tnduxoemd
  [7]: http://www.mediafire.com/?hmbmdzdmwki
