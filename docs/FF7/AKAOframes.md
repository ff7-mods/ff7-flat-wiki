---
title: AKAOframes
---

# Introduction

AKAO frames are most complicated frames in FF7 sound system. ("AKAO" is frame magic, probably developed by Minoru Akao, Square Enix sound programmer :) )

Frame is similar to MIDI sequence - it's custom tracker format for playing sequence sound, well tuned specially for PSX.

This frames are in all FF7 game modules: Field, Battle, Worldmap and in minigames.

All files with exension \*.SND are AKAO.

**MINI/ASERI2.SND** - Battle Arena theme

**MINI/SENSUI.SND** - used in Submarine minigame

**ENEMY6/OVER2.SND** - game over sequence

**ENEMY6/FAN2.SND** - battle win "fanfare" sequence

**MOVIE/OVER2.SND** - same game over sequence, don't know, why to duplicate data

Other AKAO frames are hard-wired in other files.

# AKAO frame structure

## Header (size: 16 bytes)

struct AkaoHeader

{

`   static const uint8_t magic[4]; // "AKAO" C-string aka frame *MAGIC*`  
`   uint16_t id;                   // frame ID, used for playing sequence`  
`   uint16_t length;               // frame length - sizeof(header)`  
`   uint8_t unknown[8];            // some numbers, can't find their usage`

};

## Channel info (size: 4 bytes + 2 bytes \* <channels count>)

First there is 32-bit number (offset 0x10), which represents bitmask of used channels in this frame, after this frame there is <channels count> offsets to channel opcode data counting from current offset.

## Channel Commands \[AKAO Opcodes\]

Most complicated part.

For every channel in AKAO frame there is set of commands to perform. This is similar to Field opcodes. Here I'll call this sound commands "opcodes". Every opcode has it's own number of arguments (from no-arguments, to 3 arguments).

# Example (home-created AKAO frame):

## Header

**41 4b 41 4f** - AKAO string

**34 12** - frame ID: 0x1234

**16 00** - frame length 0x16 in hex or 22 in decimal

**04 00 96 12 18 22 46 28** - unknown data

## Channel info

**01 00 00 00** - this indicates, that used only one channel

**00 00** - offset to first channel opcodes: in our example 0x00 means that next to this offset is opcodes for first channel

## Channel commands

**e8 a8 66** - sets tempo, parameter 0x66a8

**ea 00 50** - sets reverb depth

**a8 55** - load sample 0x55 from INSTR.ALL to channel

**aa 40** - sets channel volume

**c2** - turns on reverb effect

**a1 0c** - sets volume pan

**c8** - sets loop point

**66** - 0x66 % 11 = 3 (3 means to take 3rd number from play length table), 0x66 / 11 = 9 (9 means to take pitch\[9\] from loaded instrument record index)

**ca** - returns to saved loop point with opcode c8

This example plays Chocobo "Whoo-Hoo" (instrument number 0x55) repeatedly.

# Sound Opcode list

[0xa0 (Finish Channel)](../0xa0_(Finish_Channel))

[0xa1 (Load Instrument)](../0xa1_(Load_Instrument))

[0xa5 (Pitch Divider)](../0xa5_(Pitch_Divider))

[0xa8 (Channel Volume)](../0xa8_(Channel_Volume))

[0xaa (Channel Pan)](../0xaa_(Channel_Pan))

[0xc8 (Loop Point)](../0xc8_(Loop_Point))

[0xca (Return to Loop Point)](../0xca_(Return_to_Loop_Point))

[0xe8 (Tempo)](../0xe8_(Tempo))

[0xea (Reverb Depth)](../0xea_(Reverb_Depth))
