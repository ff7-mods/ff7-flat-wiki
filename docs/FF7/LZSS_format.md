---
title: LZSS_format
---

#### Format

The LZSS archive has a very small header at 0x00 that has the length of the compressed file as an unsigned 32 bit integer. After that is the compressed data. Some files use the .lzs extension, probably to make the extension 3 characters long. It has caused some confusion, since LZS is a different compression method.

#### LZSS compression

FF7 uses LZSS compression on some of their files, as devised by Professor Haruhiko Okumura. LZSS data works on a control byte scheme. Each block in the file begins with a single byte indicating how much of the block is uncompressed ('literal data'), and how much is compressed ('references'). You read the bits LSB-first, with 0=reference, 1=literal.

Literal data means just that: read one byte in from the source (compressed) data, and write it straight to the output.

References take up two bytes, and are essentially a pointer to a piece of data that's been written out (i.e. is part of the data you've already decompressed). LZSS uses a 4KiB buffer, so it can only reference data in the last 4KiB of data.

#### Reference format

A reference takes up two bytes, and has two pieces of information in it: offset (where to find the data, or which piece of data is going to be repeated), and length (how long the piece of data is going to be). The two reference bytes look like this:

`OOOOOOOO  OOOOLLLL`  
  
`(O = Offset, L = Length)`

The 1st byte it the least significant byte of the offset. The second byte has the remaining 4 bits of the offset as it's **high** nibble, so some shifting is required to extract it properly. The remaining 4 bits is the length minus 3.

So you get a 12-bit offset and a 4-bit length, but both of these values need modifying to work on directly. The length is easy to work with: just add 3 to it. This is because if a piece of repeated data was less than 3 bytes long, you wouldn't bother repeating it - it'd take up no more space to actually just put literal data in. So all references are at least 3 in length. So a length of 0 means 3 bytes repeated, 1 means 4 bytes repeated, so on.

Since we have 4 bits available, that gives us a final length ranging from 3-18 bytes long. That also means the absolute maximum compression we can ever get using LZSS is a touch under 9:1, since the best possible is to replace 18 bytes of data with two bytes of reference, and then you have to add control bytes as well.

Offset needs a bit work doing on it, depending on how you're actually holding your data. If all you have is an input buffer and an output buffer, what you really need is an output position in your buffer to start reading data from. In other words, if you've already written 10,000 bytes to your output, you want to know where to retrieve the repeated data from - it could fall anywhere in the past 4K of data (i.e. from 5904 through to 9999 bytes).

Here's how you get it:

`real_offset = tail - ((tail - 18 - raw_offset) mod 4096)`

Here, 'tail' is your current output position (eg. 10,000), 'raw_offset' is the 12-bit data value you've retrieved from the compressed reference, and 'real_offset' is the position in your output buffer you can begin reading from. This is a bit complex because it's not exactly the way LZSS traditionally does decompression.

If you use a 4KiB buffer, you can use the offset directly. The offset is absolute, and not relative to the cursor position or the position in the input stream. You should initialize the buffer position to 0xFEE and not zero. The buffer content should be initialized to zero.

Once you've got to the start position for your reference, you just copy the appropriate length of data over to your output, and you've dealt with that piece of data.

#### Example

If we're at position 1000 in our output, and we need to read in a new control byte because we've finished with the last one. The next data to look it is:

`0xFC, 0x53, 0x12 .....`

We read in a control byte: 0xFC. In binary, that's 11111100. That informs us that the current block of data has two compressed offsets (@ 2 bytes each), followed by 6 literal data bytes. Once we'd read in the next 10 bytes (the compressed data plus the literal data), we'd be ready to read in our next control byte and start again.

Looking at the first compressed reference, we read in \$53 \$12. That gives us a base offset of \$153 (the 53 from the first byte, and the '1' from the second byte makes up the higher nybble). The base length is \$2 (we just take the low nybble of the second byte).

Our final length is obviously just 5.

Our position in output is still 1000. So our final offset is:

`= 1000 - ((1000 - 18 - 339) and $FFF)`  
` `

The 339 is just \$153 in decimal. The (and \$FFF) is a quick way to do modulus 4096.

`= 1000 - (643 and 0xFFF)`  
` = 1000 - 643`  
` = 357`  
` `

So our final offset is 357. We go to position 357 in our output data, read in 5 bytes (remember the length?), then write those 5 bytes out to our output. Now we're ready to read in the next bit of data (another compressed reference), and do the procedure again.

#### Complications

Unfortunately, that doesn't quite cover everything - there's two more things to be aware of when decompressing data that will ruin you when using FF7 files, since they do use these features.

First, if you end up with an negative offset, i.e. reading data from 'before the beginning of the file', write out nulls (zero bytes). That's because the compression buffer is, by default, initialized to zeros; so it's possible, if the start of the file contains a run of zeros, that the file may reference a block you haven't written. For example, if you're at position 50 in your output, it's possible you may get an offset indicating to go back 60 bytes to offset -10. If you have to read 5 bytes from there, you just write out 5 nulls. However, you could have to read 15 bytes from there. In that case, you write out 10 nulls (the part of the data 'before' the file start), then the 5 bytes from the beginning of the file.

Secondly, you can have a repeated run. This is almost the opposite problem: when you go off the end of your output. Say you're at offset 100 in your output, and you have to go to offset 95 to read in a reference. This is okay, but if the reference length is \>5, you loop the output. So if you had to write out 15 bytes, you'd write out the five bytes that were available, then write them out again, then again, to make up the 15 bytes you needed.

The FF7 files use both of these 'tricks', so you can't ignore them.

If you use a circular 4KiB buffer, you can ignore these issues completely, as long as you do a one-byte-at-a-time copy for the references.
