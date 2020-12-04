---
title: D2_MPJPO
---

-   Opcode: **0xD2**
-   Short name: **MPJPO**
-   Long name: Gateway Switch (Map Jump Off)

#### Memory layout

| 0xD2 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Turns on or off all the [gateways](../../3D_Related.md) in the current field. If set to off, the player will not be able to transition to other fields defined by the gateways. MAPJUMP opcodes are not affected, and so a combination of [LINEs](D0_LINE.md) and [MAPJUMP](60_MAPJUMP.md) could still achieve this.
