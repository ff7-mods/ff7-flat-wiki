---
title: 2B_SLIP
---

- Opcode: **0x2B**
- Short name: **SLIP**
- Long name: Slipability

#### Memory layout

| 0x2B | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: On/off switch (0/1, respectively).

#### Description

If SLIP is set to off, the player will be unable to let the playable character run *against* and *along* the wall by pressing two buttons together. For example, if there is a wall beyond the character running left-to-right, and the character presses up and right together, the character will normally run to the right along the wall. If SLIP is off, the character will stop moving until the player presses right by itself; the combination of up and right together is disallowed. This is sometimes used in areas such as shops.

This should be used in combination with a [LINE](D0_LINE) to specify the line along which the player may not 'slip'.
