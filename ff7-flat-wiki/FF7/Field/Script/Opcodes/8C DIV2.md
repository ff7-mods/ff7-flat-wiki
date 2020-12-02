---
title: 8C DIV2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 8C DIV2

-   Opcode: **0x8C**
-   Short name: **DIV2**
-   Long name: Division (16-bit)

#### Memory layout

| 0x8C | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: Contains the nominator of the division and
    receives the quotient.
-   **const SWord** *Den*: The denominator of the division.

#### Description

Divides â€œDestâ€ by â€œDenâ€ and stores the result back into
â€œDestâ€. The result of the division is rounded towards negative
infinity to the nearest integer. If the Source Bank is 0 then the
â€œDenâ€ is the denominator. If the Source Bank is an 16 bit bank, then
the â€œDenâ€ is the address in that bank where the denominator is.
