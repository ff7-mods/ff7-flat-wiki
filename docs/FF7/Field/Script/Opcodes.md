---
title: Opcodes
---

[Home](../../../Main%20Page.md.md) > [FF7](../../../FF7.md) > [Field](../../Field.md) > [Script](../Script.md) > Opcodes

## Arranged by category

### Script Flow & Control

[`00`` ``RET`][]  
[`01`` ``REQ`][]  
[`02`` ``REQSW`][]  
[`03`` ``REQEW`][]  
[`04`` ``PREQ`][]  
[`05`` ``PRQSW`][]  
[`06`` ``PRQEW`][]  
[`07`` ``RETTO`][]  
[`10`` ``JMPF`][]  
[`11`` ``JMPFL`][]  
[`12`` ``JMPB`][]  
[`13`` ``JMPBL`][]  
[`14`` ``IFUB`][]  
[`15`` ``IFUBL`][]  
[`16`` ``IFSW`][]  
[`17`` ``IFSWL`][]  
[`18`` ``IFUW`][]  
[`19`` ``IFUWL`][]  
[`24`` ``WAIT`][]  
[`30`` ``IFKEY`][]  
[`31`` ``IFKEYON`][]  
[`32`` ``IFKEYOFF`][]  
[`5F`` ``NOP`][]  
[`CB`` ``IFPRTYQ`][]  
[`CC`` ``IFMEMBQ`][]

### System & Module Control

[`0E`` ``DSKCG`][]  
[`0F`` ``SPECIAL`][]  
[`20`` ``MINIGAME`][]  
[`22`` ``BTMD2`][]  
[`23`` ``BTRLD`][]  
[`4B`` ``BTLTB`][]  
[`60`` ``MAPJUMP`][]  
[`6E`` ``LSTMP`][]  
[`70`` ``BATTLE`][]  
[`71`` ``BTLON`][]  
[`72`` ``BTLMD`][]  
[`D2`` ``MPJPO`][]  
[`FF`` ``GAMEOVER`][]

### Assignment & Mathematics

[`76`` ``PLUS!`][]  
[`77`` ``PLUS2!`][]  
[`78`` ``MINUS!`][]  
[`79`` ``MINUS2!`][]  
[`7A`` ``INC!`][]  
[`7B`` ``INC2!`][]  
[`7C`` ``DEC!`][]  
[`7D`` ``DEC2!`][]  
[`7F`` ``RDMSD`][]  
[`80`` ``SETBYTE`][]  
[`81`` ``SETWORD`][]  
[`82`` ``BITON`][]  
[`83`` ``BITOFF`][]  
[`84`` ``BITXOR`][]  
[`85`` ``PLUS`][]  
[`86`` ``PLUS2`][]  
[`87`` ``MINUS`][]  
[`88`` ``MINUS2`][]  
[`89`` ``MUL`][]  
[`8A`` ``MUL2`][]  
[`8B`` ``DIV`][]  
[`8C`` ``DIV2`][]  
[`8D`` ``MOD`][]  
[`8E`` ``MOD2`][]  
[`8F`` ``AND`][]  
[`90`` ``AND2`][]  
[`91`` ``OR`][]  
[`92`` ``OR2`][]  
[`93`` ``XOR`][]  
[`94`` ``XOR2`][]  
[`95`` ``INC`][]  
[`96`` ``INC2`][]  
[`97`` ``DEC`][]  
[`98`` ``DEC2`][]  
[`99`` ``RANDOM`][]  
[`9A`` ``LBYTE`][]  
[`9B`` ``HBYTE`][]  
[`9C`` ``2BYTE`][]  
[`D4`` ``SIN`][]  
[`D5`` ``COS`][]

### Windowing & Menu

[`21`` ``TUTOR`][]  
[`2E`` ``WCLS`][]  
[`2F`` ``WSIZW`][]  
[`36`` ``WSPCL`][]  
[`37`` ``WNUMB`][]  
[`38`` ``STTIM`][]  
[`40`` ``MESSAGE`][]  
[`41`` ``MPARA`][]  
[`42`` ``MPRA2`][]  
[`43`` ``MPNAM`][]  
[`48`` ``ASK`][]  
[`49`` ``MENU`][]  
[`4A`` ``MENU2`][]  
[`50`` ``WINDOW`][]  
[`51`` ``WMOVE`][]  
[`52`` ``WMODE`][]  
[`53`` ``WREST`][]  
[`54`` ``WCLSE`][]  
[`55`` ``WROW`][]  
[`56`` ``GWCOL`][]  
[`57`` ``SWCOL`][]

### Party & Inventory

[`0A`` ``SPTYE`][]  
[`0B`` ``GTPYE`][]  
[`39`` ``GOLDu`][]  
[`3A`` ``GOLDd`][]  
[`3B`` ``CHGLD`][]  
[`3C`` ``HMPMAX1`][]  
[`3D`` ``HMPMAX2`][]  
[`3E`` ``MHMMX`][]  
[`3F`` ``HMPMAX3`][]  
[`45`` ``MPu`][]  
[`47`` ``MPd`][]  
[`4D`` ``HPu`][]  
[`4F`` ``HPd`][]  
[`58`` ``STITM`][]  
[`59`` ``DLITM`][]  
[`5A`` ``CKITM`][]  
[`5B`` ``SMTRA`][]  
[`5C`` ``DMTRA`][]  
[`5D`` ``CMTRA`][]  
[`74`` ``GETPC`][]  
[`C8`` ``PRTYP`][]  
[`C9`` ``PRTYM`][]  
[`CA`` ``PRTYE`][]  
[`CB`` ``IFPRTYQ`][]  
[`CC`` ``IFMEMBQ`][]  
[`CD`` ``MMBud`][]  
[`CE`` ``MMBLK`][]  
[`CF`` ``MMBUK`][]

