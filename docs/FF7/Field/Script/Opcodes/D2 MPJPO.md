---
title: D2 MPJPO
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > D2 MPJPO

-   Opcode: **0xD2**
-   Short name: **MPJPO**
-   Long name: Gateway Switch (Map Jump Off)

#### Memory layout

| 0xD2 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Turns on or off all the [gateways][] in the current field. If set to
off, the player will not be able to transition to other fields defined
by the gateways. MAPJUMP opcodes are not affected, and so a combination
of [LINEs][] and [MAPJUMP][] could still achieve this.

  [gateways]: /ff7-flat-wiki/FF7/Field/3D%20Related.md "wikilink"
  [LINEs]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/D0%20LINE.md "wikilink"
  [MAPJUMP]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/60%20MAPJUMP.md "wikilink"
