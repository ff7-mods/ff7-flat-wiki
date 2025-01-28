---
title: B8_GETAXY
---

- Opcode: **0xB8**
- Short name: **GETAXY**
- Long name: Get Entity XY

#### Memory layout

| 0xB8 | *B1 / B2* | *E* | *X* | *Y* |
|------|-----------|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to store *X*.
- **const Bit\[4\]** *B2*: Bank to store *Y*.
- **const UByte** *E*: Entity ID to retrieve.
- **const UByte** *X*: Address to store X-coordinate.
- **const UByte** *Y*: Address to store Y-coordinate.

#### Description

Fetches the current X- and Y-coordinates of the entity given by *E* into bank *B*, address *A*. *E* is an offset into the entity list, not a visible object ID, and therefore includes non-visible entities; retrieving the co-ordinates of a non-visible entity results in unusual values being retrieved.
