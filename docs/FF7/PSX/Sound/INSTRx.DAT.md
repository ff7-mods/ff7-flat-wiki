---
title: INSTRx.DAT
---

There are two files of such type:

| File | Number of Instruments | Load Offset | Load Size | Description |
|----|----|----|----|----|
| SOUND/INSTR.DAT | 93 | 0 | 0x2000 (128 \* 0x40) | Main game sounds |
| SOUND/INSTR2.DAT | 4 | 0xD40 (53 \* 0x40) | 0x12C0 (75 \* 0x40) | Voices from ending theme "One Winged Angel" |

These files contain index data for all instruments from INSTRx.ALL.

## Record format

`struct AkaoInstrumentAttr`  
`{`  
`  /* offsets */`  
`  uint32_t addr;         // offset to attack part of instrument (SPU hardware address)`  
`  uint32_t loop_addr;    // offset to loop part of instrument (SPU hardware address)`  
`  /* ADSR Envelope settings */`  
`  uint8_t ar;            // ADSR: attack rate (0x00-0x7f)`  
`  uint8_t dr;            // ADSR: decay rate (0x00-0x0f)`  
`  uint8_t sl;            // ADSR: sustain level (0x00-0x0f)`  
`  uint8_t sr;            // ADSR: sustain rate (0x00-0x7f)`  
`  uint8_t rr;            // ADSR: release rate (0x00-0x1f)`  
`  uint8_t a_mode;        // ADSR: attack mode`  
`                         //    0x05 - (exponential)`  
`                         //    0x01 (default) - (linear)`  
`  uint8_t s_mode;        // ADSR: sustain mode`  
`                         //    0x01 - (linear, increase)`  
`                         //    0x05 - (exponential, increase)`  
`                         //    0x07 - (exponential, decrease)`  
`                         //    0x03 (default) - (linear, decrease)`  
`  uint8_t r_mode;        // ADSR: release mode`  
`                         //    0x07 - (exponential decrease)`  
`                         //    0x03 (default) - (linear decrease)`  
`  uint32_t pitch[12];    // predefined pitch set for instrument`  
`};`

Each index file takes 4 CDROM sectors, so rest unused data filled with zeroes. Attack and loop offsets isn't real file offsets, it's offsets to instruments in SPU internal memory (all instrument data from INSTRx.ALL files are copied by DMA to SPU memory in one chunk), so to translate INSTR.ALL you need to subtract 0x0ff0 (or you need to subtract 0x38540 for INSTR2.DAT). INSTR.DAT file resides in PSX RAM at address 0x80075f30 and when it's needed to load any instrument or to reset pitch for this instrument this table is used.
