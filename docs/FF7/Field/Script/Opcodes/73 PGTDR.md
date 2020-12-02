---
title: 73 PGTDR
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 73 PGTDR

-   Opcode: **0x73**
-   Short name: **PGTDR**
-   Long name: Get Party Member Direction

#### Memory layout

| 0x73 | *B* | *P* | *D* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to store direction.
-   **const UByte** *P*: Party member ID, from 0 to 2.
-   **const UByte** *D*: Address to store direction.

#### Description

Fetches the orientation of the party member specified by *P* on the
field, into the bank and address specified by *B* and *D*.
