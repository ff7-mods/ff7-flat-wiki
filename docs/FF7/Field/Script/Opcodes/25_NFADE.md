---
title: 25_NFADE
---

- Opcode: **0x25**
- Short name: **NFADE**
- Long name: NFade

#### Memory layout

| 0x6B | *B1 / B2* | *0 / B3* | *T* | *R* | *G* | *B* | *S* | *unused* |
|------|-----------|----------|-----|-----|-----|-----|-----|----------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *R*, or zero if *R* is given as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *G*, or zero if *G* is given as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B3*: Bank to retrieve *B*, or zero if *B* is given as a literal value.
- **const UByte** *T*: Type of fade; see table.
- **const UByte** *R*: Red component value, or address of red value if *B1* is non-zero.
- **const UByte** *G*: Green component value, or address of green value if *B2* is non-zero.
- **const UByte** *B*: Blue component value, or address of blue value if *B3* is non-zero.
- **const UByte** *S*: Speed of fade. Larger numbers indicate faster fades.
- **const UByte** *unused*: Unused

#### Description

See [FADE](6B_FADE) op code page for full details.
