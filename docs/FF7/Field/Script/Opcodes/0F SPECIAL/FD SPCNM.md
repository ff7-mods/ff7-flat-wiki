---
title: FD SPCNM
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > [0F SPECIAL](FF7/Field/Script/Opcodes/0F%20SPECIAL.md) > FD SPCNM

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
