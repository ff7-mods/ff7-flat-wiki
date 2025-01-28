---
title: B2_MSPED
---

- Opcode: **0xB2**
- Short name: **MSPED**
- Long name: Movement Speed (16-bit)

#### Memory layout

| 0xD7 | *B* | *S* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve *R*, or zero if *R* is specified as a literal value.
- **const UShort** *S*: Speed value (8-bit fixed point).

#### Description

Set speed of movement for MOVE-type opcodes.

Default value = 1024 -\> relative movement time scale 1

MSPED 512 -\> relative movement time scale 0.5

MSPED 2048 -\> relative movement time scale 2
