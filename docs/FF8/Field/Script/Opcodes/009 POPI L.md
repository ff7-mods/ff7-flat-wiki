---
title: 009 POPI L
permalink: 009 POPI L.html
---

[Home](../../../../Main%20Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 009 POPI L

-   Opcode: **0x009**
-   Short name: **POPI\_L**
-   Long name: Pop to Temp List (long)

#### Argument

Index position in the Temp List (0 &lt;= **Argument** &lt; 8).

#### Stack

..., *value* =&gt; ...

#### Description

Pop the top *value* from the stack and store the first four bytes (long)
at index position **Argument** in the Temp List.
