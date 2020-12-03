---
title: F6 BMUSC
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > F6 BMUSC

-   Opcode: **0xF6**
-   Short name: **BMUSC**
-   Long name: Battle Music

#### Memory layout

| 0xF6 | *I* |
|------|-----|

#### Arguments

-   **const UByte** *I*: ID of the music file to play, as set in the field file.

#### Description

Sets the [MUSIC](FF7/Field/Script/Opcodes/F0_MUSIC "wikilink") that will play when the next [BATTLE](70 BATTLE.md) set, this opcode can be used to set regular or boss battle music for the current field's encounters, or even switched between in the script.
