---
title: 01 REQ
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 01 REQ

-   Opcode: **0x01**
-   Short name: **REQ**
-   Long name: Request remote execution (asynchronous, non-guaranteed)

#### Memory layout

| 0x01 | *E* | *P / F* |
|------|-----|---------|

#### Arguments

-   **const UByte** *E*: The ID of the target [entity][].
-   **const Bit\[3\]** *P*: The [priority][] at which we want to execute
    the remote script (high 3 bits of byte).
-   **const Bit\[5\]** *F*: The ID of the specific member function of
    *E* to be executed (low 5 bits of byte).

#### Description

Requests that a remote entity executes one of its member functions at a
specified priority. The request is asynchronous and returns immediately
without waiting for the remote execution to start or finish. If the
specified priority is already busy executing, the request will fail
silently.

  [entity]: /ff7-flat-wiki/FF7/Field/Script/Entity.md "wikilink"
  [priority]: /ff7-flat-wiki/FF7/Field/Script/Priorities.md "wikilink"
