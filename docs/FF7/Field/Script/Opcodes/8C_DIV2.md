---
title: 8C_DIV2
---

- Opcode: **0x8C**
- Short name: **DIV2**
- Long name: Division (16-bit)

#### Memory layout

| 0x8C | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: Contains the nominator of the division and receives the quotient.
- **const SWord** *Den*: The denominator of the division.

#### Description

Divides â€œDestâ€ by â€œDenâ€ and stores the result back into â€œDestâ€. The result of the division is rounded towards negative infinity to the nearest integer. If the Source Bank is 0 then the â€œDenâ€ is the denominator. If the Source Bank is an 16 bit bank, then the â€œDenâ€ is the address in that bank where the denominator is.
