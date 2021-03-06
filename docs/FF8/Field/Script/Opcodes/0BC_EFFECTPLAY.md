---
title: 0BC_EFFECTPLAY
---

-   Opcode: **0x0BC**
-   Short name: **EFFECTPLAY**
-   Long name: Play sound effect

#### Argument

none

#### Stack

  
*FF8Audio Field ID -7850*

*Sound channel (must be power of 2)*

*Pan (0=left, 255=right)*

*Volume (0-127)*

**EFFECTPLAY**

#### Description

Plays a sound effect through the given sound channel. The channel is important because it's the parameter used in [SESTOP](0CD_SESTOP.md) to halt a specific sound effect (and also to avoid multiple sounds from silencing each other).

Unlike [EFFECTPLAY2](021_EFFECTPLAY2.md) which requires the field to have a list of sound IDs, this loads and plays a sound directly from the DAT based on its index in the FMT file, but with 7850 subtracted from it (That's where field IDs start counting for some reason). You'll need FF8Audio to find these IDs (FF8SND skips blank entries, which the game actually counts). For example, when you touch a save point, it calls EFFECTPLAY on sound 30, which turns out to be sound 7880 in field IDs.

Sound channel 0 appears to be able to play sounds while it's already playing sounds. Each other channels can only play one sound at a time.
