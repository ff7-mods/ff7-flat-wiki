---
title: B9_GETAI
---

- Opcode: **0xB9**
- Short name: **GETAI**
- Long name: Get Entity Triangle ID

#### Memory layout

| 0xB9 | *B* | *E* | *A* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store ID.
- **const UByte** *E*: Entity ID.
- **const UByte** *A*: Address to store triangle ID.

#### Description

Fetches the triangle ID on which the object of entity *E* is currently standing on, into bank *B*, address *A*. *E* is an offset into the entity list, not a visible object ID, and therefore includes non-visible entities; retrieving the triangle ID of a non-visible entity results in unusual values being retrieved.
