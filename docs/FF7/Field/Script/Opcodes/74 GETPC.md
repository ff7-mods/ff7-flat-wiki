---
title: 74 GETPC
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 74 GETPC

-   Opcode: **0x74**
-   Short name: **GETPC**
-   Long name: Get Party Character

#### Memory layout

| 0x74 | *B* | *C* | *A* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store the value.
-   **const UByte** *C*: Character offset in the party whose value
    should be retrieved.
-   **const UByte** *A*: Address to store the value.

#### Description

Gets the standard [Character ID][] for the party member, referenced by
*C*. This value is between 0 and 2; 0 for the party member at the top of
the list, 1 for the member in the middle, and 2 for the member in the
bottom slot, as found in the main menu. The character ID is then placed
at the specified bank and address.

  [Character ID]: /ff7-flat-wiki/FF7/Field/Character%20ID.md "wikilink"
