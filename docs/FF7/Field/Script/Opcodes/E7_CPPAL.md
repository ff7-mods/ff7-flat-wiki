---
title: E7_CPPAL
---

- Opcode: **0xE7**
- Short name: **CPPAL**
- Long name: Copy Palette

#### Memory layout

| 0xE7 | *B1/B2* | *Source palette array id* | *Destination palette array id* | *Size* |
|------|---------|---------------------------|--------------------------------|--------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for source palette array id.
- **const Bit\[4\]** *B2*: Bank for destination palette array id.
- **const UByte** *Source palette array id*: Source palette array id to copy data from.
- **const UByte** *Destination palette array id*: Destination palette array id to copy data to.
- **const UByte** *Size*: Size of palette data to copy + 1 (in unsigned short).

#### Description

Copy palette data.
