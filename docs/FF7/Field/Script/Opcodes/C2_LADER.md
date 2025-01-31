---
title: C2_LADER
---

- Opcode: **0xC2**
- Short name: **LADER**
- Long name: Ladder

#### Memory layout

| 0xC2 | *B1 / B2* | *B3 / B4* | *X* | *Y* | *Z* | *I* | *K* | *A* | *D* | *S* |
|------|-----------|-----------|-----|-----|-----|-----|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve X-coordinate, or zero if *X* is specified as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve Y-coordinate, or zero if *Y* is specified as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve Z-coordinate, or zero if *Z* is specified as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve ID, or zero if *I* is specified as a literal value.
- **const Short** *X*: X-coordinate of the end of the ladder, or address to find X-coordinate if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate of the end of the ladder, or address to find Y-coordinate if *B2* is non-zero.
- **const Short** *Z*: Z-coordinate of the end of the ladder, or address to find Z-coordinate if *B3* is non-zero.
- **const UShort** *I*: ID of the walkmesh triangle found at the end of the ladder, or address to find ID if *B4* is non-zero.
- **const UByte** *K*: The keys used to move the character on the ladder.
- **const UByte** *A*: Animation ID for the field object's movement animation.
- **const UByte** *D*: Direction the character faces when climbing the ladder.
- **const UByte** *S*: Speed of the animation whilst climbing the ladder.

#### Description

Causes the character to climb a ladder; that is, switching from standard walkmesh movement, to climbing along a line connecting two points on the walkmesh.

If *B1*, *B2*, *B3* or *B4* is non-zero, then the value for that particular component is taken from memory using the corresponding bank and address specified, rather than as a literal value. Both retrieved values and literals can be used for different components. If using *X*, *Y*, *Z* or *I* as addresses, the lower byte should hold the address whilst the higher byte should be zero.

The coordinates specify the end-point of the ladder; the current position of the character is used as the start point. The ID of the walkmesh triangle must be specified; this is the triangle the character will step onto after reaching the end point of the ladder. The **K** value specifies the keys used to move the character across the ladder; keys outside the range found in the table will cause unpredictable behaviour. The animation ID specifies an offset into the field object's animation list; this animation is played at the speed specified by **S** whilst the character climbs. Finally, the **D** argument is a direction value in the game's standard direction format, which orients the character on the ladder.

### Notes

This opcode is used as part of the character's entity, rather than in a seperate entity, as with a [LINE](FF7/Field/Script/Opcodes/D0_LINE "wikilink"). A LINE is used to set the start point of the ladder on the walkmesh. When this LINE is crossed by the player, a script in the LINE then uses a [PREQ](04_PREQ), calling the script in the party leader that defines the LADER, causing the character to switch to 'climbing mode'.

To set up a two-way ladder, two LINEs are used at either end, with different values for the LADER arguments, such as differing end points.

If this opcode is used as part of a non-playable character entity, the NPC object will automatically climb from the start to the end point without need for player interaction.

#### Key IDs

| ID  | Key: Towards the end point | Key: Towards the start point |
|-----|----------------------------|------------------------------|
| 0   | Down                       | Up                           |
| 1   | Up                         | Down                         |
| 2   | Right                      | Left                         |
| 3   | Left                       | Right                        |
|     |                            |                              |
