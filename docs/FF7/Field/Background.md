---
title: Background
---

### Section 9: Background ([Terence Fergusson](../../User:Terence_Fergusson)

Firstly, a number of variables.

At offset \$28, a Word = background width (BGWidth) At offset \$2A, a Word = background height (BGHeight) At offset \$2C, a Word = number of background sprites (NumBGSprites) At offset \$32, the background sprite data. See below for format (each sprite is 52 bytes long) After the background sprite data, another \$7 bytes, unknown purpose. Then (ie. at offset \$32 + NumBGSprites\*52 + \$7) a Word = number of 2nd layer background sprites (NumBG2Sprites) Then another \$12 bytes, unknown purpose. Then (ie. at offset \$32 + NumBGSprites\*52 + \$1B) the background layer 2 sprite data. See below for format. Then another \$3D bytes, unknown purpose. Then (ie. at offset \$32 + NumBGSprites\*52 + NumBG2Sprites\*52 + \$58) the raw image data.

#### Background format

FF7 stores its backgrounds in a rather complex format. Basically, you have the data split up into various sections:

1\) Palette. List of colours. 2) Background sprites, layers 1 and 2. Just references to other bits of data. 3) Raw image data. Palettized data (ie. "grayscale" if viewed directly).

Each background sprite represents a 16x16 pixel block on the finished background. The sprite essentially contains the following information:

\- "Target" block, ie. where on the background to draw this 16x16 square - "Source" block, ie. where on the raw image data to take the pixels from - Palette "page", ie. which 256-colour palette block to apply to the raw image data

This is a very efficient way to store the image; on the one hand, it's in 16-bit colour, far better than just palettizing the whole image (ie. 256 colours over the \*whole\* background). On the other hand, each 16x16 pixel block takes much less space than if you'd stored it directly in 16-bit colour format. It isn't, however, easy to decode or (especially) encode.

Format of a background sprite:

`Type`  
`  TFF7BgSprite = packed record`  
`    ZZ1,X,Y:  Smallint;`  
`    ZZ2:  Array[0..1] of Smallint;`  
`    SrcX,SrcY:  Smallint;`  
`    ZZ3:        Array[0..3] of Smallint;`  
`    Pal:        Smallint;`  
`    Flags:      Word;`  
`    ZZ4: Array[0..2] of Smallint;`  
`    Page,Sfx:   Smallint;`  
`    NA:         Longint;`  
`    ZZ5: Smallint;`  
`    OffX,OffY:  Longint;`  
`    ZZ6: Smallint;`  
`  end;`

ZZ1,2,3,4,5,6: Unknown data X,Y: Target position SrcX,SrcY: Source position Pal: Which palette page to use Flags: Indicate special effects ... not really understood properly. Page: Which image source page to use Sfx: More special effects? NA: Unknown OffX,OffY: Unknown

The image source data is split up into 256x256 pixel pages; that's why as well as a source X and Y, you also have a source page (which 256x256 block to take data from). On the other hand, the destination background is stored as one big bitmap with no limits on size, so there, you just have a target X/Y position which can be used directly.

Also, note that each source image data "page" is preceded by 6 bytes of header.

So, say the raw image data starts at offset ImageData. Given a background sprite, the offset where that sprites data starts is:

StartOffset := (Page shl 16) or ((SrcY shl 8) or SrcX) + (Page+1)\*6;

this is equivalent to

StartOffset := (Page \* \$FFFF) + (SrcY \* \$FF) + SrcX + (Page+1)\*6;

(Page shl 16), (Page\*\$FFFF): Each page takes up 256x256 = \$FFFF bytes, so skip that many for each page.

(SrcY shl 8), (SrcY\*\$FF): Each pixel row takes up 256 = \$FF bytes, so skip that many to get to the right row.

SrcX: Taken directly.

(Page+1)\*6: Skip 6 bytes of header per page. (Page+1) since even page 0 has 6 bytes preceding it.

Incidentally, the shifts are used in preference to multiplication since shifting is more efficient. Shifting on a computer is equivalent to multiplying/dividing by 2, 4, 8, ...

For the destination, note that you can use X/Y directly; however 0,0 appears, I think, to be at the image centre, not at the top/bottom left corner like with most programs.

So, now you know:

-Where the raw image data for that sprite starts -Where you're drawing it to -Which palette page to use

Now, you just copy the pixels across, filtering the palette into it. IE:

Read a pixel from source image (one byte). Set current colour to that colour in palette. Draw onto target.

So, if you read a byte = 55 from the source image, you'd draw colour 55 in the selected palette to the target bitmap.

#### Other points

Currently, Qhimm's (and therefore mine too) source code doesn't draw a sprite if the Sfx is non-zero; this is because we don't understand what it does.

All variables above (Page, Pal, X, Y) start from ZERO; palette page zero is the first one, page one is the next one, etc.

The image data in FF7 palettes is stored in reverse order; ie. on Windows, data is stored Red first, then Green, then Blue. FF7 stores it the opposite way around, so you need to exchange the red/blue data. Here's how I do it in Cosmo:

`DColÂ := 0;`  
`DColÂ := DCol or ( (Col^ and $1F) shl 10 );`  
`DColÂ := DCol or (Col^ and $3E0);`  
`DColÂ := DCol or ( (Col^ and $7C00) shr 10);`

Converts Col, an FF7 colour, into DCol, a (16-bit) Delphi colour.

The first background sprites are drawn "behind" the layer 2 sprites. Variable conventions; I'm using Delphi names, which are as follows:

Byte: 8 bit, unsigned, integer Word: 16 bit, unsigned, integer Smallint: 16 bit, signed, integer Integer/Longint: 32 bit, signed, integer

(Unsigned = positive values only. Signed can hold positive or negative values).

Also, whenever I use numbers with \$ signs above, it means I'm using hex values (hexadecimal).
