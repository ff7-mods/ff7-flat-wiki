---
title: 28 KAWAI
---

[Home](Main%20Page.md) > [FF7](FF7.md) > [Field](FF7/Field.md) > [Script](FF7/Field/Script.md) > [Opcodes](FF7/Field/Script/Opcodes.md) > 28 KAWAI

-   Opcode: **0x28**
-   Short name: **KAWAI**
-   Long name: Character Graphics Opcode (Multibyte sequence)

#### Memory layout

| 0x28 | *L* | *S* | *...* |
|------|-----|-----|-------|

#### Arguments

-   **const UByte** *L*: Total length of the entire opcode and argument
    list.
-   **const UByte** *S*: Operation to perform.
-   *Variable ...*: Sequence of arguments, depending on the operation
    type.

#### Description

KAWAI is a multipurpose, graphics-related opcode that performs a variety
of different operations on visible entity objects, depending on the
subop argument. It was named after Final Fantasy VII's Character
Programmer, Hiroshi Kawai.

#### Subcodes by Opcode

[`00`` ``EYETX`][]  
[`01`` ``TRNSP`][]  
[`02`` ``AMBNT`][]  
[`06`` ``LIGHT`][]  
[`0A`` ``SBOBJ`][]  
[`0D`` ``SHINE`][]  
[`FF`` ``RESET`][]

  [`00`` ``EYETX`]: FF7/Field/Script/Opcodes/28%20KAWAI/00%20EYETX.md
    "wikilink"
  [`01`` ``TRNSP`]: FF7/Field/Script/Opcodes/28%20KAWAI/01%20TRNSP.md
    "wikilink"
  [`02`` ``AMBNT`]: FF7/Field/Script/Opcodes/28%20KAWAI/02%20AMBNT.md
    "wikilink"
  [`06`` ``LIGHT`]: FF7/Field/Script/Opcodes/28%20KAWAI/06%20LIGHT.md
    "wikilink"
  [`0A`` ``SBOBJ`]: FF7/Field/Script/Opcodes/28%20KAWAI/0A%20SBOBJ.md
    "wikilink"
  [`0D`` ``SHINE`]: FF7/Field/Script/Opcodes/28%20KAWAI/0D%20SHINE.md
    "wikilink"
  [`FF`` ``RESET`]: FF7/Field/Script/Opcodes/28%20KAWAI/FF%20RESET.md
    "wikilink"
