---
title: 78_MINUS!
---

- Opcode: **0x78**
- Short name: **MINUS!**
- Long name: Saturated Subtraction (8-bit)

#### Memory layout

| 0x78 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: The destination variable, to which the operand is subtracted.
- **const UByte** *Oper*: The operand to be subtracted from the destination.

#### Description

Subtracts "Oper" from "Dest" and stores the result back into "Dest". The result of the subtraction is capped at 0. If the Source Bank is 0 then the â€œOperâ€ is subtracted from the destination value. If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
