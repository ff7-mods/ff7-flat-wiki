---
title: 89_MUL
---

- Opcode: **0x89**
- Short name: **MUL**
- Long name: Multiplication (8-bit)

#### Memory layout

| 0x89 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: The destination variable, to which the operand is multiplied.
- **const UByte** *Oper*: The operand, which is multiplied with the destination.

#### Description

Multiplies two numbers together and stores the result back into â€œDestâ€. The result of the Multiplication is capped at 255. If the Source Bank is 0 then the the value â€œOperâ€ is multiplied with the destination value. If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
