---
title: 0CD SESTOP
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > [Opcodes](FF8/Field/Script/Opcodes.md) > 0CD SESTOP

-   Opcode: **0x0CD**
-   Short name: **SESTOP**
-   Long name: Stop sound effect

#### Argument

none

#### Stack

  
*Channel (must be a power of 2)*

**SESTOP**

#### Description

Stop the sound effect currently playing on the given channel. Channel is
defined in the call to [EFFECTPLAY2][] and must be a power of 2.

  [EFFECTPLAY2]: ../021%20EFFECTPLAY2.md "wikilink"
