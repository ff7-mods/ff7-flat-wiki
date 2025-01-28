---
title: 63_SCRLA
---

- Opcode: **0x63**
- Short name: **SCRLA**
- Long name: Scroll To Entity

#### Memory layout

| 0x63 | *B* | *S* | *E* | *T* |
|------|-----|-----|-----|-----|

#### Arguments

- **const UByte** *B*: Bank for the scroll speed, or zero if it is specified as a literal value.
- **const UShort** *S*: Speed of the scroll, in frames, or the address to find the speed if *B* is non-zero.
- **const UByte** *E*: Entity ID to scroll to.
- **const UByte** *T*: Type of scroll.

#### Description

Scrolls the current view so that the field object associated with entity *E* is in the center of the view. The scroll occurs at speed *S*, and with a particular style, *T*. If an entity is given that does not have a field object, the view centers on the walkmesh origin. If the object is moving as the scroll occurs, the scroll will follow the object until it is centered. Also of note is that the scroll will not leave the boundaries of the background (as defined by the range values in section 8), unlike the standard "scroll to coordinate" opcodes.

It also appears as though any subsequent movements from this entity are also followed by the camera (field: nvdum3).

#### Scroll Types

| ID  | Scroll Type   |
|-----|---------------|
| 0   | No Scroll     |
| 1   | Instantaneous |
| 2   | Linear        |
| 3   | Smooth        |
|     |               |
