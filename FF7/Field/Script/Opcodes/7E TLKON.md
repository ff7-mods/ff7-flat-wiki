---
title: 7E TLKON
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 7E TLKON

-   Opcode: **0x7E**
-   Short name: **TLKON**
-   Long name: Talk Switch

#### Memory layout

| 0x7E | *S* |
|------|-----|

#### Arguments

-   **const UByte** *B*: Switch on/off (0/1, respectively).

#### Description

Turns on or off, for an entity, the ability for the playable character
to interact with the entity by pressing the \[X\] button. More
precisely, this enables or disables the On Press script (script 2); if
set to off, script 2 will not execute when the button is pressed and the
player is facing the entity's object. If set to on, the script will
execute, as normal.
