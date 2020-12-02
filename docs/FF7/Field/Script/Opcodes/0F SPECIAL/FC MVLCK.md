---
title: FC MVLCK
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > [0F SPECIAL](/ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL.md) > FC MVLCK

-   Opcode: **0x0FFC**
-   Short name: **SPECIAL: MVLCK**
-   Long name: Special: Movie Lock

#### Memory layout

| 0x0F | 0xFC | *B* |
|------|------|-----|

-   **const UByte** *B*: Movie lock on/off (1/0, respectively).

#### Description

Enables or disables the playing of movies; if the movie lock is set to
on (1), movies will not be played with the [MOVIE][] opcode.

  [MOVIE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/F9%20MOVIE.md "wikilink"
