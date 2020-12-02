---
title: Opcodes
---

[Home](Main%20Page.md) > [FF8](FF8.md) > [Field](FF8/Field.md) > [Script](FF8/Field/Script.md) > Opcodes

By Aali, myst6re and Shard.

## The language

The field script language in ff8 is a simple assembly language with a
stack. Here is an example:

`stack = []`

`PSHM_W       1024      # push var1024 onto the stack (stack = [var1024])`  
`PSHN_L       6         # push number 6 onto the stack (stack = [6Â ; var1024])`  
`CAL          EQ        # compare the two numbers at the top of the stack, pop this numbers, and push the result (1 or 0) into the stack (stack = [1 or 0]) `  
`JPF          LABEL1    # if the popped top of the stack is 0, jump to LABEL1 (stack = [])`  
`PSHN_L       0         # push 0 at the top of the stack (stack = [0])`  
`POPM_W       1024      # pop the top of the stack into var1024 (stack = [])`  
`JMP          LABEL2    # goto LABEL2`  
`LABEL1`  
`PSHN_L       1         # push 1 at the top of the stack (stack = [1])`  
`POPM_W       1024      # pop the top of the stack into var1024 (stack = [])`  
`LABEL2`  
`...`

In standard code, it's equivalent to:

`if(var1024 == 6) {`  
`    var1024 = 0;`  
`} else {`  
`    var1024 = 1;`  
`}`

## Reading Documentation

Each Opcode's page lists all the parameters for that function in the
order you would put them on the stack before the function call. The
inline argument is listed separately, if the function requires one. For
example, on the page for [SET3][], the parameters are listed like this:

  
*XCoord*

*YCoord*

*ZCoord*

**SET3**

Which means when you call **SET3**, the ZCoord is the top item on the
stack, YCoord is under it, and XCoord is under that, for example

`PSHN_L      402   (XCoord)`  
`PSHN_L      -381  (YCoord)`  
`PSHN_L      20    (ZCoord)`  
`SET3        17    (walkmesh triangle ID)`

## Opcode list

