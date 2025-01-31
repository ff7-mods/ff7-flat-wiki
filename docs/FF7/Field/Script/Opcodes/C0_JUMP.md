---
title: C0_JUMP
---

- Opcode: **0xC0**
- Short name: **JUMP**
- Long name: Jump

#### Memory layout

| 0xC2 | *B1 / B2* | *B3 / B4* | *X* | *Y* | *I* | *Steps* |
|------|-----------|-----------|-----|-----|-----|---------|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve X-coordinate, or zero if specifying *X* as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve Y-coordinate, or zero if specifying *Y* as a literal value.
- **const Bit\[4\]** *B3*: Bank to retrieve triangle ID, or zero if specifying *Z* as a literal value.
- **const Bit\[4\]** *B4*: Bank to retrieve jump height, or zero if specifying *H* as a literal value.
- **const Short** *X*: X-coordinate of the target to jump to, or lower byte specifying address if *B1* is non-zero.
- **const Short** *Y*: Y-coordinate of the target to jump to, or lower byte specifying address if *B2* is non-zero.
- **const Short** *I*: Triangle ID of the target to jump to, or lower byte specifying address if *B3* is non-zero.
- **const UShort** *Steps*: Steps in jump. Must be non-zero if a literal value. Alternatively, lower byte specifies address if *B4* is non-zero.

#### Description

Causes the character to jump to the specified point and triangle ID, with the jump curve peaking at a height which is increased by using a larger value for the **H** argument. In addition, the larger the number, the longer the jump will take to complete. A "normal" value is around 0x15, 0x01 is fast and instantaneous; the argument must not be zero or the game will crash. Whilst this is an unsigned two-byte number, a large value (beyond around 0x60) will not only cause a vast jump height, but also cause the screen to scroll erratically (the larger the number, the more erratic).

Main update function go through all entity with JUMP state and if stage is 0 it calculates final Z point according to triangle id. It sets current coords as start coords. The main thing this function does is set B coefficient for later calculation. It defines as follows:

B = (Z_final - Z_start) / steps - steps \* 1.45;

Then it set current step to 0 and stage to 1. On next update other part of function works. It's calculate real position. First it increment current step number. Then it calculate X and Y. They change linear so nothing interesting here. Then here we go... Z calculation:

Z_current = - step^2 \* 1.45 + step \* B + Z_start;

If current substep equal number of steps then we set current triangle to final triangle and set stage to 2. Which finilize routine on next opcode call.

Neither animation nor sound is specified in this opcode. An animation is played by using an animation opcode such as [DFANM](FF7/Field/Script/Opcodes/A2_DFANM "wikilink"), and a [SOUND](F1_SOUND) played, before the jump.