### Field Models, Animation & 3D/Walkmesh

[`08`` ``JOIN`][]  
[`09`` ``SPLIT`][]  
[`26`` ``BLINK`][]  
[`28`` ``KAWAI`][]  
[`29`` ``KAWIW`][]  
[`2A`` ``PMOVA`][]  
[`2B`` ``SLIP`][]  
[`33`` ``UC`][]  
[`34`` ``PDIRA`][]  
[`35`` ``PTURA`][]  
[`6D`` ``IDLCK`][]  
[`73`` ``PGTDR`][]  
[`75`` ``PXYZI`][]  
[`7E`` ``TLKON`][]  
[`A0`` ``PC`][]  
[`A1`` ``CHAR`][]  
[`A2`` ``DFANM`][]  
[`A3`` ``ANIME1`][]  
[`A4`` ``VISI`][]  
[`A5`` ``XYZI`][]  
[`A6`` ``XYI`][]  
[`A7`` ``XYZ`][]  
[`A8`` ``MOVE`][]  
[`A9`` ``CMOVE`][]  
[`AA`` ``MOVA`][]  
[`AB`` ``TURA`][]  
[`AC`` ``ANIMW`][]  
[`AD`` ``FMOVE`][]  
[`AE`` ``ANIME2`][]  
[`AF`` ``ANIM!1`][]  
[`B0`` ``CANIM1`][]  
[`B1`` ``CANM!1`][]  
[`B2`` ``MSPED`][]  
[`B3`` ``DIR`][]  
[`B4`` ``TURNGEN`][]  
[`B5`` ``TURN`][]  
[`B6`` ``DIRA`][]  
[`B7`` ``GETDIR`][]  
[`B8`` ``GETAXY`][]  
[`B9`` ``GETAI`][]  
[`BA`` ``ANIM!2`][]  
[`BB`` ``CANIM2`][]  
[`BC`` ``CANM!2`][]  
[`BD`` ``ASPED`][]  
[`BF`` ``CC`][]  
[`C0`` ``JUMP`][]  
[`C1`` ``AXYZI`][]  
[`C2`` ``LADER`][]  
[`C3`` ``OFST`][]  
[`C4`` ``OFSTW`][]  
[`C5`` ``TALKR`][]  
[`C6`` ``SLIDR`][]  
[`C7`` ``SOLID`][]  
[`D0`` ``LINE`][]  
[`D1`` ``LINON`][]  
[`D3`` ``SLINE`][]  
[`D6`` ``TLKR2`][]  
[`D7`` ``SLDR2`][]  
[`DC`` ``CCANM`][]  
[`DB`` ``FCFIX`][]  
[`DD`` ``ANIMB`][]  
[`DE`` ``TURNW`][]

### Background & Palette

[`27`` ``BGMOVIE`][]  
[`2C`` ``BGPDH`][]  
[`2D`` ``BGSCR`][]  
[`DF`` ``MPPAL`][]  
[`E0`` ``BGON`][]  
[`E1`` ``BGOFF`][]  
[`E2`` ``BGROL`][]  
[`E3`` ``BGROL2`][]  
[`E4`` ``BGCLR`][]  
[`E5`` ``STPAL`][]  
[`E6`` ``LDPAL`][]  
[`E7`` ``CPPAL`][]  
[`E8`` ``RTPAL`][]  
[`E9`` ``ADPAL`][]  
[`EA`` ``MPPAL2`][]  
[`EB`` ``STPLS`][]  
[`EC`` ``LDPLS`][]  
[`ED`` ``CPPAL2`][]  
[`EE`` ``RTPAL2`][]  
[`EF`` ``ADPAL2`][]

### Camera, Audio & Video

[`25`` ``NFADE`][]  
[`5E`` ``SHAKE`][]  
[`61`` ``SCRLO`][]  
[`62`` ``SCRLC`][]  
[`63`` ``SCRLA`][]  
[`64`` ``SCR2D`][]  
[`65`` ``SCRCC`][]  
[`66`` ``SCR2DC`][]  
[`67`` ``SCRLW`][]  
[`68`` ``SCR2DL`][]  
[`6B`` ``FADE`][]  
[`6C`` ``FADEW`][]  
[`6F`` ``SCRLP`][]  
[`DA`` ``AKAO2`][]  
[`F0`` ``MUSIC`][]  
[`F1`` ``SOUND`][]  
[`F2`` ``AKAO`][]  
[`F3`` ``MUSVT`][]  
[`F4`` ``MUSVM`][]  
[`F5`` ``MULCK`][]  
[`F6`` ``BMUSC`][]  
[`F7`` ``CHMPH`][]  
[`F8`` ``PMVIE`][]  
[`F9`` ``MOVIE`][]  
[`FA`` ``MVIEF`][]  
[`FB`` ``MVCAM`][]  
[`FC`` ``FMUSC`][]  
[`FD`` ``CMUSC`][]  
[`FE`` ``CHMST`][]

### Uncategorised

[`69`` ``MPDSP`][]  
[`6A`` ``VWOFT`][]  
[`9D`` ``SETX`][]  
[`9E`` ``GETX`][]  
[`9F`` ``SEARCHX`][]  
[`D8`` ``PMJMP`][]  
[`D9`` ``PMJMP2`][]

## Arranged by opcode

