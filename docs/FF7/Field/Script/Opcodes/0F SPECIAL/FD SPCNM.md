---
title: FD SPCNM
---

[Home](../../../../../Main%20Page.md.md) > [FF7](../../../../../FF7.md) > [Field](../../../../Field.md) > [Script](../../../Script.md) > [Opcodes](../../Opcodes.md) > [0F SPECIAL](../0F%20SPECIAL.md) > FD SPCNM

-   Opcode: **0x0FFD**
-   Short name: **SPECIAL: SPCNM**
-   Long name: Special: Change Character Name

#### Memory layout

| 0x0F | 0xFD | *M* | *T* |
|------|------|-----|-----|

-   **const UByte** *M*: Model ID of character.
-   **const UByte** *T*: Text ID of text.

#### Description

This needs to be tested to confirm. This changes the name of a
character.
