---
title: 06_PRQEW
---

- Opcode: **0x06**
- Short name: **PRQEW**
- Long name: Request party entity execution (synchronous, guaranteed)

#### Memory layout

| 0x06 | *PM* | *P / F* |
|------|------|---------|

#### Arguments

- **const UByte** *PM*: The ID of the current party member (0, 1 or 2).
- **const Bit\[3\]** *P*: The [priority](../Priorities).
- **const Bit\[5\]** *F*: The ID of the specific member function of *PM* 's entity to be executed (low 5 bits of byte).

#### Description

Requests that the entity associated with a character in the current party executes one of its member functions at a specified priority. The request will block until remote execution has finished before returning.
