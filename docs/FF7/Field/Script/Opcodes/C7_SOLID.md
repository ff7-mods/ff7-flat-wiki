---
title: C7_SOLID
---

- Opcode: **0xC7**
- Short name: **SOLID**
- Long name: Solid object

#### Memory layout

| 0xC7 | *S* |
|------|-----|

#### Arguments

- **const UByte** *S*: Switch on/off (0/1, respectively).

#### Description

Switches the solidity of the field object associated with this entity; that is, turns collision detection on or off. When off, the playable character will be able to walk through the entity's object, as if it were not there. This may be used for such objects as save points, where the character must be able to walk through the object to be able to access the save menu item.
