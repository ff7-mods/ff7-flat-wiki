---
title: D6_TLKR2
---

- Opcode: **0xD6**
- Short name: **TLKR2**
- Long name: Talk Range (16-bit)

#### Memory layout

| 0xC6 | *B* | *T* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *T*, or zero if *T* is specified as a literal value.
- **const UShort** *T*: Range value.

#### Description

Similar to [TALKR](C5_TALKR), but allows a two-byte range value to be used.
