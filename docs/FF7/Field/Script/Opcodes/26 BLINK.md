---
title: 26 BLINK
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > 26 BLINK

-   Opcode: **0x26**
-   Short name: **BLINK**
-   Long name: Character Blink

#### Memory layout

| 0x26 | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Specifies whether the eyes of the current entity's visible object should
blink at random intervals. As there is no argument to specify which
character this refers to, this opcode must be placed in the correct
character entity's script.

To open or shut the character's eyes (change the eye texture used), use
[KAWAI][].

  [KAWAI]: /FF7/Field/Script/Opcodes/28%20KAWAI.md "wikilink"
