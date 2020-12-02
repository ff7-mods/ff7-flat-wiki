---
title: F5 MULCK
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > F5 MULCK

-   Opcode: **0xF5**
-   Short name: **MULCK**
-   Long name: Music Lock

#### Memory layout

| 0xF5 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Lock on/off (1/0, respectively).

#### Description

Locks the [MUSIC][] to the current selection. Subsequent calls to change
the music will fail unless a corresponding MULCK set to 0 is executed.

  [MUSIC]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/F0%20MUSIC.md "wikilink"
