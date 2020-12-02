---
title: FF7
---

[Home](/ff7-flat-wiki/Main%20Page.md) > FF7

<small> This is a Stub article. A Wiki version of Gears should go here.
For more information, select the "discussion" tab above so we can best
architecture the data. For those who want to start converting, download
the [Gears pdf][] [Halkun][] 20:18, 5 Mar 2005 (CST) </small>

  

## Contents

-   [History][]
-   [Engine Basics][]
    -   Parts of the Engine
    -   Generic Program Flow
-   [The Kernel][]
    -   [Kernel Overview][]
        -   History
        -   Kernel Functionality
    -   [Memory Management][]
        -   RAM Management
        -   VRAM Management
        -   PSX CD-ROM management
    -   [Kernel.bin][]
        -   The KERNEL.BIN Archive
        -   The KERNEL2.BIN Archive
    -   [Low Level Libraries][]
        -   PC to PSX comparison
        -   Data Archives
            -   BIN Archive data format
            -   [ LZSS Archives][]
            -   [ LGP Archives][]
        -   Textures
            -   [ TIM texture data format for PSX][]
            -   [ TEX texture data format for the PC][]
        -   File formats for 3D models
            -   [Model Formats for PSX][]
            -   Model Formats for PC
-   [The Menu Module][]
    -   Menu Overview
    -   Menu Initialization
    -   Menu Modules
    -   Calling the various menus
    -   Menu dependencies
    -   [The Save Game format][]
-   [ The Field Module][]
    -   Field Overview
    -   Field Format (PC)
        -   General PC Field File Format
        -   PC Field File Header
        -   File Section Details
    -   [Field Format (PSX)][]
        -   [PSX DAT Format][]
        -   [PSX MIM Format][]
        -   [PSX BSX Format][]
        -   [PSX BCX Format][]
-   The Battle Module
    -   Battle Overview
    -   [ Battle Mechanics][]
    -   [ Battle Field][]
    -   [ Battle Scenes (scene.bin)][]
        -   [ Battle Scripts][]
    -   [ Battle Models (PSX)][]
    -   [ Battle Animation (PC)][]
-   [ The World Map Module][]
    -   [ World Map BSZ model file format (PSX)][]
    -   [ World Map TXZ file format (PSX)][]
    -   [ World Map Script Engine][]
-   Sound
    -   [PSX Sound][]
        -   [Overview][]
        -   [INSTRx.DAT][]
        -   [INSTRx.ALL][]
        -   [AKAO sequence][]
        -   [Code Map][]
    -   PC Sound
-   [ Technical Help][]
-   [Tools and patches][]
-   [Source Code Forensics][]

  [Gears pdf]: https://wiki.ffrtt.ru/gears.pdf
  [Halkun]: /ff7-flat-wiki/User:Halkun.md "wikilink"
  [History]: /ff7-flat-wiki/FF7/History.md "wikilink"
  [Engine Basics]: /ff7-flat-wiki/FF7/Engine%20basics.md "wikilink"
  [The Kernel]: /ff7-flat-wiki/FF7/Kernel.md "wikilink"
  [Kernel Overview]: /ff7-flat-wiki/FF7/Kernel/Overview.md "wikilink"
  [Memory Management]: /ff7-flat-wiki/FF7/Kernel/Memory%20management.md "wikilink"
  [Kernel.bin]: /ff7-flat-wiki/FF7/Kernel/Kernel.bin.md "wikilink"
  [Low Level Libraries]: /ff7-flat-wiki/FF7/Kernel/Low%20level%20libraries.md "wikilink"
  [LZSS Archives]: /ff7-flat-wiki/FF7/LZSS%20format.md "wikilink"
  [LGP Archives]: /ff7-flat-wiki/FF7/LGP%20format.md "wikilink"
  [TIM texture data format for PSX]: /ff7-flat-wiki/PSX/TIM%20format.md "wikilink"
  [TEX texture data format for the PC]: /ff7-flat-wiki/FF7/TEX%20format.md "wikilink"
  [Model Formats for PSX]: /ff7-flat-wiki/FF7/Kernel/Low%20level%20libraries.md#Model%20formats%20for%20PSX
    "wikilink"
  [The Menu Module]: /ff7-flat-wiki/FF7/Menu%20Module.md "wikilink"
  [The Save Game format]: /ff7-flat-wiki/FF7/Savemap.md "wikilink"
  [The Field Module]: /ff7-flat-wiki/FF7/Field%20Module.md "wikilink"
  [Field Format (PSX)]: /ff7-flat-wiki/FF7/Field%20Module.md#Field%20Format%20.28PSX.29
    "wikilink"
  [PSX DAT Format]: /ff7-flat-wiki/FF7/Field%20Module.md#PSX%20DAT%20Format "wikilink"
  [PSX MIM Format]: /ff7-flat-wiki/FF7/Field%20Module.md#PSX%20MIM%20Format "wikilink"
  [PSX BSX Format]: /ff7-flat-wiki/FF7/Field%20Module.md#PSX%20BSX%20Format "wikilink"
  [PSX BCX Format]: /ff7-flat-wiki/FF7/Field%20Module.md#PSX%20BCX%20Format "wikilink"
  [Battle Mechanics]: /ff7-flat-wiki/FF7/Battle/Battle%20Mechanics.md "wikilink"
  [Battle Field]: /ff7-flat-wiki/FF7/Battle/Battle%20Field.md "wikilink"
  [Battle Scenes (scene.bin)]: /ff7-flat-wiki/FF7/Battle/Battle%20Scenes.md "wikilink"
  [Battle Scripts]: /ff7-flat-wiki/FF7/Battle/Battle%20Scenes/Battle%20Script.md "wikilink"
  [Battle Models (PSX)]: /ff7-flat-wiki/FF7/Playstation%20Battle%20Model%20Format.md "wikilink"
  [Battle Animation (PC)]: /ff7-flat-wiki/FF7/Battle/Battle%20Animation%20(PC).md "wikilink"
  [The World Map Module]: /ff7-flat-wiki/FF7/WorldMap%20Module.md "wikilink"
  [World Map BSZ model file format (PSX)]: /ff7-flat-wiki/FF7/World%20Map/BSZ.md "wikilink"
  [World Map TXZ file format (PSX)]: /ff7-flat-wiki/FF7/World%20Map/TXZ.md "wikilink"
  [World Map Script Engine]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script.md "wikilink"
  [PSX Sound]: /ff7-flat-wiki/FF7/PSX/PSX%20Sound.md "wikilink"
  [Overview]: /ff7-flat-wiki/FF7/PSX/Sound/Overview.md "wikilink"
  [INSTRx.DAT]: /ff7-flat-wiki/FF7/PSX/Sound/INSTRx.DAT.md "wikilink"
  [INSTRx.ALL]: /ff7-flat-wiki/FF7/PSX/Sound/INSTRx.ALL.md "wikilink"
  [AKAO sequence]: /ff7-flat-wiki/FF7/PSX/Sound/AKAO%20sequence.md "wikilink"
  [Code Map]: /ff7-flat-wiki/FF7/PSX/Sound/Code%20Map.md "wikilink"
  [Technical Help]: /ff7-flat-wiki/FF7/Technical.md "wikilink"
  [Tools and patches]: /ff7-flat-wiki/FF7/Technical/Customising.md "wikilink"
  [Source Code Forensics]: /ff7-flat-wiki/FF7/Technical/Source.md "wikilink"
