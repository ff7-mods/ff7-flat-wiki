---
title: 12 JMPB
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 12 JMPB

-   Opcode: **0x12**
-   Short name: **JMPB**
-   Long name: Jump back

#### Memory layout

| 0x10 | *A* |
|------|-----|

#### Arguments

-   **const UByte** *A*: Amount to jump backwards.

#### Description

Jumps backward in the current script a specified amount. The jump begins
just before the jump opcode itself and then moves the current byte
pointer back the specified number of bytes. In the following example,
the [SOLID][] and [WAIT][] lines are repeated indefinitely.

    SOLID (01)
    WAIT (70,00)
    JMPF (05)

If a jump longer than 0xFF is required, use [JMPBL][] instead.

  [SOLID]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/C7%20SOLID.md "wikilink"
  [WAIT]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/24%20WAIT.md "wikilink"
  [JMPBL]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/13%20JMPBL.md "wikilink"
