---
title: Battle_Script
---

(Information on opcodes provided by Terence Fergusson. Almost all information comes from [this post](http://forums.qhimm.com/index.php?topic=3290.msg45951#msg45951) on the forums.)

There are four actions to be explained when dealing with any opcode in AI script: Arguments, Values to take from the stack, what to do with Arguments and Values, and what to put back on the stack. So to fully understand what is happening a brief explanation of the stack is necessary.

The stack is more-or-less a list of values with different lengths. Only the top of the stack (the most recently added value) can be accessed at any given time, but when that value is accessed it is removed from the top of the stack and the previously added value now becomes the top of the stack. Adding to the stack is called "Pushing" a value and taking a value off is called "Popping". When pushing a value to the stack, the value of the number is pushed followed by the value type. The value type can be one of three different things:  
  
{\| border="1" cellspacing="1" cellpadding="3" align="center" style="border: 1px solid black; border-collapse: collapse;" ! style="background:rgb(204,204,204)" align="center" \| Code ! style="background:rgb(204,204,204)" align="center" \| Type \|- \| align="center" \| 0Xh \| Value \|- \| align="center" \| 1Xh \| [Address](Battle_AI_Addresses) Values \|- \|}  
They are stored as DWords, but the X will determine how many bytes to use: 0 = bit, 1 = Byte, 2 = Word, 3 = Three bytes

Now that we've seen the stack, here are the opcodes:

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Code</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Arguments</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Value(s) to pop</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Value to push</p></th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Push Values</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0Xh</p></td>
<td style="text-align: center;"><p>2 byte Memory Address</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Type 0X stored at translated Address</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Push Addresses</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>1Xh</p></td>
<td style="text-align: center;"><p>2 byte Memory Address</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Address value with a scope of X</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Mathematical and Bit-wise Operators</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>30h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Sum of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>31h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Difference of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>32h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Product of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>33h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Quotient of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>34h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Remainder from quotient of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>35h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Bit-wise AND of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>36h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Bit-wise OR of pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>37h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Bit-wise NOT of pop</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Logical Operators</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>40h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if pops are EQUAL</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>41h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if pops are NOT EQUAL</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>42h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if first pop is GREATER THAN OR EQUAL TO second pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>43h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if first pop is LESS THAN OR EQUAL TO second pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>44h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if first pop is GREATER THAN second pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>45h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if first pop is LESS THAN second pop</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Logical Comparisons</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>50h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if both pops are NON-ZERO (Logical AND)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>51h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>True if either pop is NON-ZERO (Logical OR)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>52h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>True if pop is ZERO (Logical NOT)</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Push Constants</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>60h</p></td>
<td style="text-align: center;"><p>1 byte Value</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Argument of type 01</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>61h</p></td>
<td style="text-align: center;"><p>2 byte Value</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Argument of type 02</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>62h</p></td>
<td style="text-align: center;"><p>3 byte Value</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Argument of type 03</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Script Jumps (No Pushes)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>70h</p></td>
<td style="text-align: center;"><p>2 byte Script Address</p></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Jumps to script address in argument if pop is 0</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>71h</p></td>
<td style="text-align: center;"><p>2 byte Script Address</p></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Jumps to script address in argument if pop and top of stack are not equal</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>72h</p></td>
<td style="text-align: center;"><p>2 byte Script Address</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Jumps to script address in argument</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>73h</p></td>
<td colspan="3" style="text-align: center;"><p>This ends the script</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>74h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Pops one value from stack. (Not used)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>75h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Link all scripts of script owner to popped Character ID.</p></td>
</tr>
<tr>
<td colspan="4" style="text-align: center; background: rgb(224,224,224);"><p>Bit Operations</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>80h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>First pop masked by second pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>81h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Random Word (0-65535)</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>82h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Random bit of pop stored as type 02</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>83h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>If pop is Type 01, Type 01 with count of number of bits set in pop<br />
If pop is Type 02, Type 02 filled with value of first non-null value in pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>84h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 2X</p></td>
<td style="text-align: center;"><p>Type 02 indicating which values in popped set were greatest</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>85h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 2X</p></td>
<td style="text-align: center;"><p>Type 02 indicating which values in popped set were least</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>86h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 1X</p></td>
<td style="text-align: center;"><p>Type 02 indicating MP Cost of attack index referenced in pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>87h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Type 02 with only bit in pop turned on (1 &lt;&lt; [pop])</p></td>
</tr>
<tr>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

 

<table>
<thead>
<tr>
<th colspan="4" style="text-align: center; background: rgb(204,204,204);"><p>Command</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(224,224,224);"><p>Code</p></td>
<td style="text-align: center; background: rgb(224,224,224);"><p>Arguments</p></td>
<td style="text-align: center; background: rgb(224,224,224);"><p>Value(s) to pop</p></td>
<td style="text-align: center; background: rgb(224,224,224);"><p>Effect</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>90h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 1X, One of type 0X or 2X</p></td>
<td style="text-align: center;"><p>If first pop &lt; 4000h; Stores second pop at first pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>90h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 1X, One of type 0X or 2X, One of type 1X</p></td>
<td style="text-align: center;"><p>If first pop &gt;= 4000h; Stores second pop at first pop constrained by mask at third pop</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>91h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of any type</p></td>
<td style="text-align: center;"><p>Pops one value from stack.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>92h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>First pop is attack ID to perform. Second pop action type<br />
</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>93h</p></td>
<td style="text-align: center;"><p>NULL terminated string</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Displays string</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>94h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Copy current status, hp and mp as well as some other specific data (like boosts, multipliers) from units in first given mask to units in second mask.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>95h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>One of type 1X, one of type 00</p></td>
<td style="text-align: center;"><p>If second pop is 1, takes value at local address 2010 and writes value at <a href="../../Savemap#Save_Memory_Bank_1.2F2" title="wikilink">memory bank 1/2</a> at offset specified by first pop<br />
If second pop is 0, data at memory bank1/2 at offset specified by first pop is stored at local address 2010.<br />
Otherwise, command is ignored.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>96h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two of any type</p></td>
<td style="text-align: center;"><p>Get fighter elemental defense.</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>A0h</p></td>
<td style="text-align: center;"><p>One byte, NULL terminated ASCII</p></td>
<td style="text-align: center;"><p>First argument of any type</p></td>
<td style="text-align: center;"><p>Displays string to debug console, replacing "%d"s with pops</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>A1h</p></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"><p>Two values of any type</p></td>
<td style="text-align: center;"><p>Pops two values from stack (Not Used, but valid command)</p></td>
</tr>
<tr>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
<td style="text-align: center;"></td>
</tr>
</tbody>
</table>

  
GENERAL NOTES:

- Command 90h is overloaded.
- If a type 2X is popped and any type is accepted, only the first value will be considered.
- If specific type is expected and that type is not available, the game with either crash or ignore that entire line.
- TRUE and FALSE are stored as type 00 as '1' and '0' respectively.
- Commands 74h and A1h are never used, but have been documented as valid commands.
- Commands 75h and 96h only appear in the Character AI found in the KERNEL.BIN.
- Commands of group 2X, BX, CX, DX, EX, and FX are treated as NOPs. The script will ignore them and continue processing. Also, any 5X, 6X, 7X, 8X, and 9X value that isn't listed above appear to be treated the same way, but it's safest to use a value from the 2X group. An incorrect 0X, 1X, 3X, or 4X will have unintended side-effects.

0X & 1X CODES NOTES:

- Valid values for X are 0, 1, 2, and 3.
  - These will store a bit, byte, word, and dword respectively.

3X CODES NOTES:

- The pushed value is type 2x if either of the pops are a 1X or 2X. In that case, the Masks of both pops are ANDed together. In \*all\* cases, the highest pop's size is used to determine the new pop's size.

4X CODES NOTES:

- The Pushed value will be type 00 if either component is a 1X or 2X type. It will only push TRUE or FALSE
- If both were 0X types, the result will be a type 02 which contains the Mask of all the objects in the pops that passed the comparison

86 CODE NOTES:

- This get the MP Cost of the ability referenced in the pop. The value of pop is referenced to the following areas:

` If Value >= 0xFFFF, return 0`  
` If Value <= 0x00FF, Addr = 00DAAC78 + Value*0x1C`  
` If Value >= 0x0100, match Value with wr[0099AAF4+(ID=[0..31])*2]`  
`    First ID it matches, Addr = 0099A774 + ID*0x1C`  
` If no Addr is found, return 0`  
` Otherwise, return wr[Addr + 4]`

The pushed value is, thus, the MP cost of the defined ability as a type 02. Note that 0x00 to 0xFF are standard magic and always loaded, while 0x100+ are the unique abilities loaded through scene.bin.

92 CODE NOTES:

- Second pop must be one of the following:

  
[Command index](../../Command_data) in case of character AI

20h - For enemy attack

22h - Force execution of script (referenced by first pop)

24h - Pauses battle engine while string is displayed (in conjunction with code 93)
