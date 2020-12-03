---
title: 10 JMPF
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 10 JMPF

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

  [WAIT]: 24%20WAIT.md "wikilink"
  [JMPFL]: 11%20JMPFL.md "wikilink"
