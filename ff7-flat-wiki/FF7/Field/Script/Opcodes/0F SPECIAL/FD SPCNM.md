---
title: FD SPCNM
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > [0F SPECIAL](/ff7-flat-wiki/FF7/Field/Script/Opcodes/0F%20SPECIAL.md) > FD SPCNM

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
