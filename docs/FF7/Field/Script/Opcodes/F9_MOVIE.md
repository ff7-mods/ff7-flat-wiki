---
title: F9_MOVIE
---

- Opcode: **0xF9**
- Short name: **MOVIE**
- Long name: Play Movie

#### Memory layout

| 0xF9 |
|------|

#### Arguments

None.

#### Description

Plays the movie previously defined by [PMVIE](FF7/Field/Script/Opcodes/F8_PMVIE "wikilink"). Note that further execution of the current script is halted until the movie has finished playing, and a playable character is still able to move whilst the movie is being played, so player movements may be [frozen](33_UC) first. In addition, field music currently playing will continue to do so unless explicitly instructed otherwise.

Note that MOVIE removes the availability of the hand pointer above the player's head, even after the movie has finished playing. To re-enable it, use [SPECIAL: POINT](0F_SPECIAL/F5_POINT).
