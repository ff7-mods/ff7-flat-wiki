---
title: 09_SPLIT
---

- Opcode: **0x09**
- Short name: **SPLIT**
- Long name: Party Field Split

#### Memory layout

| 0x20 | *B1 / B2* | *B3 / B4* | *B5 / B6* | *XA* | *YA* | *DA* | *XB* | *YB* | *DB* | *S* |
|------|-----------|-----------|-----------|------|------|------|------|------|------|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank for *XA*, or zero if *XA* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank for *YA*, or zero if *YA* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank for *DA*, or zero if *DA* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank for *XB*, or zero if *XB* is specified as a literal value.
- **const Bit\[4\]** *B5*: Bank for *YB*, or zero if *YB* is specified as a literal value.
- **const Bit\[4\]** *B6*: Bank for *DB*, or zero if *DB* is specified as a literal value.
- **const Short** *XA*: X-coordinate of the second character in the party after the split, or address for the value if *B1* is non-zero.
- **const Short** *YA*: Y-coordinate of the second character in the party after the split, or address for the value if *B2* is non-zero.
- **const UByte** *DA*: Direction the second character faces after the split, or address for the value if *B3* is non-zero.
- **const Short** *XB*: X-coordinate of the third character in the party after the split, or address for the value if *B4* is non-zero.
- **const Short** *YB*: Y-coordinate of the third character in the party after the split, or address for the value if *B5* is non-zero.
- **const UByte** *DB*: Direction the third character faces after the split, or address for the value if *B6* is non-zero.
- **const UByte** *S*: Speed that the characters split.

#### Description

Causes the common 'split effect' whereby the second and third characters in the current party 'come out' from the party leader. That is, they become visible in the field, starting from the centre of the party leader, and move out to the coordinates specified in the argument list. This is commonly used when the other characters in the current party have an action or dialog to perform and must be individually visible in the field. As well as specifying final coordinates for the two other party characters, the directions each character faces after the split are specified as a byte, using the common direction values found throughout the game. Speed is also given and is used to specify the rate at which the characters leave the party leader, using a scale from 1 (almost instant) to FF (extremely slow walk); this must be non-zero.

In contrast to most MOVE related op codes, the speed is this setting is actually the total number of frames required. Depending on the distance from the player character and the number of frames required, the entity plays a run or walk animation. Also, all characters take the same time irrespective of distance.
