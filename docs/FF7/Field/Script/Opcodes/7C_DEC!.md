---
title: 7C_DEC!
---

- Opcode: **0x7C**
- Short name: **DEC!**
- Long name: Saturated Decrement (8-bit)

#### Memory layout

| 0x7C | *0/D* | *Dest* |
|------|-------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const UByte** *Dest*: The destination address in the bank where the variable is deccremented.

#### Description

Decreases the value in â€œDestâ€ by 1. The result is capped at 0.
