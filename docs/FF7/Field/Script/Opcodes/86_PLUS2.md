---
title: 86_PLUS2
---

- Opcode: **0x86**
- Short name: **PLUS2**
- Long name: Addition (16-bit)

#### Memory layout

| 0x86 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: The destination variable, to which the operand is added.
- **const SWord** *Oper*: The operand, added to the destination.

#### Description

Adds two numbers together and stores the result back into â€œDestâ€. The result of the addition wraps around into the 16-bit range. If the Source Bank is 0 then the â€œOperâ€ is added to the destination value. If the Source Bank is an 16 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
