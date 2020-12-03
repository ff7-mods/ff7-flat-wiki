---
title: Opcodes
---

[Home](../../../Main Page.md) > [FF8](../../../FF8.md) > [Field](../../Field.md) > [Script](../Script.md) > Opcodes

By Aali, myst6re and Shard.

## The language

The field script language in ff8 is a simple assembly language with a stack. Here is an example:

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

Each Opcode's page lists all the parameters for that function in the order you would put them on the stack before the function call. The inline argument is listed separately, if the function requires one. For example, on the page for [SET3](Opcodes/01E SET3.md), the parameters are listed like this:

  
*XCoord*

*YCoord*

*ZCoord*

**SET3**

Which means when you call **SET3**, the ZCoord is the top item on the stack, YCoord is under it, and XCoord is under that, for example

`PSHN_L      402   (XCoord)`  
`PSHN_L      -381  (YCoord)`  
`PSHN_L      20    (ZCoord)`  
`SET3        17    (walkmesh triangle ID)`

## Opcode list

| Opcode | Name                                                                              | Function Type      |
|--------|-----------------------------------------------------------------------------------|--------------------|
| 000    | [000 NOP](Opcodes/000 NOP.md)*                 | Script Processing  |
| 001    | [001 CAL](Opcodes/001 CAL.md)                            | Script Processing  |
| 002    | [002 JMP](Opcodes/002 JMP.md)                            | Script Processing  |
| 003    | [003 JPF](Opcodes/003 JPF.md)                            | Script Processing  |
| 004    | [004 GJMP](Opcodes/004 GJMP.md)*               | Script Processing  |
| 005    | [005 LBL](Opcodes/005 LBL.md)                            | Script Processing  |
| 006    | [006 RET](Opcodes/006 RET.md)                            | Script Processing  |
| 007    | [007 PSHN\_L](Opcodes/007 PSHN L.md)                     | Memory             |
| 008    | [008 PSHI\_L](Opcodes/008 PSHI L.md)                     | Memory             |
| 009    | [009 POPI\_L](Opcodes/009 POPI L.md)                     | Memory             |
| 00A    | [00A PSHM\_B](Opcodes/00A PSHM B.md)                     | Memory             |
| 00B    | [00B POPM\_B](Opcodes/00B POPM B.md)                     | Memory             |
| 00C    | [00C PSHM\_W](Opcodes/00C PSHM W.md)                     | Memory             |
| 00D    | [00D POPM\_W](Opcodes/00D POPM W.md)                     | Memory             |
| 00E    | [00E PSHM\_L](Opcodes/00E PSHM L.md)                     | Memory             |
| 00F    | [00F POPM\_L](Opcodes/00F POPM L.md)                     | Memory             |
| 010    | [010 PSHSM\_B](Opcodes/010 PSHSM B.md)                   | Memory             |
| 011    | [011 PSHSM\_W](Opcodes/011 PSHSM W.md)                   | Memory             |
| 012    | [012 PSHSM\_L](Opcodes/012 PSHSM L.md)                   | Memory             |
| 013    | [013 PSHAC](Opcodes/013 PSHAC.md)                        | Memory             |
| 014    | [014 REQ](Opcodes/014 REQ.md)                            | Script Processing  |
| 015    | [015 REQSW](Opcodes/015 REQSW.md)                        | Script Processing  |
| 016    | [016 REQEW](Opcodes/016 REQEW.md)                        | Script Processing  |
| 017    | [017 PREQ](Opcodes/017 PREQ.md)                          | Script Processing  |
| 018    | [018 PREQSW](Opcodes/018 PREQSW.md)                      | Script Processing  |
| 019    | [019 PREQEW](Opcodes/019 PREQEW.md)                      | Script Processing  |
| 01A    | [01A UNUSE](Opcodes/01A UNUSE.md)                        | Entity             |
| 01B    | [01B DEBUG](Opcodes/01B DEBUG.md)*             |                    |
| 01C    | [01C HALT](Opcodes/01C HALT.md)                          | Script Processing  |
| 01D    | [01D SET](Opcodes/01D SET.md)                            | Entity             |
| 01E    | [01E SET3](Opcodes/01E SET3.md)                          | Entity             |
| 01F    | [01F IDLOCK](Opcodes/01F IDLOCK.md)                      | Field related      |
| 020    | [020 IDUNLOCK](Opcodes/020 IDUNLOCK.md)                  | Field related      |
| 021    | [021 EFFECTPLAY2](Opcodes/021 EFFECTPLAY2.md)            | Music and Sound    |
| 022    | [022 FOOTSTEP](Opcodes/022 FOOTSTEP.md)                  |                    |
| 023    | [023 JUMP](Opcodes/023 JUMP.md)                          | Entity             |
| 024    | [024 JUMP3](Opcodes/024 JUMP3.md)                        | Entity             |
| 025    | [025 LADDERUP](Opcodes/025 LADDERUP.md)                  | Entity             |
| 026    | [026 LADDERDOWN](Opcodes/026 LADDERDOWN.md)              | Entity             |
| 027    | [027 LADDERUP2](Opcodes/027 LADDERUP2.md)                | Entity             |
| 028    | [028 LADDERDOWN2](Opcodes/028 LADDERDOWN2.md)            | Entity             |
| 029    | [029 MAPJUMP](Opcodes/029 MAPJUMP.md)                    | Field related      |
| 02A    | [02A MAPJUMP3](Opcodes/02A MAPJUMP3.md)                  | Field related      |
| 02B    | [02B SETMODEL](Opcodes/02B SETMODEL.md)                  | Entity             |
| 02C    | [02C BASEANIME](Opcodes/02C BASEANIME.md)                | Animation          |
| 02D    | [02D ANIME](Opcodes/02D ANIME.md)                        | Animation          |
| 02E    | [02E ANIMEKEEP](Opcodes/02E ANIMEKEEP.md)                | Animation          |
| 02F    | [02F CANIME](Opcodes/02F CANIME.md)                      | Animation          |
| 030    | [030 CANIMEKEEP](Opcodes/030 CANIMEKEEP.md)              | Animation          |
| 031    | [031 RANIME](Opcodes/031 RANIME.md)                      | Animation          |
| 032    | [032 RANIMEKEEP](Opcodes/032 RANIMEKEEP.md)              | Animation          |
| 033    | [033 RCANIME](Opcodes/033 RCANIME.md)                    | Animation          |
| 034    | [034 RCANIMEKEEP](Opcodes/034 RCANIMEKEEP.md)            | Animation          |
| 035    | [035 RANIMELOOP](Opcodes/035 RANIMELOOP.md)              | Animation          |
| 036    | [036 RCANIMELOOP](Opcodes/036 RCANIMELOOP.md)            | Animation          |
| 037    | [037 LADDERANIME](Opcodes/037 LADDERANIME.md)            | Animation          |
| 038    | [038 DISCJUMP](Opcodes/038 DISCJUMP.md)                  | Field related      |
| 039    | [039 SETLINE](Opcodes/039 SETLINE.md)                    | Entity             |
| 03A    | [03A LINEON](Opcodes/03A LINEON.md)                      | Entity             |
| 03B    | [03B LINEOFF](Opcodes/03B LINEOFF.md)                    | Entity             |
| 03C    | [03C WAIT](Opcodes/03C WAIT.md)                          | Script Processing  |
| 03D    | [03D MSPEED](Opcodes/03D MSPEED.md)                      |                    |
| 03E    | [03E MOVE](Opcodes/03E MOVE.md)                          | Entity             |
| 03F    | [03F MOVEA](Opcodes/03F MOVEA.md)                        |                    |
| 040    | [040 PMOVEA](Opcodes/040 PMOVEA.md)                      |                    |
| 041    | [041 CMOVE](Opcodes/041 CMOVE.md)                        |                    |
| 042    | [042 FMOVE](Opcodes/042 FMOVE.md)                        |                    |
| 043    | [043 PJUMPA](Opcodes/043 PJUMPA.md)                      |                    |
| 044    | [044 ANIMESYNC](Opcodes/044 ANIMESYNC.md)                | Script Processing  |
| 045    | [045 ANIMESTOP](Opcodes/045 ANIMESTOP.md)                | Animation          |
| 046    | [046 MESW](Opcodes/046 MESW.md)*               |                    |
| 047    | [047 MES](Opcodes/047 MES.md)                            | Message            |
| 048    | [048 MESSYNC](Opcodes/048 MESSYNC.md)                    | Script Processing  |
| 049    | [049 MESVAR](Opcodes/049 MESVAR.md)                      | Message            |
| 04A    | [04A ASK](Opcodes/04A ASK.md)                            | Message            |
| 04B    | [04B WINSIZE](Opcodes/04B WINSIZE.md)                    | Message            |
| 04C    | [04C WINCLOSE](Opcodes/04C WINCLOSE.md)                  | Message            |
| 04D    | [04D UCON](Opcodes/04D UCON.md)                          | Misc               |
| 04E    | [04E UCOFF](Opcodes/04E UCOFF.md)                        | Misc               |
| 04F    | [04F MOVIE](Opcodes/04F MOVIE.md)                        | Movie              |
| 050    | [050 MOVIESYNC](Opcodes/050 MOVIESYNC.md)                | Script Processing  |
| 051    | [051 SETPC](Opcodes/051 SETPC.md)                        | Party management   |
| 052    | [052 DIR](Opcodes/052 DIR.md)                            | Entity             |
| 053    | [053 DIRP](Opcodes/053 DIRP.md)                          |                    |
| 054    | [054 DIRA](Opcodes/054 DIRA.md)                          |                    |
| 055    | [055 PDIRA](Opcodes/055 PDIRA.md)                        |                    |
| 056    | [056 SPUREADY](Opcodes/056 SPUREADY.md)                  | Timer              |
| 057    | [057 TALKON](Opcodes/057 TALKON.md)                      | Entity             |
| 058    | [058 TALKOFF](Opcodes/058 TALKOFF.md)                    | Entity             |
| 059    | [059 PUSHON](Opcodes/059 PUSHON.md)                      | Entity             |
| 05A    | [05A PUSHOFF](Opcodes/05A PUSHOFF.md)                    | Entity             |
| 05B    | [05B ISTOUCH](Opcodes/05B ISTOUCH.md)                    |                    |
| 05C    | [05C MAPJUMPO](Opcodes/05C MAPJUMPO.md)                  | Field related      |
| 05D    | [05D MAPJUMPON](Opcodes/05D MAPJUMPON.md)                | Field related      |
| 05E    | [05E MAPJUMPOFF](Opcodes/05E MAPJUMPOFF.md)              | Field related      |
| 05F    | [05F SETMESSPEED](Opcodes/05F SETMESSPEED.md)            | Message            |
| 060    | [060 SHOW](Opcodes/060 SHOW.md)                          | Entity             |
| 061    | [061 HIDE](Opcodes/061 HIDE.md)                          | Entity             |
| 062    | [062 TALKRADIUS](Opcodes/062 TALKRADIUS.md)              | Entity             |
| 063    | [063 PUSHRADIUS](Opcodes/063 PUSHRADIUS.md)              | Entity             |
| 064    | [064 AMESW](Opcodes/064 AMESW.md)                        | Message            |
| 065    | [065 AMES](Opcodes/065 AMES.md)                          | Message            |
| 066    | [066 GETINFO](Opcodes/066 GETINFO.md)                    |                    |
| 067    | [067 THROUGHON](Opcodes/067 THROUGHON.md)                | Entity             |
| 068    | [068 THROUGHOFF](Opcodes/068 THROUGHOFF.md)              | Entity             |
| 069    | [069 BATTLE](Opcodes/069 BATTLE.md)                      | Battle             |
| 06A    | [06A BATTLERESULT](Opcodes/06A BATTLERESULT.md)          | Battle             |
| 06B    | [06B BATTLEON](Opcodes/06B BATTLEON.md)                  | Field related      |
| 06C    | [06C BATTLEOFF](Opcodes/06C BATTLEOFF.md)                | Field related      |
| 06D    | [06D KEYSCAN](Opcodes/06D KEYSCAN.md)                    | Input              |
| 06E    | [06E KEYON](Opcodes/06E KEYON.md)                        | Input              |
| 06F    | [06F AASK](Opcodes/06F AASK.md)                          | Message            |
| 070    | [070 PGETINFO](Opcodes/070 PGETINFO.md)                  |                    |
| 071    | [071 DSCROLL](Opcodes/071 DSCROLL.md)                    |                    |
| 072    | [072 LSCROLL](Opcodes/072 LSCROLL.md)                    |                    |
| 073    | [073 CSCROLL](Opcodes/073 CSCROLL.md)                    |                    |
| 074    | [074 DSCROLLA](Opcodes/074 DSCROLLA.md)                  |                    |
| 075    | [075 LSCROLLA](Opcodes/075 LSCROLLA.md)                  |                    |
| 076    | [076 CSCROLLA](Opcodes/076 CSCROLLA.md)                  |                    |
| 077    | [077 SCROLLSYNC](Opcodes/077 SCROLLSYNC.md)              | Script Processing  |
| 078    | [078 RMOVE](Opcodes/078 RMOVE.md)                        |                    |
| 079    | [079 RMOVEA](Opcodes/079 RMOVEA.md)                      |                    |
| 07A    | [07A RPMOVEA](Opcodes/07A RPMOVEA.md)                    |                    |
| 07B    | [07B RCMOVE](Opcodes/07B RCMOVE.md)                      |                    |
| 07C    | [07C RFMOVE](Opcodes/07C RFMOVE.md)                      |                    |
| 07D    | [07D MOVESYNC](Opcodes/07D MOVESYNC.md)                  | Script Processing  |
| 07E    | [07E CLEAR](Opcodes/07E CLEAR.md)                        | Field related      |
| 07F    | [07F DSCROLLP](Opcodes/07F DSCROLLP.md)                  |                    |
| 080    | [080 LSCROLLP](Opcodes/080 LSCROLLP.md)                  |                    |
| 081    | [081 CSCROLLP](Opcodes/081 CSCROLLP.md)                  |                    |
| 082    | [082 LTURNR](Opcodes/082 LTURNR.md)                      |                    |
| 083    | [083 LTURNL](Opcodes/083 LTURNL.md)                      |                    |
| 084    | [084 CTURNR](Opcodes/084 CTURNR.md)                      |                    |
| 085    | [085 CTURNL](Opcodes/085 CTURNL.md)                      |                    |
| 086    | [086 ADDPARTY](Opcodes/086 ADDPARTY.md)                  | Party Management   |
| 087    | [087 SUBPARTY](Opcodes/087 SUBPARTY.md)                  | Party Management   |
| 088    | [088 CHANGEPARTY](Opcodes/088 CHANGEPARTY.md)            | Party Management   |
| 089    | [089 REFRESHPARTY](Opcodes/089 REFRESHPARTY.md)          | Party Management   |
| 08A    | [08A SETPARTY](Opcodes/08A SETPARTY.md)                  | Party Management   |
| 08B    | [08B ISPARTY](Opcodes/08B ISPARTY.md)                    | Party Management   |
| 08C    | [08C ADDMEMBER](Opcodes/08C ADDMEMBER.md)                | Party Management   |
| 08D    | [08D SUBMEMBER](Opcodes/08D SUBMEMBER.md)                | Party Management   |
| 08E    | [08E ISMEMBER](Opcodes/08E ISMEMBER.md)*       | Party Management   |
| 08F    | [08F LTURN](Opcodes/08F LTURN.md)                        |                    |
| 090    | [090 CTURN](Opcodes/090 CTURN.md)                        |                    |
| 091    | [091 PLTURN](Opcodes/091 PLTURN.md)                      |                    |
| 092    | [092 PCTURN](Opcodes/092 PCTURN.md)                      |                    |
| 093    | [093 JOIN](Opcodes/093 JOIN.md)                          | Entity             |
| 094    | [094 MESFORCUS](Opcodes/094 MESFORCUS.md)*     |                    |
| 095    | [095 BGANIME](Opcodes/095 BGANIME.md)                    | Field related      |
| 096    | [096 RBGANIME](Opcodes/096 RBGANIME.md)                  | Field related      |
| 097    | [097 RBGANIMELOOP](Opcodes/097 RBGANIMELOOP.md)          | Field related      |
| 098    | [098 BGANIMESYNC](Opcodes/098 BGANIMESYNC.md)            | Field related      |
| 099    | [099 BGDRAW](Opcodes/099 BGDRAW.md)                      | Field related      |
| 09A    | [09A BGOFF](Opcodes/09A BGOFF.md)                        | Field related      |
| 09B    | [09B BGANIMESPEED](Opcodes/09B BGANIMESPEED.md)          | Field related      |
| 09C    | [09C SETTIMER](Opcodes/09C SETTIMER.md)                  | Timer              |
| 09D    | [09D DISPTIMER](Opcodes/09D DISPTIMER.md)                | Timer              |
| 09E    | [09E SHADETIMER](Opcodes/09E SHADETIMER.md)*   |                    |
| 09F    | [09F SETGETA](Opcodes/09F SETGETA.md)                    |                    |
| 0A0    | [0A0 SETROOTTRANS](Opcodes/0A0 SETROOTTRANS.md)          |                    |
| 0A1    | [0A1 SETVIBRATE](Opcodes/0A1 SETVIBRATE.md)              |                    |
| 0A2    | [0A2 STOPVIBRATE](Opcodes/0A2 STOPVIBRATE.md)* |                    |
| 0A3    | [0A3 MOVIEREADY](Opcodes/0A3 MOVIEREADY.md)              | Movie              |
| 0A4    | [0A4 GETTIMER](Opcodes/0A4 GETTIMER.md)                  | Timer              |
| 0A5    | [0A5 FADEIN](Opcodes/0A5 FADEIN.md)                      | Field related      |
| 0A6    | [0A6 FADEOUT](Opcodes/0A6 FADEOUT.md)                    | Field related      |
| 0A7    | [0A7 FADESYNC](Opcodes/0A7 FADESYNC.md)                  | Script Processing  |
| 0A8    | [0A8 SHAKE](Opcodes/0A8 SHAKE.md)                        | Field related      |
| 0A9    | [0A9 SHAKEOFF](Opcodes/0A9 SHAKEOFF.md)                  | Field related      |
| 0AA    | [0AA FADEBLACK](Opcodes/0AA FADEBLACK.md)                | Field related      |
| 0AB    | [0AB FOLLOWOFF](Opcodes/0AB FOLLOWOFF.md)                |                    |
| 0AC    | [0AC FOLLOWON](Opcodes/0AC FOLLOWON.md)                  |                    |
| 0AD    | [0AD GAMEOVER](Opcodes/0AD GAMEOVER.md)                  | Field related      |
| 0AE    | [0AE ENDING](Opcodes/0AE ENDING.md)*           |                    |
| 0AF    | [0AF SHADELEVEL](Opcodes/0AF SHADELEVEL.md)              |                    |
| 0B0    | [0B0 SHADEFORM](Opcodes/0B0 SHADEFORM.md)                |                    |
| 0B1    | [0B1 FMOVEA](Opcodes/0B1 FMOVEA.md)                      |                    |
| 0B2    | [0B2 FMOVEP](Opcodes/0B2 FMOVEP.md)                      |                    |
| 0B3    | [0B3 SHADESET](Opcodes/0B3 SHADESET.md)                  |                    |
| 0B4    | [0B4 MUSICCHANGE](Opcodes/0B4 MUSICCHANGE.md)            | Music and Sound    |
| 0B5    | [0B5 MUSICLOAD](Opcodes/0B5 MUSICLOAD.md)                | Music and Sound    |
| 0B6    | [0B6 FADENONE](Opcodes/0B6 FADENONE.md)                  |                    |
| 0B7    | [0B7 POLYCOLOR](Opcodes/0B7 POLYCOLOR.md)                |                    |
| 0B8    | [0B8 POLYCOLORALL](Opcodes/0B8 POLYCOLORALL.md)          |                    |
| 0B9    | [0B9 KILLTIMER](Opcodes/0B9 KILLTIMER.md)                | Timer              |
| 0BA    | [0BA CROSSMUSIC](Opcodes/0BA CROSSMUSIC.md)              |                    |
| 0BB    | [0BB DUALMUSIC](Opcodes/0BB DUALMUSIC.md)                |                    |
| 0BC    | [0BC EFFECTPLAY](Opcodes/0BC EFFECTPLAY.md)              | Music and Sound    |
| 0BD    | [0BD EFFECTLOAD](Opcodes/0BD EFFECTLOAD.md)              | Music and Sound    |
| 0BE    | [0BE LOADSYNC](Opcodes/0BE LOADSYNC.md)                  |                    |
| 0BF    | [0BF MUSICSTOP](Opcodes/0BF MUSICSTOP.md)                | Music and Sound    |
| 0C0    | [0C0 MUSICVOL](Opcodes/0C0 MUSICVOL.md)                  | Music and Sound    |
| 0C1    | [0C1 MUSICVOLTRANS](Opcodes/0C1 MUSICVOLTRANS.md)        | Music and Sound    |
| 0C2    | [0C2 MUSICVOLFADE](Opcodes/0C2 MUSICVOLFADE.md)          | Music and Sound    |
| 0C3    | [0C3 ALLSEVOL](Opcodes/0C3 ALLSEVOL.md)                  | Music and Sound    |
| 0C4    | [0C4 ALLSEVOLTRANS](Opcodes/0C4 ALLSEVOLTRANS.md)        | Music and Sound    |
| 0C5    | [0C5 ALLSEPOS](Opcodes/0C5 ALLSEPOS.md)*       | Music and Sound    |
| 0C6    | [0C6 ALLSEPOSTRANS](Opcodes/0C6 ALLSEPOSTRANS.md)        | Music and Sound    |
| 0C7    | [0C7 SEVOL](Opcodes/0C7 SEVOL.md)                        | Music and Sound    |
| 0C8    | [0C8 SEVOLTRANS](Opcodes/0C8 SEVOLTRANS.md)              | Music and Sound    |
| 0C9    | [0C9 SEPOS](Opcodes/0C9 SEPOS.md)                        | Music and Sound    |
| 0CA    | [0CA SEPOSTRANS](Opcodes/0CA SEPOSTRANS.md)              | Music and Sound    |
| 0CB    | [0CB SETBATTLEMUSIC](Opcodes/0CB SETBATTLEMUSIC.md)      | Music and Sound    |
| 0CC    | [0CC BATTLEMODE](Opcodes/0CC BATTLEMODE.md)              | Battle             |
| 0CD    | [0CD SESTOP](Opcodes/0CD SESTOP.md)                      | Music and Sound    |
| 0CE    | [0CE BGANIMEFLAG](Opcodes/0CE BGANIMEFLAG.md)* |                    |
| 0CF    | [0CF INITSOUND](Opcodes/0CF INITSOUND.md)                |                    |
| 0D0    | [0D0 BGSHADE](Opcodes/0D0 BGSHADE.md)                    |                    |
| 0D1    | [0D1 BGSHADESTOP](Opcodes/0D1 BGSHADESTOP.md)            |                    |
| 0D2    | [0D2 RBGSHADELOOP](Opcodes/0D2 RBGSHADELOOP.md)          |                    |
| 0D3    | [0D3 DSCROLL2](Opcodes/0D3 DSCROLL2.md)                  |                    |
| 0D4    | [0D4 LSCROLL2](Opcodes/0D4 LSCROLL2.md)                  |                    |
| 0D5    | [0D5 CSCROLL2](Opcodes/0D5 CSCROLL2.md)                  |                    |
| 0D6    | [0D6 DSCROLLA2](Opcodes/0D6 DSCROLLA2.md)                |                    |
| 0D7    | [0D7 LSCROLLA2](Opcodes/0D7 LSCROLLA2.md)*     |                    |
| 0D8    | [0D8 CSCROLLA2](Opcodes/0D8 CSCROLLA2.md)                |                    |
| 0D9    | [0D9 DSCROLLP2](Opcodes/0D9 DSCROLLP2.md)*     |                    |
| 0DA    | [0DA LSCROLLP2](Opcodes/0DA LSCROLLP2.md)*     |                    |
| 0DB    | [0DB CSCROLLP2](Opcodes/0DB CSCROLLP2.md)*     |                    |
| 0DC    | [0DC SCROLLSYNC2](Opcodes/0DC SCROLLSYNC2.md)            |                    |
| 0DD    | [0DD SCROLLMODE2](Opcodes/0DD SCROLLMODE2.md)            |                    |
| 0DE    | [0DE MENUENABLE](Opcodes/0DE MENUENABLE.md)              | Menus              |
| 0DF    | [0DF MENUDISABLE](Opcodes/0DF MENUDISABLE.md)            | Menus              |
| 0E0    | [0E0 FOOTSTEPON](Opcodes/0E0 FOOTSTEPON.md)              |                    |
| 0E1    | [0E1 FOOTSTEPOFF](Opcodes/0E1 FOOTSTEPOFF.md)            |                    |
| 0E2    | [0E2 FOOTSTEPOFFALL](Opcodes/0E2 FOOTSTEPOFFALL.md)      |                    |
| 0E3    | [0E3 FOOTSTEPCUT](Opcodes/0E3 FOOTSTEPCUT.md)            |                    |
| 0E4    | [0E4 PREMAPJUMP](Opcodes/0E4 PREMAPJUMP.md)              |                    |
| 0E5    | [0E5 USE](Opcodes/0E5 USE.md)                            | Entity             |
| 0E6    | [0E6 SPLIT](Opcodes/0E6 SPLIT.md)                        | Entity             |
| 0E7    | [0E7 ANIMESPEED](Opcodes/0E7 ANIMESPEED.md)              | Animation          |
| 0E8    | [0E8 RND](Opcodes/0E8 RND.md)                            |                    |
| 0E9    | [0E9 DCOLADD](Opcodes/0E9 DCOLADD.md)                    |                    |
| 0EA    | [0EA DCOLSUB](Opcodes/0EA DCOLSUB.md)                    |                    |
| 0EB    | [0EB TCOLADD](Opcodes/0EB TCOLADD.md)                    |                    |
| 0EC    | [0EC TCOLSUB](Opcodes/0EC TCOLSUB.md)                    |                    |
| 0ED    | [0ED FCOLADD](Opcodes/0ED FCOLADD.md)                    | Field related      |
| 0EE    | [0EE FCOLSUB](Opcodes/0EE FCOLSUB.md)                    | Field related      |
| 0EF    | [0EF COLSYNC](Opcodes/0EF COLSYNC.md)                    | Script processing  |
| 0F0    | [0F0 DOFFSET](Opcodes/0F0 DOFFSET.md)                    |                    |
| 0F1    | [0F1 LOFFSETS](Opcodes/0F1 LOFFSETS.md)                  |                    |
| 0F2    | [0F2 COFFSETS](Opcodes/0F2 COFFSETS.md)                  |                    |
| 0F3    | [0F3 LOFFSET](Opcodes/0F3 LOFFSET.md)                    |                    |
| 0F4    | [0F4 COFFSET](Opcodes/0F4 COFFSET.md)                    |                    |
| 0F5    | [0F5 OFFSETSYNC](Opcodes/0F5 OFFSETSYNC.md)              |                    |
| 0F6    | [0F6 RUNENABLE](Opcodes/0F6 RUNENABLE.md)                | Entity             |
| 0F7    | [0F7 RUNDISABLE](Opcodes/0F7 RUNDISABLE.md)              | Entity             |
| 0F8    | [0F8 MAPFADEOFF](Opcodes/0F8 MAPFADEOFF.md)              | Field related      |
| 0F9    | [0F9 MAPFADEON](Opcodes/0F9 MAPFADEON.md)                | Field related      |
| 0FA    | [0FA INITTRACE](Opcodes/0FA INITTRACE.md)                |                    |
| 0FB    | [0FB SETDRESS](Opcodes/0FB SETDRESS.md)                  | Entity             |
| 0FC    | [0FC GETDRESS](Opcodes/0FC GETDRESS.md)*       | Entity             |
| 0FD    | [0FD FACEDIR](Opcodes/0FD FACEDIR.md)                    | Entity             |
| 0FE    | [0FE FACEDIRA](Opcodes/0FE FACEDIRA.md)                  |                    |
| 0FF    | [0FF FACEDIRP](Opcodes/0FF FACEDIRP.md)                  |                    |
| 100    | [100 FACEDIRLIMIT](Opcodes/100 FACEDIRLIMIT.md)          |                    |
| 101    | [101 FACEDIROFF](Opcodes/101 FACEDIROFF.md)              |                    |
| 102    | [102 SARALYOFF](Opcodes/102 SARALYOFF.md)                |                    |
| 103    | [103 SARALYON](Opcodes/103 SARALYON.md)                  |                    |
| 104    | [104 SARALYDISPOFF](Opcodes/104 SARALYDISPOFF.md)        |                    |
| 105    | [105 SARALYDISPON](Opcodes/105 SARALYDISPON.md)          |                    |
| 106    | [106 MESMODE](Opcodes/106 MESMODE.md)                    | Message            |
| 107    | [107 FACEDIRINIT](Opcodes/107 FACEDIRINIT.md)            |                    |
| 108    | [108 FACEDIRI](Opcodes/108 FACEDIRI.md)                  |                    |
| 109    | [109 JUNCTION](Opcodes/109 JUNCTION.md)                  | Party Management   |
| 10A    | [10A SETCAMERA](Opcodes/10A SETCAMERA.md)                | Field related      |
| 10B    | [10B BATTLECUT](Opcodes/10B BATTLECUT.md)                |                    |
| 10C    | [10C FOOTSTEPCOPY](Opcodes/10C FOOTSTEPCOPY.md)          |                    |
| 10D    | [10D WORLDMAPJUMP](Opcodes/10D WORLDMAPJUMP.md)          | Field related      |
| 10E    | [10E RFACEDIRI](Opcodes/10E RFACEDIRI.md)*     |                    |
| 10F    | [10F RFACEDIR](Opcodes/10F RFACEDIR.md)                  |                    |
| 110    | [110 RFACEDIRA](Opcodes/110 RFACEDIRA.md)                |                    |
| 111    | [111 RFACEDIRP](Opcodes/111 RFACEDIRP.md)                |                    |
| 112    | [112 RFACEDIROFF](Opcodes/112 RFACEDIROFF.md)            |                    |
| 113    | [113 FACEDIRSYNC](Opcodes/113 FACEDIRSYNC.md)            |                    |
| 114    | [114 COPYINFO](Opcodes/114 COPYINFO.md)                  |                    |
| 115    | [115 PCOPYINFO](Opcodes/115 PCOPYINFO.md)*     |                    |
| 116    | [116 RAMESW](Opcodes/116 RAMESW.md)                      | Message            |
| 117    | [117 BGSHADEOFF](Opcodes/117 BGSHADEOFF.md)              | Field related      |
| 118    | [118 AXIS](Opcodes/118 AXIS.md)                          |                    |
| 119    | [119 AXISSYNC](Opcodes/119 AXISSYNC.md)*       |                    |
| 11A    | [11A MENUNORMAL](Opcodes/11A MENUNORMAL.md)              | Menus              |
| 11B    | [11B MENUPHS](Opcodes/11B MENUPHS.md)                    | Menus              |
| 11C    | [11C BGCLEAR](Opcodes/11C BGCLEAR.md)                    |                    |
| 11D    | [11D GETPARTY](Opcodes/11D GETPARTY.md)                  | Party Management   |
| 11E    | [11E MENUSHOP](Opcodes/11E MENUSHOP.md)                  | Menus              |
| 11F    | [11F DISC](Opcodes/11F DISC.md)                          | Field related      |
| 120    | [120 DSCROLL3](Opcodes/120 DSCROLL3.md)*       |                    |
| 121    | [121 LSCROLL3](Opcodes/121 LSCROLL3.md)                  |                    |
| 122    | [122 CSCROLL3](Opcodes/122 CSCROLL3.md)                  |                    |
| 123    | [123 MACCEL](Opcodes/123 MACCEL.md)                      |                    |
| 124    | [124 MLIMIT](Opcodes/124 MLIMIT.md)                      |                    |
| 125    | [125 ADDITEM](Opcodes/125 ADDITEM.md)                    | Item/Magic/Card/GF |
| 126    | [126 SETWITCH](Opcodes/126 SETWITCH.md)                  |                    |
| 127    | [127 SETODIN](Opcodes/127 SETODIN.md)                    |                    |
| 128    | [128 RESETGF](Opcodes/128 RESETGF.md)                    |                    |
| 129    | [129 MENUNAME](Opcodes/129 MENUNAME.md)                  | Menus              |
| 12A    | [12A REST](Opcodes/12A REST.md)                          |                    |
| 12B    | [12B MOVECANCEL](Opcodes/12B MOVECANCEL.md)              |                    |
| 12C    | [12C PMOVECANCEL](Opcodes/12C PMOVECANCEL.md)* |                    |
| 12D    | [12D ACTORMODE](Opcodes/12D ACTORMODE.md)                |                    |
| 12E    | [12E MENUSAVE](Opcodes/12E MENUSAVE.md)                  | Menus              |
| 12F    | [12F SAVEENABLE](Opcodes/12F SAVEENABLE.md)              | Menus              |
| 130    | [130 PHSENABLE](Opcodes/130 PHSENABLE.md)                | Menus              |
| 131    | [131 HOLD](Opcodes/131 HOLD.md)                          | Party Management   |
| 132    | [132 MOVIECUT](Opcodes/132 MOVIECUT.md)                  |                    |
| 133    | [133 SETPLACE](Opcodes/133 SETPLACE.md)                  |                    |
| 134    | [134 SETDCAMERA](Opcodes/134 SETDCAMERA.md)              |                    |
| 135    | [135 CHOICEMUSIC](Opcodes/135 CHOICEMUSIC.md)            |                    |
| 136    | [136 GETCARD](Opcodes/136 GETCARD.md)                    |                    |
| 137    | [137 DRAWPOINT](Opcodes/137 DRAWPOINT.md)                | Menus              |
| 138    | [138 PHSPOWER](Opcodes/138 PHSPOWER.md)                  |                    |
| 139    | [139 KEY](Opcodes/139 KEY.md)                            |                    |
| 13A    | [13A CARDGAME](Opcodes/13A CARDGAME.md)                  | Menus              |
| 13B    | [13B SETBAR](Opcodes/13B SETBAR.md)                      |                    |
| 13C    | [13C DISPBAR](Opcodes/13C DISPBAR.md)                    |                    |
| 13D    | [13D KILLBAR](Opcodes/13D KILLBAR.md)                    |                    |
| 13E    | [13E SCROLLRATIO2](Opcodes/13E SCROLLRATIO2.md)          |                    |
| 13F    | [13F WHOAMI](Opcodes/13F WHOAMI.md)                      |                    |
| 140    | [140 MUSICSTATUS](Opcodes/140 MUSICSTATUS.md)            |                    |
| 141    | [141 MUSICREPLAY](Opcodes/141 MUSICREPLAY.md)            |                    |
| 142    | [142 DOORLINEOFF](Opcodes/142 DOORLINEOFF.md)            | Entity             |
| 143    | [143 DOORLINEON](Opcodes/143 DOORLINEON.md)              | Entity             |
| 144    | [144 MUSICSKIP](Opcodes/144 MUSICSKIP.md)                |                    |
| 145    | [145 DYING](Opcodes/145 DYING.md)                        | Party Management   |
| 146    | [146 SETHP](Opcodes/146 SETHP.md)                        | Party Management   |
| 147    | [147 GETHP](Opcodes/147 GETHP.md)*             | Party Management   |
| 148    | [148 MOVEFLUSH](Opcodes/148 MOVEFLUSH.md)                |                    |
| 149    | [149 MUSICVOLSYNC](Opcodes/149 MUSICVOLSYNC.md)          |                    |
| 14A    | [14A PUSHANIME](Opcodes/14A PUSHANIME.md)                |                    |
| 14B    | [14B POPANIME](Opcodes/14B POPANIME.md)                  |                    |
| 14C    | [14C KEYSCAN2](Opcodes/14C KEYSCAN2.md)                  | Input              |
| 14D    | [14D KEYON2](Opcodes/14D KEYON2.md)*           | Input              |
| 14E    | [14E PARTICLEON](Opcodes/14E PARTICLEON.md)              |                    |
| 14F    | [14F PARTICLEOFF](Opcodes/14F PARTICLEOFF.md)            |                    |
| 150    | [150 KEYSIGHNCHANGE](Opcodes/150 KEYSIGHNCHANGE.md)      |                    |
| 151    | [151 ADDGIL](Opcodes/151 ADDGIL.md)                      | Item/Magic/Card/GF |
| 152    | [152 ADDPASTGIL](Opcodes/152 ADDPASTGIL.md)              | Item/Magic/Card/GF |
| 153    | [153 ADDSEEDLEVEL](Opcodes/153 ADDSEEDLEVEL.md)          | Item/Magic/Card/GF |
| 154    | [154 PARTICLESET](Opcodes/154 PARTICLESET.md)            |                    |
| 155    | [155 SETDRAWPOINT](Opcodes/155 SETDRAWPOINT.md)          |                    |
| 156    | [156 MENUTIPS](Opcodes/156 MENUTIPS.md)                  | Menus              |
| 157    | [157 LASTIN](Opcodes/157 LASTIN.md)                      |                    |
| 158    | [158 LASTOUT](Opcodes/158 LASTOUT.md)                    |                    |
| 159    | [159 SEALEDOFF](Opcodes/159 SEALEDOFF.md)                |                    |
| 15A    | [15A MENUTUTO](Opcodes/15A MENUTUTO.md)                  | Menus              |
| 15B    | [15B OPENEYES](Opcodes/15B OPENEYES.md)*       |                    |
| 15C    | [15C CLOSEEYES](Opcodes/15C CLOSEEYES.md)                |                    |
| 15D    | [15D BLINKEYES](Opcodes/15D BLINKEYES.md)*     |                    |
| 15E    | [15E SETCARD](Opcodes/15E SETCARD.md)                    | Item/Magic/Card/GF |
| 15F    | [15F HOWMANYCARD](Opcodes/15F HOWMANYCARD.md)            | Item/Magic/Card/GF |
| 160    | [160 WHERECARD](Opcodes/160 WHERECARD.md)                | Item/Magic/Card/GF |
| 161    | [161 ADDMAGIC](Opcodes/161 ADDMAGIC.md)                  | Item/Magic/Card/GF |
| 162    | [162 SWAP](Opcodes/162 SWAP.md)                          |                    |
| 163    | [163 SETPARTY2](Opcodes/163 SETPARTY2.md)*     |                    |
| 164    | [164 SPUSYNC](Opcodes/164 SPUSYNC.md)                    | Timer              |
| 165    | [165 BROKEN](Opcodes/165 BROKEN.md)                      |                    |
| 166    | [166 UNKNOWN1](Opcodes/166 UNKNOWN1.md)                  |                    |
| 167    | [167 UNKNOWN2](Opcodes/167 UNKNOWN2.md)                  |                    |
| 168    | [168 UNKNOWN3](Opcodes/168 UNKNOWN3.md)                  |                    |
| 169    | [169 UNKNOWN4](Opcodes/169 UNKNOWN4.md)                  |                    |
| 170    | [170 UNKNOWN5](Opcodes/170 UNKNOWN5.md)                  | Item/Magic/Card/GF |
| 171    | [171 UNKNOWN6](Opcodes/171 UNKNOWN6.md)                  | Animation          |
| 172    | [172 UNKNOWN7](Opcodes/172 UNKNOWN7.md)                  | Animation          |
| 173    | [173 UNKNOWN8](Opcodes/173 UNKNOWN8.md)                  | Animation          |
| 174    | [174 UNKNOWN9](Opcodes/174 UNKNOWN9.md)                  | Animation          |
| 175    | [175 UNKNOWN10](Opcodes/175 UNKNOWN10.md)                |                    |
| 176    | [176 UNKNOWN11](Opcodes/176 UNKNOWN11.md)                |                    |
| 177    | [177 UNKNOWN12](Opcodes/177 UNKNOWN12.md)                |                    |
| 178    | [178 UNKNOWN13](Opcodes/178 UNKNOWN13.md)                | Music and Sound    |
| 179    | [179 UNKNOWN14](Opcodes/179 UNKNOWN14.md)                | Music and Sound    |
| 180    | [180 UNKNOWN15](Opcodes/180 UNKNOWN15.md)                |                    |
| 181    | [181 UNKNOWN16](Opcodes/181 UNKNOWN16.md)                | Field related      |
| 182    | [182 UNKNOWN17](Opcodes/182 UNKNOWN17.md)                | Field related      |
| 183    | [183 UNKNOWN18](Opcodes/183 UNKNOWN18.md)                | Menus              |
