---
title: 4A MENU2
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > 4A MENU2

-   Opcode: **0x4A**
-   Short name: **MENU2**
-   Long name: Main menu accessibility

#### Memory layout

| 0x4A | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: On/off switch (0/1, respectively).

#### Description

Disables or enables access to the main menu through the \[MENU\]
key/button. Transitioning to another field will re-enable the menu.
