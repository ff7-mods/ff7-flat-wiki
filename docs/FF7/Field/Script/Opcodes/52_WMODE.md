---
title: 52_WMODE
---

- Opcode: **0x52**
- Short name: **WMODE**
- Long name: Window Mode

#### Memory layout

| 0x52 | *N* | *M* | *C* |
|------|-----|-----|-----|

#### Arguments

- **const UByte** *N*: The ID of the window whose mode will be set.
- **const UByte** *M*: Mode of the window.
- **const UByte** *C*: Window permanency.

#### Description

Changes properties associated with the [WINDOW](50_WINDOW) whose ID is specified. The mode byte sets the style of the window, as detailed below. If the final byte is set to 1, the window cannot be closed by the player pushing \[OK\].

The mode of the window should be changed before it is displayed with [MESSAGE](FF7/Field/Script/Opcodes/40_MESSAGE "wikilink") or [ASK](48_ASK), or the changes will not be visible unless the window is closed and reopened.

#### Mode Table

| ID  | Mode                   |
|-----|------------------------|
| 0   | Normal                 |
| 1   | No Background/Border   |
| 2   | Transparent Background |
|     |                        |
