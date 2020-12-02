---
title: BF CC
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > BF CC

-   Opcode: **0xBF**
-   Short name: **CC**
-   Long name: Character Control

#### Memory layout

| 0xBF | *E* |
|------|-----|

#### Arguments

-   **const UByte** *E*: Entity ID.

#### Description

Passes playable character control to the entity given. The screen will
instantaneously center on the given entity's field object, and the
player will then be able to control the given character around the
walkmesh, and if currently set to be visible, the 'hand' pointer will
hover above the specified entity's field object. The entity ID is an
offset into the entire entity list, not a field object offset;
attempting to pass control to a non-visible field object will have no
effect.
