---
title: 34 PDIRA
permalink: 34 PDIRA.html
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 34 PDIRA

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

  [PTURA]: 35%20PTURA.md "wikilink"
  [MMBud]: CD%20MMBud.md "wikilink"
