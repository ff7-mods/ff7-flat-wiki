---
title: MIMfile
---

## MIM File structure

The MIM filestructure begins with the

### MIM Header

`typedef struct`  
`{`  
`   UINT32   sizeofpaletteData; // <=> 12 + PalWidth*2*PalHeight`  
`   UINT16   PalX, PalY;`  
`   UINT16   PalWidth, PalHeight;`  
`} MIMHeader;`

which is followed by PalHeight number of

### MIM Palette

`typedef struct`  
`{`  
`   UINT16   Palette[256];`  
`} BGRPal256;`

After the palettes comes the

### MIM Block Header (1)

`typedef struct`  
`{`  
`   UINT32   sizeofimageData; // <=> 12 + Width*2*Height`  
`   UINT16   ImageX, ImageY; // location of blocks on 1024x512 display area`  
`   UINT16   Width, Height;  // Width is the # of Word units (UINT16) the blocks are wide`  
`} MIMBaseImage;`

lastly the actual block data for display follows. The palettes are selected from information in the DAT section 3 data.

Sometimes there is a second MIM Block:

### MIM Block Header (2)

Same header as MIM Block 1.
