---
title: C8_PRTYP
---

-   Opcode: **0xC8**
-   Short name: **PRTYP**
-   Long name: Party Add

#### Memory layout

| 0xC8 | *C* |
|------|-----|

#### Arguments

-   **const UByte** *C*: Character ID to add.

#### Description

Adds a character to the party, given by *C*. The character is added in the first given empty party slot (which can be set by [PRTYE](CA_PRTYE.md) and an argument of FE for a slot). If there are no party members, the newly added character is the leader; if there is only the leader in the party, the newly added character occupies the second slot; if there are two members, the character occupies the last remaining slot. If the opcode is used when there is already a full party (with three members), the newly added party member occupies the last slot, overwriting the party member already there.
