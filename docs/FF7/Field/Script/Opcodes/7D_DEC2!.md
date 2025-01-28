---
title: 7D_DEC2!
---

- Opcode: **0x7D**
- Short name: **DEC2!**
- Long name: Saturated Decrement (16-bit)

#### Memory layout

| 0x7D | *0/D* | *Dest* |
|------|-------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const UByte** *Dest*: The destination address in the bank where the variable is Decremented.

#### Description

Decreases the value in â€œDestâ€ by 1. The result is capped at -32768.
