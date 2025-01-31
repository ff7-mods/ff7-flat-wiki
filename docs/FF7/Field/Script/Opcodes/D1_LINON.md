---
title: D1_LINON
---

- Opcode: **0xD1**
- Short name: **LINON**
- Long name: Line Switch

#### Memory layout

| 0xD1 | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: Switch on/off (1/0, respectively).

#### Description

Turns on or off the [LINE](D0_LINE) that was registered by this entity in the current field. If set to off, the line will not be triggered by the character walking through them.
