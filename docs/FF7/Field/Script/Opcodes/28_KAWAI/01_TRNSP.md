---
title: 01_TRNSP
---

- Opcode: **0x28/01**
- Short name: **KAWAI/TRNSP**
- Long name: Character Transparency

#### Memory layout

| 0x28 | *4* | *1* | *S* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *4*: Total length of opcode and argument list.
- **const UByte** *1*: Subop code.
- **const UByte** *S*: Switch on/off (1/0, respectively).

#### Description

Makes the whole field object, associated with the entity in which script this opcode resides, semi-transparent.
