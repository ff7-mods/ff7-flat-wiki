---
title: C1_AXYZI
---

- Opcode: **0xC1**
- Short name: **AXYZI**
- Long name: Entity Get Position

#### Memory layout

| 0xC1 | *B1 / B2* | *B3 / B4* | *A* | *X* | *Y* | *Z* | *I* |
|------|-----------|-----------|-----|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to store *X*.
- **const Bit\[4\]** *B2*: Bank to store *Y*.
- **const Bit\[4\]** *B3*: Bank to store *Z*.
- **const Bit\[4\]** *B4*: Bank to store *I*.
- **const UByte** *A*: Entity ID whose field object will have its position retrieved from.
- **const UByte** *X*: Address to store the X-coordinate of the entity's object.
- **const UByte** *Y*: Address to store the Y-coordinate of the entity's object.
- **const UByte** *Z*: Address to store the Z-coordinate of the entity's object.
- **const UByte** *I*: Address to store the ID of the walkmesh triangle the object is standing on.

#### Description

Retrieves the coordinates of the field object that the entity, whose ID specified in *A*, is associated with. This opcode uses an entity ID, not a field object offset; as such, if an entity ID is given that does not have a field object, this opcode will store zero in each of the four address specified.
