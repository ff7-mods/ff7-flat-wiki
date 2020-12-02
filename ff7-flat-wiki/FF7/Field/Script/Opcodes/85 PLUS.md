---
title: 85 PLUS
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 85 PLUS

-   Opcode: **0x85**
-   Short name: **PLUS**
-   Long name: Addition (8-bit)

#### Memory layout

| 0x85 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: The destination variable, to which the
    operand is added.
-   **const UByte** *Oper*: The operand, added to the destination.

#### Description

Adds two numbers together and stores the result back into â€œDestâ€.
The result of the addition wraps around into the range of 0-255. If the
Source Bank is 0 then the â€œOperâ€ is added to the destination value.
If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the address
in that bank where the operand is.
