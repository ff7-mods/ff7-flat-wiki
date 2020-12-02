---
title: 32 IFKEYOFF
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 32 IFKEYOFF

-   Opcode: **0x32**
-   Short name: **IFKEYOFF**
-   Long name: If Key Lifted

#### Memory layout

| 0x32 | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UShort (Bit field)** *B*: Button ID to check for.
-   **const UByte** *A*: Amount to jump if condition is false.

#### Description

Similar to [IFKEYON][]. Rather than check if this is the first time the
user has pressed the button with the given ID, **IFKEYOFF** will not
execute the body of the "if" statement until the user has lifted the key
that was previously held down or pressed. This way, the body of the
statement will only be executed once, when the key is no longer pressed.

  [IFKEYON]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/31%20IFKEYON.md "wikilink"
