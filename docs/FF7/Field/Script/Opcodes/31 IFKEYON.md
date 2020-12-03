---
title: 31 IFKEYON
---

[Home](../../../../Main%20Page.md.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 31 IFKEYON

-   Opcode: **0x31**
-   Short name: **IFKEYON**
-   Long name: If Key Pressed (First Time)

#### Memory layout

| 0x31 | *B* | *A* |
|------|-----|-----|

#### Arguments

-   **const UShort (Bit field)** *B*: Button ID to check for.
-   **const UByte** *A*: Amount to jump if condition is false.

#### Description

Similar to [IFKEY][], **IFKEYON** checks if a button is being pressed
with the given ID (matching those in IFKEY). However, the body of the
"if" statement only executes if this is the first time the button has
been recorded as being pressed. If this is not the first time it is
being pressed (that is, the user has held the key down), the condition
evaluates to false, and the "if" statement body does not execute, moving
the script pointer forward by *A*.

This is an effective way to stop repeatedly executing the body of the
"if" statement due to the user holding the key down; thus, the body of
the statement will only execute once. The button state is reset when the
user lets go of the button, and at this point, IFKEYON may evaluate to
true once more when the button is repressed.

  [IFKEY]: 30%20IFKEY.md "wikilink"
