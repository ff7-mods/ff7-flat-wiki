---
title: 7B_INC2!
---

- Opcode: **0x7B**
- Short name: **INC2!**
- Long name: Saturated Increment (16-bit)

#### Memory layout

| 0x7B | *0/D* | *Dest* |
|------|-------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const UByte** *Dest*: The destination address in the bank where the variable is incremented.

#### Description

Increments the value in â€œDestâ€ by 1. The result is capped at 32767.
