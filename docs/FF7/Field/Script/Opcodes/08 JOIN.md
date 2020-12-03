---
title: 08 JOIN
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 08 JOIN

-   Opcode: **0x08**
-   Short name: **JOIN**
-   Long name: Party Field Join

#### Memory layout

| 0x08 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Speed that the characters join back together.

#### Description

Causes seperated party characters that have previously been [SPLIT][]
onto the field, to be joined back together again; that is, only the
party leader becomes visible on the field. This should be called if a
previous SPLIT has completed (the party members have finished speaking,
or performing their actions, for example). As with SPLIT, the speed of
the join is specified, from a scale of 1 (almost instant) to FF (very
slow walk), and must be non-zero. In contrast to most MOVE related op
codes, the speed is this setting is actually the total number of frames
required. Depending on the distance from the player character and the
number of frames required, the entity plays a run or walk animation.
Also, all characters take the same time irrespective of distance.

Calling JOIN without having previously SPLIT the characters will cause
the party members to appear at the walkmesh origin and attempt to JOIN
from there. This is not normally the required behaviour and should be
avoided.

  [SPLIT]: 09%20SPLIT.md "wikilink"
