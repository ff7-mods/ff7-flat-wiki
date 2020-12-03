---
title: 03 REQEW
---

[Home](../../../../Main%20Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 03 REQEW

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

  [entity]: ../Entity.md "wikilink"
  [priority]: ../Priorities.md "wikilink"
