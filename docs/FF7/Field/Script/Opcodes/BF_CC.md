---
title: BF_CC
---

- Opcode: **0xBF**
- Short name: **CC**
- Long name: Character Control

#### Memory layout

| 0xBF | *E* |
|------|-----|

#### Arguments

- **const UByte** *E*: Entity ID.

#### Description

Passes playable character control to the entity given. The screen will instantaneously center on the given entity's field object, and the player will then be able to control the given character around the walkmesh, and if currently set to be visible, the 'hand' pointer will hover above the specified entity's field object. The entity ID is an offset into the entire entity list, not a field object offset; attempting to pass control to a non-visible field object will have no effect.
