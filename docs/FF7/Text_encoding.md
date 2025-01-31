---
title: Text_encoding
---

FF Text is a format that Squaresoft used to store strings in the English version of Final Fantasy VII. Large subsets of the character (e.g. A-Z, a-z, 0-9) set are coded as simply their ASCII values offset by 0x20.

|  | 00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 0A | 0B | 0C | 0D | 0E | 0F |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 00 | {SPACE} | ! | " | \# | \$ | % | & | ' | ( | ) | \* | \+ | , | \- | . | / |
| 10 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; | \< | = | \> | ? |
| 20 | @ | A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
| 30 | P | Q | R | S | T | U | V | W | X | Y | Z | \[| \\ | \] | ^ | \_ |
| 40 | \` | a | b | c | d | e | f | g | h | i | j | k | l | m | n | o |
| 50 | p | q | r | s | t | u | v | w | x | y | z | { | \| | } | ~ |  |
| 60 | Ä | Á | Ç | É | Ñ | Ö | Ü | á | à | â | ä | ã | å | ç | é | è |
| 70 | ê | ë | í | ì | î | ï | ñ | ó | ò | ô | ö | õ | ú | ù | û | ü |
| 80 | ⌘ | ° | ¢ | £ | Ù | Û | ¶ | ß | ® | © | ™ | ´ | ¨ | ≠ | Æ | Ø |
| 90 | ∞ | ± | ≤ | ≥ | ¥ | µ | ∂ | Σ | Π | π | ⌡ | <u>ª</u> | <u>º</u> | Ω | æ | ø |
| A0 | ¿ | ¡ | ¬ | √ | ƒ | ≈ | ∆ | « | » | … | {NOTHING} | À | Ã | Õ | Œ | œ |
| B0 | – | — | “ | ” | ‘ | ’ | ÷ | ◊ | ÿ | Ÿ | ⁄ | ¤ | ‹ | › | ﬁ | ﬂ |
| C0 | ■ | ▪ | ‚ | „ | ‰ | Â | Ê | Ë | Á | È | í | î | ï | ì | Ó | Ô |
| D0 | {SPACE} | Ò | Ù | Û |  |  |  |  |  |  |  |  |  |  |  |  |
| E0 | {Choice} | {Tab} | , | ." | ..." |  |  | {EOL} | {New Scr} | {New Scr?} | {Cloud} | {Barret} | {Tifa} | {Aerith} | {Red XIII} | {Yuffie} |
| F0 | {Cait Sith} | {Vincent} | {Cid} | {Party #1} | {Party #2} | {Party #3} | 〇 | △ | ☐ | ✕ |  |  |  |  | {FUNC} | {END} |

There is no equivalent character to 80h in most font families.  
Characters D4h - DFh appear to produce odd graphical errors.

### {FUNC} Character

This character is in fact an opcode, that takes one or more arguments. For the most time it's used to indicate colours, which are as follows:

`FE D2: Gray colour`  
`FE D3: Blue colour`  
`FE D4: Red colour`  
`FE D5: Purple colour`  
`FE D6: Green colour`  
`FE D7: Cyan colour`  
`FE D8: Yellow colour`  
`FE D9: White colour`  
`FE DA: Flash colour*`  
`FE DB: Rainbow colour*`

\* these colours are global for a window, you can't reset them with other modifiers.

More info can be found in [Dialog Window](Field/DialogWindow#Special_Letters) section of the wiki.

### Battle Text within the KERNEL.BIN

Sections 10-17 and 26 of the [KERNEL.BIN](Kernel/Kernel.bin) are encoded differently than the rest of the text data. Several other values have additional functions:

**EA - F0**: These are variable position markers used in the Battle Text section (25) of KERNEL.BIN. These will only appear in specific texts and should only be used in those texts. These tell the battle engine that when a title needs to be displayed that certain values need to be inserted into the string. These are always followed by two NULL pointers (FFFFh).

EA: Name of a Character EB: Name of an Item EC: Number ED: Name of the Target EF: Name of Attack FO: Target's Letter (for enemies)

Example

`S  t  o  l  e     X        !`  
`33 54 4F 4C 45 00 EB FF FF 01 FF`

The battle engine will replace the "EB FF FF" with the name of the item at the index passed to it.

**F8**: This appears at the beginning of a text. It tells the battle engine that the next byte will determine the color of the box the text is to be displayed in. 02h is the only one used and it displays a red box associated with Limit Breaks.

**F9**: This is an encoding technique designed to make the raw data smaller. It is based on the LZS compression method, but optimized for smaller files with fewer large similar blocks. A byte following this value will tell the game's memory the location of, and how much, text to read. The byte is set up like this:

`In binary:`  
`YYXXXXXX`  
`Where YY is the number of bytes to read and XXXXXX is how far back from the F9 byte to look.`

The number of bytes to read uses the formula:

`no_of_bytes = (YY) * 2 + 4  [Where YY is binary]`

The location starts at the position that the data read the byte F9 and proceeds backwards XXXXXX + 1 times.  
Ex: This is the description of the Poison Ring stored in section 15 of the kernel, both raw data and decoded text.

`24 52 41 49 4E 53 00 3B 30 4F 49 53 4F 4E 3D 00 41 54 54 41 43 4B 53 0C 00 50 52 4F 54 45 43 54 53 00 41 47 F9 21 54 F9 A0 3D`  
` D  r  a  i  n  s     [  P  o  i  s  o  n  ]     a  t  t  a  c  k  s  ,     p  r  o  t  e  c  t  s     a  g ** ??  t ** ??  ]`

At the end we have two F9 functions located at the end. The first one references the "ains" in the word "Drains" earlier in the description and the second one references the " \[Poison" shortly after. The bytes following the F9 describe how to get to those texts:

`21`  
`00 100001 - go back 34 bytes and display four characters`  
`A0`  
`10 100000 - go back 33 bytes and display eight characters`

This is an absolute position so it does not matter if there are other encrypted segments between it and the text it is trying to read.

NOTE: This may even request that a NULL terminator (0xFF) be output as well, but the data will then be terminated after the last piece of encoded text. This encoding can span back to previous descriptions as well.

### Useful downloads

- [Ficedula's FF7 Text decoder](http://aaronserv.dyndns.org/hosting/qhimmwiki/ficedula_ff7textdecoder_1.00.zip)
- [Reference table with FF7 Text values](http://www.subfan.pl/ff7pl/fieldtool.tbl)
