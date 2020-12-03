---
title: FB BTLCK
---

[Home](../../../../../Main%20Page.md) > [FF7](../../../../../FF7.md) > [Field](../../../../Field.md) > [Script](../../../Script.md) > [Opcodes](../../Opcodes.md) > [0F SPECIAL](../0F%20SPECIAL.md) > FB BTLCK

-   Opcode: **0x0FFB**
-   Short name: **SPECIAL: BTLCK**
-   Long name: Special: Battle Lock

#### Memory layout

| 0x0F | 0xFB | *B* |
|------|------|-----|

-   **const UByte** *B*: Battle lock on/off (1/0, respectively).

#### Description

Enables or disables the battle module; if battle lock is set to on (1),
battles will not occur anywhere in the game (this has an unusual effect
in the world map when it attempts to load the battle module). Battle
lock off (0) returns encounters to normal.
