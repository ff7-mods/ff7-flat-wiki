---
title: 0CD SESTOP
---

[Home](../../../../Main Page.md) > [FF8](../../../../FF8.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 0CD SESTOP

-   Opcode: **0x0CD**
-   Short name: **SESTOP**
-   Long name: Stop sound effect

#### Argument

none

#### Stack

  
*Channel (must be a power of 2)*

**SESTOP**

#### Description

Stop the sound effect currently playing on the given channel. Channel is defined in the call to [EFFECTPLAY2](021 EFFECTPLAY2.md) and must be a power of 2.
