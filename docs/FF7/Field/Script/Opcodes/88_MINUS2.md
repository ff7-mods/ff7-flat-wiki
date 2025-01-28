---
title: 88_MINUS2
---

- Opcode: **0x88**
- Short name: **MINUS2**
- Long name: Subtraction (16-bit)

#### Memory layout

| 0x88 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: The destination variable, to which the operand is subtracted.
- **const SWord** *Oper*: The operand to be subtracted from the destination.

#### Description

Subtracts two numbers and stores the result back into â€œDestâ€. The result of the subtraction wraps around into the 16-bit range. If the Source Bank is 0 then the â€œOperâ€ is subtracted from the destination value. If the Source Bank is an 16 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
