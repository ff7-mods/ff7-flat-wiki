---
title: Script
---

[Home](../../Main%20Page.md) > [FF7](../../FF7.md) > [Field](../Field.md) > Script

### Section 1: Dialog and Event ([Halkun][], [Lasyan][], [Qhimm][] and [Ficedula][])

The First section holds the Field Script logic and Dialog data for that
particular field file. The first section of the PSX DAT file (excluding
the DAT header) and the data in this section are the same. A recap of
the PSX DAT file format is later in this document.

The data in this section also has a header with the following format.

#### Section 1 Header

` struct FF7SCRIPTHEADER {`  
`   u16 unknown1;           // Always 0x0502`  
`   char nEntities;         // Number of entities`  
`   char nModels;           // Number of models`  
`   u16 wStringOffset;          // Offset to strings`  
`   u16 nAkaoOffsets;           // Specifies the number of Akao/tuto blocks/offsets`  
`   u16 scale;                          // Scale of field. For move and talk calculation (9bit fixed point).`  
`   u16 blank[3];`  
`   char szCreator[8];          // Field creator (never shown)`  
`   char szName[8];         // Field name (never shown)`  
`   char szEntities[nEntities][8];  // Field entity names`  
`   u32 dwAkaoOffsets[nAkaoOffsets];    // Akao/Tuto block offsets`  
`   u16 vEntityScripts[nEntities][32];  // Entity script entry points, or more`  
`                   // explicitly, subroutine offsets`  
` };`

#### Event Script Subsection

Here we have all of the pointers tables, one for each section. Pointers
are 2 bytes length. Each table has a length of 64 bytes, which means a
section can have 32 scripts max. Each pointer refers to the first
command of the current script. The section number N begins at the offset
header\_length+N\*64. Note: the only way to retrieve the length of a
script is to subtract the position of the next script to the position of
the current script.

[Cyberman][] 14:05, 30 Dec 2006 (CST) Unused events in the event script
subsection point to a [00 RET][] opcode (each empty script has a unique
RET opcode for it in the script). This must be strictly adhered too or
the FF7 engine will crash.

#### Event Script

The actual script follows immediately after the aforementioned pointer
tables. For a list of opcodes and their arguments, see the [opcode
table][].

#### Dialog Subsection

Right after the last script of the preceding section, we find the 2 byte
dialog count, followed by the dialog pointer table. Using the dialog
count, you can deduce the length of the table: number\_of\_dialogs\*2.
After these 2 bytes we have the pointers for each dialog. Be aware that
the pointers are relative to the table, which means you must add the
position of the table to each pointer in order to find the right
position of the dialog. The dialogs begin right after the table, and the
code 255 means the end of the dialog. Note: some hidden dialogs are not
referenced in the table!

#### Akao blocks

If there are any Akao offsets (as specified by nExtraOffsets and
dwExtraOffsets), they follow after the dialog subsection, beginning with
the four-letter AKAO. Akao blocks contain sound-related data such as the
music file index for this field. In some fields (junpb\_2, mds7pb\_1,
mds7pb\_2 and msd7\_w2), the Akaos are mixed with tutorials. I do not
know why, but the PC version uses a separate file (junpb.tut,
mds7\_w.tut or mds7pb.tut) instead of these tutorials.  
**Note:** Between dialogs and akaos there may be a padding to align the
akaos section.

  [Halkun]: ../../User:Halkun.md "wikilink"
  [Lasyan]: ../../User:Lasyan.md "wikilink"
  [Qhimm]: ../../User:Qhimm.md "wikilink"
  [Ficedula]: ../../User:Ficedula.md "wikilink"
  [Cyberman]: ../../User:Cyberman.md "wikilink"
  [00 RET]: Script/Opcodes/00%20RET.md "wikilink"
  [opcode table]: Script/Opcodes.md "wikilink"
