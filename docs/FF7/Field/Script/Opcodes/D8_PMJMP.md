---
title: D8_PMJMP
---

- Opcode: **0xD8**
- Short name: **PMJMP**
- Long name: Prepare Field Change

#### Memory layout

| 0xD8 | *I* |
|------|-----|

#### Arguments

- **const UShort** *I*: [Field ID](../../Field_List) of the map to prepare to jump to.

#### Description

Prepare to jump to the field indicated by *I*. Use before making the [map jump](60_MAPJUMP).
