---
title: 28 KAWAI
---

[Home](../../../../Main Page.md) > [FF7](../../../../FF7.md) > [Field](../../../Field.md) > [Script](../../Script.md) > [Opcodes](../Opcodes.md) > 28 KAWAI

-   Opcode: **0x28**
-   Short name: **KAWAI**
-   Long name: Character Graphics Opcode (Multibyte sequence)

#### Memory layout

| 0x28 | *L* | *S* | *...* |
|------|-----|-----|-------|

#### Arguments

-   **const UByte** *L*: Total length of the entire opcode and argument list.
-   **const UByte** *S*: Operation to perform.
-   *Variable ...*: Sequence of arguments, depending on the operation type.

#### Description

KAWAI is a multipurpose, graphics-related opcode that performs a variety of different operations on visible entity objects, depending on the subop argument. It was named after Final Fantasy VII's Character Programmer, Hiroshi Kawai.

#### Subcodes by Opcode

[`00`` ``EYETX`](28 KAWAI/00 EYETX.md)  
[`01`` ``TRNSP`](28 KAWAI/01 TRNSP.md)  
[`02`` ``AMBNT`](28 KAWAI/02 AMBNT.md)  
[`06`` ``LIGHT`](28 KAWAI/06 LIGHT.md)  
[`0A`` ``SBOBJ`](28 KAWAI/0A SBOBJ.md)  
[`0D`` ``SHINE`](28 KAWAI/0D SHINE.md)  
[`FF`` ``RESET`](28 KAWAI/FF RESET.md)
