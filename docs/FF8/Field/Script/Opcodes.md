---
title: Opcodes
---

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

Each Opcode's page lists all the parameters for that function in the order you would put them on the stack before the function call. The inline argument is listed separately, if the function requires one. For example, on the page for [SET3](Opcodes/01E_SET3.md), the parameters are listed like this:

  
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
| 000    | [000 NOP](Opcodes/000_NOP.md)*                 | Script Processing  |
| 001    | [001 CAL](Opcodes/001_CAL.md)                            | Script Processing  |
| 002    | [002 JMP](Opcodes/002_JMP.md)                            | Script Processing  |
| 003    | [003 JPF](Opcodes/003_JPF.md)                            | Script Processing  |
| 004    | [004 GJMP](Opcodes/004_GJMP.md)*               | Script Processing  |
| 005    | [005 LBL](Opcodes/005_LBL.md)                            | Script Processing  |
| 006    | [006 RET](Opcodes/006_RET.md)                            | Script Processing  |
| 007    | [007 PSHN\_L](Opcodes/007_PSHN_L.md)                     | Memory             |
| 008    | [008 PSHI\_L](Opcodes/008_PSHI_L.md)                     | Memory             |
| 009    | [009 POPI\_L](Opcodes/009_POPI_L.md)                     | Memory             |
| 00A    | [00A PSHM\_B](Opcodes/00A_PSHM_B.md)                     | Memory             |
| 00B    | [00B POPM\_B](Opcodes/00B_POPM_B.md)                     | Memory             |
| 00C    | [00C PSHM\_W](Opcodes/00C_PSHM_W.md)                     | Memory             |
| 00D    | [00D POPM\_W](Opcodes/00D_POPM_W.md)                     | Memory             |
| 00E    | [00E PSHM\_L](Opcodes/00E_PSHM_L.md)                     | Memory             |
| 00F    | [00F POPM\_L](Opcodes/00F_POPM_L.md)                     | Memory             |
| 010    | [010 PSHSM\_B](Opcodes/010_PSHSM_B.md)                   | Memory             |
| 011    | [011 PSHSM\_W](Opcodes/011_PSHSM_W.md)                   | Memory             |
| 012    | [012 PSHSM\_L](Opcodes/012_PSHSM_L.md)                   | Memory             |
| 013    | [013 PSHAC](Opcodes/013_PSHAC.md)                        | Memory             |
| 014    | [014 REQ](Opcodes/014_REQ.md)                            | Script Processing  |
| 015    | [015 REQSW](Opcodes/015_REQSW.md)                        | Script Processing  |
| 016    | [016 REQEW](Opcodes/016_REQEW.md)                        | Script Processing  |
| 017    | [017 PREQ](Opcodes/017_PREQ.md)                          | Script Processing  |
| 018    | [018 PREQSW](Opcodes/018_PREQSW.md)                      | Script Processing  |
| 019    | [019 PREQEW](Opcodes/019_PREQEW.md)                      | Script Processing  |
| 01A    | [01A UNUSE](Opcodes/01A_UNUSE.md)                        | Entity             |
| 01B    | [01B DEBUG](Opcodes/01B_DEBUG.md)*             |                    |
| 01C    | [01C HALT](Opcodes/01C_HALT.md)                          | Script Processing  |
| 01D    | [01D SET](Opcodes/01D_SET.md)                            | Entity             |
| 01E    | [01E SET3](Opcodes/01E_SET3.md)                          | Entity             |
| 01F    | [01F IDLOCK](Opcodes/01F_IDLOCK.md)                      | Field related      |
| 020    | [020 IDUNLOCK](Opcodes/020_IDUNLOCK.md)                  | Field related      |
| 021    | [021 EFFECTPLAY2](Opcodes/021_EFFECTPLAY2.md)            | Music and Sound    |
| 022    | [022 FOOTSTEP](Opcodes/022_FOOTSTEP.md)                  |                    |
| 023    | [023 JUMP](Opcodes/023_JUMP.md)                          | Entity             |
| 024    | [024 JUMP3](Opcodes/024_JUMP3.md)                        | Entity             |
| 025    | [025 LADDERUP](Opcodes/025_LADDERUP.md)                  | Entity             |
| 026    | [026 LADDERDOWN](Opcodes/026_LADDERDOWN.md)              | Entity             |
| 027    | [027 LADDERUP2](Opcodes/027_LADDERUP2.md)                | Entity             |
| 028    | [028 LADDERDOWN2](Opcodes/028_LADDERDOWN2.md)            | Entity             |
| 029    | [029 MAPJUMP](Opcodes/029_MAPJUMP.md)                    | Field related      |
| 02A    | [02A MAPJUMP3](Opcodes/02A_MAPJUMP3.md)                  | Field related      |
| 02B    | [02B SETMODEL](Opcodes/02B_SETMODEL.md)                  | Entity             |
| 02C    | [02C BASEANIME](Opcodes/02C_BASEANIME.md)                | Animation          |
| 02D    | [02D ANIME](Opcodes/02D_ANIME.md)                        | Animation          |
| 02E    | [02E ANIMEKEEP](Opcodes/02E_ANIMEKEEP.md)                | Animation          |
| 02F    | [02F CANIME](Opcodes/02F_CANIME.md)                      | Animation          |
| 030    | [030 CANIMEKEEP](Opcodes/030_CANIMEKEEP.md)              | Animation          |
| 031    | [031 RANIME](Opcodes/031_RANIME.md)                      | Animation          |
| 032    | [032 RANIMEKEEP](Opcodes/032_RANIMEKEEP.md)              | Animation          |
| 033    | [033 RCANIME](Opcodes/033_RCANIME.md)                    | Animation          |
| 034    | [034 RCANIMEKEEP](Opcodes/034_RCANIMEKEEP.md)            | Animation          |
| 035    | [035 RANIMELOOP](Opcodes/035_RANIMELOOP.md)              | Animation          |
| 036    | [036 RCANIMELOOP](Opcodes/036_RCANIMELOOP.md)            | Animation          |
| 037    | [037 LADDERANIME](Opcodes/037_LADDERANIME.md)            | Animation          |
| 038    | [038 DISCJUMP](Opcodes/038_DISCJUMP.md)                  | Field related      |
| 039    | [039 SETLINE](Opcodes/039_SETLINE.md)                    | Entity             |
| 03A    | [03A LINEON](Opcodes/03A_LINEON.md)                      | Entity             |
| 03B    | [03B LINEOFF](Opcodes/03B_LINEOFF.md)                    | Entity             |
| 03C    | [03C WAIT](Opcodes/03C_WAIT.md)                          | Script Processing  |
| 03D    | [03D MSPEED](Opcodes/03D_MSPEED.md)                      |                    |
| 03E    | [03E MOVE](Opcodes/03E_MOVE.md)                          | Entity             |
| 03F    | [03F MOVEA](Opcodes/03F_MOVEA.md)                        |                    |
| 040    | [040 PMOVEA](Opcodes/040_PMOVEA.md)                      |                    |
| 041    | [041 CMOVE](Opcodes/041_CMOVE.md)                        |                    |
| 042    | [042 FMOVE](Opcodes/042_FMOVE.md)                        |                    |
| 043    | [043 PJUMPA](Opcodes/043_PJUMPA.md)                      |                    |
| 044    | [044 ANIMESYNC](Opcodes/044_ANIMESYNC.md)                | Script Processing  |
| 045    | [045 ANIMESTOP](Opcodes/045_ANIMESTOP.md)                | Animation          |
| 046    | [046 MESW](Opcodes/046_MESW.md)*               |                    |
| 047    | [047 MES](Opcodes/047_MES.md)                            | Message            |
| 048    | [048 MESSYNC](Opcodes/048_MESSYNC.md)                    | Script Processing  |
| 049    | [049 MESVAR](Opcodes/049_MESVAR.md)                      | Message            |
| 04A    | [04A ASK](Opcodes/04A_ASK.md)                            | Message            |
| 04B    | [04B WINSIZE](Opcodes/04B_WINSIZE.md)                    | Message            |
| 04C    | [04C WINCLOSE](Opcodes/04C_WINCLOSE.md)                  | Message            |
| 04D    | [04D UCON](Opcodes/04D_UCON.md)                          | Misc               |
| 04E    | [04E UCOFF](Opcodes/04E_UCOFF.md)                        | Misc               |
| 04F    | [04F MOVIE](Opcodes/04F_MOVIE.md)                        | Movie              |
| 050    | [050 MOVIESYNC](Opcodes/050_MOVIESYNC.md)                | Script Processing  |
| 051    | [051 SETPC](Opcodes/051_SETPC.md)                        | Party management   |
| 052    | [052 DIR](Opcodes/052_DIR.md)                            | Entity             |
| 053    | [053 DIRP](Opcodes/053_DIRP.md)                          |                    |
| 054    | [054 DIRA](Opcodes/054_DIRA.md)                          |                    |
| 055    | [055 PDIRA](Opcodes/055_PDIRA.md)                        |                    |
| 056    | [056 SPUREADY](Opcodes/056_SPUREADY.md)                  | Timer              |
| 057    | [057 TALKON](Opcodes/057_TALKON.md)                      | Entity             |
| 058    | [058 TALKOFF](Opcodes/058_TALKOFF.md)                    | Entity             |
| 059    | [059 PUSHON](Opcodes/059_PUSHON.md)                      | Entity             |
| 05A    | [05A PUSHOFF](Opcodes/05A_PUSHOFF.md)                    | Entity             |
| 05B    | [05B ISTOUCH](Opcodes/05B_ISTOUCH.md)                    |                    |
| 05C    | [05C MAPJUMPO](Opcodes/05C_MAPJUMPO.md)                  | Field related      |
| 05D    | [05D MAPJUMPON](Opcodes/05D_MAPJUMPON.md)                | Field related      |
| 05E    | [05E MAPJUMPOFF](Opcodes/05E_MAPJUMPOFF.md)              | Field related      |
| 05F    | [05F SETMESSPEED](Opcodes/05F_SETMESSPEED.md)            | Message            |
| 060    | [060 SHOW](Opcodes/060_SHOW.md)                          | Entity             |
| 061    | [061 HIDE](Opcodes/061_HIDE.md)                          | Entity             |
| 062    | [062 TALKRADIUS](Opcodes/062_TALKRADIUS.md)              | Entity             |
| 063    | [063 PUSHRADIUS](Opcodes/063_PUSHRADIUS.md)              | Entity             |
| 064    | [064 AMESW](Opcodes/064_AMESW.md)                        | Message            |
| 065    | [065 AMES](Opcodes/065_AMES.md)                          | Message            |
| 066    | [066 GETINFO](Opcodes/066_GETINFO.md)                    |                    |
| 067    | [067 THROUGHON](Opcodes/067_THROUGHON.md)                | Entity             |
| 068    | [068 THROUGHOFF](Opcodes/068_THROUGHOFF.md)              | Entity             |
| 069    | [069 BATTLE](Opcodes/069_BATTLE.md)                      | Battle             |
| 06A    | [06A BATTLERESULT](Opcodes/06A_BATTLERESULT.md)          | Battle             |
| 06B    | [06B BATTLEON](Opcodes/06B_BATTLEON.md)                  | Field related      |
| 06C    | [06C BATTLEOFF](Opcodes/06C_BATTLEOFF.md)                | Field related      |
| 06D    | [06D KEYSCAN](Opcodes/06D_KEYSCAN.md)                    | Input              |
| 06E    | [06E KEYON](Opcodes/06E_KEYON.md)                        | Input              |
| 06F    | [06F AASK](Opcodes/06F_AASK.md)                          | Message            |
| 070    | [070 PGETINFO](Opcodes/070_PGETINFO.md)                  |                    |
| 071    | [071 DSCROLL](Opcodes/071_DSCROLL.md)                    |                    |
| 072    | [072 LSCROLL](Opcodes/072_LSCROLL.md)                    |                    |
| 073    | [073 CSCROLL](Opcodes/073_CSCROLL.md)                    |                    |
| 074    | [074 DSCROLLA](Opcodes/074_DSCROLLA.md)                  |                    |
| 075    | [075 LSCROLLA](Opcodes/075_LSCROLLA.md)                  |                    |
| 076    | [076 CSCROLLA](Opcodes/076_CSCROLLA.md)                  |                    |
| 077    | [077 SCROLLSYNC](Opcodes/077_SCROLLSYNC.md)              | Script Processing  |
| 078    | [078 RMOVE](Opcodes/078_RMOVE.md)                        |                    |
| 079    | [079 RMOVEA](Opcodes/079_RMOVEA.md)                      |                    |
| 07A    | [07A RPMOVEA](Opcodes/07A_RPMOVEA.md)                    |                    |
| 07B    | [07B RCMOVE](Opcodes/07B_RCMOVE.md)                      |                    |
| 07C    | [07C RFMOVE](Opcodes/07C_RFMOVE.md)                      |                    |
| 07D    | [07D MOVESYNC](Opcodes/07D_MOVESYNC.md)                  | Script Processing  |
| 07E    | [07E CLEAR](Opcodes/07E_CLEAR.md)                        | Field related      |
| 07F    | [07F DSCROLLP](Opcodes/07F_DSCROLLP.md)                  |                    |
| 080    | [080 LSCROLLP](Opcodes/080_LSCROLLP.md)                  |                    |
| 081    | [081 CSCROLLP](Opcodes/081_CSCROLLP.md)                  |                    |
| 082    | [082 LTURNR](Opcodes/082_LTURNR.md)                      |                    |
| 083    | [083 LTURNL](Opcodes/083_LTURNL.md)                      |                    |
| 084    | [084 CTURNR](Opcodes/084_CTURNR.md)                      |                    |
| 085    | [085 CTURNL](Opcodes/085_CTURNL.md)                      |                    |
| 086    | [086 ADDPARTY](Opcodes/086_ADDPARTY.md)                  | Party Management   |
| 087    | [087 SUBPARTY](Opcodes/087_SUBPARTY.md)                  | Party Management   |
| 088    | [088 CHANGEPARTY](Opcodes/088_CHANGEPARTY.md)            | Party Management   |
| 089    | [089 REFRESHPARTY](Opcodes/089_REFRESHPARTY.md)          | Party Management   |
| 08A    | [08A SETPARTY](Opcodes/08A_SETPARTY.md)                  | Party Management   |
| 08B    | [08B ISPARTY](Opcodes/08B_ISPARTY.md)                    | Party Management   |
| 08C    | [08C ADDMEMBER](Opcodes/08C_ADDMEMBER.md)                | Party Management   |
| 08D    | [08D SUBMEMBER](Opcodes/08D_SUBMEMBER.md)                | Party Management   |
| 08E    | [08E ISMEMBER](Opcodes/08E_ISMEMBER.md)*       | Party Management   |
| 08F    | [08F LTURN](Opcodes/08F_LTURN.md)                        |                    |
| 090    | [090 CTURN](Opcodes/090_CTURN.md)                        |                    |
| 091    | [091 PLTURN](Opcodes/091_PLTURN.md)                      |                    |
| 092    | [092 PCTURN](Opcodes/092_PCTURN.md)                      |                    |
| 093    | [093 JOIN](Opcodes/093_JOIN.md)                          | Entity             |
| 094    | [094 MESFORCUS](Opcodes/094_MESFORCUS.md)*     |                    |
| 095    | [095 BGANIME](Opcodes/095_BGANIME.md)                    | Field related      |
| 096    | [096 RBGANIME](Opcodes/096_RBGANIME.md)                  | Field related      |
| 097    | [097 RBGANIMELOOP](Opcodes/097_RBGANIMELOOP.md)          | Field related      |
| 098    | [098 BGANIMESYNC](Opcodes/098_BGANIMESYNC.md)            | Field related      |
| 099    | [099 BGDRAW](Opcodes/099_BGDRAW.md)                      | Field related      |
| 09A    | [09A BGOFF](Opcodes/09A_BGOFF.md)                        | Field related      |
| 09B    | [09B BGANIMESPEED](Opcodes/09B_BGANIMESPEED.md)          | Field related      |
| 09C    | [09C SETTIMER](Opcodes/09C_SETTIMER.md)                  | Timer              |
| 09D    | [09D DISPTIMER](Opcodes/09D_DISPTIMER.md)                | Timer              |
| 09E    | [09E SHADETIMER](Opcodes/09E_SHADETIMER.md)*   |                    |
| 09F    | [09F SETGETA](Opcodes/09F_SETGETA.md)                    |                    |
| 0A0    | [0A0 SETROOTTRANS](Opcodes/0A0_SETROOTTRANS.md)          |                    |
| 0A1    | [0A1 SETVIBRATE](Opcodes/0A1_SETVIBRATE.md)              |                    |
| 0A2    | [0A2 STOPVIBRATE](Opcodes/0A2_STOPVIBRATE.md)* |                    |
| 0A3    | [0A3 MOVIEREADY](Opcodes/0A3_MOVIEREADY.md)              | Movie              |
| 0A4    | [0A4 GETTIMER](Opcodes/0A4_GETTIMER.md)                  | Timer              |
| 0A5    | [0A5 FADEIN](Opcodes/0A5_FADEIN.md)                      | Field related      |
| 0A6    | [0A6 FADEOUT](Opcodes/0A6_FADEOUT.md)                    | Field related      |
| 0A7    | [0A7 FADESYNC](Opcodes/0A7_FADESYNC.md)                  | Script Processing  |
| 0A8    | [0A8 SHAKE](Opcodes/0A8_SHAKE.md)                        | Field related      |
| 0A9    | [0A9 SHAKEOFF](Opcodes/0A9_SHAKEOFF.md)                  | Field related      |
| 0AA    | [0AA FADEBLACK](Opcodes/0AA_FADEBLACK.md)                | Field related      |
| 0AB    | [0AB FOLLOWOFF](Opcodes/0AB_FOLLOWOFF.md)                |                    |
| 0AC    | [0AC FOLLOWON](Opcodes/0AC_FOLLOWON.md)                  |                    |
| 0AD    | [0AD GAMEOVER](Opcodes/0AD_GAMEOVER.md)                  | Field related      |
| 0AE    | [0AE ENDING](Opcodes/0AE_ENDING.md)*           |                    |
| 0AF    | [0AF SHADELEVEL](Opcodes/0AF_SHADELEVEL.md)              |                    |
| 0B0    | [0B0 SHADEFORM](Opcodes/0B0_SHADEFORM.md)                |                    |
| 0B1    | [0B1 FMOVEA](Opcodes/0B1_FMOVEA.md)                      |                    |
| 0B2    | [0B2 FMOVEP](Opcodes/0B2_FMOVEP.md)                      |                    |
| 0B3    | [0B3 SHADESET](Opcodes/0B3_SHADESET.md)                  |                    |
| 0B4    | [0B4 MUSICCHANGE](Opcodes/0B4_MUSICCHANGE.md)            | Music and Sound    |
| 0B5    | [0B5 MUSICLOAD](Opcodes/0B5_MUSICLOAD.md)                | Music and Sound    |
| 0B6    | [0B6 FADENONE](Opcodes/0B6_FADENONE.md)                  |                    |
| 0B7    | [0B7 POLYCOLOR](Opcodes/0B7_POLYCOLOR.md)                |                    |
| 0B8    | [0B8 POLYCOLORALL](Opcodes/0B8_POLYCOLORALL.md)          |                    |
| 0B9    | [0B9 KILLTIMER](Opcodes/0B9_KILLTIMER.md)                | Timer              |
| 0BA    | [0BA CROSSMUSIC](Opcodes/0BA_CROSSMUSIC.md)              |                    |
| 0BB    | [0BB DUALMUSIC](Opcodes/0BB_DUALMUSIC.md)                |                    |
| 0BC    | [0BC EFFECTPLAY](Opcodes/0BC_EFFECTPLAY.md)              | Music and Sound    |
| 0BD    | [0BD EFFECTLOAD](Opcodes/0BD_EFFECTLOAD.md)              | Music and Sound    |
| 0BE    | [0BE LOADSYNC](Opcodes/0BE_LOADSYNC.md)                  |                    |
| 0BF    | [0BF MUSICSTOP](Opcodes/0BF_MUSICSTOP.md)                | Music and Sound    |
| 0C0    | [0C0 MUSICVOL](Opcodes/0C0_MUSICVOL.md)                  | Music and Sound    |
| 0C1    | [0C1 MUSICVOLTRANS](Opcodes/0C1_MUSICVOLTRANS.md)        | Music and Sound    |
| 0C2    | [0C2 MUSICVOLFADE](Opcodes/0C2_MUSICVOLFADE.md)          | Music and Sound    |
| 0C3    | [0C3 ALLSEVOL](Opcodes/0C3_ALLSEVOL.md)                  | Music and Sound    |
| 0C4    | [0C4 ALLSEVOLTRANS](Opcodes/0C4_ALLSEVOLTRANS.md)        | Music and Sound    |
| 0C5    | [0C5 ALLSEPOS](Opcodes/0C5_ALLSEPOS.md)*       | Music and Sound    |
| 0C6    | [0C6 ALLSEPOSTRANS](Opcodes/0C6_ALLSEPOSTRANS.md)        | Music and Sound    |
| 0C7    | [0C7 SEVOL](Opcodes/0C7_SEVOL.md)                        | Music and Sound    |
| 0C8    | [0C8 SEVOLTRANS](Opcodes/0C8_SEVOLTRANS.md)              | Music and Sound    |
| 0C9    | [0C9 SEPOS](Opcodes/0C9_SEPOS.md)                        | Music and Sound    |
| 0CA    | [0CA SEPOSTRANS](Opcodes/0CA_SEPOSTRANS.md)              | Music and Sound    |
| 0CB    | [0CB SETBATTLEMUSIC](Opcodes/0CB_SETBATTLEMUSIC.md)      | Music and Sound    |
| 0CC    | [0CC BATTLEMODE](Opcodes/0CC_BATTLEMODE.md)              | Battle             |
| 0CD    | [0CD SESTOP](Opcodes/0CD_SESTOP.md)                      | Music and Sound    |
| 0CE    | [0CE BGANIMEFLAG](Opcodes/0CE_BGANIMEFLAG.md)* |                    |
| 0CF    | [0CF INITSOUND](Opcodes/0CF_INITSOUND.md)                |                    |
| 0D0    | [0D0 BGSHADE](Opcodes/0D0_BGSHADE.md)                    |                    |
| 0D1    | [0D1 BGSHADESTOP](Opcodes/0D1_BGSHADESTOP.md)            |                    |
| 0D2    | [0D2 RBGSHADELOOP](Opcodes/0D2_RBGSHADELOOP.md)          |                    |
| 0D3    | [0D3 DSCROLL2](Opcodes/0D3_DSCROLL2.md)                  |                    |
| 0D4    | [0D4 LSCROLL2](Opcodes/0D4_LSCROLL2.md)                  |                    |
| 0D5    | [0D5 CSCROLL2](Opcodes/0D5_CSCROLL2.md)                  |                    |
| 0D6    | [0D6 DSCROLLA2](Opcodes/0D6_DSCROLLA2.md)                |                    |
| 0D7    | [0D7 LSCROLLA2](Opcodes/0D7_LSCROLLA2.md)*     |                    |
| 0D8    | [0D8 CSCROLLA2](Opcodes/0D8_CSCROLLA2.md)                |                    |
| 0D9    | [0D9 DSCROLLP2](Opcodes/0D9_DSCROLLP2.md)*     |                    |
| 0DA    | [0DA LSCROLLP2](Opcodes/0DA_LSCROLLP2.md)*     |                    |
| 0DB    | [0DB CSCROLLP2](Opcodes/0DB_CSCROLLP2.md)*     |                    |
| 0DC    | [0DC SCROLLSYNC2](Opcodes/0DC_SCROLLSYNC2.md)            |                    |
| 0DD    | [0DD SCROLLMODE2](Opcodes/0DD_SCROLLMODE2.md)            |                    |
| 0DE    | [0DE MENUENABLE](Opcodes/0DE_MENUENABLE.md)              | Menus              |
| 0DF    | [0DF MENUDISABLE](Opcodes/0DF_MENUDISABLE.md)            | Menus              |
| 0E0    | [0E0 FOOTSTEPON](Opcodes/0E0_FOOTSTEPON.md)              |                    |
| 0E1    | [0E1 FOOTSTEPOFF](Opcodes/0E1_FOOTSTEPOFF.md)            |                    |
| 0E2    | [0E2 FOOTSTEPOFFALL](Opcodes/0E2_FOOTSTEPOFFALL.md)      |                    |
| 0E3    | [0E3 FOOTSTEPCUT](Opcodes/0E3_FOOTSTEPCUT.md)            |                    |
| 0E4    | [0E4 PREMAPJUMP](Opcodes/0E4_PREMAPJUMP.md)              |                    |
| 0E5    | [0E5 USE](Opcodes/0E5_USE.md)                            | Entity             |
| 0E6    | [0E6 SPLIT](Opcodes/0E6_SPLIT.md)                        | Entity             |
| 0E7    | [0E7 ANIMESPEED](Opcodes/0E7_ANIMESPEED.md)              | Animation          |
| 0E8    | [0E8 RND](Opcodes/0E8_RND.md)                            |                    |
| 0E9    | [0E9 DCOLADD](Opcodes/0E9_DCOLADD.md)                    |                    |
| 0EA    | [0EA DCOLSUB](Opcodes/0EA_DCOLSUB.md)                    |                    |
| 0EB    | [0EB TCOLADD](Opcodes/0EB_TCOLADD.md)                    |                    |
| 0EC    | [0EC TCOLSUB](Opcodes/0EC_TCOLSUB.md)                    |                    |
| 0ED    | [0ED FCOLADD](Opcodes/0ED_FCOLADD.md)                    | Field related      |
| 0EE    | [0EE FCOLSUB](Opcodes/0EE_FCOLSUB.md)                    | Field related      |
| 0EF    | [0EF COLSYNC](Opcodes/0EF_COLSYNC.md)                    | Script processing  |
| 0F0    | [0F0 DOFFSET](Opcodes/0F0_DOFFSET.md)                    |                    |
| 0F1    | [0F1 LOFFSETS](Opcodes/0F1_LOFFSETS.md)                  |                    |
| 0F2    | [0F2 COFFSETS](Opcodes/0F2_COFFSETS.md)                  |                    |
| 0F3    | [0F3 LOFFSET](Opcodes/0F3_LOFFSET.md)                    |                    |
| 0F4    | [0F4 COFFSET](Opcodes/0F4_COFFSET.md)                    |                    |
| 0F5    | [0F5 OFFSETSYNC](Opcodes/0F5_OFFSETSYNC.md)              |                    |
| 0F6    | [0F6 RUNENABLE](Opcodes/0F6_RUNENABLE.md)                | Entity             |
| 0F7    | [0F7 RUNDISABLE](Opcodes/0F7_RUNDISABLE.md)              | Entity             |
| 0F8    | [0F8 MAPFADEOFF](Opcodes/0F8_MAPFADEOFF.md)              | Field related      |
| 0F9    | [0F9 MAPFADEON](Opcodes/0F9_MAPFADEON.md)                | Field related      |
| 0FA    | [0FA INITTRACE](Opcodes/0FA_INITTRACE.md)                |                    |
| 0FB    | [0FB SETDRESS](Opcodes/0FB_SETDRESS.md)                  | Entity             |
| 0FC    | [0FC GETDRESS](Opcodes/0FC_GETDRESS.md)*       | Entity             |
| 0FD    | [0FD FACEDIR](Opcodes/0FD_FACEDIR.md)                    | Entity             |
| 0FE    | [0FE FACEDIRA](Opcodes/0FE_FACEDIRA.md)                  |                    |
| 0FF    | [0FF FACEDIRP](Opcodes/0FF_FACEDIRP.md)                  |                    |
| 100    | [100 FACEDIRLIMIT](Opcodes/100_FACEDIRLIMIT.md)          |                    |
| 101    | [101 FACEDIROFF](Opcodes/101_FACEDIROFF.md)              |                    |
| 102    | [102 SARALYOFF](Opcodes/102_SARALYOFF.md)                |                    |
| 103    | [103 SARALYON](Opcodes/103_SARALYON.md)                  |                    |
| 104    | [104 SARALYDISPOFF](Opcodes/104_SARALYDISPOFF.md)        |                    |
| 105    | [105 SARALYDISPON](Opcodes/105_SARALYDISPON.md)          |                    |
| 106    | [106 MESMODE](Opcodes/106_MESMODE.md)                    | Message            |
| 107    | [107 FACEDIRINIT](Opcodes/107_FACEDIRINIT.md)            |                    |
| 108    | [108 FACEDIRI](Opcodes/108_FACEDIRI.md)                  |                    |
| 109    | [109 JUNCTION](Opcodes/109_JUNCTION.md)                  | Party Management   |
| 10A    | [10A SETCAMERA](Opcodes/10A_SETCAMERA.md)                | Field related      |
| 10B    | [10B BATTLECUT](Opcodes/10B_BATTLECUT.md)                |                    |
| 10C    | [10C FOOTSTEPCOPY](Opcodes/10C_FOOTSTEPCOPY.md)          |                    |
| 10D    | [10D WORLDMAPJUMP](Opcodes/10D_WORLDMAPJUMP.md)          | Field related      |
| 10E    | [10E RFACEDIRI](Opcodes/10E_RFACEDIRI.md)*     |                    |
| 10F    | [10F RFACEDIR](Opcodes/10F_RFACEDIR.md)                  |                    |
| 110    | [110 RFACEDIRA](Opcodes/110_RFACEDIRA.md)                |                    |
| 111    | [111 RFACEDIRP](Opcodes/111_RFACEDIRP.md)                |                    |
| 112    | [112 RFACEDIROFF](Opcodes/112_RFACEDIROFF.md)            |                    |
| 113    | [113 FACEDIRSYNC](Opcodes/113_FACEDIRSYNC.md)            |                    |
| 114    | [114 COPYINFO](Opcodes/114_COPYINFO.md)                  |                    |
| 115    | [115 PCOPYINFO](Opcodes/115_PCOPYINFO.md)*     |                    |
| 116    | [116 RAMESW](Opcodes/116_RAMESW.md)                      | Message            |
| 117    | [117 BGSHADEOFF](Opcodes/117_BGSHADEOFF.md)              | Field related      |
| 118    | [118 AXIS](Opcodes/118_AXIS.md)                          |                    |
| 119    | [119 AXISSYNC](Opcodes/119_AXISSYNC.md)*       |                    |
| 11A    | [11A MENUNORMAL](Opcodes/11A_MENUNORMAL.md)              | Menus              |
| 11B    | [11B MENUPHS](Opcodes/11B_MENUPHS.md)                    | Menus              |
| 11C    | [11C BGCLEAR](Opcodes/11C_BGCLEAR.md)                    |                    |
| 11D    | [11D GETPARTY](Opcodes/11D_GETPARTY.md)                  | Party Management   |
| 11E    | [11E MENUSHOP](Opcodes/11E_MENUSHOP.md)                  | Menus              |
| 11F    | [11F DISC](Opcodes/11F_DISC.md)                          | Field related      |
| 120    | [120 DSCROLL3](Opcodes/120_DSCROLL3.md)*       |                    |
| 121    | [121 LSCROLL3](Opcodes/121_LSCROLL3.md)                  |                    |
| 122    | [122 CSCROLL3](Opcodes/122_CSCROLL3.md)                  |                    |
| 123    | [123 MACCEL](Opcodes/123_MACCEL.md)                      |                    |
| 124    | [124 MLIMIT](Opcodes/124_MLIMIT.md)                      |                    |
| 125    | [125 ADDITEM](Opcodes/125_ADDITEM.md)                    | Item/Magic/Card/GF |
| 126    | [126 SETWITCH](Opcodes/126_SETWITCH.md)                  |                    |
| 127    | [127 SETODIN](Opcodes/127_SETODIN.md)                    |                    |
| 128    | [128 RESETGF](Opcodes/128_RESETGF.md)                    |                    |
| 129    | [129 MENUNAME](Opcodes/129_MENUNAME.md)                  | Menus              |
| 12A    | [12A REST](Opcodes/12A_REST.md)                          |                    |
| 12B    | [12B MOVECANCEL](Opcodes/12B_MOVECANCEL.md)              |                    |
| 12C    | [12C PMOVECANCEL](Opcodes/12C_PMOVECANCEL.md)* |                    |
| 12D    | [12D ACTORMODE](Opcodes/12D_ACTORMODE.md)                |                    |
| 12E    | [12E MENUSAVE](Opcodes/12E_MENUSAVE.md)                  | Menus              |
| 12F    | [12F SAVEENABLE](Opcodes/12F_SAVEENABLE.md)              | Menus              |
| 130    | [130 PHSENABLE](Opcodes/130_PHSENABLE.md)                | Menus              |
| 131    | [131 HOLD](Opcodes/131_HOLD.md)                          | Party Management   |
| 132    | [132 MOVIECUT](Opcodes/132_MOVIECUT.md)                  |                    |
| 133    | [133 SETPLACE](Opcodes/133_SETPLACE.md)                  |                    |
| 134    | [134 SETDCAMERA](Opcodes/134_SETDCAMERA.md)              |                    |
| 135    | [135 CHOICEMUSIC](Opcodes/135_CHOICEMUSIC.md)            |                    |
| 136    | [136 GETCARD](Opcodes/136_GETCARD.md)                    |                    |
| 137    | [137 DRAWPOINT](Opcodes/137_DRAWPOINT.md)                | Menus              |
| 138    | [138 PHSPOWER](Opcodes/138_PHSPOWER.md)                  |                    |
| 139    | [139 KEY](Opcodes/139_KEY.md)                            |                    |
| 13A    | [13A CARDGAME](Opcodes/13A_CARDGAME.md)                  | Menus              |
| 13B    | [13B SETBAR](Opcodes/13B_SETBAR.md)                      |                    |
| 13C    | [13C DISPBAR](Opcodes/13C_DISPBAR.md)                    |                    |
| 13D    | [13D KILLBAR](Opcodes/13D_KILLBAR.md)                    |                    |
| 13E    | [13E SCROLLRATIO2](Opcodes/13E_SCROLLRATIO2.md)          |                    |
| 13F    | [13F WHOAMI](Opcodes/13F_WHOAMI.md)                      |                    |
| 140    | [140 MUSICSTATUS](Opcodes/140_MUSICSTATUS.md)            |                    |
| 141    | [141 MUSICREPLAY](Opcodes/141_MUSICREPLAY.md)            |                    |
| 142    | [142 DOORLINEOFF](Opcodes/142_DOORLINEOFF.md)            | Entity             |
| 143    | [143 DOORLINEON](Opcodes/143_DOORLINEON.md)              | Entity             |
| 144    | [144 MUSICSKIP](Opcodes/144_MUSICSKIP.md)                |                    |
| 145    | [145 DYING](Opcodes/145_DYING.md)                        | Party Management   |
| 146    | [146 SETHP](Opcodes/146_SETHP.md)                        | Party Management   |
| 147    | [147 GETHP](Opcodes/147_GETHP.md)*             | Party Management   |
| 148    | [148 MOVEFLUSH](Opcodes/148_MOVEFLUSH.md)                |                    |
| 149    | [149 MUSICVOLSYNC](Opcodes/149_MUSICVOLSYNC.md)          |                    |
| 14A    | [14A PUSHANIME](Opcodes/14A_PUSHANIME.md)                |                    |
| 14B    | [14B POPANIME](Opcodes/14B_POPANIME.md)                  |                    |
| 14C    | [14C KEYSCAN2](Opcodes/14C_KEYSCAN2.md)                  | Input              |
| 14D    | [14D KEYON2](Opcodes/14D_KEYON2.md)*           | Input              |
| 14E    | [14E PARTICLEON](Opcodes/14E_PARTICLEON.md)              |                    |
| 14F    | [14F PARTICLEOFF](Opcodes/14F_PARTICLEOFF.md)            |                    |
| 150    | [150 KEYSIGHNCHANGE](Opcodes/150_KEYSIGHNCHANGE.md)      |                    |
| 151    | [151 ADDGIL](Opcodes/151_ADDGIL.md)                      | Item/Magic/Card/GF |
| 152    | [152 ADDPASTGIL](Opcodes/152_ADDPASTGIL.md)              | Item/Magic/Card/GF |
| 153    | [153 ADDSEEDLEVEL](Opcodes/153_ADDSEEDLEVEL.md)          | Item/Magic/Card/GF |
| 154    | [154 PARTICLESET](Opcodes/154_PARTICLESET.md)            |                    |
| 155    | [155 SETDRAWPOINT](Opcodes/155_SETDRAWPOINT.md)          |                    |
| 156    | [156 MENUTIPS](Opcodes/156_MENUTIPS.md)                  | Menus              |
| 157    | [157 LASTIN](Opcodes/157_LASTIN.md)                      |                    |
| 158    | [158 LASTOUT](Opcodes/158_LASTOUT.md)                    |                    |
| 159    | [159 SEALEDOFF](Opcodes/159_SEALEDOFF.md)                |                    |
| 15A    | [15A MENUTUTO](Opcodes/15A_MENUTUTO.md)                  | Menus              |
| 15B    | [15B OPENEYES](Opcodes/15B_OPENEYES.md)*       |                    |
| 15C    | [15C CLOSEEYES](Opcodes/15C_CLOSEEYES.md)                |                    |
| 15D    | [15D BLINKEYES](Opcodes/15D_BLINKEYES.md)*     |                    |
| 15E    | [15E SETCARD](Opcodes/15E_SETCARD.md)                    | Item/Magic/Card/GF |
| 15F    | [15F HOWMANYCARD](Opcodes/15F_HOWMANYCARD.md)            | Item/Magic/Card/GF |
| 160    | [160 WHERECARD](Opcodes/160_WHERECARD.md)                | Item/Magic/Card/GF |
| 161    | [161 ADDMAGIC](Opcodes/161_ADDMAGIC.md)                  | Item/Magic/Card/GF |
| 162    | [162 SWAP](Opcodes/162_SWAP.md)                          |                    |
| 163    | [163 SETPARTY2](Opcodes/163_SETPARTY2.md)*     |                    |
| 164    | [164 SPUSYNC](Opcodes/164_SPUSYNC.md)                    | Timer              |
| 165    | [165 BROKEN](Opcodes/165_BROKEN.md)                      |                    |
| 166    | [166 UNKNOWN1](Opcodes/166_UNKNOWN1.md)                  |                    |
| 167    | [167 UNKNOWN2](Opcodes/167_UNKNOWN2.md)                  |                    |
| 168    | [168 UNKNOWN3](Opcodes/168_UNKNOWN3.md)                  |                    |
| 169    | [169 UNKNOWN4](Opcodes/169_UNKNOWN4.md)                  |                    |
| 170    | [170 UNKNOWN5](Opcodes/170_UNKNOWN5.md)                  | Item/Magic/Card/GF |
| 171    | [171 UNKNOWN6](Opcodes/171_UNKNOWN6.md)                  | Animation          |
| 172    | [172 UNKNOWN7](Opcodes/172_UNKNOWN7.md)                  | Animation          |
| 173    | [173 UNKNOWN8](Opcodes/173_UNKNOWN8.md)                  | Animation          |
| 174    | [174 UNKNOWN9](Opcodes/174_UNKNOWN9.md)                  | Animation          |
| 175    | [175 UNKNOWN10](Opcodes/175_UNKNOWN10.md)                |                    |
| 176    | [176 UNKNOWN11](Opcodes/176_UNKNOWN11.md)                |                    |
| 177    | [177 UNKNOWN12](Opcodes/177_UNKNOWN12.md)                |                    |
| 178    | [178 UNKNOWN13](Opcodes/178_UNKNOWN13.md)                | Music and Sound    |
| 179    | [179 UNKNOWN14](Opcodes/179_UNKNOWN14.md)                | Music and Sound    |
| 180    | [180 UNKNOWN15](Opcodes/180_UNKNOWN15.md)                |                    |
| 181    | [181 UNKNOWN16](Opcodes/181_UNKNOWN16.md)                | Field related      |
| 182    | [182 UNKNOWN17](Opcodes/182_UNKNOWN17.md)                | Field related      |
| 183    | [183 UNKNOWN18](Opcodes/183_UNKNOWN18.md)                | Menus              |
