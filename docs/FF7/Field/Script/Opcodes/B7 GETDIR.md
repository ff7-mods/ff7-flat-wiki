---
title: B7 GETDIR
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > B7 GETDIR

-   Opcode: **0xB7**
-   Short name: **GETDIR**
-   Long name: Get Entity Direction

#### Memory layout

| 0xB7 | *B* | *E* | *A* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store direction.
-   **const UByte** *E*: Entity ID to retrieve.
-   **const UByte** *A*: Address to store direction.

#### Description

Fetches the direction of the entity given by *E* into bank *B*, address
*A*. *E* is an offset into the entity list, not a visible object ID, and
therefore includes non-visible entities; retrieving the direction of a
non-visible entity results in unusual values being retrieved.
