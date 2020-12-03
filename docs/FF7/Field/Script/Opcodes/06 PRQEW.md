---
title: 06 PRQEW
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 06 PRQEW

-   Opcode: **0x06**
-   Short name: **PRQEW**
-   Long name: Request party entity execution (synchronous, guaranteed)

#### Memory layout

| 0x06 | *PM* | *P / F* |
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
request will block until remote execution has finished before returning.

  [priority]: ../Priorities.md "wikilink"
