---
title: 021 EFFECTPLAY2
---

[Home](/Main%20Page.md) > [FF8](/FF8.md) > [Field](/FF8/Field.md) > [Script](/FF8/Field/Script.md) > [Opcodes](/FF8/Field/Script/Opcodes.md) > 021 EFFECTPLAY2

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

Plays a sound effect through the given sound channel. The channel is
important because it's the parameter used in [SESTOP][] to halt a
specific sound effect (and to prevent multiple counds from silencing
each other). AFAIK Channels go up to 2^20 (which is 1048576), so you can
theoretically have 20 sounds playing at once. 0 doesn't seem like it's a
usable channel, but this is untested.

Note: It seems each area can have a maximum of 32 sounds predefined
(meaning sound ID 31 is the highest you can play with this). You have to
use [EFFECTPLAY][] to use more than 32 sounds.

  [SESTOP]: /FF8/Field/Script/Opcodes/0CD%20SESTOP.md "wikilink"
  [EFFECTPLAY]: /FF8/Field/Script/Opcodes/0BC%20EFFECTPLAY.md "wikilink"
