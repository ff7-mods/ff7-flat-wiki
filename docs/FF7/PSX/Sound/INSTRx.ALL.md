---
title: INSTRx.ALL
---

There is two files of this structure on FF7 game discs:

- SOUND/INSTR.ALL - Main game sounds (93 instruments)
- SOUND/INSTR2.ALL - Voices from ending theme "One Winged Angel" (4 instruments)

These files contain all sample data for every instrument in game. Every instrument consists of 16-byte PSX ADPCM frames. Frame format is known and there is numerous decompressors for it whether on the net, or in Q-Gears source.

## File Structure

At file beginning there is two 32-bit numbers. Counting from 0x10 file offset there is sample data for all instruments. (using term "Instrument" I actually mean serie of ADPCM samples, although in some context I can use term "Sample", "Sound" or "Voice" to describe instrument). All data from INSTR.ALL are loaded by DMA to SPU RAM in one chunk, offset 0x0202.

`struct AkaoSampleSet`  
`{`  
`  uint32_t addr;         // transfer destination address (SPU hardware address, between 0x1010 - 0x7ffff)`  
`  uint32_t size;         // transfer size`  
`  uint8_t unknown[8];    // unused? padded with 0s`  
  
`  uint8_t data[size];    // PSX ADPCM frames`  
`};`
