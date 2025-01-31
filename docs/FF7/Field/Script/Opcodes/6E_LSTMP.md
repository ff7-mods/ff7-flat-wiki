---
title: 6E_LSTMP
---

- Opcode: **0x6E**
- Short name: **LSTMP**
- Long name: Last Map

#### Memory layout

| 0x6E | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store value.
- **const UByte** *A*: Address to store value.

#### Description

Retrieves the [field ID](../../Field_ID), so traversing via a gateway to the world map, then back to the field, will not cause the world map ID to be retrieved; rather, that same field ID will be loaded.
