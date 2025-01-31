---
title: 01_REQ
---

- Opcode: **0x01**
- Short name: **REQ**
- Long name: Request remote execution (asynchronous, non-guaranteed)

#### Memory layout

| 0x01 | *E* | *P / F* |
|------|-----|---------|

#### Arguments

- **const UByte** *E*: The ID of the target [entity](../Entity).
- **const Bit\[3\]** *P*: The [priority](../Priorities).
- **const Bit\[5\]** *F*: The ID of the specific member function of *E* to be executed (low 5 bits of byte).

#### Description

Requests that a remote entity executes one of its member functions at a specified priority. The request is asynchronous and returns immediately without waiting for the remote execution to start or finish. If the specified priority is already busy executing, the request will fail silently.
