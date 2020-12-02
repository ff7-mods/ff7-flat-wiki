---
title: F6 BMUSC
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > F6 BMUSC

-   Opcode: **0xF6**
-   Short name: **BMUSC**
-   Long name: Battle Music

#### Memory layout

| 0xF6 | *I* |
|------|-----|

#### Arguments

-   **const UByte** *I*: ID of the music file to play, as set in the
    field file.

#### Description

Sets the [MUSIC][] that will play when the next [BATTLE][] is issued. As
with the MUSIC opcode, the ID represents an offset into the list of
music files that have been set by the field file. Hence, provided the
field file has the correct music file(s) set, this opcode can be used to
set regular or boss battle music for the current field's encounters, or
even switched between in the script.

  [MUSIC]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/F0%20MUSIC.md "wikilink"
  [BATTLE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/70%20BATTLE.md "wikilink"
