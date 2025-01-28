---
title: CA_PRTYE
---

- Opcode: **0xCA**
- Short name: **PRTYE**
- Long name: Party Change

#### Memory layout

| 0xCA | *1* | *2* | *3* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *1*: Character ID for first party character.
- **const UByte** *2*: Character ID for second party character.
- **const UByte** *3*: Character ID for third party character.

#### Description

Changes the current party to the characters specified by each of the three arguments, or leaves the party member blank if the ID is 0xFE. Note that the chocobo entry will crash during battle, and that Young Cloud and Sephiroth occupy the same 'slots' used by Vincent and Cait Sith's character entries.

#### Character IDs

| ID  | Character    |
|-----|--------------|
| 0   | Cloud        |
| 1   | Barret       |
| 2   | Tifa         |
| 3   | Aeris        |
| 4   | Red XIII     |
| 5   | Yuffie       |
| 6   | Cait Sith    |
| 7   | Vincent      |
| 8   | Cid          |
| 9   | Young Cloud  |
| A   | Sephiroth    |
| B   | Chocobo      |
| FE  | No character |
|     |              |
