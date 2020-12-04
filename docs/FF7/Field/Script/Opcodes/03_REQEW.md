---
title: 03_REQEW
---

-   Opcode: **0x03**
-   Short name: **REQEW**
-   Long name: Request remote execution (synchronous, guaranteed)

#### Memory layout

| 0x03 | *E* | *P / F* |
|------|-----|---------|

#### Arguments

-   **const UByte** *E*: The ID of the target [entity](../Entity.md).
-   **const Bit\[3\]** *P*: The [priority](../Priorities.md) at which we want to execute the remote script (high 3 bits of byte).
-   **const Bit\[5\]** *F*: The ID of the specific member function of *E* to be executed (low 5 bits of byte).

#### Description

Requests that a remote entity executes one of its member functions at a specified priority. The request will block until remote execution has finished before returning.
