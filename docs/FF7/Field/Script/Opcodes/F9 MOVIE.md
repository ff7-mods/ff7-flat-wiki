---
title: F9 MOVIE
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > F9 MOVIE

-   Opcode: **0xF9**
-   Short name: **MOVIE**
-   Long name: Play Movie

#### Memory layout

| 0xF9 |
|------|

#### Arguments

None.

#### Description

Plays the movie previously defined by [PMVIE][]. Note that further
execution of the current script is halted until the movie has finished
playing, and a playable character is still able to move whilst the movie
is being played, so player movements may be [frozen][] first. In
addition, field music currently playing will continue to do so unless
explicitly instructed otherwise.

Note that MOVIE removes the availability of the hand pointer above the
player's head, even after the movie has finished playing. To re-enable
it, use [SPECIAL: POINT][].

  [PMVIE]: ../F8%20PMVIE.md "wikilink"
  [frozen]: ../33%20UC.md "wikilink"
  [SPECIAL: POINT]: ../0F%20SPECIAL/F5%20POINT.md
    "wikilink"
