---
title: 70 BATTLE
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 70 BATTLE

-   Opcode: **0x70**
-   Short name: **BATTLE**
-   Long name: Start Battle

#### Memory layout

| 0x70 | *B* | *N* |
|------|-----|-----|

#### Arguments

-   **const UByte** *B*: Bank (16-bit) to retrieve the address of the
    battle ID, or zero if it is given as a literal value.
-   **const UWord** *N*: Battle ID, or address to find ID if *B* is
    non-zero.

#### Description

This launches the battle module with whatever battle number is used in
the argument, or the value retrieved from memory location *N* if *B* is
non-zero. Battle 1, 2, and 999 (0x03E7) are debug battles.
