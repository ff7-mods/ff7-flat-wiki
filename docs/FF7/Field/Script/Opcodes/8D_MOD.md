---
title: 8D_MOD
---

- Opcode: **0x8D**
- Short name: **MOD**
- Long name: Modulus (8-bit)

#### Memory layout

| 0x8D | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: Contains the nominator of the division and receives the remainder.
- **const UByte** *Den*: The denominator of the division.

#### Description

Divides â€œDestâ€ by â€œDenâ€ and stores the remainder back into â€œDestâ€. If the Source Bank is 0 then the â€œDenâ€ is the denominator. If the Source Bank is an 8 bit bank, then the â€œDenâ€ is the address in that bank where the denominator is.
