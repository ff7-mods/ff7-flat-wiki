---
title: DC_CCANM
---

- Opcode: **0xDC**
- Short name: **CCANM**
- Long name: Stand/Walk/Run animation.

#### Memory layout

| 0xDC | *A* | *unused* | *I* |
|------|-----|----------|-----|

#### Arguments

- **const UByte** *A*: Animation ID for selected action.
- **const UByte** *I*: Id of selected action. (0 - stand, 1 - walk, 2 - run).

#### Description

Opcode set animation id used for standart player action: stand, walk and run. This is global for location so if you want to change your player model you need to be sure that this model has animation with this id.
