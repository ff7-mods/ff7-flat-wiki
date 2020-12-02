---
title: 03 REQEW
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 03 REQEW

-   Opcode: **0x03**
-   Short name: **REQEW**
-   Long name: Request remote execution (synchronous, guaranteed)

#### Memory layout

| 0x03 | *E* | *P / F* |
|------|-----|---------|

#### Arguments

-   **const UByte** *E*: The ID of the target [entity][].
-   **const Bit\[3\]** *P*: The [priority][] at which we want to execute
    the remote script (high 3 bits of byte).
-   **const Bit\[5\]** *F*: The ID of the specific member function of
    *E* to be executed (low 5 bits of byte).

#### Description

Requests that a remote entity executes one of its member functions at a
specified priority. The request will block until remote execution has
finished before returning.

  [entity]: /ff7-flat-wiki/FF7/Field/Script/Entity.md "wikilink"
  [priority]: /ff7-flat-wiki/FF7/Field/Script/Priorities.md "wikilink"
