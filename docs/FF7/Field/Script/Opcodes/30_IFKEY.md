---
title: 30_IFKEY
---

- Opcode: **0x30**
- Short name: **IFKEY**
- Long name: If Key Pressed

#### Memory layout

| 0x30 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UShort (Bit field)** *B*: Button ID to check for.
- **const UByte** *A*: Amount to jump if button not pressed.

#### Description

Checks the status of a button being pressed; if pressed, regardless of the previous condition of the button press state (see [IFKEYON](FF7/Field/Script/Opcodes/31_IFKEYON "wikilink") / [IFKEYOFF](32_IFKEYOFF). If the checked button fails the condition check, then the script pointer moves ahead *A* bytes.

The highlighted keys in the button ID table below do not quite act as the rest when used with this particular opcode. For these keys, IFKEY acts in the same manner as IFKEYON; these keys cannot be checked repeatedly, and the if statement body will only execute once, regardless of whether the key is being held down.

Button IDs can be ORd with each other to produce a combination of keys to check in one statement. For example, IFKEY with a key ID of 0x00F0 will check if any of the directional buttons are being pressed.

#### Button IDs

| ID                         | Button \|-#     | 0b1 / 1 | L2 / Camera |
|----------------------------|-----------------|---------|-------------|
| 0b10 / 2                   | R2 / Target     |         |             |
| 0b100 / 4                  | L1 / PageUp     |         |             |
| 0b1000 / 8                 | L2 / PageDown   |         |             |
| 0b10000 / 16               | Triangle / Menu |         |             |
| 0b100000 / 32              | Circle / OK     |         |             |
| 0b1000000 / 64             | Cross / Cancel  |         |             |
| 0b10000000 / 128           | Square / Switch |         |             |
| 0b100000000 / 256          | Select / Assist |         |             |
| 0b1000000000 / 512         | Unknown 1       |         |             |
| 0b10000000000 / 1024       | Unknown 2       |         |             |
| 0b100000000000 / 2048      | Start / Pause   |         |             |
| 0b1000000000000 / 4096     | Up              |         |             |
| 0b10000000000000 / 8192    | Right           |         |             |
| 0b100000000000000 / 16384  | Down            |         |             |
| 0b1000000000000000 / 32768 | Left            |         |             |
|                            |                 |         |             |
