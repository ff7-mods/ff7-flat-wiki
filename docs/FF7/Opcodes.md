---
title: Opcodes
---

# Opcode Matrix

|   | 00 | 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09 | 0A | 0B | 0C | 0D | 0E | 0F |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 00 | RET | REQ | REQSW | REQEW | PREQ | PRQSW | PRQEW | RETTO | JOIN | SPLIT | SPTYPE | GTPYE | ?OC? | ?OD? | DSKCG | SPECIAL |
| 10 | GotoNext | GotoNextLong | GotoPrev | GotoPrevLong | IfUByte | IfUByteL | IfSWord | IfSWordL | IfUSWord | IfUSWordL | \- | \- | ?1C? | \- | \- | \- |
| 20 | MINIGAME | TUTOR | BTMD2 | BTRLD | wait | NFADE | BLINK | BGMOVIE | KAWAI | KAWIW | PMOVA | SLIP | BGPDH | BGSCR | WCLS | WSIZW |
| 30 | IF-KEY | IF-KEYON | IF-KEYOF | UC | PDIRA | PTURA | WSPCL | WNUMB | STTIM | GOLD+ | GOLD- | CHGLD | HMPMAX1 | HMPMAX2 | MHMMX | HMPMAX3 |
| 40 | message | MPARA | MPRA2 | MPNAM | \- | MP+ | \- | MP- | ASK | MENU | MENU2 | BTLTB | \- | HP+ | \- | HP- |
| 50 | window | WMOVE | WMODE | WREST | WCLSE | WROW | GWCOL | SWCOL | ST-ITM | DL-ITM | CK-ITM | SM-TRA | DM-TRA | CM-TRA | SHAKE | NOP |
| 60 | MAPJUMP | SCRLO | SCRLC | SCRLA | SCR2D | SCRCC | SCR2DC | SCRLW | SCR2DL | MPDSP | VWOFT | FADE | FADEW | IDLCK | LSTMP | SCRLP |
| 70 | battle | BTLON | BTLMD | PGTDR | GETPC | PXYZI | PLUS! | PLUS2! | MINUS! | MINUS2! | INC! | INC2! | DEC! | DEC2! | TLKON | RDMSD |
| 80 | set byte | SET-WORD | BIT-ON | BIT-OFF | BIT-XOR | PLUS | PLUS2 | MINUS | MINUS2 | MUL | MUL2 | DIV | DIV2 | MOD | MOD2 | AND |
| 90 | AND2 | OR | OR2 | XOR | XOR2 | INC | INC2 | DEC | DEC2 | RANDOM | LBYTE | HBYTE | 2BYTE | SETX | GETX | SEARCHX |
| A0 | PC | CHAR | DFANM | ANIME1 | VISI | XYZI | XYI | XYZ | MOVE | CMOVE | MOVA | TURA | ANIMW | FMOVE | ANIME2 | ANIM!1 |
| B0 | CANIM1 | CANIM!1 | MSPED | DIR | TURNGEN | TURN | DIRA | GETDIR | GETAXY | GETAI | ANIM!2 | CANIM2 | CANIM!2 | ASPED | \- | CC |
| C0 | JUMP | AXYZ | LADER | OFST | OFSTW | TALKR | SLIDR | SOLID | PRTYP | PRTYM | PRTYE | IF-PRTYQ | IF-MEMBQ | MMB+- | MMBLK | MMBUK |
| D0 | LINE | LINON | MPJPO | SLINE | SIN | COS | TLKR2 | SLDR2 | PMJMP | PMJMP2 | AKAO2 | FCFIX | CCANM | ANIMB | TURNW | MPPAL |
| E0 | BGON | BGOFF | BGROL | BGROL2 | BGCLR | STPAL | LDPAL | CPPA | RTPAL | ADPAL | MPPAL2 | STPLS | LDPLS | CPPAL2 | RTPAL2 | ADPAL2 |
| F0 | MUSIC | Sound | AKAO | MUSVT | MUSVM | MULCK | BMUSC | CHMPH | PMVIE | MOVIE | MVIEF | MVCAM | FMUSC | CMUSC | CHMST | GAMEOVER |

## Opcode Listings, Arguments & Descriptions

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Opcode</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Name</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0x00</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>RET</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(204,204,204);"><p>Arguments</p></td>
<td style="text-align: center; background: rgb(204,204,204);"><p>Definition</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>(none)</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>(none)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(204,204,204);"><p>Description</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(255,255,255);"><p>Returns control back to the standard program loop.<br />
Usually you can control the PC again after this point.</p></td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Opcode</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Name</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0x01</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>REQ</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(204,204,204);"><p>Arguments</p></td>
<td style="text-align: center; background: rgb(204,204,204);"><p>Definition</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>(none)</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>(none)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(204,204,204);"><p>Description</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(255,255,255);"><p>Returns control back to the standard program loop.<br />
Usually you can control the PC again after this point.</p></td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Opcode</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Name</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0x30</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>WINDOW</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(204,204,204);"><p>Arguments</p></td>
<td style="text-align: center; background: rgb(204,204,204);"><p>Definition</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>id = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Window ID</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>x = long</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>X coordinate for the upper left hand corner</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>y = long</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Y coordinate for the upper left hand corner</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>h = long</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Width of window in pixels</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>w = long</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Height of window in pixels</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(204,204,204);"><p>Description</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(255,255,255);"><p>Initializes a windowpane. This does not display a window, but allows for a<br />
"container" for the commands ASK and MESSAGE to place text within. It<br />
is referenced by it's window ID.</p></td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th style="text-align: center; background: rgb(204,204,204);"><p>Opcode</p></th>
<th style="text-align: center; background: rgb(204,204,204);"><p>Name</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>0x48</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>ASK</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(204,204,204);"><p>Arguments</p></td>
<td style="text-align: center; background: rgb(204,204,204);"><p>Definition</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>unknown = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Unknown</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>win = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Window ID to place data into</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>mes = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Which dialog to display from dialog table</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>1st = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Which line is the first choice</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>nth = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Which line is the last choice</p></td>
</tr>
<tr>
<td style="text-align: center; background: rgb(255,255,255);"><p>var = byte</p></td>
<td style="text-align: center; background: rgb(255,255,255);"><p>Unknown</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(204,204,204);"><p>Description</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center; background: rgb(255,255,255);"><p>The ASK command opens a window with a set of choices to be picked<br />
with the "selector finger" (Yubi) [WHERE IS THIS RETURNED?]</p></td>
</tr>
</tbody>
</table>
