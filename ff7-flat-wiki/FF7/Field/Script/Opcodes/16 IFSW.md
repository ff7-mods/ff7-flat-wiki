---
title: 16 IFSW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 16 IFSW

-   Opcode: **0x16**
-   Short name: **IFSW**
-   Long name: If (Signed Word)

#### Memory layout

| 0x16 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: First memory bank to access.
-   **const Bit\[4\]** *B2*: Second memory bank to access.
-   **const UShort** *A*: Address, from the first bank, of the value to
    retrieve.
-   **const Short** *V*: Unsigned value to compare the retrieved value
    to, or address from the second bank of the value to retrieve, if
    *B2* is non-zero.
-   **const UByte** *C*: Type of comparison to perform.
-   **const UByte** *E*: Amount to jump if the comparison does not hold.

#### Description

This is similar to the [IFUW][] opcode, but the value compared to may be
negative.

  [IFUW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/18%20IFUW.md "wikilink"
