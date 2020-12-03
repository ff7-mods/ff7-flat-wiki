---
title: FB MVCAM
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > FB MVCAM

-   Opcode: **0xFB**
-   Short name: **MVCAM**
-   Long name: Movie Camera Switch

#### Memory layout

| 0xFB | *S* |
|------|-----|

#### Arguments

-   **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Turns on or off the use of the camera supplied by a movie file, that will be played at a future point in the script. If off, the field camera remains in use. If set to on, the camera defined in the movie file is used, including any movement of the camera to match the movie itself.
