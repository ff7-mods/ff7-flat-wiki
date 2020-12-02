---
title: 6C FADEW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 6C FADEW

-   Opcode: **0x6C**
-   Short name: **FADEW**
-   Long name: Wait for fade

#### Memory layout

| 0x6C |
|------|

#### Arguments

None.

#### Description

Halts execution of the current script for a preceding [FADE][] command,
issued by any entity, to fully complete before continuing execution. If
no FADE has been issued by any entity, or previous FADE calls have
already completed, the FADEW call is ignored.

  [FADE]: /ff7-flat-wiki/FF7/Field/Script/Opcodes/6B%20FADE.md "wikilink"
