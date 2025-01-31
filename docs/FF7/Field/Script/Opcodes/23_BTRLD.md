---
title: 23_BTRLD
---

- Opcode: **0x23**
- Short name: **BTRLD**
- Long name: Battle Result Load

#### Memory layout

| 0x23 | *B* | *A* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to store result; should be a 16-bit bank.
- **const UByte** *A*: Address to store result.

#### Description

Stores the result of the last [BATTLE](70_BATTLE) to an address in memory. The resulting value can then be examined to see what the outcome of the battle was.

#### Results

| Bit to AND | Bit Result & Description |
|----|----|
| 8 (0x1000) | 1: The party escaped the battle. |
|  | 0: The party did not escape. |
| 1 (0x1) | 1: The party was defeated (correct [battle mode](FF7/Field/Script/Opcodes/22_BTMD2 "wikilink") must be set to avoid [game over](FF_GAMEOVER). |
|  | 0: The party was not defeated. |
|  |  |
