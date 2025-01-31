---
title: B6_DIRA
---

- Opcode: **0xB6**
- Short name: **DIRA**
- Long name: Direction to Entity

#### Memory layout

| 0xB6 | *E* |
|------|-----|

#### Arguments

- **const UByte** *E*: Entity ID to direct towards.

#### Description

Instantaneously directs the field object towards the entity with the given ID. As with [MOVA](AA_MOVA), the entity ID is an offset in the entire entity list, and not into the visible object/entities list, and will also have no effect if a non-visible entity is given.
