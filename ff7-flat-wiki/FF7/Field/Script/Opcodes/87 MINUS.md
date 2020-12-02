---
title: 87 MINUS
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 87 MINUS

-   Opcode: **0x87**
-   Short name: **MINUS**
-   Long name: Subtraction (8-bit)

#### Memory layout

| 0x87 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: The destination variable, to which the
    operand is subtracted.
-   **const UByte** *Oper*: The operand to be subtracted from the
    destination.

#### Description

Subtracts two numbers and stores the result back into â€œDestâ€. The
result of the subtraction wraps around into the range of 0-255. If the
Source Bank is 0 then the â€œOperâ€ is subtracted from the destination
value. If the Source Bank is an 8 bit bank, then the â€œOperâ€ is the
address in that bank where the operand is.
