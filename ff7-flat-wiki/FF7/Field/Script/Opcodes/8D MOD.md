---
title: 8D MOD
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 8D MOD

-   Opcode: **0x8D**
-   Short name: **MOD**
-   Long name: Modulus (8-bit)

#### Memory layout

| 0x8D | *D/S* | *Dest* | *Den* |
|------|-------|--------|-------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: Contains the nominator of the division and
    receives the remainder.
-   **const UByte** *Den*: The denominator of the division.

#### Description

Divides â€œDestâ€ by â€œDenâ€ and stores the remainder back into
â€œDestâ€. If the Source Bank is 0 then the â€œDenâ€ is the
denominator. If the Source Bank is an 8 bit bank, then the â€œDenâ€ is
the address in that bank where the denominator is.
