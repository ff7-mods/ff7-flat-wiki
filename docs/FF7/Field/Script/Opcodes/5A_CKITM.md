---
title: 5A_CKITM
---

- Opcode: **0x5A**
- Short name: **CKITM**
- Long name: Check Item

#### Memory layout

| 0x5A | *B* | *I* | *A* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store result.
- **const UShort** *I*: [Item ID](../../Item_ID) to check.
- **const UByte** *A*: Address to store result.

#### Description

Copies the amount of item **I** the player has in their inventory, to the bank and address specified.
