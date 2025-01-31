---
title: 41_MPARA
---

- Opcode: **0x41**
- Short name: **MPARA**
- Long name: Message Parameter (8-bit value/address)

#### Memory layout

| 0x41 | *B* | *W* | *I* | *V* |
|------|-----|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve value from, or zero if using a literal value.
- **const UByte** *W*: [WINDOW](50_WINDOW) ID for this parameter.
- **const UByte** *I*: ID of the "[Variable](../../Variable_Dialog)" dialog code that this value will replace.
- **const UByte** *V*: Value to insert into dialog, or address of value, if *B* is non-zero.

#### Description

Replaces the [Variable Control Code](FF7/Field/Variable_Dialog "wikilink"), found in lines of dialog, with a specific value. This allows either literal values or values retrieved from memory to be displayed in message boxes. Message parameters are set, and then the dialog with the Variable control codes is displayed using [MESSAGE](40_MESSAGE), as normal.

The ID of the *W*indow must be provided, but this can be still be provided before the window has been created using [WINDOW](50_WINDOW). For lines of dialog with multiple Variable codes, the *I* argument identifies which code this value should replace, starting from zero for the first Variable code found in the line of dialog about to be displayed.

If *B* is non-zero, then bank *B* and address *V* will be accessed to retrieve the value that will be used in inserting into the dialog. Otherwise, the value provided by *V* is inserted as-is into the control code.

Whilst the *V* argument is one byte, if the address retrieved from is a 16-bit bank, a 16-bit value will display. The 8-bit nature of this opcode refers solely to the final argument size, and the size of the literal that can be specified. If a literal of greater than 0xFF is needed, [MPRA2](42_MPRA2) is used instead.
