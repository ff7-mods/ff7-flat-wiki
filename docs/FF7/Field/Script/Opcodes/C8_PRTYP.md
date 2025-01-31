---
title: C8_PRTYP
---

- Opcode: **0xC8**
- Short name: **PRTYP**
- Long name: Party Add

#### Memory layout

| 0xC8 | *C* |
|------|-----|

#### Arguments

- **const UByte** *C*: Character ID to add.

#### Description

Adds a character to the party, given by *C*. The character is added in the first given empty party slot (which can be set by [PRTYE](CA_PRTYE), the newly added party member occupies the last slot, overwriting the party member already there.
