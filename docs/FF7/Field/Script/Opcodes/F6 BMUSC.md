---
title: F6 BMUSC
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > F6 BMUSC

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

  [MUSIC]: F0%20MUSIC.md "wikilink"
  [BATTLE]: 70%20BATTLE.md "wikilink"
