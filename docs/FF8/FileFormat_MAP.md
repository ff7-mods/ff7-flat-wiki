---
title: FileFormat_MAP
---

By Aali.

# MAP Files

MAP files contain data about the tiles used to draw the field background. There is no header, every 16 bytes of the file is one 16x16 tile from the MIM data, ending with the special signature 0x7FFF followed by 12 zero bytes. To determine whether you're dealing with a type 1 or type 2 file, look at the MIM filesize, there is no obvious marker for type 2 in the MAP file.

## Tile format

### Type 1

Two signed 16-bit integers, X and Y relative to center (0, 0)  
Another 16-bit value, probably a fixed-point representation of the Z coordinate (divide by 4096 to get a floating point value)  
4 bits, which 128x256 texture to use, if you consider the MIM to be one big image, just multiply this value by 128 and add it to the source X coordinate  
1 unknown bit, always 1 (except in ending.map)  
3 bits, related to image deph. If &lt; 4 there is two color indexes per byte (4-bit indexed), else there is one color index per byte (8-bit indexed)  
1 Unknown byte, always 0 (except in ending.map)  
6 unknown bits, always 0  
4 bits specifying which palette to use, add 8 to this number to get the right palette from the MIM  
6 unknown bits, always 15  
2 bytes, source X and Y coordinates to sample the tile from  
1 bit, always 0  
7 bits, layer id  
1 byte specifying which blend mode to use for this tile, 1 is additive blending, 2 is subtractive blending, 3 seems to be +25%, 4 seems to be the default (no blending) and 0 is unknown (elview1)  
1 byte, background animation id  
1 byte, animation state  

### Type 2

X and Y, same as above  
Source coordinates, both 16-bit this time  
Possible Z coordinate  
4 bits, which 128x256 texture to use, same as above  
4 unknown bits (maybe same as above)  
1 unknown byte, always 0  
6 unknown bits, always 0  
4 bits specifying which palette to use, add 8 to this number to get the right palette from the MIM  
6 unknown bits, always 15  
1 byte, background animation id  
1 byte, animation state  
