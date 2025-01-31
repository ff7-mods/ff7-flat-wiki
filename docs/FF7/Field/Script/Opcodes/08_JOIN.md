---
title: 08_JOIN
---

- Opcode: **0x08**
- Short name: **JOIN**
- Long name: Party Field Join

#### Memory layout

| 0x08 | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: Speed that the characters join back together.

#### Description

Causes seperated party characters that have previously been [SPLIT](09_SPLIT), and must be non-zero. In contrast to most MOVE related op codes, the speed is this setting is actually the total number of frames required. Depending on the distance from the player character and the number of frames required, the entity plays a run or walk animation. Also, all characters take the same time irrespective of distance.

Calling JOIN without having previously SPLIT the characters will cause the party members to appear at the walkmesh origin and attempt to JOIN from there. This is not normally the required behaviour and should be avoided.
