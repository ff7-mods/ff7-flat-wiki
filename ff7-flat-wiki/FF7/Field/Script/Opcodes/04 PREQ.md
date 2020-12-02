---
title: 04 PREQ
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 04 PREQ

-   Opcode: **0x04**
-   Short name: **PREQ**
-   Long name: Request party entity execution (asynchronous,
    non-guaranteed)

#### Memory layout

| 0x04 | *PM* | *P / F* |
|------|------|---------|

#### Arguments

-   **const UByte** *PM*: The ID of the current party member (0, 1 or
    2).
-   **const Bit\[3\]** *P*: The [priority][] at which we want to execute
    the remote script (high 3 bits of byte).
-   **const Bit\[5\]** *F*: The ID of the specific member function of
    *PM* 's entity to be executed (low 5 bits of byte).

#### Description

Requests that the entity associated with a character in the current
party executes one of its member functions at a specified priority. The
request is asynchronous and returns immediately without waiting for the
remote execution to start or finish. If the specified priority is
already busy executing, the request will fail silently.

  [priority]: /ff7-flat-wiki/FF7/Field/Script/Priorities.md "wikilink"
