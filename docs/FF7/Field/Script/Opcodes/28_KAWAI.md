---
title: 28_KAWAI
---

- Opcode: **0x28**
- Short name: **KAWAI**
- Long name: Character Graphics Opcode (Multibyte sequence)

#### Memory layout

| 0x28 | *L* | *S* | *...* |
|------|-----|-----|-------|

#### Arguments

- **const UByte** *L*: Total length of the entire opcode and argument list.
- **const UByte** *S*: Operation to perform.
- *Variable ...*: Sequence of arguments, depending on the operation type.

#### Description

KAWAI is a multipurpose, graphics-related opcode that performs a variety of different operations on visible entity objects, depending on the subop argument. It was named after Final Fantasy VII's Character Programmer, Hiroshi Kawai.

#### Subcodes by Opcode

[`00 EYETX`](28_KAWAI/00_EYETX)  
[`01 TRNSP`](28_KAWAI/01_TRNSP)  
[`02 AMBNT`](28_KAWAI/02_AMBNT)  
[`06 LIGHT`](28_KAWAI/06_LIGHT)  
[`0A SBOBJ`](28_KAWAI/0A_SBOBJ)  
[`0D SHINE`](28_KAWAI/0D_SHINE)  
[`FF RESET`](28_KAWAI/FF_RESET)
