---
title: 01 TRNSP
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [Field](/ff7-flat-wiki/FF7/Field.md) > [Script](/ff7-flat-wiki/FF7/Field/Script.md) > [Opcodes](/ff7-flat-wiki/FF7/Field/Script/Opcodes.md) > [28 KAWAI](/ff7-flat-wiki/FF7/Field/Script/Opcodes/28%20KAWAI.md) > 01 TRNSP

-   Opcode: **0x28/01**
-   Short name: **KAWAI/TRNSP**
-   Long name: Character Transparency

#### Memory layout

| 0x28 | *4* | *1* | *S* |
|------|-----|-----|-----|

#### Arguments

-   **const UByte** *4*: Total length of opcode and argument list.
-   **const UByte** *1*: Subop code.
-   **const UByte** *S*: Switch on/off (1/0, respectively).

#### Description

Makes the whole field object, associated with the entity in which script
this opcode resides, semi-transparent.
