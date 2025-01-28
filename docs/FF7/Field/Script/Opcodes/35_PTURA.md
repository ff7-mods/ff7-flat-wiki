---
title: 35_PTURA
---

- Opcode: **0x35**
- Short name: **PTURA**
- Long name: Turn to Party Member

#### Memory layout

| 0x35 | *P* | *S* | *A* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *P*: Party member to turn towards.
- **const UByte** *S*: Speed of turning; the larger the number, the slower the turn.
- **const UByte** *A*: Larger numbers increase the likelihood that the turn will be anticlockwise.

#### Description

Rotates (turns) the field object to face the party member specified by **P** (from 0 to 2), at the speed **S**. The "standard" value for **A** is 2.
