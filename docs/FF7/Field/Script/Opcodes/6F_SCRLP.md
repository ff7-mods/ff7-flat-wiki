---
title: 6F_SCRLP
---

[Home](../../../../index.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 6F SCRLP

-   Opcode: **0x6F**
-   Short name: **SCRLP**
-   Long name: Scroll To Party Member

#### Memory layout

| 0x63 | *B* | *S* | *P* | *T* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank for the scroll speed, or zero if it is specified as a literal value.
-   **const UShort** *S*: Speed of the scroll, in frames, or the address to find the speed if *B* is non-zero.
-   **const UByte** *P*: Party ID to scroll to, between 0 and 2.
-   **const UByte** *T*: [Type](63_SCRLA.md) of scroll.

#### Description

Similar to [SCRLA](63_SCRLA.md), except the scroll moves towards the given party member, rather than a particular entity.
