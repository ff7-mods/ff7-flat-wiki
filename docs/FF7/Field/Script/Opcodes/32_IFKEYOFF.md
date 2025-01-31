---
title: 32_IFKEYOFF
---

- Opcode: **0x32**
- Short name: **IFKEYOFF**
- Long name: If Key Lifted

#### Memory layout

| 0x32 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UShort (Bit field)** *B*: Button ID to check for.
- **const UByte** *A*: Amount to jump if condition is false.

#### Description

Similar to [IFKEYON](31_IFKEYON). Rather than check if this is the first time the user has pressed the button with the given ID, **IFKEYOFF** will not execute the body of the "if" statement until the user has lifted the key that was previously held down or pressed. This way, the body of the statement will only be executed once, when the key is no longer pressed.
