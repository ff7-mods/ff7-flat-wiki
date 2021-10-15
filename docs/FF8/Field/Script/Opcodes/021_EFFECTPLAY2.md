---
title: 021_EFFECTPLAY2
---

-   Opcode: **0x021**
-   Short name: **EFFECTPLAY2**
-   Long name: Play sound effect

#### Argument

Field SFXID (in the SFX list for that field)

#### Stack

  
*Pan (0=left, 255=right)*

*Volume (0-127)*

*Channel (must be a power of 2)*

**EFFECTPLAY2**

#### Description

Plays a sound effect through the given sound channel. The channel is important because it's the parameter used in [SESTOP](0CD_SESTOP.md), so you can theoretically have 20 sounds playing at once. 0 doesn't seem like it's a usable channel, but this is untested.

Note: It seems each area can have a maximum of 32 sounds predefined (meaning sound ID 31 is the highest you can play with this). You have to use [EFFECTPLAY](0BC_EFFECTPLAY.md) to use more than 32 sounds.
