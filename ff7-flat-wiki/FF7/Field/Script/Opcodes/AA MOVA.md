---
title: AA MOVA
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > AA MOVA

-   Opcode: **0xAA**
-   Short name: **MOVA**
-   Long name: Move to Entity

#### Memory layout

| 0xAA | *E* |
|------|-----|

#### Arguments

-   **const UByte** *E*: Entity ID to move towards.

#### Description

Moves the field object towards the entity with the given ID. Note that
this is *not* a field object ID, in that the entity ID includes
non-visible entities; in other words, this is an offset to an entity in
the entire entity list, not just the visible entity list. However,
attempting to move the field object to an entity that is not visible
will fail, in that the MOVA opcode is ignored.

Also, the movement of the model comes up to the point of collision
between the source and target models. It does not go all the way to the
target models' position.

The moved entity also has to take a path adhering to the current active
triangles on the walkmesh
