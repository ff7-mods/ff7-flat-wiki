---
title: 6F SCRLP
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 6F SCRLP

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

  [Type]: ../63%20SCRLA.md "wikilink"
