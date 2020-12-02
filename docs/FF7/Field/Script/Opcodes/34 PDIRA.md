---
title: 34 PDIRA
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 34 PDIRA

-   Opcode: **0x34**
-   Short name: **PDIRA**
-   Long name: Face Party Member

#### Memory layout

| 0x34 | *C* |
|------|-----|

#### Arguments

-   **const UByte** *C*: Character ID to face.

#### Description

Instantly turns the field object to face the party member specified by
**C**. In contrast to [PTURA][], the turn is not gradual, and the
parameter is not a party member ID (from 0 for the first to 2 for the
third in the party), but a Character ID (like in [MMBud][]). If the
specified character ID is not in your party, the field object will turn
to the main character.

  [PTURA]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/35%20PTURA.md "wikilink"
  [MMBud]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/CD%20MMBud.md "wikilink"
