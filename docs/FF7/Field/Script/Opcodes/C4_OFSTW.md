---
title: C4_OFSTW
---

- Opcode: **0xC4**
- Short name: **OFSTW**
- Long name: Wait for Offset

#### Memory layout

| 0xC4 |
|------|

#### Arguments

None.

#### Description

Halts current script execution until a previous [OFST](C3_OFST) has completed. This is only of use if the offset type is not instantaneous.
