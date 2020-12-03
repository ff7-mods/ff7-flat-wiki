---
title: 19 IFUWL
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 19 IFUWL

-   Opcode: **0x19**
-   Short name: **IFUWL**
-   Long name: If (Unsigned Word, Long Jump)

#### Memory layout

| 0x19 | *B1 / B2* | *A* | *V* | *C* | *E* |
|------|-----------|-----|-----|-----|-----|

#### Arguments

-   **const Bit\[4\]** *B1*: First memory bank to access.
-   **const Bit\[4\]** *B2*: Second memory bank to access.
-   **const UShort** *A*: Address, from the first bank, of the value to
    retrieve.
-   **const UShort** *V*: Unsigned value to compare the retrieved value
    to, or address from the second bank of the value to retrieve, if
    *B2* is non-zero.
-   **const UByte** *C*: Type of comparison to perform.
-   **const UShort** *E*: Amount to jump if the comparison does not
    hold.

#### Description

This is similar to the [IFUW][] opcode, but allows for a jump on
comparison failure of more than 0xFF bytes.

  [IFUW]: 18%20IFUW.md "wikilink"
