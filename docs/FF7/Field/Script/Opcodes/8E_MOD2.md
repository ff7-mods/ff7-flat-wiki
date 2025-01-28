---
title: 8E_MOD2
---

- Opcode: **0x8E**
- Short name: **MOD2**
- Long name: Modulus (16-bit)

#### Memory layout

| 0x8E | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

- **const Bit\[4\]** *D*: Destination bank
- **const Bit\[4\]** *S*: Source bank
- **const UByte** *Dest*: Contains the nominator of the division and receives the remainder.
- **const SWord** *Den*: The denominator of the division.

#### Description

Divides Ã¢â¬ÅDestÃ¢â¬Â by Ã¢â¬ÅDenÃ¢â¬Â and stores the remainder back into Ã¢â¬ÅDestÃ¢â¬Â. If the Source Bank is 0 then the Ã¢â¬ÅDenÃ¢â¬Â is the denominator. If the Source Bank is an 16 bit bank, then the Ã¢â¬ÅDenÃ¢â¬Â is the address in that bank where the denominator is.
