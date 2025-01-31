---
title: D7_SLDR2
---

- Opcode: **0xD7**
- Short name: **SLDR2**
- Long name: Solid Range (16-bit)

#### Memory layout

| 0xD7 | *B* | *R* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is specified as a literal value.
- **const UShort** *R*: Range value.

#### Description

Similar to [SLIDR](C6_SLIDR), but allows a two-byte range value to be used.
