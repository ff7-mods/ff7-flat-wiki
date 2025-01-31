---
title: A1_CHAR
---

- Opcode: **0xA1**
- Short name: **CHAR**
- Long name: Character definition

#### Memory layout

| 0xA1 | *N* |
|------|-----|

#### Arguments

- **const UByte** *N*: Character ID.

#### Description

Defines a character, or rather, a visible entity. This means that the entity executing this opcode can be associated with a field object, and thus displayed on the walkmesh, as defined in [Section 3](../../../../../../../../../FF7/Field/Object_Loader).

#### Notes

Note that the character ID does *not* provide an index into the field object array as you might expect. Infact, the field object that this CHARacter will use is related solely to the position of this entity amongst the other visible entities in the set. For example, if you have the following entities and objects loaded:

- Ent1 (Visible, CHAR (00))
- Ent2 (Visible, CHAR (01))
- Ent3 (Visible, CHAR (02))
- Ent4
- FObject1
- FObject2
- FObject3

Ent1 will be associated with FObject 1, Ent2 with FObject 2, and Ent3 with FObject3. If you were to edit as such:

- Ent1 (Visible, CHAR (60))
- Ent2 (Visible, CHAR (12))
- Ent3
- Ent4 (Visible, CHAR (FF))
- FObject1
- FObject2
- FObject3

Ent1 will be associated with FObject 1, Ent2 with FObject 2, and Ent4 with FObject3. As you can see, the argument provides no information as to which object to use. Simply put, as each CHAR entity is read, the next sequential field object in the loader is assigned to it.
