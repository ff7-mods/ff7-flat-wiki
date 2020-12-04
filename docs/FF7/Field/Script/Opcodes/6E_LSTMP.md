---
title: 6E_LSTMP
---

-   Opcode: **0x6E**
-   Short name: **LSTMP**
-   Long name: Last Map

#### Memory layout

| 0x6E | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store value.
-   **const UByte** *A*: Address to store value.

#### Description

Retrieves the [field ID](../../Field_ID.md) number of the field that was played directly before the current one, into the bank *B* and address *A* specified. The previous area does not include the specific world map locations that are given a field ID (0x1 to 0x40), so traversing via a gateway to the world map, then back to the field, will not cause the world map ID to be retrieved; rather, that same field ID will be loaded.
