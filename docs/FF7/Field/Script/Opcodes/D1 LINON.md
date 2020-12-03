---
title: D1 LINON
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > D1 LINON

-   Opcode: **0xD1**
-   Short name: **LINON**
-   Long name: Line Switch

#### Memory layout

| 0xD1 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch on/off (1/0, respectively).

#### Description

Turns on or off the [LINE][] that was registered by this entity in the
current field. If set to off, the line will not be triggered by the
character walking through them.

  [LINE]: D0%20LINE.md "wikilink"
