---
title: Image_Formats
---

# Image Interlacing

Pixel-Data for all texture formats appears to have the same interlacing mechanism.

The data is divided into 16x8 pixel-chunks, but is arranged in a strange sort of way:

`ABCD  MNOP  YZ...`  
`EFGH  QRST   ...`  
`IJKL  UVWX   ...`

Then reading each chunk (in that order), grab rows of 16-pixels (like 8 scanlines, top to bottom of chunk) and plot them like so:

`  1,  17,  33,  49,     5,  21,  37,  53,     9,  25,  41,  57,    13,  29,  45,  61,`  
`  2,  18,  34,  50,     6,  22,  38,  54,    10,  26,  42,  58,    14,  30,  46,  62,`  
`  3,  19,  35,  51,     7,  23,  39,  55,    11,  27,  43,  59,    15,  31,  47,  63,`  
`  4   20,  36,  52,     8,  24,  40,  56,    12,  28,  44,  60,    16,  32,  48,  64`

Interlacing is exactly the same, except that the interlacing in columns (numbered above: 1,17,33,49, 5,21,37,53, ... ) is determined by the width of the image.

So,

if width = 512, then you get 4 interlaced columns

if width = 256, then you get 2 interlaced columns

if width = 128, then you get 1 interlaced column

(ie, divide image width by 128)

  

# Known FF7:CC Image Formats

- [\[IMG](Image_Formats#IMG_Format)\]
- [\[TEX](Image_Formats#TEX_Format)\]
- [\[GT](Image_Formats#GT_Format)\]

  
Note that the Pixel-data is interlaced for all of these formats, as described above.

  

## IMG Format

<small>Stub</small>

  
\[IMG\] contain multiple palletted Images, perhaps sprites or HUD images.

  
The image palettes are 32bit format R8G8B8A8. Palettes for textures are fairly easy to notice because the alpha channel is pretty much all the time fully solid. For sprites it is slightly harder as they use alot of transparency. <small>-- Zande</small>

  

## TEX Format

Note: the FF7:CC \[TEX\] format is NOT the same as the FF7 PC [TEX](../FF7/TEX_format) format.

  
\[TEX\] Files are Texture images used by Models, frequently found embedded within \[ATEL\] and \[!\] files which use them.

`Header: 48 bytes [upto 0x2f]`  
  
`   0x00   magic "TEX"`  
`   0x1C   DWORD: size Width`  
`   0x20   DWORD: size height`  
  
`Pixel Data: 0x30 offset`  
  
`   (Width * Height) number of bytes, 1 byte per-pixel index (to pallete entry color, below)`  
  
`Pallete data: (immedietly following Pixel data)`  
  
`   16 bytes of mostly zeros (don't seem important)`  
`   255 4-byte chunks [RGBA] (per pallete entry)`

  

## GT Format

\[GT\] Files are Chapter End images, dispersed throughout the \[ATEL\] Event files in-line with when they are displayed during gameplay.

  
The "Format-Byte": - for GT files, this is always "4" = 256 colours and 1-BpP.

  
For the GT files, the 4th byte in the header tells the colour depth format, if this byte is 3 the palette has 16 colours and 1 nibble per pixel. If the byte has a value of 4, there's 256 colours and 1 byte per pixel <small>-- Zande</small>

  

`Header: 16 bytes`  
`   0x00   DWORD: magic "GT"`  
`   0x04   format-byte [see notes]`  
`   0x08   width (pixels)`  
`   0x10   height (pixels)`  
  
`Pallete Data: start offset = 0x10`  
`   255 [RGBA] 4-byte chunks`  
  
`Pixel Data: immedietly following Pallete [start offset = 0x410]`  
`   width * height bytes (index to pallete entry)`