[`00`` ``RET`][]  
[`01`` ``REQ`][]  
[`02`` ``REQSW`][]  
[`03`` ``REQEW`][]  
[`04`` ``PREQ`][]  
[`05`` ``PRQSW`][]  
[`06`` ``PRQEW`][]  
[`07`` ``RETTO`][]  
[`08`` ``JOIN`][]  
[`09`` ``SPLIT`][]  
[`0A`` ``SPTYE`][]  
[`0B`` ``GTPYE`][]  
<font color="gray">`0C (unused)`</font>  
<font color="gray">`0D (unused)`</font>  
[`0E`` ``DSKCG`][]  
[`0F`` ``SPECIAL`][]  
[`10`` ``JMPF`][]  
[`11`` ``JMPFL`][]  
[`12`` ``JMPB`][]  
[`13`` ``JMPBL`][]  
[`14`` ``IFUB`][]  
[`15`` ``IFUBL`][]  
[`16`` ``IFSW`][]  
[`17`` ``IFSWL`][]  
[`18`` ``IFUW`][]  
[`19`` ``IFUWL`][]  
<font color="gray">`1A (unused)`</font>  
<font color="gray">`1B (unused)`</font>  
<font color="gray">`1C (unused)`</font>  
<font color="gray">`1D (unused)`</font>  
<font color="gray">`1E (unused)`</font>  
<font color="gray">`1F (unused)`</font>  
[`20`` ``MINIGAME`][]  
[`21`` ``TUTOR`][]  
[`22`` ``BTMD2`][]  
[`23`` ``BTRLD`][]  
[`24`` ``WAIT`][]  
[`25`` ``NFADE`][]  
[`26`` ``BLINK`][]  
[`27`` ``BGMOVIE`][]  
[`28`` ``KAWAI`][]  
[`29`` ``KAWIW`][]  
[`2A`` ``PMOVA`][]  
[`2B`` ``SLIP`][]  
[`2C`` ``BGPDH`][]  
[`2D`` ``BGSCR`][]  
[`2E`` ``WCLS`][]  
[`2F`` ``WSIZW`][]  
[`30`` ``IFKEY`][]  
[`31`` ``IFKEYON`][]  
[`32`` ``IFKEYOFF`][]  
[`33`` ``UC`][]  
[`34`` ``PDIRA`][]  
[`35`` ``PTURA`][]  
[`36`` ``WSPCL`][]  
[`37`` ``WNUMB`][]  
[`38`` ``STTIM`][]  
[`39`` ``GOLDu`][]  
[`3A`` ``GOLDd`][]  
[`3B`` ``CHGLD`][]  
[`3C`` ``HMPMAX1`][]  
[`3D`` ``HMPMAX2`][]  
[`3E`` ``MHMMX`][]  
[`3F`` ``HMPMAX3`][]  
[`40`` ``MESSAGE`][]  
[`41`` ``MPARA`][]  
[`42`` ``MPRA2`][]  
[`43`` ``MPNAM`][]  
<font color="gray">`44 (unused)`</font>  
[`45`` ``MPu`][]  
<font color="gray">`46 (unused)`</font>  
[`47`` ``MPd`][]  
[`48`` ``ASK`][]  
[`49`` ``MENU`][]  
[`4A`` ``MENU2`][]  
[`4B`` ``BTLTB`][]  
<font color="gray">`4C (unused)`</font>  
[`4D`` ``HPu`][]  
<font color="gray">`4E (unused)`</font>  
[`4F`` ``HPd`][]  
[`50`` ``WINDOW`][]  
[`51`` ``WMOVE`][]  
[`52`` ``WMODE`][]  
[`53`` ``WREST`][]  
[`54`` ``WCLSE`][]  
[`55`` ``WROW`][]  
[`56`` ``GWCOL`][]  
[`57`` ``SWCOL`][]  
[`58`` ``STITM`][]  
[`59`` ``DLITM`][]  
[`5A`` ``CKITM`][]  
[`5B`` ``SMTRA`][]  
[`5C`` ``DMTRA`][]  
[`5D`` ``CMTRA`][]  
[`5E`` ``SHAKE`][]  
[`5F`` ``NOP`][]  
[`60`` ``MAPJUMP`][]  
[`61`` ``SCRLO`][]  
[`62`` ``SCRLC`][]  
[`63`` ``SCRLA`][]  
[`64`` ``SCR2D`][]  
[`65`` ``SCRCC`][]  
[`66`` ``SCR2DC`][]  
[`67`` ``SCRLW`][]  
[`68`` ``SCR2DL`][]  
[`69`` ``MPDSP`][]  
[`6A`` ``VWOFT`][]  
[`6B`` ``FADE`][]  
[`6C`` ``FADEW`][]  
[`6D`` ``IDLCK`][]  
[`6E`` ``LSTMP`][]  
[`6F`` ``SCRLP`][]  
[`70`` ``BATTLE`][]  
[`71`` ``BTLON`][]  
[`72`` ``BTLMD`][]  
[`73`` ``PGTDR`][]  
[`74`` ``GETPC`][]  
[`75`` ``PXYZI`][]  
[`76`` ``PLUS!`][]  
[`77`` ``PLUS2!`][]  
[`78`` ``MINUS!`][]  
[`79`` ``MINUS2!`][]  
[`7A`` ``INC!`][]  
[`7B`` ``INC2!`][]  
[`7C`` ``DEC!`][]  
[`7D`` ``DEC2!`][]  
[`7E`` ``TLKON`][]  
[`7F`` ``RDMSD`][]  
[`80`` ``SETBYTE`][]  
[`81`` ``SETWORD`][]  
[`82`` ``BITON`][]  
[`83`` ``BITOFF`][]  
[`84`` ``BITXOR`][]  
[`85`` ``PLUS`][]  
[`86`` ``PLUS2`][]  
[`87`` ``MINUS`][]  
[`88`` ``MINUS2`][]  
[`89`` ``MUL`][]  
[`8A`` ``MUL2`][]  
[`8B`` ``DIV`][]  
[`8C`` ``DIV2`][]  
[`8D`` ``MOD`][]  
[`8E`` ``MOD2`][]  
[`8F`` ``AND`][]  
[`90`` ``AND2`][]  
[`91`` ``OR`][]  
[`92`` ``OR2`][]  
[`93`` ``XOR`][]  
[`94`` ``XOR2`][]  
[`95`` ``INC`][]  
[`96`` ``INC2`][]  
[`97`` ``DEC`][]  
[`98`` ``DEC2`][]  
[`99`` ``RANDOM`][]  
[`9A`` ``LBYTE`][]  
[`9B`` ``HBYTE`][]  
[`9C`` ``2BYTE`][]  
[`9D`` ``SETX`][]  
[`9E`` ``GETX`][]  
[`9F`` ``SEARCHX`][]  
[`A0`` ``PC`][]  
[`A1`` ``CHAR`][]  
[`A2`` ``DFANM`][]  
[`A3`` ``ANIME1`][]  
[`A4`` ``VISI`][]  
[`A5`` ``XYZI`][]  
[`A6`` ``XYI`][]  
[`A7`` ``XYZ`][]  
[`A8`` ``MOVE`][]  
[`A9`` ``CMOVE`][]  
[`AA`` ``MOVA`][]  
[`AB`` ``TURA`][]  
[`AC`` ``ANIMW`][]  
[`AD`` ``FMOVE`][]  
[`AE`` ``ANIME2`][]  
[`AF`` ``ANIM!1`][]  
[`B0`` ``CANIM1`][]  
[`B1`` ``CANM!1`][]  
[`B2`` ``MSPED`][]  
[`B3`` ``DIR`][]  
[`B4`` ``TURNGEN`][]  
[`B5`` ``TURN`][]  
[`B6`` ``DIRA`][]  
[`B7`` ``GETDIR`][]  
[`B8`` ``GETAXY`][]  
[`B9`` ``GETAI`][]  
[`BA`` ``ANIM!2`][]  
[`BB`` ``CANIM2`][]  
[`BC`` ``CANM!2`][]  
[`BD`` ``ASPED`][]  
<font color="gray">`BE (unused)`</font>  
[`BF`` ``CC`][]  
[`C0`` ``JUMP`][]  
[`C1`` ``AXYZI`][]  
[`C2`` ``LADER`][]  
[`C3`` ``OFST`][]  
[`C4`` ``OFSTW`][]  
[`C5`` ``TALKR`][]  
[`C6`` ``SLIDR`][]  
[`C7`` ``SOLID`][]  
[`C8`` ``PRTYP`][]  
[`C9`` ``PRTYM`][]  
[`CA`` ``PRTYE`][]  
[`CB`` ``IFPRTYQ`][]  
[`CC`` ``IFMEMBQ`][]  
[`CD`` ``MMBud`][]  
[`CE`` ``MMBLK`][]  
[`CF`` ``MMBUK`][]  
[`D0`` ``LINE`][]  
[`D1`` ``LINON`][]  
[`D2`` ``MPJPO`][]  
[`D3`` ``SLINE`][]  
[`D4`` ``SIN`][]  
[`D5`` ``COS`][]  
[`D6`` ``TLKR2`][]  
[`D7`` ``SLDR2`][]  
[`D8`` ``PMJMP`][]  
[`D9`` ``PMJMP2`][]  
[`DA`` ``AKAO2`][]  
[`DB`` ``FCFIX`][]  
[`DC`` ``CCANM`][]  
[`DD`` ``ANIMB`][]  
[`DE`` ``TURNW`][]  
[`DF`` ``MPPAL`][]  
[`E0`` ``BGON`][]  
[`E1`` ``BGOFF`][]  
[`E2`` ``BGROL`][]  
[`E3`` ``BGROL2`][]  
[`E4`` ``BGCLR`][]  
[`E5`` ``STPAL`][]  
[`E6`` ``LDPAL`][]  
[`E7`` ``CPPAL`][]  
[`E8`` ``RTPAL`][]  
[`E9`` ``ADPAL`][]  
[`EA`` ``MPPAL2`][]  
[`EB`` ``STPLS`][]  
[`EC`` ``LDPLS`][]  
[`ED`` ``CPPAL2`][]  
[`EE`` ``RTPAL2`][]  
[`EF`` ``ADPAL2`][]  
[`F0`` ``MUSIC`][]  
[`F1`` ``SOUND`][]  
[`F2`` ``AKAO`][]  
[`F3`` ``MUSVT`][]  
[`F4`` ``MUSVM`][]  
[`F5`` ``MULCK`][]  
[`F6`` ``BMUSC`][]  
[`F7`` ``CHMPH`][]  
[`F8`` ``PMVIE`][]  
[`F9`` ``MOVIE`][]  
[`FA`` ``MVIEF`][]  
[`FB`` ``MVCAM`][]  
[`FC`` ``FMUSC`][]  
[`FD`` ``CMUSC`][]  
[`FE`` ``CHMST`][]  
[`FF`` ``GAMEOVER`][]

  [`00`` ``RET`]: Opcodes/00%20RET.md "wikilink"
  [`01`` ``REQ`]: Opcodes/01%20REQ.md "wikilink"
  [`02`` ``REQSW`]: Opcodes/02%20REQSW.md "wikilink"
  [`03`` ``REQEW`]: Opcodes/03%20REQEW.md "wikilink"
  [`04`` ``PREQ`]: Opcodes/04%20PREQ.md "wikilink"
  [`05`` ``PRQSW`]: Opcodes/05%20PRQSW.md "wikilink"
  [`06`` ``PRQEW`]: Opcodes/06%20PRQEW.md "wikilink"
  [`07`` ``RETTO`]: Opcodes/07%20RETTO.md "wikilink"
  [`10`` ``JMPF`]: Opcodes/10%20JMPF.md "wikilink"
  [`11`` ``JMPFL`]: Opcodes/11%20JMPFL.md "wikilink"
  [`12`` ``JMPB`]: Opcodes/12%20JMPB.md "wikilink"
  [`13`` ``JMPBL`]: Opcodes/13%20JMPBL.md "wikilink"
  [`14`` ``IFUB`]: Opcodes/14%20IFUB.md "wikilink"
  [`15`` ``IFUBL`]: Opcodes/15%20IFUBL.md "wikilink"
  [`16`` ``IFSW`]: Opcodes/16%20IFSW.md "wikilink"
  [`17`` ``IFSWL`]: Opcodes/17%20IFSWL.md "wikilink"
  [`18`` ``IFUW`]: Opcodes/18%20IFUW.md "wikilink"
  [`19`` ``IFUWL`]: Opcodes/19%20IFUWL.md "wikilink"
  [`24`` ``WAIT`]: Opcodes/24%20WAIT.md "wikilink"
  [`30`` ``IFKEY`]: Opcodes/30%20IFKEY.md "wikilink"
  [`31`` ``IFKEYON`]: Opcodes/31%20IFKEYON.md "wikilink"
  [`32`` ``IFKEYOFF`]: Opcodes/32%20IFKEYOFF.md "wikilink"
  [`5F`` ``NOP`]: Opcodes/5F%20NOP.md "wikilink"
  [`CB`` ``IFPRTYQ`]: Opcodes/CB%20IFPRTYQ.md "wikilink"
  [`CC`` ``IFMEMBQ`]: Opcodes/CC%20IFMEMBQ.md "wikilink"
  [`0E`` ``DSKCG`]: Opcodes/0E%20DSKCG.md "wikilink"
  [`0F`` ``SPECIAL`]: Opcodes/0F%20SPECIAL.md "wikilink"
  [`20`` ``MINIGAME`]: Opcodes/20%20MINIGAME.md "wikilink"
  [`22`` ``BTMD2`]: Opcodes/22%20BTMD2.md "wikilink"
  [`23`` ``BTRLD`]: Opcodes/23%20BTRLD.md "wikilink"
  [`4B`` ``BTLTB`]: Opcodes/4B%20BTLTB.md "wikilink"
  [`60`` ``MAPJUMP`]: Opcodes/60%20MAPJUMP.md "wikilink"
  [`6E`` ``LSTMP`]: Opcodes/6E%20LSTMP.md "wikilink"
  [`70`` ``BATTLE`]: Opcodes/70%20BATTLE.md "wikilink"
  [`71`` ``BTLON`]: Opcodes/71%20BTLON.md "wikilink"
  [`72`` ``BTLMD`]: Opcodes/72%20BTLMD.md "wikilink"
  [`D2`` ``MPJPO`]: Opcodes/D2%20MPJPO.md "wikilink"
  [`FF`` ``GAMEOVER`]: Opcodes/FF%20GAMEOVER.md "wikilink"
  [`76`` ``PLUS!`]: Opcodes/76%20PLUS!.md "wikilink"
  [`77`` ``PLUS2!`]: Opcodes/77%20PLUS2!.md "wikilink"
  [`78`` ``MINUS!`]: Opcodes/78%20MINUS!.md "wikilink"
  [`79`` ``MINUS2!`]: Opcodes/79%20MINUS2!.md "wikilink"
  [`7A`` ``INC!`]: Opcodes/7A%20INC!.md "wikilink"
  [`7B`` ``INC2!`]: Opcodes/7B%20INC2!.md "wikilink"
  [`7C`` ``DEC!`]: Opcodes/7C%20DEC!.md "wikilink"
  [`7D`` ``DEC2!`]: Opcodes/7D%20DEC2!.md "wikilink"
  [`7F`` ``RDMSD`]: Opcodes/7F%20RDMSD.md "wikilink"
  [`80`` ``SETBYTE`]: Opcodes/80%20SETBYTE.md "wikilink"
  [`81`` ``SETWORD`]: Opcodes/81%20SETWORD.md "wikilink"
  [`82`` ``BITON`]: Opcodes/82%20BITON.md "wikilink"
  [`83`` ``BITOFF`]: Opcodes/83%20BITOFF.md "wikilink"
  [`84`` ``BITXOR`]: Opcodes/84%20BITXOR.md "wikilink"
  [`85`` ``PLUS`]: Opcodes/85%20PLUS.md "wikilink"
  [`86`` ``PLUS2`]: Opcodes/86%20PLUS2.md "wikilink"
  [`87`` ``MINUS`]: Opcodes/87%20MINUS.md "wikilink"
  [`88`` ``MINUS2`]: Opcodes/88%20MINUS2.md "wikilink"
  [`89`` ``MUL`]: Opcodes/89%20MUL.md "wikilink"
  [`8A`` ``MUL2`]: Opcodes/8A%20MUL2.md "wikilink"
  [`8B`` ``DIV`]: Opcodes/8B%20DIV.md "wikilink"
  [`8C`` ``DIV2`]: Opcodes/8C%20DIV2.md "wikilink"
  [`8D`` ``MOD`]: Opcodes/8D%20MOD.md "wikilink"
  [`8E`` ``MOD2`]: Opcodes/8E%20MOD2.md "wikilink"
  [`8F`` ``AND`]: Opcodes/8F%20AND.md "wikilink"
  [`90`` ``AND2`]: Opcodes/90%20AND2.md "wikilink"
  [`91`` ``OR`]: Opcodes/91%20OR.md "wikilink"
  [`92`` ``OR2`]: Opcodes/92%20OR2.md "wikilink"
  [`93`` ``XOR`]: Opcodes/93%20XOR.md "wikilink"
  [`94`` ``XOR2`]: Opcodes/94%20XOR2.md "wikilink"
  [`95`` ``INC`]: Opcodes/95%20INC.md "wikilink"
  [`96`` ``INC2`]: Opcodes/96%20INC2.md "wikilink"
  [`97`` ``DEC`]: Opcodes/97%20DEC.md "wikilink"
  [`98`` ``DEC2`]: Opcodes/98%20DEC2.md "wikilink"
  [`99`` ``RANDOM`]: Opcodes/99%20RANDOM.md "wikilink"
  [`9A`` ``LBYTE`]: Opcodes/9A%20LBYTE.md "wikilink"
  [`9B`` ``HBYTE`]: Opcodes/9B%20HBYTE.md "wikilink"
  [`9C`` ``2BYTE`]: Opcodes/9C%202BYTE.md "wikilink"
  [`D4`` ``SIN`]: Opcodes/D4%20SIN.md "wikilink"
  [`D5`` ``COS`]: Opcodes/D5%20COS.md "wikilink"
  [`21`` ``TUTOR`]: Opcodes/21%20TUTOR.md "wikilink"
  [`2E`` ``WCLS`]: Opcodes/2E%20WCLS.md "wikilink"
  [`2F`` ``WSIZW`]: Opcodes/2F%20WSIZW.md "wikilink"
  [`36`` ``WSPCL`]: Opcodes/36%20WSPCL.md "wikilink"
  [`37`` ``WNUMB`]: Opcodes/37%20WNUMB.md "wikilink"
  [`38`` ``STTIM`]: Opcodes/38%20STTIM.md "wikilink"
  [`40`` ``MESSAGE`]: Opcodes/40%20MESSAGE.md "wikilink"
  [`41`` ``MPARA`]: Opcodes/41%20MPARA.md "wikilink"
  [`42`` ``MPRA2`]: Opcodes/42%20MPRA2.md "wikilink"
  [`43`` ``MPNAM`]: Opcodes/43%20MPNAM.md "wikilink"
  [`48`` ``ASK`]: Opcodes/48%20ASK.md "wikilink"
  [`49`` ``MENU`]: Opcodes/49%20MENU.md "wikilink"
  [`4A`` ``MENU2`]: Opcodes/4A%20MENU2.md "wikilink"
  [`50`` ``WINDOW`]: Opcodes/50%20WINDOW.md "wikilink"
  [`51`` ``WMOVE`]: Opcodes/51%20WMOVE.md "wikilink"
  [`52`` ``WMODE`]: Opcodes/52%20WMODE.md "wikilink"
  [`53`` ``WREST`]: Opcodes/53%20WREST.md "wikilink"
  [`54`` ``WCLSE`]: Opcodes/54%20WCLSE.md "wikilink"
  [`55`` ``WROW`]: Opcodes/55%20WROW.md "wikilink"
  [`56`` ``GWCOL`]: Opcodes/56%20GWCOL.md "wikilink"
  [`57`` ``SWCOL`]: Opcodes/57%20SWCOL.md "wikilink"
  [`0A`` ``SPTYE`]: Opcodes/0A%20SPTYE.md "wikilink"
  [`0B`` ``GTPYE`]: Opcodes/0B%20GTPYE.md "wikilink"
  [`39`` ``GOLDu`]: Opcodes/39%20GOLDu.md "wikilink"
  [`3A`` ``GOLDd`]: Opcodes/3A%20GOLDd.md "wikilink"
  [`3B`` ``CHGLD`]: Opcodes/3B%20CHGLD.md "wikilink"
  [`3C`` ``HMPMAX1`]: Opcodes/3C%20HMPMAX1.md "wikilink"
  [`3D`` ``HMPMAX2`]: Opcodes/3D%20HMPMAX2.md "wikilink"
  [`3E`` ``MHMMX`]: Opcodes/3E%20MHMMX.md "wikilink"
  [`3F`` ``HMPMAX3`]: Opcodes/3F%20HMPMAX3.md "wikilink"
  [`45`` ``MPu`]: Opcodes/45%20MPu.md "wikilink"
  [`47`` ``MPd`]: Opcodes/47%20MPd.md "wikilink"
  [`4D`` ``HPu`]: Opcodes/4D%20HPu.md "wikilink"
  [`4F`` ``HPd`]: Opcodes/4F%20HPd.md "wikilink"
  [`58`` ``STITM`]: Opcodes/58%20STITM.md "wikilink"
  [`59`` ``DLITM`]: Opcodes/59%20DLITM.md "wikilink"
  [`5A`` ``CKITM`]: Opcodes/5A%20CKITM.md "wikilink"
  [`5B`` ``SMTRA`]: Opcodes/5B%20SMTRA.md "wikilink"
  [`5C`` ``DMTRA`]: Opcodes/5C%20DMTRA.md "wikilink"
  [`5D`` ``CMTRA`]: Opcodes/5D%20CMTRA.md "wikilink"
  [`74`` ``GETPC`]: Opcodes/74%20GETPC.md "wikilink"
  [`C8`` ``PRTYP`]: Opcodes/C8%20PRTYP.md "wikilink"
  [`C9`` ``PRTYM`]: Opcodes/C9%20PRTYM.md "wikilink"
  [`CA`` ``PRTYE`]: Opcodes/CA%20PRTYE.md "wikilink"
  [`CD`` ``MMBud`]: Opcodes/CD%20MMBud.md "wikilink"
  [`CE`` ``MMBLK`]: Opcodes/CE%20MMBLK.md "wikilink"
  [`CF`` ``MMBUK`]: Opcodes/CF%20MMBUK.md "wikilink"
  [`08`` ``JOIN`]: Opcodes/08%20JOIN.md "wikilink"
  [`09`` ``SPLIT`]: Opcodes/09%20SPLIT.md "wikilink"
  [`26`` ``BLINK`]: Opcodes/26%20BLINK.md "wikilink"
  [`28`` ``KAWAI`]: Opcodes/28%20KAWAI.md "wikilink"
  [`29`` ``KAWIW`]: Opcodes/29%20KAWIW.md "wikilink"
  [`2A`` ``PMOVA`]: Opcodes/2A%20PMOVA.md "wikilink"
  [`2B`` ``SLIP`]: Opcodes/2B%20SLIP.md "wikilink"
  [`33`` ``UC`]: Opcodes/33%20UC.md "wikilink"
  [`34`` ``PDIRA`]: Opcodes/34%20PDIRA.md "wikilink"
  [`35`` ``PTURA`]: Opcodes/35%20PTURA.md "wikilink"
  [`6D`` ``IDLCK`]: Opcodes/6D%20IDLCK.md "wikilink"
  [`73`` ``PGTDR`]: Opcodes/73%20PGTDR.md "wikilink"
  [`75`` ``PXYZI`]: Opcodes/75%20PXYZI.md "wikilink"
  [`7E`` ``TLKON`]: Opcodes/7E%20TLKON.md "wikilink"
  [`A0`` ``PC`]: Opcodes/A0%20PC.md "wikilink"
  [`A1`` ``CHAR`]: Opcodes/A1%20CHAR.md "wikilink"
  [`A2`` ``DFANM`]: Opcodes/A2%20DFANM.md "wikilink"
  [`A3`` ``ANIME1`]: Opcodes/A3%20ANIME1.md "wikilink"
  [`A4`` ``VISI`]: Opcodes/A4%20VISI.md "wikilink"
  [`A5`` ``XYZI`]: Opcodes/A5%20XYZI.md "wikilink"
  [`A6`` ``XYI`]: Opcodes/A6%20XYI.md "wikilink"
  [`A7`` ``XYZ`]: Opcodes/A7%20XYZ.md "wikilink"
  [`A8`` ``MOVE`]: Opcodes/A8%20MOVE.md "wikilink"
  [`A9`` ``CMOVE`]: Opcodes/A9%20CMOVE.md "wikilink"
  [`AA`` ``MOVA`]: Opcodes/AA%20MOVA.md "wikilink"
  [`AB`` ``TURA`]: Opcodes/AB%20TURA.md "wikilink"
  [`AC`` ``ANIMW`]: Opcodes/AC%20ANIMW.md "wikilink"
  [`AD`` ``FMOVE`]: Opcodes/AD%20FMOVE.md "wikilink"
  [`AE`` ``ANIME2`]: Opcodes/AE%20ANIME2.md "wikilink"
  [`AF`` ``ANIM!1`]: Opcodes/AF%20ANIM!1.md "wikilink"
  [`B0`` ``CANIM1`]: Opcodes/B0%20CANIM1.md "wikilink"
  [`B1`` ``CANM!1`]: Opcodes/B1%20CANM!1.md "wikilink"
  [`B2`` ``MSPED`]: Opcodes/B2%20MSPED.md "wikilink"
  [`B3`` ``DIR`]: Opcodes/B3%20DIR.md "wikilink"
  [`B4`` ``TURNGEN`]: Opcodes/B4%20TURNGEN.md "wikilink"
  [`B5`` ``TURN`]: Opcodes/B5%20TURN.md "wikilink"
  [`B6`` ``DIRA`]: Opcodes/B6%20DIRA.md "wikilink"
  [`B7`` ``GETDIR`]: Opcodes/B7%20GETDIR.md "wikilink"
  [`B8`` ``GETAXY`]: Opcodes/B8%20GETAXY.md "wikilink"
  [`B9`` ``GETAI`]: Opcodes/B9%20GETAI.md "wikilink"
  [`BA`` ``ANIM!2`]: Opcodes/BA%20ANIM!2.md "wikilink"
  [`BB`` ``CANIM2`]: Opcodes/BB%20CANIM2.md "wikilink"
  [`BC`` ``CANM!2`]: Opcodes/BC%20CANM!2.md "wikilink"
  [`BD`` ``ASPED`]: Opcodes/BD%20ASPED.md "wikilink"
  [`BF`` ``CC`]: Opcodes/BF%20CC.md "wikilink"
  [`C0`` ``JUMP`]: Opcodes/C0%20JUMP.md "wikilink"
  [`C1`` ``AXYZI`]: Opcodes/C1%20AXYZI.md "wikilink"
  [`C2`` ``LADER`]: Opcodes/C2%20LADER.md "wikilink"
  [`C3`` ``OFST`]: Opcodes/C3%20OFST.md "wikilink"
  [`C4`` ``OFSTW`]: Opcodes/C4%20OFSTW.md "wikilink"
  [`C5`` ``TALKR`]: Opcodes/C5%20TALKR.md "wikilink"
  [`C6`` ``SLIDR`]: Opcodes/C6%20SLIDR.md "wikilink"
  [`C7`` ``SOLID`]: Opcodes/C7%20SOLID.md "wikilink"
  [`D0`` ``LINE`]: Opcodes/D0%20LINE.md "wikilink"
  [`D1`` ``LINON`]: Opcodes/D1%20LINON.md "wikilink"
  [`D3`` ``SLINE`]: Opcodes/D3%20SLINE.md "wikilink"
  [`D6`` ``TLKR2`]: Opcodes/D6%20TLKR2.md "wikilink"
  [`D7`` ``SLDR2`]: Opcodes/D7%20SLDR2.md "wikilink"
  [`DC`` ``CCANM`]: Opcodes/DC%20CCANM.md "wikilink"
  [`DB`` ``FCFIX`]: Opcodes/DB%20FCFIX.md "wikilink"
  [`DD`` ``ANIMB`]: Opcodes/DD%20ANIMB.md "wikilink"
  [`DE`` ``TURNW`]: Opcodes/DE%20TURNW.md "wikilink"
  [`27`` ``BGMOVIE`]: Opcodes/27%20BGMOVIE.md "wikilink"
  [`2C`` ``BGPDH`]: Opcodes/2C%20BGPDH.md "wikilink"
  [`2D`` ``BGSCR`]: Opcodes/2D%20BGSCR.md "wikilink"
  [`DF`` ``MPPAL`]: Opcodes/DF%20MPPAL.md "wikilink"
  [`E0`` ``BGON`]: Opcodes/E0%20BGON.md "wikilink"
  [`E1`` ``BGOFF`]: Opcodes/E1%20BGOFF.md "wikilink"
  [`E2`` ``BGROL`]: Opcodes/E2%20BGROL.md "wikilink"
  [`E3`` ``BGROL2`]: Opcodes/E3%20BGROL2.md "wikilink"
  [`E4`` ``BGCLR`]: Opcodes/E4%20BGCLR.md "wikilink"
  [`E5`` ``STPAL`]: Opcodes/E5%20STPAL.md "wikilink"
  [`E6`` ``LDPAL`]: Opcodes/E6%20LDPAL.md "wikilink"
  [`E7`` ``CPPAL`]: Opcodes/E7%20CPPAL.md "wikilink"
  [`E8`` ``RTPAL`]: Opcodes/E8%20RTPAL.md "wikilink"
  [`E9`` ``ADPAL`]: Opcodes/E9%20ADPAL.md "wikilink"
  [`EA`` ``MPPAL2`]: Opcodes/EA%20MPPAL2.md "wikilink"
  [`EB`` ``STPLS`]: Opcodes/EB%20STPLS.md "wikilink"
  [`EC`` ``LDPLS`]: Opcodes/EC%20LDPLS.md "wikilink"
  [`ED`` ``CPPAL2`]: Opcodes/ED%20CPPAL2.md "wikilink"
  [`EE`` ``RTPAL2`]: Opcodes/EE%20RTPAL2.md "wikilink"
  [`EF`` ``ADPAL2`]: Opcodes/EF%20ADPAL2.md "wikilink"
  [`25`` ``NFADE`]: Opcodes/25%20NFADE.md "wikilink"
  [`5E`` ``SHAKE`]: Opcodes/5E%20SHAKE.md "wikilink"
  [`61`` ``SCRLO`]: Opcodes/61%20SCRLO.md "wikilink"
  [`62`` ``SCRLC`]: Opcodes/62%20SCRLC.md "wikilink"
  [`63`` ``SCRLA`]: Opcodes/63%20SCRLA.md "wikilink"
  [`64`` ``SCR2D`]: Opcodes/64%20SCR2D.md "wikilink"
  [`65`` ``SCRCC`]: Opcodes/65%20SCRCC.md "wikilink"
  [`66`` ``SCR2DC`]: Opcodes/66%20SCR2DC.md "wikilink"
  [`67`` ``SCRLW`]: Opcodes/67%20SCRLW.md "wikilink"
  [`68`` ``SCR2DL`]: Opcodes/68%20SCR2DL.md "wikilink"
  [`6B`` ``FADE`]: Opcodes/6B%20FADE.md "wikilink"
  [`6C`` ``FADEW`]: Opcodes/6C%20FADEW.md "wikilink"
  [`6F`` ``SCRLP`]: Opcodes/6F%20SCRLP.md "wikilink"
  [`DA`` ``AKAO2`]: Opcodes/DA%20AKAO2.md "wikilink"
  [`F0`` ``MUSIC`]: Opcodes/F0%20MUSIC.md "wikilink"
  [`F1`` ``SOUND`]: Opcodes/F1%20SOUND.md "wikilink"
  [`F2`` ``AKAO`]: Opcodes/F2%20AKAO.md "wikilink"
  [`F3`` ``MUSVT`]: Opcodes/F3%20MUSVT.md "wikilink"
  [`F4`` ``MUSVM`]: Opcodes/F4%20MUSVM.md "wikilink"
  [`F5`` ``MULCK`]: Opcodes/F5%20MULCK.md "wikilink"
  [`F6`` ``BMUSC`]: Opcodes/F6%20BMUSC.md "wikilink"
  [`F7`` ``CHMPH`]: Opcodes/F7%20CHMPH.md "wikilink"
  [`F8`` ``PMVIE`]: Opcodes/F8%20PMVIE.md "wikilink"
  [`F9`` ``MOVIE`]: Opcodes/F9%20MOVIE.md "wikilink"
  [`FA`` ``MVIEF`]: Opcodes/FA%20MVIEF.md "wikilink"
  [`FB`` ``MVCAM`]: Opcodes/FB%20MVCAM.md "wikilink"
  [`FC`` ``FMUSC`]: Opcodes/FC%20FMUSC.md "wikilink"
  [`FD`` ``CMUSC`]: Opcodes/FD%20CMUSC.md "wikilink"
  [`FE`` ``CHMST`]: Opcodes/FE%20CHMST.md "wikilink"
  [`69`` ``MPDSP`]: Opcodes/69%20MPDSP.md "wikilink"
  [`6A`` ``VWOFT`]: Opcodes/6A%20VWOFT.md "wikilink"
  [`9D`` ``SETX`]: Opcodes/9D%20SETX.md "wikilink"
  [`9E`` ``GETX`]: Opcodes/9E%20GETX.md "wikilink"
  [`9F`` ``SEARCHX`]: Opcodes/9F%20SEARCHX.md "wikilink"
  [`D8`` ``PMJMP`]: Opcodes/D8%20PMJMP.md "wikilink"
  [`D9`` ``PMJMP2`]: Opcodes/D9%20PMJMP2.md "wikilink"
