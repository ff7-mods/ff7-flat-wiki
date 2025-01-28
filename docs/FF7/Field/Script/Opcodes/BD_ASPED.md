---
title: BD_ASPED
---

- Opcode: **0xBD**
- Short name: **ASPED**
- Long name: Animation Speed

#### Memory layout

| 0xBD | *B* | *S* |
|------|-----|-----|

#### Arguments

- **const UByte** *B*: Bank to retrieve direction value, or zero if it is specified as a literal value.
- **const UShort** *S*: Speed of animation.

#### Description

Set global model animation speed. Lager the value - faster all animation played by this model.

Default value = 16 -\> relative animation time scale 1

ASPED 8 -\> relative animation time scale 0.5

ASPED 32 -\> relative animation time scale 2
