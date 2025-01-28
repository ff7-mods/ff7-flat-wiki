---
title: 73_PGTDR
---

- Opcode: **0x73**
- Short name: **PGTDR**
- Long name: Get Party Member Direction

#### Memory layout

| 0x73 | *B* | *P* | *D* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store direction.
- **const UByte** *P*: Party member ID, from 0 to 2.
- **const UByte** *D*: Address to store direction.

#### Description

Fetches the orientation of the party member specified by *P* on the field, into the bank and address specified by *B* and *D*.
