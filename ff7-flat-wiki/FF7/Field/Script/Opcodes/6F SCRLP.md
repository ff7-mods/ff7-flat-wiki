---
title: 6F SCRLP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 6F SCRLP

-   Opcode: **0x6F**
-   Short name: **SCRLP**
-   Long name: Scroll To Party Member

#### Memory layout

| 0x63 | *B* | *S* | *P* | *T* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank for the scroll speed, or zero if it is
    specified as a literal value.
-   **const UShort** *S*: Speed of the scroll, in frames, or the address
    to find the speed if *B* is non-zero.
-   **const UByte** *P*: Party ID to scroll to, between 0 and 2.
-   **const UByte** *T*: [Type][] of scroll.

#### Description

Similar to [SCRLA][Type], except the scroll moves towards the given
party member, rather than a particular entity.

  [Type]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/63%20SCRLA.md "wikilink"
