---
title: 52 WMODE
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > [Opcodes](/FF7/Field/Script/Opcodes.md) > 52 WMODE

-   Opcode: **0x52**
-   Short name: **WMODE**
-   Long name: Window Mode

#### Memory layout

| 0x52 | *N* | *M* | *C* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *N*: The ID of the window whose mode will be set.
-   **const UByte** *M*: Mode of the window.
-   **const UByte** *C*: Window permanency.

#### Description

Changes properties associated with the [WINDOW][] whose ID is specified.
The mode byte sets the style of the window, as detailed below. If the
final byte is set to 1, the window cannot be closed by the player
pushing \[OK\].

The mode of the window should be changed before it is displayed with
[MESSAGE][] or [ASK][], or the changes will not be visible unless the
window is closed and reopened.

#### Mode Table

| ID  | Mode                   |
|-----|------------------------|
| 0   | Normal                 |
| 1   | No Background/Border   |
| 2   | Transparent Background |
|     |                        |

  [WINDOW]: /FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [MESSAGE]: /FF7/Field/Script/Opcodes/40%20MESSAGE.md "wikilink"
  [ASK]: /FF7/Field/Script/Opcodes/48%20ASK.md "wikilink"
