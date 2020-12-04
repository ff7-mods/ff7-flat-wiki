---
title: String_Encoding
---

# String Encoding

FF8 strings are converted to byte arrays.[Char Table](https://sourceforge.net/p/ifrit/code-0/HEAD/tree/trunk%20ifrit-code-0/Resources/textformat.ifr) Some of which aligns to the grid of text in the texture if you -32 from the value. Some values are 1 byte = 2 characters, most are 1 byte = 1 character. There are also special bytes that use up 1-3 bytes.

## Special Bytes

These bytes are points where things are inserted or a change in formatting. Some just say to ignore this string unless the player unlocked something.

<table><thead><tr class="header"><th><p>Starting Byte</p></th><th><p>Size</p></th><th><p>Name</p></th><th><p>Description</p></th></tr></thead><tbody><tr class="odd"><td><p>0x00</p></td><td><p>1</p></td><td><p>NULL</p></td><td><p>End of string</p></td></tr><tr class="even"><td><p>0x02</p></td><td><p>1</p></td><td><p>\n</p></td><td><p>Inserts new line Some areas ignore this character.</p></td></tr><tr class="odd"><td><p>0x03</p></td><td><p>2</p></td><td><p>Name</p></td><td><p>When see 0x03??, in a string, it's usually a characters name.</p></td></tr><tr class="even"><td><p>0x05</p></td><td><p>2</p></td><td><p>Icon</p></td><td><p>0x05?? used to draw a symbol from icons.tex, like controller buttons. On PC it draws the letter of keyboard keys assigned to the controls.</p></td></tr><tr class="odd"><td><p>0x06</p></td><td><p>2</p></td><td><p>Color</p></td><td><p>0x06?? used to show a change in formatting like color</p></td></tr><tr class="even"><td><p>0x0A</p></td><td><p>2</p></td><td><p>Special_Value</p></td><td><p>0x0A?? can be a string or number value. Depending on which string you are reading it can be a different value.</p></td></tr><tr class="odd"><td><p>0x0B</p></td><td><p>2 or 3</p></td><td><p>Cursor_Locations</p></td><td><p>Might be number of possible return values that determine whether this is 3 or 2 bytes. Like YES or NO questions will only be 2 bytes<br />
but screens with a list of multiple selections will will use 3 bytes.</p></td></tr><tr class="even"><td><p><a href="http://forums.qhimm.com/index.php?topic=17120.msg243579#msg243579">0x0C</a></p></td><td><p>2</p></td><td><p>SpellID</p></td><td><p>Used to place a name of a spell.</p></td></tr></tbody></table>
