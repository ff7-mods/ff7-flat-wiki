---
title: 8D_MOD
---

[Home](../../../../Main_Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 8D MOD

-   Opcode: **0x8D**
-   Short name: **MOD**
-   Long name: Modulus (8-bit)

#### Memory layout

| 0x8D | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: Contains the nominator of the division and receives the remainder.
-   **const UByte** *Den*: The denominator of the division.

#### Description

Divides â€œDestâ€ by â€œDenâ€ and stores the remainder back into â€œDestâ€. If the Source Bank is 0 then the â€œDenâ€ is the denominator. If the Source Bank is an 8 bit bank, then the â€œDenâ€ is the address in that bank where the denominator is.
