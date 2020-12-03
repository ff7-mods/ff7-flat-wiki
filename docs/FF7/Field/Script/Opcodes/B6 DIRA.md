---
title: B6 DIRA
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > B6 DIRA

-   Opcode: **0xB6**
-   Short name: **DIRA**
-   Long name: Direction to Entity

#### Memory layout

| 0xB6 | *E* |
|------|-----|

#### Arguments

-   **const UByte** *E*: Entity ID to direct towards.

#### Description

Instantaneously directs the field object towards the entity with the
given ID. As with [MOVA][], the entity ID is an offset in the entire
entity list, and not into the visible object/entities list, and will
also have no effect if a non-visible entity is given.

  [MOVA]: AA%20MOVA.md "wikilink"
