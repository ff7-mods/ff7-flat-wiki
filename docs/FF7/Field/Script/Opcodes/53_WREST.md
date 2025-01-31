---
title: 53_WREST
---

- Opcode: **0x53**
- Short name: **WREST**
- Long name: Window Reset

#### Memory layout

| 0x53 | *N* |
|------|-----|

#### Arguments

- **const UByte** *N*: The ID of the window to reset.

#### Description

Resets the given window, including the following parameters:

- Position and size, set by [WMOVE](FF7/Field/Script/Opcodes/51_WMOVE "wikilink"), [WSIZW](FF7/Field/Script/Opcodes/2F_WSIZW "wikilink"), [WROW](FF7/Field/Script/Opcodes/55_WROW "wikilink") or even the initial values set by [WINDOW](50_WINDOW);
- Background type, set by [WMODE](52_WMODE);
- Numerical displays, set by [WSPCL](36_WSPCL);
- Message parameters, set by [MPARA](FF7/Field/Script/Opcodes/41_MPARA "wikilink") and [MPRA2](42_MPRA2).

The reset window has a position of approximately (5,5), with a width and height of approximately (0x130, 0x45).
