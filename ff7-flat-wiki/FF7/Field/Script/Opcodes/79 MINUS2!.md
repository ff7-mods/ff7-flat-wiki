---
title: 79 MINUS2!
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 79 MINUS2!

-   Opcode: **0x79**
-   Short name: **MINUS2!**
-   Long name: Saturated Subtraction (16-bit)

#### Memory layout

| 0x79 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: The destination variable, to which the
    operand is subtracted.
-   **const SWord** *Oper*: The operand to be subtracted from the
    destination.

#### Description

Subtracts "Oper" from "Dest" and stores the result back into "Dest". The
result of the subtraction is capped at -32768. The result is not capped
at the positive end (32767), so subtracting a large negative number from
a large positive number will still produce wrap-around. If the Source
Bank is 0 then the â€œOperâ€ is subtracted from the destination value.
If the Source Bank is an 16 bit bank, then the â€œOperâ€ is the address
in that bank where the operand is.
