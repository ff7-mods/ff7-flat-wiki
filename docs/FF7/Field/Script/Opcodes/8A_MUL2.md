---
title: 8A_MUL2
---

- Opcode: **0x8A**
- Short name: **MUL2**
- Long name: Multiplication (16-bit)

#### Memory layout

| 0x8A | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: The destination variable, to which the operand is multiplied.
- **const SWord** *Oper*: The operand, which is multiplied with the destination.

#### Description

Multiplies two numbers together and stores the result back into â€œDestâ€. The result of the Multiplication is capped at 32767. If the Source Bank is 0 then the the value â€œOperâ€ is multiplied with the destination value. If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
