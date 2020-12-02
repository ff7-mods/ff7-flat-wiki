---
title: FB BTLCK
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > [0F SPECIAL](/ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL.md) > FB BTLCK

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
