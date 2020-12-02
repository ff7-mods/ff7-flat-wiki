---
title: 93 XOR
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 93 XOR

-   Opcode: **0x93**
-   Short name: **XOR**
-   Long name: Bitwise XOR (8-bit)

#### Memory layout

| 0x93 | *D/S* | *Dest* | *Oper* |
|------|-------|--------|--------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank
-   **const Bit\[4\]** *S*: Source bank
-   **const UByte** *Dest*: Contains an operand of the bitwise XOR and
    receives the result.
-   **const UByte** *Oper*: The second operand of the bitwise XOR.

#### Description

Performs a bitwise XOR operation between "Dest" and "Oper" and stores
the result back into "Dest". If the Source Bank is 0 then the â€œOperâ€
is the operand to XOR with. If the Source Bank is an 8 bit bank, then
the â€œOperâ€ is the address in that bank where the operand is.
