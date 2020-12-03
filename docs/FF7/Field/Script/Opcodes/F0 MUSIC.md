---
title: F0 MUSIC
permalink: F0 MUSIC.html
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > F0 MUSIC

-   Opcode: **0xF0**
-   Short name: **MUSIC**
-   Long name: Play Music

#### Memory layout

| 0xF0 | *I* |
|------|-----|

#### Arguments

-   **const UByte** *I*: ID for the music file that has been set in the
    field file.

#### Description

Plays the music that has been defined for the field file. Multiple files
of music can be set to play in one field file, so that they may be
switched between during play in the field. If the argument is an index
beyond the size of the list of music files set in the current field
file, the game will crash.
