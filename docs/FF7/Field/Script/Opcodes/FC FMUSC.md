---
title: FC FMUSC
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > FC FMUSC

-   Opcode: **0xFC**
-   Short name: **FMUSC**
-   Long name: Field Music

#### Memory layout

| 0xFC | *I* |
|------|-----|

#### Arguments

-   **const UByte** *I*: ID of the music file to play, as set in the
    field file.

#### Description

Sets the [MUSIC][] that will play after the next [BATTLE][] has been
issued and fought, this music (I) will be player when the player rejoins
the field. As with the MUSIC opcode, the ID represents an offset into
the list of music files that have been set by the field file. Hence,
provided the field file has the correct music file(s) set, this opcode
can be used to set regular or boss battle music for the current field's
encounters, or even switched between in the script.

  [MUSIC]: ../F0%20MUSIC.md "wikilink"
  [BATTLE]: ../70%20BATTLE.md "wikilink"
