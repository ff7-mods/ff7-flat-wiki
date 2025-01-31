---
title: 02_REQSW
---

- Opcode: **0x02**
- Short name: **REQSW**
- Long name: Request remote execution (asynchronous execution, guaranteed)

#### Memory layout

| 0x02 | *E* | *P / F* |
|------|-----|---------|

#### Arguments

- **const UByte** *E*: The ID of the target [entity](../Entity).
- **const Bit\[3\]** *P*: The [priority](../Priorities).
- **const Bit\[5\]** *F*: The ID of the specific member function of *E* to be executed (low 5 bits of byte).

#### Description

Requests that a remote entity executes one of its member functions at a specified priority. If the specified priority is already busy executing, the request will block until it becomes available and only then return. The remote execution is still carried out asynchronously, with no notification of completion.
