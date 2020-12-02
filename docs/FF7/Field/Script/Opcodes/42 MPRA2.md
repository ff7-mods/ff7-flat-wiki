---
title: 42 MPRA2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 42 MPRA2

-   Opcode: **0x42**
-   Short name: **MPRA2**
-   Long name: Message Parameter (16-bit)

#### Memory layout

| 0x42 | *B* | *W* | *I* | *V* |
|------|-----|-----|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank to retrieve value from, or zero if using a
    literal value.
-   **const UByte** *W*: [WINDOW][] ID for this parameter.
-   **const UByte** *I*: ID of the "[Variable][]" dialog code that this
    value will replace.
-   **const UShort** *V*: Value to insert into dialog, or address of
    value, if *B* is non-zero.

#### Description

Similar to [MPARA][], but allows a constant value of greater than one
byte to be supplied. This does not apply if *B* is non-zero, as the
address the value is retrieved from must be in the range 0 to 0xFF.

  [WINDOW]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [Variable]: /ff7-flat-wiki/FF7/Field/Variable%20Dialog.md "wikilink"
  [MPARA]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/41%20MPARA.md "wikilink"
