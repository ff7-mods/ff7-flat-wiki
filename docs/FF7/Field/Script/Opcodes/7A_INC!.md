---
title: 7A_INC!
---

- Opcode: **0x7A**
- Short name: **INC!**
- Long name: Saturated Increment (8-bit)

#### Memory layout

| 0x7A | *0/D* | *Dest* |
|------|-------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const UByte** *Dest*: The destination address in the bank where the variable is incremented.

#### Description

Increments the value in â€œDestâ€ by 1. The result is capped at 255.
