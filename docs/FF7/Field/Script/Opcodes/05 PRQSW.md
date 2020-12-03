---
title: 05 PRQSW
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 05 PRQSW

-   Opcode: **0x05**
-   Short name: **PRQSW**
-   Long name: Request party entity execution (asynchronous execution,
    guaranteed)

#### Memory layout

| 0x05 | *PM* | *P / F* |
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
party executes one of its member functions at a specified priority. If
the specified priority is already busy executing, the request will block
until it becomes available and only then return. The remote execution is
still carried out asynchronously, with no notification of completion.

  [priority]: FF7/Field/Script/Priorities.md "wikilink"
