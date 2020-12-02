---
title: C6 SLIDR
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > C6 SLIDR

-   Opcode: **0xC6**
-   Short name: **SLIDR**
-   Long name: Solid Range

#### Memory layout

| 0xC6 | *B* | *R* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is
    specified as a literal value.
-   **const UByte** *R*: Range value.

#### Description

Adjusts the range of the collision circle for the entity's field object,
changing the distance threshold for collisions between the object, and
both other objects and the walkmesh boundaries. Lower values produce a
lower circle for the object; higher values increase the circle size.