| Opcode | Name                           | Function Type      |
|--------|--------------------------------|--------------------|
| 000    | [000 NOP][] *(Unused)*         | Script Processing  |
| 001    | [001 CAL][]                    | Script Processing  |
| 002    | [002 JMP][]                    | Script Processing  |
| 003    | [003 JPF][]                    | Script Processing  |
| 004    | [004 GJMP][] *(Unused)*        | Script Processing  |
| 005    | [005 LBL][]                    | Script Processing  |
| 006    | [006 RET][]                    | Script Processing  |
| 007    | [007 PSHN\_L][]                | Memory             |
| 008    | [008 PSHI\_L][]                | Memory             |
| 009    | [009 POPI\_L][]                | Memory             |
| 00A    | [00A PSHM\_B][]                | Memory             |
| 00B    | [00B POPM\_B][]                | Memory             |
| 00C    | [00C PSHM\_W][]                | Memory             |
| 00D    | [00D POPM\_W][]                | Memory             |
| 00E    | [00E PSHM\_L][]                | Memory             |
| 00F    | [00F POPM\_L][]                | Memory             |
| 010    | [010 PSHSM\_B][]               | Memory             |
| 011    | [011 PSHSM\_W][]               | Memory             |
| 012    | [012 PSHSM\_L][]               | Memory             |
| 013    | [013 PSHAC][]                  | Memory             |
| 014    | [014 REQ][]                    | Script Processing  |
| 015    | [015 REQSW][]                  | Script Processing  |
| 016    | [016 REQEW][]                  | Script Processing  |
| 017    | [017 PREQ][]                   | Script Processing  |
| 018    | [018 PREQSW][]                 | Script Processing  |
| 019    | [019 PREQEW][]                 | Script Processing  |
| 01A    | [01A UNUSE][]                  | Entity             |
| 01B    | [01B DEBUG][] *(Unused)*       |                    |
| 01C    | [01C HALT][]                   | Script Processing  |
| 01D    | [01D SET][]                    | Entity             |
| 01E    | [01E SET3][SET3]               | Entity             |
| 01F    | [01F IDLOCK][]                 | Field related      |
| 020    | [020 IDUNLOCK][]               | Field related      |
| 021    | [021 EFFECTPLAY2][]            | Music and Sound    |
| 022    | [022 FOOTSTEP][]               |                    |
| 023    | [023 JUMP][]                   | Entity             |
| 024    | [024 JUMP3][]                  | Entity             |
| 025    | [025 LADDERUP][]               | Entity             |
| 026    | [026 LADDERDOWN][]             | Entity             |
| 027    | [027 LADDERUP2][]              | Entity             |
| 028    | [028 LADDERDOWN2][]            | Entity             |
| 029    | [029 MAPJUMP][]                | Field related      |
| 02A    | [02A MAPJUMP3][]               | Field related      |
| 02B    | [02B SETMODEL][]               | Entity             |
| 02C    | [02C BASEANIME][]              | Animation          |
| 02D    | [02D ANIME][]                  | Animation          |
| 02E    | [02E ANIMEKEEP][]              | Animation          |
| 02F    | [02F CANIME][]                 | Animation          |
| 030    | [030 CANIMEKEEP][]             | Animation          |
| 031    | [031 RANIME][]                 | Animation          |
| 032    | [032 RANIMEKEEP][]             | Animation          |
| 033    | [033 RCANIME][]                | Animation          |
| 034    | [034 RCANIMEKEEP][]            | Animation          |
| 035    | [035 RANIMELOOP][]             | Animation          |
| 036    | [036 RCANIMELOOP][]            | Animation          |
| 037    | [037 LADDERANIME][]            | Animation          |
| 038    | [038 DISCJUMP][]               | Field related      |
| 039    | [039 SETLINE][]                | Entity             |
| 03A    | [03A LINEON][]                 | Entity             |
| 03B    | [03B LINEOFF][]                | Entity             |
| 03C    | [03C WAIT][]                   | Script Processing  |
| 03D    | [03D MSPEED][]                 |                    |
| 03E    | [03E MOVE][]                   | Entity             |
| 03F    | [03F MOVEA][]                  |                    |
| 040    | [040 PMOVEA][]                 |                    |
| 041    | [041 CMOVE][]                  |                    |
| 042    | [042 FMOVE][]                  |                    |
| 043    | [043 PJUMPA][]                 |                    |
| 044    | [044 ANIMESYNC][]              | Script Processing  |
| 045    | [045 ANIMESTOP][]              | Animation          |
| 046    | [046 MESW][] *(Unused)*        |                    |
| 047    | [047 MES][]                    | Message            |
| 048    | [048 MESSYNC][]                | Script Processing  |
| 049    | [049 MESVAR][]                 | Message            |
| 04A    | [04A ASK][]                    | Message            |
| 04B    | [04B WINSIZE][]                | Message            |
| 04C    | [04C WINCLOSE][]               | Message            |
| 04D    | [04D UCON][]                   | Misc               |
| 04E    | [04E UCOFF][]                  | Misc               |
| 04F    | [04F MOVIE][]                  | Movie              |
| 050    | [050 MOVIESYNC][]              | Script Processing  |
| 051    | [051 SETPC][]                  | Party management   |
| 052    | [052 DIR][]                    | Entity             |
| 053    | [053 DIRP][]                   |                    |
| 054    | [054 DIRA][]                   |                    |
| 055    | [055 PDIRA][]                  |                    |
| 056    | [056 SPUREADY][]               | Timer              |
| 057    | [057 TALKON][]                 | Entity             |
| 058    | [058 TALKOFF][]                | Entity             |
| 059    | [059 PUSHON][]                 | Entity             |
| 05A    | [05A PUSHOFF][]                | Entity             |
| 05B    | [05B ISTOUCH][]                |                    |
| 05C    | [05C MAPJUMPO][]               | Field related      |
| 05D    | [05D MAPJUMPON][]              | Field related      |
| 05E    | [05E MAPJUMPOFF][]             | Field related      |
| 05F    | [05F SETMESSPEED][]            | Message            |
| 060    | [060 SHOW][]                   | Entity             |
| 061    | [061 HIDE][]                   | Entity             |
| 062    | [062 TALKRADIUS][]             | Entity             |
| 063    | [063 PUSHRADIUS][]             | Entity             |
| 064    | [064 AMESW][]                  | Message            |
| 065    | [065 AMES][]                   | Message            |
| 066    | [066 GETINFO][]                |                    |
| 067    | [067 THROUGHON][]              | Entity             |
| 068    | [068 THROUGHOFF][]             | Entity             |
| 069    | [069 BATTLE][]                 | Battle             |
| 06A    | [06A BATTLERESULT][]           | Battle             |
| 06B    | [06B BATTLEON][]               | Field related      |
| 06C    | [06C BATTLEOFF][]              | Field related      |
| 06D    | [06D KEYSCAN][]                | Input              |
| 06E    | [06E KEYON][]                  | Input              |
| 06F    | [06F AASK][]                   | Message            |
| 070    | [070 PGETINFO][]               |                    |
| 071    | [071 DSCROLL][]                |                    |
| 072    | [072 LSCROLL][]                |                    |
| 073    | [073 CSCROLL][]                |                    |
| 074    | [074 DSCROLLA][]               |                    |
| 075    | [075 LSCROLLA][]               |                    |
| 076    | [076 CSCROLLA][]               |                    |
| 077    | [077 SCROLLSYNC][]             | Script Processing  |
| 078    | [078 RMOVE][]                  |                    |
| 079    | [079 RMOVEA][]                 |                    |
| 07A    | [07A RPMOVEA][]                |                    |
| 07B    | [07B RCMOVE][]                 |                    |
| 07C    | [07C RFMOVE][]                 |                    |
| 07D    | [07D MOVESYNC][]               | Script Processing  |
| 07E    | [07E CLEAR][]                  | Field related      |
| 07F    | [07F DSCROLLP][]               |                    |
| 080    | [080 LSCROLLP][]               |                    |
| 081    | [081 CSCROLLP][]               |                    |
| 082    | [082 LTURNR][]                 |                    |
| 083    | [083 LTURNL][]                 |                    |
| 084    | [084 CTURNR][]                 |                    |
| 085    | [085 CTURNL][]                 |                    |
| 086    | [086 ADDPARTY][]               | Party Management   |
| 087    | [087 SUBPARTY][]               | Party Management   |
| 088    | [088 CHANGEPARTY][]            | Party Management   |
| 089    | [089 REFRESHPARTY][]           | Party Management   |
| 08A    | [08A SETPARTY][]               | Party Management   |
| 08B    | [08B ISPARTY][]                | Party Management   |
| 08C    | [08C ADDMEMBER][]              | Party Management   |
| 08D    | [08D SUBMEMBER][]              | Party Management   |
| 08E    | [08E ISMEMBER][] *(Unused)*    | Party Management   |
| 08F    | [08F LTURN][]                  |                    |
| 090    | [090 CTURN][]                  |                    |
| 091    | [091 PLTURN][]                 |                    |
| 092    | [092 PCTURN][]                 |                    |
| 093    | [093 JOIN][]                   | Entity             |
| 094    | [094 MESFORCUS][] *(Unused)*   |                    |
| 095    | [095 BGANIME][]                | Field related      |
| 096    | [096 RBGANIME][]               | Field related      |
| 097    | [097 RBGANIMELOOP][]           | Field related      |
| 098    | [098 BGANIMESYNC][]            | Field related      |
| 099    | [099 BGDRAW][]                 | Field related      |
| 09A    | [09A BGOFF][]                  | Field related      |
| 09B    | [09B BGANIMESPEED][]           | Field related      |
| 09C    | [09C SETTIMER][]               | Timer              |
| 09D    | [09D DISPTIMER][]              | Timer              |
| 09E    | [09E SHADETIMER][] *(Unused)*  |                    |
| 09F    | [09F SETGETA][]                |                    |
| 0A0    | [0A0 SETROOTTRANS][]           |                    |
| 0A1    | [0A1 SETVIBRATE][]             |                    |
| 0A2    | [0A2 STOPVIBRATE][] *(Unused)* |                    |
| 0A3    | [0A3 MOVIEREADY][]             | Movie              |
| 0A4    | [0A4 GETTIMER][]               | Timer              |
| 0A5    | [0A5 FADEIN][]                 | Field related      |
| 0A6    | [0A6 FADEOUT][]                | Field related      |
| 0A7    | [0A7 FADESYNC][]               | Script Processing  |
| 0A8    | [0A8 SHAKE][]                  | Field related      |
| 0A9    | [0A9 SHAKEOFF][]               | Field related      |
| 0AA    | [0AA FADEBLACK][]              | Field related      |
| 0AB    | [0AB FOLLOWOFF][]              |                    |
| 0AC    | [0AC FOLLOWON][]               |                    |
| 0AD    | [0AD GAMEOVER][]               | Field related      |
| 0AE    | [0AE ENDING][] *(Unused)*      |                    |
| 0AF    | [0AF SHADELEVEL][]             |                    |
| 0B0    | [0B0 SHADEFORM][]              |                    |
| 0B1    | [0B1 FMOVEA][]                 |                    |
| 0B2    | [0B2 FMOVEP][]                 |                    |
| 0B3    | [0B3 SHADESET][]               |                    |
| 0B4    | [0B4 MUSICCHANGE][]            | Music and Sound    |
| 0B5    | [0B5 MUSICLOAD][]              | Music and Sound    |
| 0B6    | [0B6 FADENONE][]               |                    |
| 0B7    | [0B7 POLYCOLOR][]              |                    |
| 0B8    | [0B8 POLYCOLORALL][]           |                    |
| 0B9    | [0B9 KILLTIMER][]              | Timer              |
| 0BA    | [0BA CROSSMUSIC][]             |                    |
| 0BB    | [0BB DUALMUSIC][]              |                    |
| 0BC    | [0BC EFFECTPLAY][]             | Music and Sound    |
| 0BD    | [0BD EFFECTLOAD][]             | Music and Sound    |
| 0BE    | [0BE LOADSYNC][]               |                    |
| 0BF    | [0BF MUSICSTOP][]              | Music and Sound    |
| 0C0    | [0C0 MUSICVOL][]               | Music and Sound    |
| 0C1    | [0C1 MUSICVOLTRANS][]          | Music and Sound    |
| 0C2    | [0C2 MUSICVOLFADE][]           | Music and Sound    |
| 0C3    | [0C3 ALLSEVOL][]               | Music and Sound    |
| 0C4    | [0C4 ALLSEVOLTRANS][]          | Music and Sound    |
| 0C5    | [0C5 ALLSEPOS][] *(Unused)*    | Music and Sound    |
| 0C6    | [0C6 ALLSEPOSTRANS][]          | Music and Sound    |
| 0C7    | [0C7 SEVOL][]                  | Music and Sound    |
| 0C8    | [0C8 SEVOLTRANS][]             | Music and Sound    |
| 0C9    | [0C9 SEPOS][]                  | Music and Sound    |
| 0CA    | [0CA SEPOSTRANS][]             | Music and Sound    |
| 0CB    | [0CB SETBATTLEMUSIC][]         | Music and Sound    |
| 0CC    | [0CC BATTLEMODE][]             | Battle             |
| 0CD    | [0CD SESTOP][]                 | Music and Sound    |
| 0CE    | [0CE BGANIMEFLAG][] *(Unused)* |                    |
| 0CF    | [0CF INITSOUND][]              |                    |
| 0D0    | [0D0 BGSHADE][]                |                    |
| 0D1    | [0D1 BGSHADESTOP][]            |                    |
| 0D2    | [0D2 RBGSHADELOOP][]           |                    |
| 0D3    | [0D3 DSCROLL2][]               |                    |
| 0D4    | [0D4 LSCROLL2][]               |                    |
| 0D5    | [0D5 CSCROLL2][]               |                    |
| 0D6    | [0D6 DSCROLLA2][]              |                    |
| 0D7    | [0D7 LSCROLLA2][] *(Unused)*   |                    |
| 0D8    | [0D8 CSCROLLA2][]              |                    |
| 0D9    | [0D9 DSCROLLP2][] *(Unused)*   |                    |
| 0DA    | [0DA LSCROLLP2][] *(Unused)*   |                    |
| 0DB    | [0DB CSCROLLP2][] *(Unused)*   |                    |
| 0DC    | [0DC SCROLLSYNC2][]            |                    |
| 0DD    | [0DD SCROLLMODE2][]            |                    |
| 0DE    | [0DE MENUENABLE][]             | Menus              |
| 0DF    | [0DF MENUDISABLE][]            | Menus              |
| 0E0    | [0E0 FOOTSTEPON][]             |                    |
| 0E1    | [0E1 FOOTSTEPOFF][]            |                    |
| 0E2    | [0E2 FOOTSTEPOFFALL][]         |                    |
| 0E3    | [0E3 FOOTSTEPCUT][]            |                    |
| 0E4    | [0E4 PREMAPJUMP][]             |                    |
| 0E5    | [0E5 USE][]                    | Entity             |
| 0E6    | [0E6 SPLIT][]                  | Entity             |
| 0E7    | [0E7 ANIMESPEED][]             | Animation          |
| 0E8    | [0E8 RND][]                    |                    |
| 0E9    | [0E9 DCOLADD][]                |                    |
| 0EA    | [0EA DCOLSUB][]                |                    |
| 0EB    | [0EB TCOLADD][]                |                    |
| 0EC    | [0EC TCOLSUB][]                |                    |
| 0ED    | [0ED FCOLADD][]                | Field related      |
| 0EE    | [0EE FCOLSUB][]                | Field related      |
| 0EF    | [0EF COLSYNC][]                | Script processing  |
| 0F0    | [0F0 DOFFSET][]                |                    |
| 0F1    | [0F1 LOFFSETS][]               |                    |
| 0F2    | [0F2 COFFSETS][]               |                    |
| 0F3    | [0F3 LOFFSET][]                |                    |
| 0F4    | [0F4 COFFSET][]                |                    |
| 0F5    | [0F5 OFFSETSYNC][]             |                    |
| 0F6    | [0F6 RUNENABLE][]              | Entity             |
| 0F7    | [0F7 RUNDISABLE][]             | Entity             |
| 0F8    | [0F8 MAPFADEOFF][]             | Field related      |
| 0F9    | [0F9 MAPFADEON][]              | Field related      |
| 0FA    | [0FA INITTRACE][]              |                    |
| 0FB    | [0FB SETDRESS][]               | Entity             |
| 0FC    | [0FC GETDRESS][] *(Unused)*    | Entity             |
| 0FD    | [0FD FACEDIR][]                | Entity             |
| 0FE    | [0FE FACEDIRA][]               |                    |
| 0FF    | [0FF FACEDIRP][]               |                    |
| 100    | [100 FACEDIRLIMIT][]           |                    |
| 101    | [101 FACEDIROFF][]             |                    |
| 102    | [102 SARALYOFF][]              |                    |
| 103    | [103 SARALYON][]               |                    |
| 104    | [104 SARALYDISPOFF][]          |                    |
| 105    | [105 SARALYDISPON][]           |                    |
| 106    | [106 MESMODE][]                | Message            |
| 107    | [107 FACEDIRINIT][]            |                    |
| 108    | [108 FACEDIRI][]               |                    |
| 109    | [109 JUNCTION][]               | Party Management   |
| 10A    | [10A SETCAMERA][]              | Field related      |
| 10B    | [10B BATTLECUT][]              |                    |
| 10C    | [10C FOOTSTEPCOPY][]           |                    |
| 10D    | [10D WORLDMAPJUMP][]           | Field related      |
| 10E    | [10E RFACEDIRI][] *(Unused)*   |                    |
| 10F    | [10F RFACEDIR][]               |                    |
| 110    | [110 RFACEDIRA][]              |                    |
| 111    | [111 RFACEDIRP][]              |                    |
| 112    | [112 RFACEDIROFF][]            |                    |
| 113    | [113 FACEDIRSYNC][]            |                    |
| 114    | [114 COPYINFO][]               |                    |
| 115    | [115 PCOPYINFO][] *(Unused)*   |                    |
| 116    | [116 RAMESW][]                 | Message            |
| 117    | [117 BGSHADEOFF][]             | Field related      |
| 118    | [118 AXIS][]                   |                    |
| 119    | [119 AXISSYNC][] *(Unused)*    |                    |
| 11A    | [11A MENUNORMAL][]             | Menus              |
| 11B    | [11B MENUPHS][]                | Menus              |
| 11C    | [11C BGCLEAR][]                |                    |
| 11D    | [11D GETPARTY][]               | Party Management   |
| 11E    | [11E MENUSHOP][]               | Menus              |
| 11F    | [11F DISC][]                   | Field related      |
| 120    | [120 DSCROLL3][] *(Unused)*    |                    |
| 121    | [121 LSCROLL3][]               |                    |
| 122    | [122 CSCROLL3][]               |                    |
| 123    | [123 MACCEL][]                 |                    |
| 124    | [124 MLIMIT][]                 |                    |
| 125    | [125 ADDITEM][]                | Item/Magic/Card/GF |
| 126    | [126 SETWITCH][]               |                    |
| 127    | [127 SETODIN][]                |                    |
| 128    | [128 RESETGF][]                |                    |
| 129    | [129 MENUNAME][]               | Menus              |
| 12A    | [12A REST][]                   |                    |
| 12B    | [12B MOVECANCEL][]             |                    |
| 12C    | [12C PMOVECANCEL][] *(Unused)* |                    |
| 12D    | [12D ACTORMODE][]              |                    |
| 12E    | [12E MENUSAVE][]               | Menus              |
| 12F    | [12F SAVEENABLE][]             | Menus              |
| 130    | [130 PHSENABLE][]              | Menus              |
| 131    | [131 HOLD][]                   | Party Management   |
| 132    | [132 MOVIECUT][]               |                    |
| 133    | [133 SETPLACE][]               |                    |
| 134    | [134 SETDCAMERA][]             |                    |
| 135    | [135 CHOICEMUSIC][]            |                    |
| 136    | [136 GETCARD][]                |                    |
| 137    | [137 DRAWPOINT][]              | Menus              |
| 138    | [138 PHSPOWER][]               |                    |
| 139    | [139 KEY][]                    |                    |
| 13A    | [13A CARDGAME][]               | Menus              |
| 13B    | [13B SETBAR][]                 |                    |
| 13C    | [13C DISPBAR][]                |                    |
| 13D    | [13D KILLBAR][]                |                    |
| 13E    | [13E SCROLLRATIO2][]           |                    |
| 13F    | [13F WHOAMI][]                 |                    |
| 140    | [140 MUSICSTATUS][]            |                    |
| 141    | [141 MUSICREPLAY][]            |                    |
| 142    | [142 DOORLINEOFF][]            | Entity             |
| 143    | [143 DOORLINEON][]             | Entity             |
| 144    | [144 MUSICSKIP][]              |                    |
| 145    | [145 DYING][]                  | Party Management   |
| 146    | [146 SETHP][]                  | Party Management   |
| 147    | [147 GETHP][] *(Unused)*       | Party Management   |
| 148    | [148 MOVEFLUSH][]              |                    |
| 149    | [149 MUSICVOLSYNC][]           |                    |
| 14A    | [14A PUSHANIME][]              |                    |
| 14B    | [14B POPANIME][]               |                    |
| 14C    | [14C KEYSCAN2][]               | Input              |
| 14D    | [14D KEYON2][] *(Unused)*      | Input              |
| 14E    | [14E PARTICLEON][]             |                    |
| 14F    | [14F PARTICLEOFF][]            |                    |
| 150    | [150 KEYSIGHNCHANGE][]         |                    |
| 151    | [151 ADDGIL][]                 | Item/Magic/Card/GF |
| 152    | [152 ADDPASTGIL][]             | Item/Magic/Card/GF |
| 153    | [153 ADDSEEDLEVEL][]           | Item/Magic/Card/GF |
| 154    | [154 PARTICLESET][]            |                    |
| 155    | [155 SETDRAWPOINT][]           |                    |
| 156    | [156 MENUTIPS][]               | Menus              |
| 157    | [157 LASTIN][]                 |                    |
| 158    | [158 LASTOUT][]                |                    |
| 159    | [159 SEALEDOFF][]              |                    |
| 15A    | [15A MENUTUTO][]               | Menus              |
| 15B    | [15B OPENEYES][] *(Unused)*    |                    |
| 15C    | [15C CLOSEEYES][]              |                    |
| 15D    | [15D BLINKEYES][] *(Unused)*   |                    |
| 15E    | [15E SETCARD][]                | Item/Magic/Card/GF |
| 15F    | [15F HOWMANYCARD][]            | Item/Magic/Card/GF |
| 160    | [160 WHERECARD][]              | Item/Magic/Card/GF |
| 161    | [161 ADDMAGIC][]               | Item/Magic/Card/GF |
| 162    | [162 SWAP][]                   |                    |
| 163    | [163 SETPARTY2][] *(Unused)*   |                    |
| 164    | [164 SPUSYNC][]                | Timer              |
| 165    | [165 BROKEN][]                 |                    |
| 166    | [166 UNKNOWN1][]               |                    |
| 167    | [167 UNKNOWN2][]               |                    |
| 168    | [168 UNKNOWN3][]               |                    |
| 169    | [169 UNKNOWN4][]               |                    |
| 170    | [170 UNKNOWN5][]               | Item/Magic/Card/GF |
| 171    | [171 UNKNOWN6][]               | Animation          |
| 172    | [172 UNKNOWN7][]               | Animation          |
| 173    | [173 UNKNOWN8][]               | Animation          |
| 174    | [174 UNKNOWN9][]               | Animation          |
| 175    | [175 UNKNOWN10][]              |                    |
| 176    | [176 UNKNOWN11][]              |                    |
| 177    | [177 UNKNOWN12][]              |                    |
| 178    | [178 UNKNOWN13][]              | Music and Sound    |
| 179    | [179 UNKNOWN14][]              | Music and Sound    |
| 180    | [180 UNKNOWN15][]              |                    |
| 181    | [181 UNKNOWN16][]              | Field related      |
| 182    | [182 UNKNOWN17][]              | Field related      |
| 183    | [183 UNKNOWN18][]              | Menus              |

  [SET3]: FF8/Field/Script/Opcodes/01E%20SET3.md "wikilink"
  [000 NOP]: FF8/Field/Script/Opcodes/000%20NOP.md "wikilink"
  [001 CAL]: FF8/Field/Script/Opcodes/001%20CAL.md "wikilink"
  [002 JMP]: FF8/Field/Script/Opcodes/002%20JMP.md "wikilink"
  [003 JPF]: FF8/Field/Script/Opcodes/003%20JPF.md "wikilink"
  [004 GJMP]: FF8/Field/Script/Opcodes/004%20GJMP.md "wikilink"
  [005 LBL]: FF8/Field/Script/Opcodes/005%20LBL.md "wikilink"
  [006 RET]: FF8/Field/Script/Opcodes/006%20RET.md "wikilink"
  [007 PSHN\_L]: FF8/Field/Script/Opcodes/007%20PSHN%20L.md "wikilink"
  [008 PSHI\_L]: FF8/Field/Script/Opcodes/008%20PSHI%20L.md "wikilink"
  [009 POPI\_L]: FF8/Field/Script/Opcodes/009%20POPI%20L.md "wikilink"
  [00A PSHM\_B]: FF8/Field/Script/Opcodes/00A%20PSHM%20B.md "wikilink"
  [00B POPM\_B]: FF8/Field/Script/Opcodes/00B%20POPM%20B.md "wikilink"
  [00C PSHM\_W]: FF8/Field/Script/Opcodes/00C%20PSHM%20W.md "wikilink"
  [00D POPM\_W]: FF8/Field/Script/Opcodes/00D%20POPM%20W.md "wikilink"
  [00E PSHM\_L]: FF8/Field/Script/Opcodes/00E%20PSHM%20L.md "wikilink"
  [00F POPM\_L]: FF8/Field/Script/Opcodes/00F%20POPM%20L.md "wikilink"
  [010 PSHSM\_B]: FF8/Field/Script/Opcodes/010%20PSHSM%20B.md "wikilink"
  [011 PSHSM\_W]: FF8/Field/Script/Opcodes/011%20PSHSM%20W.md "wikilink"
  [012 PSHSM\_L]: FF8/Field/Script/Opcodes/012%20PSHSM%20L.md "wikilink"
  [013 PSHAC]: FF8/Field/Script/Opcodes/013%20PSHAC.md "wikilink"
  [014 REQ]: FF8/Field/Script/Opcodes/014%20REQ.md "wikilink"
  [015 REQSW]: FF8/Field/Script/Opcodes/015%20REQSW.md "wikilink"
  [016 REQEW]: FF8/Field/Script/Opcodes/016%20REQEW.md "wikilink"
  [017 PREQ]: FF8/Field/Script/Opcodes/017%20PREQ.md "wikilink"
  [018 PREQSW]: FF8/Field/Script/Opcodes/018%20PREQSW.md "wikilink"
  [019 PREQEW]: FF8/Field/Script/Opcodes/019%20PREQEW.md "wikilink"
  [01A UNUSE]: FF8/Field/Script/Opcodes/01A%20UNUSE.md "wikilink"
  [01B DEBUG]: FF8/Field/Script/Opcodes/01B%20DEBUG.md "wikilink"
  [01C HALT]: FF8/Field/Script/Opcodes/01C%20HALT.md "wikilink"
  [01D SET]: FF8/Field/Script/Opcodes/01D%20SET.md "wikilink"
  [01F IDLOCK]: FF8/Field/Script/Opcodes/01F%20IDLOCK.md "wikilink"
  [020 IDUNLOCK]: FF8/Field/Script/Opcodes/020%20IDUNLOCK.md "wikilink"
  [021 EFFECTPLAY2]: FF8/Field/Script/Opcodes/021%20EFFECTPLAY2.md "wikilink"
  [022 FOOTSTEP]: FF8/Field/Script/Opcodes/022%20FOOTSTEP.md "wikilink"
  [023 JUMP]: FF8/Field/Script/Opcodes/023%20JUMP.md "wikilink"
  [024 JUMP3]: FF8/Field/Script/Opcodes/024%20JUMP3.md "wikilink"
  [025 LADDERUP]: FF8/Field/Script/Opcodes/025%20LADDERUP.md "wikilink"
  [026 LADDERDOWN]: FF8/Field/Script/Opcodes/026%20LADDERDOWN.md "wikilink"
  [027 LADDERUP2]: FF8/Field/Script/Opcodes/027%20LADDERUP2.md "wikilink"
  [028 LADDERDOWN2]: FF8/Field/Script/Opcodes/028%20LADDERDOWN2.md "wikilink"
  [029 MAPJUMP]: FF8/Field/Script/Opcodes/029%20MAPJUMP.md "wikilink"
  [02A MAPJUMP3]: FF8/Field/Script/Opcodes/02A%20MAPJUMP3.md "wikilink"
  [02B SETMODEL]: FF8/Field/Script/Opcodes/02B%20SETMODEL.md "wikilink"
  [02C BASEANIME]: FF8/Field/Script/Opcodes/02C%20BASEANIME.md "wikilink"
  [02D ANIME]: FF8/Field/Script/Opcodes/02D%20ANIME.md "wikilink"
  [02E ANIMEKEEP]: FF8/Field/Script/Opcodes/02E%20ANIMEKEEP.md "wikilink"
  [02F CANIME]: FF8/Field/Script/Opcodes/02F%20CANIME.md "wikilink"
  [030 CANIMEKEEP]: FF8/Field/Script/Opcodes/030%20CANIMEKEEP.md "wikilink"
  [031 RANIME]: FF8/Field/Script/Opcodes/031%20RANIME.md "wikilink"
  [032 RANIMEKEEP]: FF8/Field/Script/Opcodes/032%20RANIMEKEEP.md "wikilink"
  [033 RCANIME]: FF8/Field/Script/Opcodes/033%20RCANIME.md "wikilink"
  [034 RCANIMEKEEP]: FF8/Field/Script/Opcodes/034%20RCANIMEKEEP.md "wikilink"
  [035 RANIMELOOP]: FF8/Field/Script/Opcodes/035%20RANIMELOOP.md "wikilink"
  [036 RCANIMELOOP]: FF8/Field/Script/Opcodes/036%20RCANIMELOOP.md "wikilink"
  [037 LADDERANIME]: FF8/Field/Script/Opcodes/037%20LADDERANIME.md "wikilink"
  [038 DISCJUMP]: FF8/Field/Script/Opcodes/038%20DISCJUMP.md "wikilink"
  [039 SETLINE]: FF8/Field/Script/Opcodes/039%20SETLINE.md "wikilink"
  [03A LINEON]: FF8/Field/Script/Opcodes/03A%20LINEON.md "wikilink"
  [03B LINEOFF]: FF8/Field/Script/Opcodes/03B%20LINEOFF.md "wikilink"
  [03C WAIT]: FF8/Field/Script/Opcodes/03C%20WAIT.md "wikilink"
  [03D MSPEED]: FF8/Field/Script/Opcodes/03D%20MSPEED.md "wikilink"
  [03E MOVE]: FF8/Field/Script/Opcodes/03E%20MOVE.md "wikilink"
  [03F MOVEA]: FF8/Field/Script/Opcodes/03F%20MOVEA.md "wikilink"
  [040 PMOVEA]: FF8/Field/Script/Opcodes/040%20PMOVEA.md "wikilink"
  [041 CMOVE]: FF8/Field/Script/Opcodes/041%20CMOVE.md "wikilink"
  [042 FMOVE]: FF8/Field/Script/Opcodes/042%20FMOVE.md "wikilink"
  [043 PJUMPA]: FF8/Field/Script/Opcodes/043%20PJUMPA.md "wikilink"
  [044 ANIMESYNC]: FF8/Field/Script/Opcodes/044%20ANIMESYNC.md "wikilink"
  [045 ANIMESTOP]: FF8/Field/Script/Opcodes/045%20ANIMESTOP.md "wikilink"
  [046 MESW]: FF8/Field/Script/Opcodes/046%20MESW.md "wikilink"
  [047 MES]: FF8/Field/Script/Opcodes/047%20MES.md "wikilink"
  [048 MESSYNC]: FF8/Field/Script/Opcodes/048%20MESSYNC.md "wikilink"
  [049 MESVAR]: FF8/Field/Script/Opcodes/049%20MESVAR.md "wikilink"
  [04A ASK]: FF8/Field/Script/Opcodes/04A%20ASK.md "wikilink"
  [04B WINSIZE]: FF8/Field/Script/Opcodes/04B%20WINSIZE.md "wikilink"
  [04C WINCLOSE]: FF8/Field/Script/Opcodes/04C%20WINCLOSE.md "wikilink"
  [04D UCON]: FF8/Field/Script/Opcodes/04D%20UCON.md "wikilink"
  [04E UCOFF]: FF8/Field/Script/Opcodes/04E%20UCOFF.md "wikilink"
  [04F MOVIE]: FF8/Field/Script/Opcodes/04F%20MOVIE.md "wikilink"
  [050 MOVIESYNC]: FF8/Field/Script/Opcodes/050%20MOVIESYNC.md "wikilink"
  [051 SETPC]: FF8/Field/Script/Opcodes/051%20SETPC.md "wikilink"
  [052 DIR]: FF8/Field/Script/Opcodes/052%20DIR.md "wikilink"
  [053 DIRP]: FF8/Field/Script/Opcodes/053%20DIRP.md "wikilink"
  [054 DIRA]: FF8/Field/Script/Opcodes/054%20DIRA.md "wikilink"
  [055 PDIRA]: FF8/Field/Script/Opcodes/055%20PDIRA.md "wikilink"
  [056 SPUREADY]: FF8/Field/Script/Opcodes/056%20SPUREADY.md "wikilink"
  [057 TALKON]: FF8/Field/Script/Opcodes/057%20TALKON.md "wikilink"
  [058 TALKOFF]: FF8/Field/Script/Opcodes/058%20TALKOFF.md "wikilink"
  [059 PUSHON]: FF8/Field/Script/Opcodes/059%20PUSHON.md "wikilink"
  [05A PUSHOFF]: FF8/Field/Script/Opcodes/05A%20PUSHOFF.md "wikilink"
  [05B ISTOUCH]: FF8/Field/Script/Opcodes/05B%20ISTOUCH.md "wikilink"
  [05C MAPJUMPO]: FF8/Field/Script/Opcodes/05C%20MAPJUMPO.md "wikilink"
  [05D MAPJUMPON]: FF8/Field/Script/Opcodes/05D%20MAPJUMPON.md "wikilink"
  [05E MAPJUMPOFF]: FF8/Field/Script/Opcodes/05E%20MAPJUMPOFF.md "wikilink"
  [05F SETMESSPEED]: FF8/Field/Script/Opcodes/05F%20SETMESSPEED.md "wikilink"
  [060 SHOW]: FF8/Field/Script/Opcodes/060%20SHOW.md "wikilink"
  [061 HIDE]: FF8/Field/Script/Opcodes/061%20HIDE.md "wikilink"
  [062 TALKRADIUS]: FF8/Field/Script/Opcodes/062%20TALKRADIUS.md "wikilink"
  [063 PUSHRADIUS]: FF8/Field/Script/Opcodes/063%20PUSHRADIUS.md "wikilink"
  [064 AMESW]: FF8/Field/Script/Opcodes/064%20AMESW.md "wikilink"
  [065 AMES]: FF8/Field/Script/Opcodes/065%20AMES.md "wikilink"
  [066 GETINFO]: FF8/Field/Script/Opcodes/066%20GETINFO.md "wikilink"
  [067 THROUGHON]: FF8/Field/Script/Opcodes/067%20THROUGHON.md "wikilink"
  [068 THROUGHOFF]: FF8/Field/Script/Opcodes/068%20THROUGHOFF.md "wikilink"
  [069 BATTLE]: FF8/Field/Script/Opcodes/069%20BATTLE.md "wikilink"
  [06A BATTLERESULT]: FF8/Field/Script/Opcodes/06A%20BATTLERESULT.md
    "wikilink"
  [06B BATTLEON]: FF8/Field/Script/Opcodes/06B%20BATTLEON.md "wikilink"
  [06C BATTLEOFF]: FF8/Field/Script/Opcodes/06C%20BATTLEOFF.md "wikilink"
  [06D KEYSCAN]: FF8/Field/Script/Opcodes/06D%20KEYSCAN.md "wikilink"
  [06E KEYON]: FF8/Field/Script/Opcodes/06E%20KEYON.md "wikilink"
  [06F AASK]: FF8/Field/Script/Opcodes/06F%20AASK.md "wikilink"
  [070 PGETINFO]: FF8/Field/Script/Opcodes/070%20PGETINFO.md "wikilink"
  [071 DSCROLL]: FF8/Field/Script/Opcodes/071%20DSCROLL.md "wikilink"
  [072 LSCROLL]: FF8/Field/Script/Opcodes/072%20LSCROLL.md "wikilink"
  [073 CSCROLL]: FF8/Field/Script/Opcodes/073%20CSCROLL.md "wikilink"
  [074 DSCROLLA]: FF8/Field/Script/Opcodes/074%20DSCROLLA.md "wikilink"
  [075 LSCROLLA]: FF8/Field/Script/Opcodes/075%20LSCROLLA.md "wikilink"
  [076 CSCROLLA]: FF8/Field/Script/Opcodes/076%20CSCROLLA.md "wikilink"
  [077 SCROLLSYNC]: FF8/Field/Script/Opcodes/077%20SCROLLSYNC.md "wikilink"
  [078 RMOVE]: FF8/Field/Script/Opcodes/078%20RMOVE.md "wikilink"
  [079 RMOVEA]: FF8/Field/Script/Opcodes/079%20RMOVEA.md "wikilink"
  [07A RPMOVEA]: FF8/Field/Script/Opcodes/07A%20RPMOVEA.md "wikilink"
  [07B RCMOVE]: FF8/Field/Script/Opcodes/07B%20RCMOVE.md "wikilink"
  [07C RFMOVE]: FF8/Field/Script/Opcodes/07C%20RFMOVE.md "wikilink"
  [07D MOVESYNC]: FF8/Field/Script/Opcodes/07D%20MOVESYNC.md "wikilink"
  [07E CLEAR]: FF8/Field/Script/Opcodes/07E%20CLEAR.md "wikilink"
  [07F DSCROLLP]: FF8/Field/Script/Opcodes/07F%20DSCROLLP.md "wikilink"
  [080 LSCROLLP]: FF8/Field/Script/Opcodes/080%20LSCROLLP.md "wikilink"
  [081 CSCROLLP]: FF8/Field/Script/Opcodes/081%20CSCROLLP.md "wikilink"
  [082 LTURNR]: FF8/Field/Script/Opcodes/082%20LTURNR.md "wikilink"
  [083 LTURNL]: FF8/Field/Script/Opcodes/083%20LTURNL.md "wikilink"
  [084 CTURNR]: FF8/Field/Script/Opcodes/084%20CTURNR.md "wikilink"
  [085 CTURNL]: FF8/Field/Script/Opcodes/085%20CTURNL.md "wikilink"
  [086 ADDPARTY]: FF8/Field/Script/Opcodes/086%20ADDPARTY.md "wikilink"
  [087 SUBPARTY]: FF8/Field/Script/Opcodes/087%20SUBPARTY.md "wikilink"
  [088 CHANGEPARTY]: FF8/Field/Script/Opcodes/088%20CHANGEPARTY.md "wikilink"
  [089 REFRESHPARTY]: FF8/Field/Script/Opcodes/089%20REFRESHPARTY.md
    "wikilink"
  [08A SETPARTY]: FF8/Field/Script/Opcodes/08A%20SETPARTY.md "wikilink"
  [08B ISPARTY]: FF8/Field/Script/Opcodes/08B%20ISPARTY.md "wikilink"
  [08C ADDMEMBER]: FF8/Field/Script/Opcodes/08C%20ADDMEMBER.md "wikilink"
  [08D SUBMEMBER]: FF8/Field/Script/Opcodes/08D%20SUBMEMBER.md "wikilink"
  [08E ISMEMBER]: FF8/Field/Script/Opcodes/08E%20ISMEMBER.md "wikilink"
  [08F LTURN]: FF8/Field/Script/Opcodes/08F%20LTURN.md "wikilink"
  [090 CTURN]: FF8/Field/Script/Opcodes/090%20CTURN.md "wikilink"
  [091 PLTURN]: FF8/Field/Script/Opcodes/091%20PLTURN.md "wikilink"
  [092 PCTURN]: FF8/Field/Script/Opcodes/092%20PCTURN.md "wikilink"
  [093 JOIN]: FF8/Field/Script/Opcodes/093%20JOIN.md "wikilink"
  [094 MESFORCUS]: FF8/Field/Script/Opcodes/094%20MESFORCUS.md "wikilink"
  [095 BGANIME]: FF8/Field/Script/Opcodes/095%20BGANIME.md "wikilink"
  [096 RBGANIME]: FF8/Field/Script/Opcodes/096%20RBGANIME.md "wikilink"
  [097 RBGANIMELOOP]: FF8/Field/Script/Opcodes/097%20RBGANIMELOOP.md
    "wikilink"
  [098 BGANIMESYNC]: FF8/Field/Script/Opcodes/098%20BGANIMESYNC.md "wikilink"
  [099 BGDRAW]: FF8/Field/Script/Opcodes/099%20BGDRAW.md "wikilink"
  [09A BGOFF]: FF8/Field/Script/Opcodes/09A%20BGOFF.md "wikilink"
  [09B BGANIMESPEED]: FF8/Field/Script/Opcodes/09B%20BGANIMESPEED.md
    "wikilink"
  [09C SETTIMER]: FF8/Field/Script/Opcodes/09C%20SETTIMER.md "wikilink"
  [09D DISPTIMER]: FF8/Field/Script/Opcodes/09D%20DISPTIMER.md "wikilink"
  [09E SHADETIMER]: FF8/Field/Script/Opcodes/09E%20SHADETIMER.md "wikilink"
  [09F SETGETA]: FF8/Field/Script/Opcodes/09F%20SETGETA.md "wikilink"
  [0A0 SETROOTTRANS]: FF8/Field/Script/Opcodes/0A0%20SETROOTTRANS.md
    "wikilink"
  [0A1 SETVIBRATE]: FF8/Field/Script/Opcodes/0A1%20SETVIBRATE.md "wikilink"
  [0A2 STOPVIBRATE]: FF8/Field/Script/Opcodes/0A2%20STOPVIBRATE.md "wikilink"
  [0A3 MOVIEREADY]: FF8/Field/Script/Opcodes/0A3%20MOVIEREADY.md "wikilink"
  [0A4 GETTIMER]: FF8/Field/Script/Opcodes/0A4%20GETTIMER.md "wikilink"
  [0A5 FADEIN]: FF8/Field/Script/Opcodes/0A5%20FADEIN.md "wikilink"
  [0A6 FADEOUT]: FF8/Field/Script/Opcodes/0A6%20FADEOUT.md "wikilink"
  [0A7 FADESYNC]: FF8/Field/Script/Opcodes/0A7%20FADESYNC.md "wikilink"
  [0A8 SHAKE]: FF8/Field/Script/Opcodes/0A8%20SHAKE.md "wikilink"
  [0A9 SHAKEOFF]: FF8/Field/Script/Opcodes/0A9%20SHAKEOFF.md "wikilink"
  [0AA FADEBLACK]: FF8/Field/Script/Opcodes/0AA%20FADEBLACK.md "wikilink"
  [0AB FOLLOWOFF]: FF8/Field/Script/Opcodes/0AB%20FOLLOWOFF.md "wikilink"
  [0AC FOLLOWON]: FF8/Field/Script/Opcodes/0AC%20FOLLOWON.md "wikilink"
  [0AD GAMEOVER]: FF8/Field/Script/Opcodes/0AD%20GAMEOVER.md "wikilink"
  [0AE ENDING]: FF8/Field/Script/Opcodes/0AE%20ENDING.md "wikilink"
  [0AF SHADELEVEL]: FF8/Field/Script/Opcodes/0AF%20SHADELEVEL.md "wikilink"
  [0B0 SHADEFORM]: FF8/Field/Script/Opcodes/0B0%20SHADEFORM.md "wikilink"
  [0B1 FMOVEA]: FF8/Field/Script/Opcodes/0B1%20FMOVEA.md "wikilink"
  [0B2 FMOVEP]: FF8/Field/Script/Opcodes/0B2%20FMOVEP.md "wikilink"
  [0B3 SHADESET]: FF8/Field/Script/Opcodes/0B3%20SHADESET.md "wikilink"
  [0B4 MUSICCHANGE]: FF8/Field/Script/Opcodes/0B4%20MUSICCHANGE.md "wikilink"
  [0B5 MUSICLOAD]: FF8/Field/Script/Opcodes/0B5%20MUSICLOAD.md "wikilink"
  [0B6 FADENONE]: FF8/Field/Script/Opcodes/0B6%20FADENONE.md "wikilink"
  [0B7 POLYCOLOR]: FF8/Field/Script/Opcodes/0B7%20POLYCOLOR.md "wikilink"
  [0B8 POLYCOLORALL]: FF8/Field/Script/Opcodes/0B8%20POLYCOLORALL.md
    "wikilink"
  [0B9 KILLTIMER]: FF8/Field/Script/Opcodes/0B9%20KILLTIMER.md "wikilink"
  [0BA CROSSMUSIC]: FF8/Field/Script/Opcodes/0BA%20CROSSMUSIC.md "wikilink"
  [0BB DUALMUSIC]: FF8/Field/Script/Opcodes/0BB%20DUALMUSIC.md "wikilink"
  [0BC EFFECTPLAY]: FF8/Field/Script/Opcodes/0BC%20EFFECTPLAY.md "wikilink"
  [0BD EFFECTLOAD]: FF8/Field/Script/Opcodes/0BD%20EFFECTLOAD.md "wikilink"
  [0BE LOADSYNC]: FF8/Field/Script/Opcodes/0BE%20LOADSYNC.md "wikilink"
  [0BF MUSICSTOP]: FF8/Field/Script/Opcodes/0BF%20MUSICSTOP.md "wikilink"
  [0C0 MUSICVOL]: FF8/Field/Script/Opcodes/0C0%20MUSICVOL.md "wikilink"
  [0C1 MUSICVOLTRANS]: FF8/Field/Script/Opcodes/0C1%20MUSICVOLTRANS.md
    "wikilink"
  [0C2 MUSICVOLFADE]: FF8/Field/Script/Opcodes/0C2%20MUSICVOLFADE.md
    "wikilink"
  [0C3 ALLSEVOL]: FF8/Field/Script/Opcodes/0C3%20ALLSEVOL.md "wikilink"
  [0C4 ALLSEVOLTRANS]: FF8/Field/Script/Opcodes/0C4%20ALLSEVOLTRANS.md
    "wikilink"
  [0C5 ALLSEPOS]: FF8/Field/Script/Opcodes/0C5%20ALLSEPOS.md "wikilink"
  [0C6 ALLSEPOSTRANS]: FF8/Field/Script/Opcodes/0C6%20ALLSEPOSTRANS.md
    "wikilink"
  [0C7 SEVOL]: FF8/Field/Script/Opcodes/0C7%20SEVOL.md "wikilink"
  [0C8 SEVOLTRANS]: FF8/Field/Script/Opcodes/0C8%20SEVOLTRANS.md "wikilink"
  [0C9 SEPOS]: FF8/Field/Script/Opcodes/0C9%20SEPOS.md "wikilink"
  [0CA SEPOSTRANS]: FF8/Field/Script/Opcodes/0CA%20SEPOSTRANS.md "wikilink"
  [0CB SETBATTLEMUSIC]: FF8/Field/Script/Opcodes/0CB%20SETBATTLEMUSIC.md
    "wikilink"
  [0CC BATTLEMODE]: FF8/Field/Script/Opcodes/0CC%20BATTLEMODE.md "wikilink"
  [0CD SESTOP]: FF8/Field/Script/Opcodes/0CD%20SESTOP.md "wikilink"
  [0CE BGANIMEFLAG]: FF8/Field/Script/Opcodes/0CE%20BGANIMEFLAG.md "wikilink"
  [0CF INITSOUND]: FF8/Field/Script/Opcodes/0CF%20INITSOUND.md "wikilink"
  [0D0 BGSHADE]: FF8/Field/Script/Opcodes/0D0%20BGSHADE.md "wikilink"
  [0D1 BGSHADESTOP]: FF8/Field/Script/Opcodes/0D1%20BGSHADESTOP.md "wikilink"
  [0D2 RBGSHADELOOP]: FF8/Field/Script/Opcodes/0D2%20RBGSHADELOOP.md
    "wikilink"
  [0D3 DSCROLL2]: FF8/Field/Script/Opcodes/0D3%20DSCROLL2.md "wikilink"
  [0D4 LSCROLL2]: FF8/Field/Script/Opcodes/0D4%20LSCROLL2.md "wikilink"
  [0D5 CSCROLL2]: FF8/Field/Script/Opcodes/0D5%20CSCROLL2.md "wikilink"
  [0D6 DSCROLLA2]: FF8/Field/Script/Opcodes/0D6%20DSCROLLA2.md "wikilink"
  [0D7 LSCROLLA2]: FF8/Field/Script/Opcodes/0D7%20LSCROLLA2.md "wikilink"
  [0D8 CSCROLLA2]: FF8/Field/Script/Opcodes/0D8%20CSCROLLA2.md "wikilink"
  [0D9 DSCROLLP2]: FF8/Field/Script/Opcodes/0D9%20DSCROLLP2.md "wikilink"
  [0DA LSCROLLP2]: FF8/Field/Script/Opcodes/0DA%20LSCROLLP2.md "wikilink"
  [0DB CSCROLLP2]: FF8/Field/Script/Opcodes/0DB%20CSCROLLP2.md "wikilink"
  [0DC SCROLLSYNC2]: FF8/Field/Script/Opcodes/0DC%20SCROLLSYNC2.md "wikilink"
  [0DD SCROLLMODE2]: FF8/Field/Script/Opcodes/0DD%20SCROLLMODE2.md "wikilink"
  [0DE MENUENABLE]: FF8/Field/Script/Opcodes/0DE%20MENUENABLE.md "wikilink"
  [0DF MENUDISABLE]: FF8/Field/Script/Opcodes/0DF%20MENUDISABLE.md "wikilink"
  [0E0 FOOTSTEPON]: FF8/Field/Script/Opcodes/0E0%20FOOTSTEPON.md "wikilink"
  [0E1 FOOTSTEPOFF]: FF8/Field/Script/Opcodes/0E1%20FOOTSTEPOFF.md "wikilink"
  [0E2 FOOTSTEPOFFALL]: FF8/Field/Script/Opcodes/0E2%20FOOTSTEPOFFALL.md
    "wikilink"
  [0E3 FOOTSTEPCUT]: FF8/Field/Script/Opcodes/0E3%20FOOTSTEPCUT.md "wikilink"
  [0E4 PREMAPJUMP]: FF8/Field/Script/Opcodes/0E4%20PREMAPJUMP.md "wikilink"
  [0E5 USE]: FF8/Field/Script/Opcodes/0E5%20USE.md "wikilink"
  [0E6 SPLIT]: FF8/Field/Script/Opcodes/0E6%20SPLIT.md "wikilink"
  [0E7 ANIMESPEED]: FF8/Field/Script/Opcodes/0E7%20ANIMESPEED.md "wikilink"
  [0E8 RND]: FF8/Field/Script/Opcodes/0E8%20RND.md "wikilink"
  [0E9 DCOLADD]: FF8/Field/Script/Opcodes/0E9%20DCOLADD.md "wikilink"
  [0EA DCOLSUB]: FF8/Field/Script/Opcodes/0EA%20DCOLSUB.md "wikilink"
  [0EB TCOLADD]: FF8/Field/Script/Opcodes/0EB%20TCOLADD.md "wikilink"
  [0EC TCOLSUB]: FF8/Field/Script/Opcodes/0EC%20TCOLSUB.md "wikilink"
  [0ED FCOLADD]: FF8/Field/Script/Opcodes/0ED%20FCOLADD.md "wikilink"
  [0EE FCOLSUB]: FF8/Field/Script/Opcodes/0EE%20FCOLSUB.md "wikilink"
  [0EF COLSYNC]: FF8/Field/Script/Opcodes/0EF%20COLSYNC.md "wikilink"
  [0F0 DOFFSET]: FF8/Field/Script/Opcodes/0F0%20DOFFSET.md "wikilink"
  [0F1 LOFFSETS]: FF8/Field/Script/Opcodes/0F1%20LOFFSETS.md "wikilink"
  [0F2 COFFSETS]: FF8/Field/Script/Opcodes/0F2%20COFFSETS.md "wikilink"
  [0F3 LOFFSET]: FF8/Field/Script/Opcodes/0F3%20LOFFSET.md "wikilink"
  [0F4 COFFSET]: FF8/Field/Script/Opcodes/0F4%20COFFSET.md "wikilink"
  [0F5 OFFSETSYNC]: FF8/Field/Script/Opcodes/0F5%20OFFSETSYNC.md "wikilink"
  [0F6 RUNENABLE]: FF8/Field/Script/Opcodes/0F6%20RUNENABLE.md "wikilink"
  [0F7 RUNDISABLE]: FF8/Field/Script/Opcodes/0F7%20RUNDISABLE.md "wikilink"
  [0F8 MAPFADEOFF]: FF8/Field/Script/Opcodes/0F8%20MAPFADEOFF.md "wikilink"
  [0F9 MAPFADEON]: FF8/Field/Script/Opcodes/0F9%20MAPFADEON.md "wikilink"
  [0FA INITTRACE]: FF8/Field/Script/Opcodes/0FA%20INITTRACE.md "wikilink"
  [0FB SETDRESS]: FF8/Field/Script/Opcodes/0FB%20SETDRESS.md "wikilink"
  [0FC GETDRESS]: FF8/Field/Script/Opcodes/0FC%20GETDRESS.md "wikilink"
  [0FD FACEDIR]: FF8/Field/Script/Opcodes/0FD%20FACEDIR.md "wikilink"
  [0FE FACEDIRA]: FF8/Field/Script/Opcodes/0FE%20FACEDIRA.md "wikilink"
  [0FF FACEDIRP]: FF8/Field/Script/Opcodes/0FF%20FACEDIRP.md "wikilink"
  [100 FACEDIRLIMIT]: FF8/Field/Script/Opcodes/100%20FACEDIRLIMIT.md
    "wikilink"
  [101 FACEDIROFF]: FF8/Field/Script/Opcodes/101%20FACEDIROFF.md "wikilink"
  [102 SARALYOFF]: FF8/Field/Script/Opcodes/102%20SARALYOFF.md "wikilink"
  [103 SARALYON]: FF8/Field/Script/Opcodes/103%20SARALYON.md "wikilink"
  [104 SARALYDISPOFF]: FF8/Field/Script/Opcodes/104%20SARALYDISPOFF.md
    "wikilink"
  [105 SARALYDISPON]: FF8/Field/Script/Opcodes/105%20SARALYDISPON.md
    "wikilink"
  [106 MESMODE]: FF8/Field/Script/Opcodes/106%20MESMODE.md "wikilink"
  [107 FACEDIRINIT]: FF8/Field/Script/Opcodes/107%20FACEDIRINIT.md "wikilink"
  [108 FACEDIRI]: FF8/Field/Script/Opcodes/108%20FACEDIRI.md "wikilink"
  [109 JUNCTION]: FF8/Field/Script/Opcodes/109%20JUNCTION.md "wikilink"
  [10A SETCAMERA]: FF8/Field/Script/Opcodes/10A%20SETCAMERA.md "wikilink"
  [10B BATTLECUT]: FF8/Field/Script/Opcodes/10B%20BATTLECUT.md "wikilink"
  [10C FOOTSTEPCOPY]: FF8/Field/Script/Opcodes/10C%20FOOTSTEPCOPY.md
    "wikilink"
  [10D WORLDMAPJUMP]: FF8/Field/Script/Opcodes/10D%20WORLDMAPJUMP.md
    "wikilink"
  [10E RFACEDIRI]: FF8/Field/Script/Opcodes/10E%20RFACEDIRI.md "wikilink"
  [10F RFACEDIR]: FF8/Field/Script/Opcodes/10F%20RFACEDIR.md "wikilink"
  [110 RFACEDIRA]: FF8/Field/Script/Opcodes/110%20RFACEDIRA.md "wikilink"
  [111 RFACEDIRP]: FF8/Field/Script/Opcodes/111%20RFACEDIRP.md "wikilink"
  [112 RFACEDIROFF]: FF8/Field/Script/Opcodes/112%20RFACEDIROFF.md "wikilink"
  [113 FACEDIRSYNC]: FF8/Field/Script/Opcodes/113%20FACEDIRSYNC.md "wikilink"
  [114 COPYINFO]: FF8/Field/Script/Opcodes/114%20COPYINFO.md "wikilink"
  [115 PCOPYINFO]: FF8/Field/Script/Opcodes/115%20PCOPYINFO.md "wikilink"
  [116 RAMESW]: FF8/Field/Script/Opcodes/116%20RAMESW.md "wikilink"
  [117 BGSHADEOFF]: FF8/Field/Script/Opcodes/117%20BGSHADEOFF.md "wikilink"
  [118 AXIS]: FF8/Field/Script/Opcodes/118%20AXIS.md "wikilink"
  [119 AXISSYNC]: FF8/Field/Script/Opcodes/119%20AXISSYNC.md "wikilink"
  [11A MENUNORMAL]: FF8/Field/Script/Opcodes/11A%20MENUNORMAL.md "wikilink"
  [11B MENUPHS]: FF8/Field/Script/Opcodes/11B%20MENUPHS.md "wikilink"
  [11C BGCLEAR]: FF8/Field/Script/Opcodes/11C%20BGCLEAR.md "wikilink"
  [11D GETPARTY]: FF8/Field/Script/Opcodes/11D%20GETPARTY.md "wikilink"
  [11E MENUSHOP]: FF8/Field/Script/Opcodes/11E%20MENUSHOP.md "wikilink"
  [11F DISC]: FF8/Field/Script/Opcodes/11F%20DISC.md "wikilink"
  [120 DSCROLL3]: FF8/Field/Script/Opcodes/120%20DSCROLL3.md "wikilink"
  [121 LSCROLL3]: FF8/Field/Script/Opcodes/121%20LSCROLL3.md "wikilink"
  [122 CSCROLL3]: FF8/Field/Script/Opcodes/122%20CSCROLL3.md "wikilink"
  [123 MACCEL]: FF8/Field/Script/Opcodes/123%20MACCEL.md "wikilink"
  [124 MLIMIT]: FF8/Field/Script/Opcodes/124%20MLIMIT.md "wikilink"
  [125 ADDITEM]: FF8/Field/Script/Opcodes/125%20ADDITEM.md "wikilink"
  [126 SETWITCH]: FF8/Field/Script/Opcodes/126%20SETWITCH.md "wikilink"
  [127 SETODIN]: FF8/Field/Script/Opcodes/127%20SETODIN.md "wikilink"
  [128 RESETGF]: FF8/Field/Script/Opcodes/128%20RESETGF.md "wikilink"
  [129 MENUNAME]: FF8/Field/Script/Opcodes/129%20MENUNAME.md "wikilink"
  [12A REST]: FF8/Field/Script/Opcodes/12A%20REST.md "wikilink"
  [12B MOVECANCEL]: FF8/Field/Script/Opcodes/12B%20MOVECANCEL.md "wikilink"
  [12C PMOVECANCEL]: FF8/Field/Script/Opcodes/12C%20PMOVECANCEL.md "wikilink"
  [12D ACTORMODE]: FF8/Field/Script/Opcodes/12D%20ACTORMODE.md "wikilink"
  [12E MENUSAVE]: FF8/Field/Script/Opcodes/12E%20MENUSAVE.md "wikilink"
  [12F SAVEENABLE]: FF8/Field/Script/Opcodes/12F%20SAVEENABLE.md "wikilink"
  [130 PHSENABLE]: FF8/Field/Script/Opcodes/130%20PHSENABLE.md "wikilink"
  [131 HOLD]: FF8/Field/Script/Opcodes/131%20HOLD.md "wikilink"
  [132 MOVIECUT]: FF8/Field/Script/Opcodes/132%20MOVIECUT.md "wikilink"
  [133 SETPLACE]: FF8/Field/Script/Opcodes/133%20SETPLACE.md "wikilink"
  [134 SETDCAMERA]: FF8/Field/Script/Opcodes/134%20SETDCAMERA.md "wikilink"
  [135 CHOICEMUSIC]: FF8/Field/Script/Opcodes/135%20CHOICEMUSIC.md "wikilink"
  [136 GETCARD]: FF8/Field/Script/Opcodes/136%20GETCARD.md "wikilink"
  [137 DRAWPOINT]: FF8/Field/Script/Opcodes/137%20DRAWPOINT.md "wikilink"
  [138 PHSPOWER]: FF8/Field/Script/Opcodes/138%20PHSPOWER.md "wikilink"
  [139 KEY]: FF8/Field/Script/Opcodes/139%20KEY.md "wikilink"
  [13A CARDGAME]: FF8/Field/Script/Opcodes/13A%20CARDGAME.md "wikilink"
  [13B SETBAR]: FF8/Field/Script/Opcodes/13B%20SETBAR.md "wikilink"
  [13C DISPBAR]: FF8/Field/Script/Opcodes/13C%20DISPBAR.md "wikilink"
  [13D KILLBAR]: FF8/Field/Script/Opcodes/13D%20KILLBAR.md "wikilink"
  [13E SCROLLRATIO2]: FF8/Field/Script/Opcodes/13E%20SCROLLRATIO2.md
    "wikilink"
  [13F WHOAMI]: FF8/Field/Script/Opcodes/13F%20WHOAMI.md "wikilink"
  [140 MUSICSTATUS]: FF8/Field/Script/Opcodes/140%20MUSICSTATUS.md "wikilink"
  [141 MUSICREPLAY]: FF8/Field/Script/Opcodes/141%20MUSICREPLAY.md "wikilink"
  [142 DOORLINEOFF]: FF8/Field/Script/Opcodes/142%20DOORLINEOFF.md "wikilink"
  [143 DOORLINEON]: FF8/Field/Script/Opcodes/143%20DOORLINEON.md "wikilink"
  [144 MUSICSKIP]: FF8/Field/Script/Opcodes/144%20MUSICSKIP.md "wikilink"
  [145 DYING]: FF8/Field/Script/Opcodes/145%20DYING.md "wikilink"
  [146 SETHP]: FF8/Field/Script/Opcodes/146%20SETHP.md "wikilink"
  [147 GETHP]: FF8/Field/Script/Opcodes/147%20GETHP.md "wikilink"
  [148 MOVEFLUSH]: FF8/Field/Script/Opcodes/148%20MOVEFLUSH.md "wikilink"
  [149 MUSICVOLSYNC]: FF8/Field/Script/Opcodes/149%20MUSICVOLSYNC.md
    "wikilink"
  [14A PUSHANIME]: FF8/Field/Script/Opcodes/14A%20PUSHANIME.md "wikilink"
  [14B POPANIME]: FF8/Field/Script/Opcodes/14B%20POPANIME.md "wikilink"
  [14C KEYSCAN2]: FF8/Field/Script/Opcodes/14C%20KEYSCAN2.md "wikilink"
  [14D KEYON2]: FF8/Field/Script/Opcodes/14D%20KEYON2.md "wikilink"
  [14E PARTICLEON]: FF8/Field/Script/Opcodes/14E%20PARTICLEON.md "wikilink"
  [14F PARTICLEOFF]: FF8/Field/Script/Opcodes/14F%20PARTICLEOFF.md "wikilink"
  [150 KEYSIGHNCHANGE]: FF8/Field/Script/Opcodes/150%20KEYSIGHNCHANGE.md
    "wikilink"
  [151 ADDGIL]: FF8/Field/Script/Opcodes/151%20ADDGIL.md "wikilink"
  [152 ADDPASTGIL]: FF8/Field/Script/Opcodes/152%20ADDPASTGIL.md "wikilink"
  [153 ADDSEEDLEVEL]: FF8/Field/Script/Opcodes/153%20ADDSEEDLEVEL.md
    "wikilink"
  [154 PARTICLESET]: FF8/Field/Script/Opcodes/154%20PARTICLESET.md "wikilink"
  [155 SETDRAWPOINT]: FF8/Field/Script/Opcodes/155%20SETDRAWPOINT.md
    "wikilink"
  [156 MENUTIPS]: FF8/Field/Script/Opcodes/156%20MENUTIPS.md "wikilink"
  [157 LASTIN]: FF8/Field/Script/Opcodes/157%20LASTIN.md "wikilink"
  [158 LASTOUT]: FF8/Field/Script/Opcodes/158%20LASTOUT.md "wikilink"
  [159 SEALEDOFF]: FF8/Field/Script/Opcodes/159%20SEALEDOFF.md "wikilink"
  [15A MENUTUTO]: FF8/Field/Script/Opcodes/15A%20MENUTUTO.md "wikilink"
  [15B OPENEYES]: FF8/Field/Script/Opcodes/15B%20OPENEYES.md "wikilink"
  [15C CLOSEEYES]: FF8/Field/Script/Opcodes/15C%20CLOSEEYES.md "wikilink"
  [15D BLINKEYES]: FF8/Field/Script/Opcodes/15D%20BLINKEYES.md "wikilink"
  [15E SETCARD]: FF8/Field/Script/Opcodes/15E%20SETCARD.md "wikilink"
  [15F HOWMANYCARD]: FF8/Field/Script/Opcodes/15F%20HOWMANYCARD.md "wikilink"
  [160 WHERECARD]: FF8/Field/Script/Opcodes/160%20WHERECARD.md "wikilink"
  [161 ADDMAGIC]: FF8/Field/Script/Opcodes/161%20ADDMAGIC.md "wikilink"
  [162 SWAP]: FF8/Field/Script/Opcodes/162%20SWAP.md "wikilink"
  [163 SETPARTY2]: FF8/Field/Script/Opcodes/163%20SETPARTY2.md "wikilink"
  [164 SPUSYNC]: FF8/Field/Script/Opcodes/164%20SPUSYNC.md "wikilink"
  [165 BROKEN]: FF8/Field/Script/Opcodes/165%20BROKEN.md "wikilink"
  [166 UNKNOWN1]: FF8/Field/Script/Opcodes/166%20UNKNOWN1.md "wikilink"
  [167 UNKNOWN2]: FF8/Field/Script/Opcodes/167%20UNKNOWN2.md "wikilink"
  [168 UNKNOWN3]: FF8/Field/Script/Opcodes/168%20UNKNOWN3.md "wikilink"
  [169 UNKNOWN4]: FF8/Field/Script/Opcodes/169%20UNKNOWN4.md "wikilink"
  [170 UNKNOWN5]: FF8/Field/Script/Opcodes/170%20UNKNOWN5.md "wikilink"
  [171 UNKNOWN6]: FF8/Field/Script/Opcodes/171%20UNKNOWN6.md "wikilink"
  [172 UNKNOWN7]: FF8/Field/Script/Opcodes/172%20UNKNOWN7.md "wikilink"
  [173 UNKNOWN8]: FF8/Field/Script/Opcodes/173%20UNKNOWN8.md "wikilink"
  [174 UNKNOWN9]: FF8/Field/Script/Opcodes/174%20UNKNOWN9.md "wikilink"
  [175 UNKNOWN10]: FF8/Field/Script/Opcodes/175%20UNKNOWN10.md "wikilink"
  [176 UNKNOWN11]: FF8/Field/Script/Opcodes/176%20UNKNOWN11.md "wikilink"
  [177 UNKNOWN12]: FF8/Field/Script/Opcodes/177%20UNKNOWN12.md "wikilink"
  [178 UNKNOWN13]: FF8/Field/Script/Opcodes/178%20UNKNOWN13.md "wikilink"
  [179 UNKNOWN14]: FF8/Field/Script/Opcodes/179%20UNKNOWN14.md "wikilink"
  [180 UNKNOWN15]: FF8/Field/Script/Opcodes/180%20UNKNOWN15.md "wikilink"
  [181 UNKNOWN16]: FF8/Field/Script/Opcodes/181%20UNKNOWN16.md "wikilink"
  [182 UNKNOWN17]: FF8/Field/Script/Opcodes/182%20UNKNOWN17.md "wikilink"
  [183 UNKNOWN18]: FF8/Field/Script/Opcodes/183%20UNKNOWN18.md "wikilink"
