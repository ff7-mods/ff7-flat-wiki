---
title: 84 BITXOR
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 84 BITXOR

-   Opcode: **0x84**
-   Short name: **BITXOR**
-   Long name: Toggle Bit

#### Memory layout

| 0x84 | *D / S* | *Dest* | *Bit* |
|------|---------|--------|-------|

#### Arguments

-   **const Bit\[4\]** *D*: Destination bank.
-   **const Bit\[4\]** *S*: Source bank.
-   **const UByte** *Dest*: Destination address.
-   **const UByte** *Bit*: The number of the bit to turn toggle.

#### Description

Toggles the nth bit in the "Dest" location, where n is a number between
0-7 supplied in "Bit". A value of zero in "Bit" will toggle the least
significant bit. If the Source Bank is 0 then the bit to be changed is
taken from "Bit". If the Source Bank is an 8 bit bank, then the
â€œBitâ€ is the address in that bank where the operand is.
