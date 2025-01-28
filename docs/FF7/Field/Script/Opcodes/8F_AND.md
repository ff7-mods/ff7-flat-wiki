---
title: 8F_AND
---

- Opcode: **0x8F**
- Short name: **AND**
- Long name: Bitwise AND (8-bit)

#### Memory layout

| 0x8F | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: Contains an operand of the bitwise AND and receives the result.
- **const UByte** *Oper*: The second operand of the bitwise AND.

#### Description

Performs a bitwise AND operation between "Dest" and "Oper" and stores the result back into "Dest". If the Source Bank is 0 then the â€œOperâ€ is the operand to AND with. If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the address in that bank where the operand is.
