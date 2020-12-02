---
title: 10 JMPF
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 10 JMPF

-   Opcode: **0x10**
-   Short name: **JMPF**
-   Long name: Jump forward

#### Memory layout

| 0x10 | *A* |
|------|-----|

#### Arguments

-   **const UByte** *A*: Amount to jump forward.

#### Description

Jumps forward in the current script a specified amount. The jump begins
just after the jump opcode itself and then skips the specified number of
bytes. In the following example, the [WAIT][] line is skipped.

    JMPF (04)
    WAIT (70,00)
    SOLID (01)

If a jump longer than 0xFF is required, use [JMPFL][] instead.

  [WAIT]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/24%20WAIT.md "wikilink"
  [JMPFL]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/11%20JMPFL.md "wikilink"
