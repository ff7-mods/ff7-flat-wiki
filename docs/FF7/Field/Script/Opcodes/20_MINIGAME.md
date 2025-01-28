---
title: 20_MINIGAME
---

- Opcode: **0x20**
- Short name: **MINIGAME**
- Long name: Minigame Start

#### Memory layout

| 0x20 | *M* | *X* | *Y* | *Z* | *G* | *T* |
|------|-----|-----|-----|-----|-----|-----|

#### Arguments

- **const UShort** *M*: Map ID to return to after game has completed.
- **const Short** *X*: X-coordinate of the player after game has completed.
- **const Short** *Y*: Y-coordinate of the player after game has completed.
- **const Short** *Z*: Z-coordinate of the player after game has completed.
- **const UByte** *G*: Game-specific value.
- **const UByte** *T*: Minigame type; see table below.

#### Description

Begins the minigame as defined by the final byte. Once the minigame has completed, the map ID given as the argument is loaded and the playable character is moved to the XYZ co-ordinates also specified. If an invalid minigame ID is passed as the final argument, the return map is loaded immediately.

#### Minigame IDs

| ID | Minigame |
|----|----|
| 0 | Bike |
| 1 | Chocobo Races |
| 2 | Snowboard (Icicle version; no music or menu) |
| 3 | Fort Condor |
| 4 | Submarine |
| 5 | Speed Square |
| 6 | Snowboard (Gold Saucer version; music plays and the Retry menu can be accessed) |
|  |  |
