---
title: FF8
---

[Home](/ff7-flat-wiki/Main%20Page.md) > FF8

# Contents

### History

Final Fantasy VIII came after the mega hit [Final Fantasy VII][], it in
itself was a very successful game release for Square. For more on the
[history of Final Fantasy VIII read here][]. The Game Engine

-   [Final Fantasy VIII's Engine][]

### Engine constants

-   [Array of Battle files][]

### Details of the Game

-   [Final Fantasy VIII's Kernel][]
-   [Game variables used in scripting][]
-   [World map camera][]
-   [Battle encounters list][]
-   [String Encoding][]

### Media Formats

-   [Final Fantasy VIII PS1][] media information.
-   [Final Fantasy VIII PC][] media information.
-   [Final Fantasy VIII Save data][]

  
= File Formats =

### Movie Files

-   [\[PAK][1]\] Movie Archives

### Sound Files

-   [\[FMT][2]\] Sound Archives

### Battle files

-   [\[X][3]\] Battle Fields
-   [\[DAT][4]\] Battle Models
-   [Scene.out][] Battle encounter data
-   [r0win.dat][] Winning sequence
-   [b0wave.dat][] Core battle data (Textures+Music+Font)
-   [a9btlfnt.bft][] Battle Font (Redirect to TDW)
-   [.mag files][] - MAG files

### Field files

-   [Opcodes][] Field script opcodes
-   [\[MCH][5]\] Field Character Models
-   [\[ONE][6]\] Field Character Models Container
-   [\[MIM][7]\] Field Background Image Data
-   [\[MAP][8]\] Field Background Tile Data
-   [\[JSM][9]\] Field Scripts
-   [\[SYM][10]\] Field Script names (unused)
-   [\[MSD][11]\] Field Dialogs
-   [\[INF][12]\] Field Gateways
-   [\[ID][13]\] Field Walkmesh (same format as FF7)
-   [\[CA][14]\] Field Camera
-   [\[TDW][a9btlfnt.bft]\] Extra font
-   [\[MSK][15]\] Movie cam (?)
-   [\[RAT][16] & \[MRT\]\] Battle related
-   [\[PMD][17]\] Particle Info
-   [\[PMP][18]\] Particle Image Data
-   [\[PVP][19]\] Unknown (often 0x0c000000, sometimes 0x0a000000 or
    0x0b000000)
-   [\[SFX][20]\] Indexes to Sound Effects (?)

### World map files

-   [music0.obj][]
-   [music1.obj][music0.obj]
-   [music2.obj][music0.obj]
-   [music3.obj][music0.obj]
-   [music4.obj][music0.obj]
-   [music5.obj][music0.obj]
-   [rail.obj][]
-   [texl.obj][]
-   [wmset.obj][]
-   [wmsetXX.obj][]
-   [wmx.obj][]
-   [chara.one][]

### Main

-   [wm2field.tbl][]
-   [kernel.bin][]
-   [harata.cnf][]
-   [init.out][]
-   [namedic.bin][]

### Menu

-   [\*.sp1/\*.sp2][]
-   [mngrphd.bin][]
-   [mngrp.bin][]
-   [tkmnmes\*.bin][]
-   [mag\*.tex][]
-   [mngrp strings][]
-   [mngrp complex strings][]
-   [m00\*.bin and m00\*.msg][]
-   [areames.dc1][]

# Tools and Patches

-   [Tools and Patches][]

  [Final Fantasy VII]: /ff7-flat-wiki/FF7.md "wikilink"
  [history of Final Fantasy VIII read here]: /ff7-flat-wiki/FF8/HistoryOf.md "wikilink"
  [Final Fantasy VIII's Engine]: /ff7-flat-wiki/FF8/Engine.md "wikilink"
  [Array of Battle files]: /ff7-flat-wiki/FF8/Engine%20const/BattleFiles.md "wikilink"
  [Final Fantasy VIII's Kernel]: /ff7-flat-wiki/FF8/Kernel.md "wikilink"
  [Game variables used in scripting]: /ff7-flat-wiki/FF8/Variables.md "wikilink"
  [World map camera]: /ff7-flat-wiki/FF8/Engine/WorldMapCamera.md "wikilink"
  [Battle encounters list]: /ff7-flat-wiki/FF8/Encounter%20Codes.md "wikilink"
  [String Encoding]: /ff7-flat-wiki/FF8/String%20Encoding.md "wikilink"
  [Final Fantasy VIII PS1]: /ff7-flat-wiki/FF8/PlaystationMedia.md "wikilink"
  [Final Fantasy VIII PC]: /ff7-flat-wiki/FF8/PC%20Media.md "wikilink"
  [Final Fantasy VIII Save data]: /ff7-flat-wiki/FF8/GameSaveFormat.md "wikilink"
  [1]: /ff7-flat-wiki/FF8/FileFormat%20PAK.md "wikilink"
  [2]: /ff7-flat-wiki/FF8/FileFormat%20FMT.md "wikilink"
  [3]: /ff7-flat-wiki/FF8/FileFormat%20X.md "wikilink"
  [4]: /ff7-flat-wiki/FF8/FileFormat%20DAT.md "wikilink"
  [Scene.out]: /ff7-flat-wiki/FF8/BattleStructure.md "wikilink"
  [r0win.dat]: /ff7-flat-wiki/FF8/FileFormat%20r0win.md "wikilink"
  [b0wave.dat]: /ff7-flat-wiki/FF8/FileFormat%20b0wave.md "wikilink"
  [a9btlfnt.bft]: /ff7-flat-wiki/FF8/FileFormat%20TDW.md "wikilink"
  [.mag files]: /ff7-flat-wiki/FF8/FileFormat%20magfiles.md "wikilink"
  [Opcodes]: /ff7-flat-wiki/FF8/Field/Script/Opcodes.md "wikilink"
  [5]: /ff7-flat-wiki/FF8/FileFormat%20MCH.md "wikilink"
  [6]: /ff7-flat-wiki/FF8/FileFormat%20ONE.md "wikilink"
  [7]: /ff7-flat-wiki/FF8/FileFormat%20MIM.md "wikilink"
  [8]: /ff7-flat-wiki/FF8/FileFormat%20MAP.md "wikilink"
  [9]: /ff7-flat-wiki/FF8/FileFormat%20JSM.md "wikilink"
  [10]: /ff7-flat-wiki/FF8/FileFormat%20SYM.md "wikilink"
  [11]: /ff7-flat-wiki/FF8/FileFormat%20MSD.md "wikilink"
  [12]: /ff7-flat-wiki/FF8/FileFormat%20INF.md "wikilink"
  [13]: /ff7-flat-wiki/FF7/Field/Walkmesh.md "wikilink"
  [14]: /ff7-flat-wiki/FF8/FileFormat%20CA.md "wikilink"
  [15]: /ff7-flat-wiki/FF8/FileFormat%20MSK.md "wikilink"
  [16]: /ff7-flat-wiki/FF8/FileFormat%20RAT%20MRT.md "wikilink"
  [17]: /ff7-flat-wiki/FF8/FileFormat%20PMD.md "wikilink"
  [18]: /ff7-flat-wiki/FF8/FileFormat%20PMP.md "wikilink"
  [19]: /ff7-flat-wiki/FF8/FileFormat%20PVP.md "wikilink"
  [20]: /ff7-flat-wiki/FF8/FileFormat%20SFX.md "wikilink"
  [music0.obj]: /ff7-flat-wiki/FF8/WorldMap%20music.md "wikilink"
  [rail.obj]: /ff7-flat-wiki/FF8/WorldMap%20rail.md "wikilink"
  [texl.obj]: /ff7-flat-wiki/FF8/WorldMap%20texl.md "wikilink"
  [wmset.obj]: /ff7-flat-wiki/FF8/WorldMap%20wmset.md "wikilink"
  [wmsetXX.obj]: /ff7-flat-wiki/FF8/WorldMap%20wmsetxx.md "wikilink"
  [wmx.obj]: /ff7-flat-wiki/FF8/WorldMap%20wmx.md "wikilink"
  [chara.one]: /ff7-flat-wiki/FF8/WorldMap%20charaone.md "wikilink"
  [wm2field.tbl]: /ff7-flat-wiki/FF8/Main%20wm2.md "wikilink"
  [kernel.bin]: /ff7-flat-wiki/FF8/Main%20kernel.md "wikilink"
  [harata.cnf]: /ff7-flat-wiki/FF8/Main%20harata.md "wikilink"
  [init.out]: /ff7-flat-wiki/FF8/Main%20init.md "wikilink"
  [namedic.bin]: /ff7-flat-wiki/FF8/Main%20namedic.md "wikilink"
  [\*.sp1/\*.sp2]: /ff7-flat-wiki/FF8/Menu%20sp2.md "wikilink"
  [mngrphd.bin]: /ff7-flat-wiki/FF8/Menu%20mngrphd%20bin.md "wikilink"
  [mngrp.bin]: /ff7-flat-wiki/FF8/Menu%20mngrp%20bin.md "wikilink"
  [tkmnmes\*.bin]: /ff7-flat-wiki/FF8/Menu%20tkmnmes.md "wikilink"
  [mag\*.tex]: /ff7-flat-wiki/Ff8/Menu%20mag%20textures.md "wikilink"
  [mngrp strings]: /ff7-flat-wiki/FF8/Menu%20mngrp%20strings%20locations.md "wikilink"
  [mngrp complex strings]: /ff7-flat-wiki/FF8/Menu%20mngrp%20complex%20strings.md "wikilink"
  [m00\*.bin and m00\*.msg]: /ff7-flat-wiki/FF8/Menu%20m000%20m004.md "wikilink"
  [areames.dc1]: /ff7-flat-wiki/FF8/Menu%20areames%20dc1.md "wikilink"
  [Tools and Patches]: /ff7-flat-wiki/FF8/Tools.md "wikilink"
