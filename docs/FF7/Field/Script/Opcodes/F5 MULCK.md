---
title: F5 MULCK
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > F5 MULCK

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

  [MUSIC]: ../F0%20MUSIC.md "wikilink"
