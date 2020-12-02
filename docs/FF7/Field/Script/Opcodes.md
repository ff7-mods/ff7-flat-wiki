---
title: Opcodes
---

[Home](/Main%20Page.md) > [FF7](/FF7.md) > [Field](/FF7/Field.md) > [Script](/FF7/Field/Script.md) > Opcodes

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

  [`00`` ``RET`]: /FF7/Field/Script/Opcodes/00%20RET.md "wikilink"
  [`01`` ``REQ`]: /FF7/Field/Script/Opcodes/01%20REQ.md "wikilink"
  [`02`` ``REQSW`]: /FF7/Field/Script/Opcodes/02%20REQSW.md "wikilink"
  [`03`` ``REQEW`]: /FF7/Field/Script/Opcodes/03%20REQEW.md "wikilink"
  [`04`` ``PREQ`]: /FF7/Field/Script/Opcodes/04%20PREQ.md "wikilink"
  [`05`` ``PRQSW`]: /FF7/Field/Script/Opcodes/05%20PRQSW.md "wikilink"
  [`06`` ``PRQEW`]: /FF7/Field/Script/Opcodes/06%20PRQEW.md "wikilink"
  [`07`` ``RETTO`]: /FF7/Field/Script/Opcodes/07%20RETTO.md "wikilink"
  [`10`` ``JMPF`]: /FF7/Field/Script/Opcodes/10%20JMPF.md "wikilink"
  [`11`` ``JMPFL`]: /FF7/Field/Script/Opcodes/11%20JMPFL.md "wikilink"
  [`12`` ``JMPB`]: /FF7/Field/Script/Opcodes/12%20JMPB.md "wikilink"
  [`13`` ``JMPBL`]: /FF7/Field/Script/Opcodes/13%20JMPBL.md "wikilink"
  [`14`` ``IFUB`]: /FF7/Field/Script/Opcodes/14%20IFUB.md "wikilink"
  [`15`` ``IFUBL`]: /FF7/Field/Script/Opcodes/15%20IFUBL.md "wikilink"
  [`16`` ``IFSW`]: /FF7/Field/Script/Opcodes/16%20IFSW.md "wikilink"
  [`17`` ``IFSWL`]: /FF7/Field/Script/Opcodes/17%20IFSWL.md "wikilink"
  [`18`` ``IFUW`]: /FF7/Field/Script/Opcodes/18%20IFUW.md "wikilink"
  [`19`` ``IFUWL`]: /FF7/Field/Script/Opcodes/19%20IFUWL.md "wikilink"
  [`24`` ``WAIT`]: /FF7/Field/Script/Opcodes/24%20WAIT.md "wikilink"
  [`30`` ``IFKEY`]: /FF7/Field/Script/Opcodes/30%20IFKEY.md "wikilink"
  [`31`` ``IFKEYON`]: /FF7/Field/Script/Opcodes/31%20IFKEYON.md "wikilink"
  [`32`` ``IFKEYOFF`]: /FF7/Field/Script/Opcodes/32%20IFKEYOFF.md "wikilink"
  [`5F`` ``NOP`]: /FF7/Field/Script/Opcodes/5F%20NOP.md "wikilink"
  [`CB`` ``IFPRTYQ`]: /FF7/Field/Script/Opcodes/CB%20IFPRTYQ.md "wikilink"
  [`CC`` ``IFMEMBQ`]: /FF7/Field/Script/Opcodes/CC%20IFMEMBQ.md "wikilink"
  [`0E`` ``DSKCG`]: /FF7/Field/Script/Opcodes/0E%20DSKCG.md "wikilink"
  [`0F`` ``SPECIAL`]: /FF7/Field/Script/Opcodes/0F%20SPECIAL.md "wikilink"
  [`20`` ``MINIGAME`]: /FF7/Field/Script/Opcodes/20%20MINIGAME.md "wikilink"
  [`22`` ``BTMD2`]: /FF7/Field/Script/Opcodes/22%20BTMD2.md "wikilink"
  [`23`` ``BTRLD`]: /FF7/Field/Script/Opcodes/23%20BTRLD.md "wikilink"
  [`4B`` ``BTLTB`]: /FF7/Field/Script/Opcodes/4B%20BTLTB.md "wikilink"
  [`60`` ``MAPJUMP`]: /FF7/Field/Script/Opcodes/60%20MAPJUMP.md "wikilink"
  [`6E`` ``LSTMP`]: /FF7/Field/Script/Opcodes/6E%20LSTMP.md "wikilink"
  [`70`` ``BATTLE`]: /FF7/Field/Script/Opcodes/70%20BATTLE.md "wikilink"
  [`71`` ``BTLON`]: /FF7/Field/Script/Opcodes/71%20BTLON.md "wikilink"
  [`72`` ``BTLMD`]: /FF7/Field/Script/Opcodes/72%20BTLMD.md "wikilink"
  [`D2`` ``MPJPO`]: /FF7/Field/Script/Opcodes/D2%20MPJPO.md "wikilink"
  [`FF`` ``GAMEOVER`]: /FF7/Field/Script/Opcodes/FF%20GAMEOVER.md "wikilink"
  [`76`` ``PLUS!`]: /FF7/Field/Script/Opcodes/76%20PLUS!.md "wikilink"
  [`77`` ``PLUS2!`]: /FF7/Field/Script/Opcodes/77%20PLUS2!.md "wikilink"
  [`78`` ``MINUS!`]: /FF7/Field/Script/Opcodes/78%20MINUS!.md "wikilink"
  [`79`` ``MINUS2!`]: /FF7/Field/Script/Opcodes/79%20MINUS2!.md "wikilink"
  [`7A`` ``INC!`]: /FF7/Field/Script/Opcodes/7A%20INC!.md "wikilink"
  [`7B`` ``INC2!`]: /FF7/Field/Script/Opcodes/7B%20INC2!.md "wikilink"
  [`7C`` ``DEC!`]: /FF7/Field/Script/Opcodes/7C%20DEC!.md "wikilink"
  [`7D`` ``DEC2!`]: /FF7/Field/Script/Opcodes/7D%20DEC2!.md "wikilink"
  [`7F`` ``RDMSD`]: /FF7/Field/Script/Opcodes/7F%20RDMSD.md "wikilink"
  [`80`` ``SETBYTE`]: /FF7/Field/Script/Opcodes/80%20SETBYTE.md "wikilink"
  [`81`` ``SETWORD`]: /FF7/Field/Script/Opcodes/81%20SETWORD.md "wikilink"
  [`82`` ``BITON`]: /FF7/Field/Script/Opcodes/82%20BITON.md "wikilink"
  [`83`` ``BITOFF`]: /FF7/Field/Script/Opcodes/83%20BITOFF.md "wikilink"
  [`84`` ``BITXOR`]: /FF7/Field/Script/Opcodes/84%20BITXOR.md "wikilink"
  [`85`` ``PLUS`]: /FF7/Field/Script/Opcodes/85%20PLUS.md "wikilink"
  [`86`` ``PLUS2`]: /FF7/Field/Script/Opcodes/86%20PLUS2.md "wikilink"
  [`87`` ``MINUS`]: /FF7/Field/Script/Opcodes/87%20MINUS.md "wikilink"
  [`88`` ``MINUS2`]: /FF7/Field/Script/Opcodes/88%20MINUS2.md "wikilink"
  [`89`` ``MUL`]: /FF7/Field/Script/Opcodes/89%20MUL.md "wikilink"
  [`8A`` ``MUL2`]: /FF7/Field/Script/Opcodes/8A%20MUL2.md "wikilink"
  [`8B`` ``DIV`]: /FF7/Field/Script/Opcodes/8B%20DIV.md "wikilink"
  [`8C`` ``DIV2`]: /FF7/Field/Script/Opcodes/8C%20DIV2.md "wikilink"
  [`8D`` ``MOD`]: /FF7/Field/Script/Opcodes/8D%20MOD.md "wikilink"
  [`8E`` ``MOD2`]: /FF7/Field/Script/Opcodes/8E%20MOD2.md "wikilink"
  [`8F`` ``AND`]: /FF7/Field/Script/Opcodes/8F%20AND.md "wikilink"
  [`90`` ``AND2`]: /FF7/Field/Script/Opcodes/90%20AND2.md "wikilink"
  [`91`` ``OR`]: /FF7/Field/Script/Opcodes/91%20OR.md "wikilink"
  [`92`` ``OR2`]: /FF7/Field/Script/Opcodes/92%20OR2.md "wikilink"
  [`93`` ``XOR`]: /FF7/Field/Script/Opcodes/93%20XOR.md "wikilink"
  [`94`` ``XOR2`]: /FF7/Field/Script/Opcodes/94%20XOR2.md "wikilink"
  [`95`` ``INC`]: /FF7/Field/Script/Opcodes/95%20INC.md "wikilink"
  [`96`` ``INC2`]: /FF7/Field/Script/Opcodes/96%20INC2.md "wikilink"
  [`97`` ``DEC`]: /FF7/Field/Script/Opcodes/97%20DEC.md "wikilink"
  [`98`` ``DEC2`]: /FF7/Field/Script/Opcodes/98%20DEC2.md "wikilink"
  [`99`` ``RANDOM`]: /FF7/Field/Script/Opcodes/99%20RANDOM.md "wikilink"
  [`9A`` ``LBYTE`]: /FF7/Field/Script/Opcodes/9A%20LBYTE.md "wikilink"
  [`9B`` ``HBYTE`]: /FF7/Field/Script/Opcodes/9B%20HBYTE.md "wikilink"
  [`9C`` ``2BYTE`]: /FF7/Field/Script/Opcodes/9C%202BYTE.md "wikilink"
  [`D4`` ``SIN`]: /FF7/Field/Script/Opcodes/D4%20SIN.md "wikilink"
  [`D5`` ``COS`]: /FF7/Field/Script/Opcodes/D5%20COS.md "wikilink"
  [`21`` ``TUTOR`]: /FF7/Field/Script/Opcodes/21%20TUTOR.md "wikilink"
  [`2E`` ``WCLS`]: /FF7/Field/Script/Opcodes/2E%20WCLS.md "wikilink"
  [`2F`` ``WSIZW`]: /FF7/Field/Script/Opcodes/2F%20WSIZW.md "wikilink"
  [`36`` ``WSPCL`]: /FF7/Field/Script/Opcodes/36%20WSPCL.md "wikilink"
  [`37`` ``WNUMB`]: /FF7/Field/Script/Opcodes/37%20WNUMB.md "wikilink"
  [`38`` ``STTIM`]: /FF7/Field/Script/Opcodes/38%20STTIM.md "wikilink"
  [`40`` ``MESSAGE`]: /FF7/Field/Script/Opcodes/40%20MESSAGE.md "wikilink"
  [`41`` ``MPARA`]: /FF7/Field/Script/Opcodes/41%20MPARA.md "wikilink"
  [`42`` ``MPRA2`]: /FF7/Field/Script/Opcodes/42%20MPRA2.md "wikilink"
  [`43`` ``MPNAM`]: /FF7/Field/Script/Opcodes/43%20MPNAM.md "wikilink"
  [`48`` ``ASK`]: /FF7/Field/Script/Opcodes/48%20ASK.md "wikilink"
  [`49`` ``MENU`]: /FF7/Field/Script/Opcodes/49%20MENU.md "wikilink"
  [`4A`` ``MENU2`]: /FF7/Field/Script/Opcodes/4A%20MENU2.md "wikilink"
  [`50`` ``WINDOW`]: /FF7/Field/Script/Opcodes/50%20WINDOW.md "wikilink"
  [`51`` ``WMOVE`]: /FF7/Field/Script/Opcodes/51%20WMOVE.md "wikilink"
  [`52`` ``WMODE`]: /FF7/Field/Script/Opcodes/52%20WMODE.md "wikilink"
  [`53`` ``WREST`]: /FF7/Field/Script/Opcodes/53%20WREST.md "wikilink"
  [`54`` ``WCLSE`]: /FF7/Field/Script/Opcodes/54%20WCLSE.md "wikilink"
  [`55`` ``WROW`]: /FF7/Field/Script/Opcodes/55%20WROW.md "wikilink"
  [`56`` ``GWCOL`]: /FF7/Field/Script/Opcodes/56%20GWCOL.md "wikilink"
  [`57`` ``SWCOL`]: /FF7/Field/Script/Opcodes/57%20SWCOL.md "wikilink"
  [`0A`` ``SPTYE`]: /FF7/Field/Script/Opcodes/0A%20SPTYE.md "wikilink"
  [`0B`` ``GTPYE`]: /FF7/Field/Script/Opcodes/0B%20GTPYE.md "wikilink"
  [`39`` ``GOLDu`]: /FF7/Field/Script/Opcodes/39%20GOLDu.md "wikilink"
  [`3A`` ``GOLDd`]: /FF7/Field/Script/Opcodes/3A%20GOLDd.md "wikilink"
  [`3B`` ``CHGLD`]: /FF7/Field/Script/Opcodes/3B%20CHGLD.md "wikilink"
  [`3C`` ``HMPMAX1`]: /FF7/Field/Script/Opcodes/3C%20HMPMAX1.md "wikilink"
  [`3D`` ``HMPMAX2`]: /FF7/Field/Script/Opcodes/3D%20HMPMAX2.md "wikilink"
  [`3E`` ``MHMMX`]: /FF7/Field/Script/Opcodes/3E%20MHMMX.md "wikilink"
  [`3F`` ``HMPMAX3`]: /FF7/Field/Script/Opcodes/3F%20HMPMAX3.md "wikilink"
  [`45`` ``MPu`]: /FF7/Field/Script/Opcodes/45%20MPu.md "wikilink"
  [`47`` ``MPd`]: /FF7/Field/Script/Opcodes/47%20MPd.md "wikilink"
  [`4D`` ``HPu`]: /FF7/Field/Script/Opcodes/4D%20HPu.md "wikilink"
  [`4F`` ``HPd`]: /FF7/Field/Script/Opcodes/4F%20HPd.md "wikilink"
  [`58`` ``STITM`]: /FF7/Field/Script/Opcodes/58%20STITM.md "wikilink"
  [`59`` ``DLITM`]: /FF7/Field/Script/Opcodes/59%20DLITM.md "wikilink"
  [`5A`` ``CKITM`]: /FF7/Field/Script/Opcodes/5A%20CKITM.md "wikilink"
  [`5B`` ``SMTRA`]: /FF7/Field/Script/Opcodes/5B%20SMTRA.md "wikilink"
  [`5C`` ``DMTRA`]: /FF7/Field/Script/Opcodes/5C%20DMTRA.md "wikilink"
  [`5D`` ``CMTRA`]: /FF7/Field/Script/Opcodes/5D%20CMTRA.md "wikilink"
  [`74`` ``GETPC`]: /FF7/Field/Script/Opcodes/74%20GETPC.md "wikilink"
  [`C8`` ``PRTYP`]: /FF7/Field/Script/Opcodes/C8%20PRTYP.md "wikilink"
  [`C9`` ``PRTYM`]: /FF7/Field/Script/Opcodes/C9%20PRTYM.md "wikilink"
  [`CA`` ``PRTYE`]: /FF7/Field/Script/Opcodes/CA%20PRTYE.md "wikilink"
  [`CD`` ``MMBud`]: /FF7/Field/Script/Opcodes/CD%20MMBud.md "wikilink"
  [`CE`` ``MMBLK`]: /FF7/Field/Script/Opcodes/CE%20MMBLK.md "wikilink"
  [`CF`` ``MMBUK`]: /FF7/Field/Script/Opcodes/CF%20MMBUK.md "wikilink"
  [`08`` ``JOIN`]: /FF7/Field/Script/Opcodes/08%20JOIN.md "wikilink"
  [`09`` ``SPLIT`]: /FF7/Field/Script/Opcodes/09%20SPLIT.md "wikilink"
  [`26`` ``BLINK`]: /FF7/Field/Script/Opcodes/26%20BLINK.md "wikilink"
  [`28`` ``KAWAI`]: /FF7/Field/Script/Opcodes/28%20KAWAI.md "wikilink"
  [`29`` ``KAWIW`]: /FF7/Field/Script/Opcodes/29%20KAWIW.md "wikilink"
  [`2A`` ``PMOVA`]: /FF7/Field/Script/Opcodes/2A%20PMOVA.md "wikilink"
  [`2B`` ``SLIP`]: /FF7/Field/Script/Opcodes/2B%20SLIP.md "wikilink"
  [`33`` ``UC`]: /FF7/Field/Script/Opcodes/33%20UC.md "wikilink"
  [`34`` ``PDIRA`]: /FF7/Field/Script/Opcodes/34%20PDIRA.md "wikilink"
  [`35`` ``PTURA`]: /FF7/Field/Script/Opcodes/35%20PTURA.md "wikilink"
  [`6D`` ``IDLCK`]: /FF7/Field/Script/Opcodes/6D%20IDLCK.md "wikilink"
  [`73`` ``PGTDR`]: /FF7/Field/Script/Opcodes/73%20PGTDR.md "wikilink"
  [`75`` ``PXYZI`]: /FF7/Field/Script/Opcodes/75%20PXYZI.md "wikilink"
  [`7E`` ``TLKON`]: /FF7/Field/Script/Opcodes/7E%20TLKON.md "wikilink"
  [`A0`` ``PC`]: /FF7/Field/Script/Opcodes/A0%20PC.md "wikilink"
  [`A1`` ``CHAR`]: /FF7/Field/Script/Opcodes/A1%20CHAR.md "wikilink"
  [`A2`` ``DFANM`]: /FF7/Field/Script/Opcodes/A2%20DFANM.md "wikilink"
  [`A3`` ``ANIME1`]: /FF7/Field/Script/Opcodes/A3%20ANIME1.md "wikilink"
  [`A4`` ``VISI`]: /FF7/Field/Script/Opcodes/A4%20VISI.md "wikilink"
  [`A5`` ``XYZI`]: /FF7/Field/Script/Opcodes/A5%20XYZI.md "wikilink"
  [`A6`` ``XYI`]: /FF7/Field/Script/Opcodes/A6%20XYI.md "wikilink"
  [`A7`` ``XYZ`]: /FF7/Field/Script/Opcodes/A7%20XYZ.md "wikilink"
  [`A8`` ``MOVE`]: /FF7/Field/Script/Opcodes/A8%20MOVE.md "wikilink"
  [`A9`` ``CMOVE`]: /FF7/Field/Script/Opcodes/A9%20CMOVE.md "wikilink"
  [`AA`` ``MOVA`]: /FF7/Field/Script/Opcodes/AA%20MOVA.md "wikilink"
  [`AB`` ``TURA`]: /FF7/Field/Script/Opcodes/AB%20TURA.md "wikilink"
  [`AC`` ``ANIMW`]: /FF7/Field/Script/Opcodes/AC%20ANIMW.md "wikilink"
  [`AD`` ``FMOVE`]: /FF7/Field/Script/Opcodes/AD%20FMOVE.md "wikilink"
  [`AE`` ``ANIME2`]: /FF7/Field/Script/Opcodes/AE%20ANIME2.md "wikilink"
  [`AF`` ``ANIM!1`]: /FF7/Field/Script/Opcodes/AF%20ANIM!1.md "wikilink"
  [`B0`` ``CANIM1`]: /FF7/Field/Script/Opcodes/B0%20CANIM1.md "wikilink"
  [`B1`` ``CANM!1`]: /FF7/Field/Script/Opcodes/B1%20CANM!1.md "wikilink"
  [`B2`` ``MSPED`]: /FF7/Field/Script/Opcodes/B2%20MSPED.md "wikilink"
  [`B3`` ``DIR`]: /FF7/Field/Script/Opcodes/B3%20DIR.md "wikilink"
  [`B4`` ``TURNGEN`]: /FF7/Field/Script/Opcodes/B4%20TURNGEN.md "wikilink"
  [`B5`` ``TURN`]: /FF7/Field/Script/Opcodes/B5%20TURN.md "wikilink"
  [`B6`` ``DIRA`]: /FF7/Field/Script/Opcodes/B6%20DIRA.md "wikilink"
  [`B7`` ``GETDIR`]: /FF7/Field/Script/Opcodes/B7%20GETDIR.md "wikilink"
  [`B8`` ``GETAXY`]: /FF7/Field/Script/Opcodes/B8%20GETAXY.md "wikilink"
  [`B9`` ``GETAI`]: /FF7/Field/Script/Opcodes/B9%20GETAI.md "wikilink"
  [`BA`` ``ANIM!2`]: /FF7/Field/Script/Opcodes/BA%20ANIM!2.md "wikilink"
  [`BB`` ``CANIM2`]: /FF7/Field/Script/Opcodes/BB%20CANIM2.md "wikilink"
  [`BC`` ``CANM!2`]: /FF7/Field/Script/Opcodes/BC%20CANM!2.md "wikilink"
  [`BD`` ``ASPED`]: /FF7/Field/Script/Opcodes/BD%20ASPED.md "wikilink"
  [`BF`` ``CC`]: /FF7/Field/Script/Opcodes/BF%20CC.md "wikilink"
  [`C0`` ``JUMP`]: /FF7/Field/Script/Opcodes/C0%20JUMP.md "wikilink"
  [`C1`` ``AXYZI`]: /FF7/Field/Script/Opcodes/C1%20AXYZI.md "wikilink"
  [`C2`` ``LADER`]: /FF7/Field/Script/Opcodes/C2%20LADER.md "wikilink"
  [`C3`` ``OFST`]: /FF7/Field/Script/Opcodes/C3%20OFST.md "wikilink"
  [`C4`` ``OFSTW`]: /FF7/Field/Script/Opcodes/C4%20OFSTW.md "wikilink"
  [`C5`` ``TALKR`]: /FF7/Field/Script/Opcodes/C5%20TALKR.md "wikilink"
  [`C6`` ``SLIDR`]: /FF7/Field/Script/Opcodes/C6%20SLIDR.md "wikilink"
  [`C7`` ``SOLID`]: /FF7/Field/Script/Opcodes/C7%20SOLID.md "wikilink"
  [`D0`` ``LINE`]: /FF7/Field/Script/Opcodes/D0%20LINE.md "wikilink"
  [`D1`` ``LINON`]: /FF7/Field/Script/Opcodes/D1%20LINON.md "wikilink"
  [`D3`` ``SLINE`]: /FF7/Field/Script/Opcodes/D3%20SLINE.md "wikilink"
  [`D6`` ``TLKR2`]: /FF7/Field/Script/Opcodes/D6%20TLKR2.md "wikilink"
  [`D7`` ``SLDR2`]: /FF7/Field/Script/Opcodes/D7%20SLDR2.md "wikilink"
  [`DC`` ``CCANM`]: /FF7/Field/Script/Opcodes/DC%20CCANM.md "wikilink"
  [`DB`` ``FCFIX`]: /FF7/Field/Script/Opcodes/DB%20FCFIX.md "wikilink"
  [`DD`` ``ANIMB`]: /FF7/Field/Script/Opcodes/DD%20ANIMB.md "wikilink"
  [`DE`` ``TURNW`]: /FF7/Field/Script/Opcodes/DE%20TURNW.md "wikilink"
  [`27`` ``BGMOVIE`]: /FF7/Field/Script/Opcodes/27%20BGMOVIE.md "wikilink"
  [`2C`` ``BGPDH`]: /FF7/Field/Script/Opcodes/2C%20BGPDH.md "wikilink"
  [`2D`` ``BGSCR`]: /FF7/Field/Script/Opcodes/2D%20BGSCR.md "wikilink"
  [`DF`` ``MPPAL`]: /FF7/Field/Script/Opcodes/DF%20MPPAL.md "wikilink"
  [`E0`` ``BGON`]: /FF7/Field/Script/Opcodes/E0%20BGON.md "wikilink"
  [`E1`` ``BGOFF`]: /FF7/Field/Script/Opcodes/E1%20BGOFF.md "wikilink"
  [`E2`` ``BGROL`]: /FF7/Field/Script/Opcodes/E2%20BGROL.md "wikilink"
  [`E3`` ``BGROL2`]: /FF7/Field/Script/Opcodes/E3%20BGROL2.md "wikilink"
  [`E4`` ``BGCLR`]: /FF7/Field/Script/Opcodes/E4%20BGCLR.md "wikilink"
  [`E5`` ``STPAL`]: /FF7/Field/Script/Opcodes/E5%20STPAL.md "wikilink"
  [`E6`` ``LDPAL`]: /FF7/Field/Script/Opcodes/E6%20LDPAL.md "wikilink"
  [`E7`` ``CPPAL`]: /FF7/Field/Script/Opcodes/E7%20CPPAL.md "wikilink"
  [`E8`` ``RTPAL`]: /FF7/Field/Script/Opcodes/E8%20RTPAL.md "wikilink"
  [`E9`` ``ADPAL`]: /FF7/Field/Script/Opcodes/E9%20ADPAL.md "wikilink"
  [`EA`` ``MPPAL2`]: /FF7/Field/Script/Opcodes/EA%20MPPAL2.md "wikilink"
  [`EB`` ``STPLS`]: /FF7/Field/Script/Opcodes/EB%20STPLS.md "wikilink"
  [`EC`` ``LDPLS`]: /FF7/Field/Script/Opcodes/EC%20LDPLS.md "wikilink"
  [`ED`` ``CPPAL2`]: /FF7/Field/Script/Opcodes/ED%20CPPAL2.md "wikilink"
  [`EE`` ``RTPAL2`]: /FF7/Field/Script/Opcodes/EE%20RTPAL2.md "wikilink"
  [`EF`` ``ADPAL2`]: /FF7/Field/Script/Opcodes/EF%20ADPAL2.md "wikilink"
  [`25`` ``NFADE`]: /FF7/Field/Script/Opcodes/25%20NFADE.md "wikilink"
  [`5E`` ``SHAKE`]: /FF7/Field/Script/Opcodes/5E%20SHAKE.md "wikilink"
  [`61`` ``SCRLO`]: /FF7/Field/Script/Opcodes/61%20SCRLO.md "wikilink"
  [`62`` ``SCRLC`]: /FF7/Field/Script/Opcodes/62%20SCRLC.md "wikilink"
  [`63`` ``SCRLA`]: /FF7/Field/Script/Opcodes/63%20SCRLA.md "wikilink"
  [`64`` ``SCR2D`]: /FF7/Field/Script/Opcodes/64%20SCR2D.md "wikilink"
  [`65`` ``SCRCC`]: /FF7/Field/Script/Opcodes/65%20SCRCC.md "wikilink"
  [`66`` ``SCR2DC`]: /FF7/Field/Script/Opcodes/66%20SCR2DC.md "wikilink"
  [`67`` ``SCRLW`]: /FF7/Field/Script/Opcodes/67%20SCRLW.md "wikilink"
  [`68`` ``SCR2DL`]: /FF7/Field/Script/Opcodes/68%20SCR2DL.md "wikilink"
  [`6B`` ``FADE`]: /FF7/Field/Script/Opcodes/6B%20FADE.md "wikilink"
  [`6C`` ``FADEW`]: /FF7/Field/Script/Opcodes/6C%20FADEW.md "wikilink"
  [`6F`` ``SCRLP`]: /FF7/Field/Script/Opcodes/6F%20SCRLP.md "wikilink"
  [`DA`` ``AKAO2`]: /FF7/Field/Script/Opcodes/DA%20AKAO2.md "wikilink"
  [`F0`` ``MUSIC`]: /FF7/Field/Script/Opcodes/F0%20MUSIC.md "wikilink"
  [`F1`` ``SOUND`]: /FF7/Field/Script/Opcodes/F1%20SOUND.md "wikilink"
  [`F2`` ``AKAO`]: /FF7/Field/Script/Opcodes/F2%20AKAO.md "wikilink"
  [`F3`` ``MUSVT`]: /FF7/Field/Script/Opcodes/F3%20MUSVT.md "wikilink"
  [`F4`` ``MUSVM`]: /FF7/Field/Script/Opcodes/F4%20MUSVM.md "wikilink"
  [`F5`` ``MULCK`]: /FF7/Field/Script/Opcodes/F5%20MULCK.md "wikilink"
  [`F6`` ``BMUSC`]: /FF7/Field/Script/Opcodes/F6%20BMUSC.md "wikilink"
  [`F7`` ``CHMPH`]: /FF7/Field/Script/Opcodes/F7%20CHMPH.md "wikilink"
  [`F8`` ``PMVIE`]: /FF7/Field/Script/Opcodes/F8%20PMVIE.md "wikilink"
  [`F9`` ``MOVIE`]: /FF7/Field/Script/Opcodes/F9%20MOVIE.md "wikilink"
  [`FA`` ``MVIEF`]: /FF7/Field/Script/Opcodes/FA%20MVIEF.md "wikilink"
  [`FB`` ``MVCAM`]: /FF7/Field/Script/Opcodes/FB%20MVCAM.md "wikilink"
  [`FC`` ``FMUSC`]: /FF7/Field/Script/Opcodes/FC%20FMUSC.md "wikilink"
  [`FD`` ``CMUSC`]: /FF7/Field/Script/Opcodes/FD%20CMUSC.md "wikilink"
  [`FE`` ``CHMST`]: /FF7/Field/Script/Opcodes/FE%20CHMST.md "wikilink"
  [`69`` ``MPDSP`]: /FF7/Field/Script/Opcodes/69%20MPDSP.md "wikilink"
  [`6A`` ``VWOFT`]: /FF7/Field/Script/Opcodes/6A%20VWOFT.md "wikilink"
  [`9D`` ``SETX`]: /FF7/Field/Script/Opcodes/9D%20SETX.md "wikilink"
  [`9E`` ``GETX`]: /FF7/Field/Script/Opcodes/9E%20GETX.md "wikilink"
  [`9F`` ``SEARCHX`]: /FF7/Field/Script/Opcodes/9F%20SEARCHX.md "wikilink"
  [`D8`` ``PMJMP`]: /FF7/Field/Script/Opcodes/D8%20PMJMP.md "wikilink"
  [`D9`` ``PMJMP2`]: /FF7/Field/Script/Opcodes/D9%20PMJMP2.md "wikilink"
