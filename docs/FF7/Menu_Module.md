---
title: Menu_Module
---

## Menu Overview

### Important Files

|   PSX Version    |       PC Version        |
|:----------------:|:-----------------------:|
|   /MENU/\*.MNU   | /DATA/MENU/MENU_US.LGP  |
| /INIT/WINDOW.BIN | /DATA/KERNEL/WINDOW.BIN |

The menu module is probably the second most powerful module in the game. From here you can set a multitude of environment variables and view character records directly. It's really more of a master variable controller than the "select-o-thing" it appears to be.

Because the menu can have some rather fancy and complicated management features, it also can be placed in "Tutorial mode". This mode, when called from the field module will "play" prerecorded menu selections for the player.

Another major function of the menu system is the ability to save your game. This is probably the most powerful and vital part as the Menu has access to every single variable in the system, excluding the script temporary variables.

The Menu module is actually a collection of 13 modules, to which 4 can be called from the field scripting language. The 13 are called Begin, Party, Item, Magic, Eqip, Stat, Change, Limit, Config, Form, Save, Name, and Shop.

## Menu Initialization

Menu has the incredible honor of being initialized right after the kernel. It is also the only module that keeps permanent data in VRAM for other modules to access. In the case of the PSX version, the graphics are loaded out of /INIT/WINDOW.BIN. This is a BIN-GZIP archive described in the Kernel section of this document. WINDOW.BIN has the following format.

| Offset | Length     |       Description       |
|--------|------------|:-----------------------:|
| 0x0000 | 6 bytes    | Header \[0x4827208200\] |
| 0x0006 | 1062 bytes |  Static Menu textures   |
| 0x2754 | 3034 bytes |      Font texture       |
| 0x332E | 163 bytes  |         Unknown         |

After initialization, the first Menu module ran is "Begin" The following is a picture of "Begin" in VRAM. Things to note is the font and static menu textures from /INIT/WINNDOW.BIN are highlighted in the lower right hand corner.

![Menu_Windowbin.jpg]({{site.baseurl}}/assets/Menu_Windowbin.jpg)

The following is an expanded picture of the textures from the PC version. The PSX version only differs in texture size and the way the buttons are displayed.

![Menu_PC_Textures.jpg]({{site.baseurl}}/assets/Menu_PC_Textures.jpg)

To better see what each section is, here is an annotated version with the more obvious textures labeled.

![Menu_PCT_Annotated.jpg]({{site.baseurl}}/assets/Menu_PCT_Annotated.jpg)

This is never banked out, however small parts are overwritten and cashed for a while when Battle is loaded, but are overwritten again when menu is loaded. The large blank spot under the menu text is for the Japanese characters that were removed in the non-Japanese version of the game. This spot is unused in these versions.

## Menu Modules

The 13 Modules are displayed like the following.

### Begin

This is the begin menu.

![Menu_Begin.jpg]({{site.baseurl}}/assets/Menu_Begin.jpg)

This is a screen form the "save" module. Begin initializes the menu system and calls save to load a game or to start the game.

### Party

![Menu_Party.jpg]({{site.baseurl}}/assets/Menu_Party.jpg)

This is the menu you see when you manually enter the menu system. Things to note is the empty box in the lower screen shows what location you are in. Debug rooms have no name most of the time.

### Item

This is the item menu.

![Menu_Item.jpg]({{site.baseurl}}/assets/Menu_Item.jpg)

### Magic

This is the magic menu.

![Menu_Magic.jpg]({{site.baseurl}}/assets/Menu_Magic.jpg)

Both magic and summon are accessed in the same module.

### Equip

The equip menu is a little strange.

![Menu_Equip.jpg]({{site.baseurl}}/assets/Menu_Equip.jpg)

Equip and Materia are in the same module.

### Status

This is the status menu.

![Menu_Status.jpg]({{site.baseurl}}/assets/Menu_Status.jpg)

### Change

![Menu_Change.jpg]({{site.baseurl}}/assets/Menu_Change.jpg)

Also known as "Order", this is the simplest and smallest of all the menu modules, it just changes the order of the party, it uses the party screen as a background.

### Limit

This is the limit menu.

![Menu_Limit.jpg]({{site.baseurl}}/assets/Menu_Limit.jpg)

### Config

![Menu_Config.jpg]({{site.baseurl}}/assets/Menu_Config.jpg)

This is where a good deal of environment variables can be changed.

### Form

This is also known as the PHS screen.

![Menu_Form.jpg]({{site.baseurl}}/assets/Menu_Form.jpg)

Form can also be called when you need to make a two or three teams of people.

### Save

The all important save screen.

![Menu_Save.jpg]({{site.baseurl}}/assets/Menu_Save.jpg)

To save time, this will only load the first 80 bytes of each save as a preview. It allows a quick look without having to load the whole memory card, which can take upward of a minute. This is also responsible for loading games too, when called from "Begin".

### Name

This is the naming screen.

![Menu_Name.jpg]({{site.baseurl}}/assets/Menu_Name.jpg)

If you try and use the same name screen twice in a game, you will loose your old name and will be overwritten with the default one.

### Shop

This is your typical shop.

![Menu_Shop.jpg]({{site.baseurl}}/assets/Menu_Shop.jpg)

You can, of course, sell items from this module as well.

## Calling the various menus

The PSX version keeps the menu modules contained in a .MNU file. The PC version has the menu code internal to the executable. The highlighted modules can be called with the MENU script command. The MENU command always takes a first argument of 00. The second argument is the Menu ID number, and the third is the argument.

| Module Name | PSX Filename       | Menu ID Number | Argument                   |
|-------------|--------------------|:--------------:|----------------------------|
| Begin       | /MENU/BGINMENU.MNU |      N/A       | N/A                        |
| Party       | /MENU/PATYMENU.MNU |      0x09      | 0x00                       |
| Item        | /MENU/ITEMMENU.MNU |      N/A       | N/A                        |
| Magic       | /MENU/MGICMENU.MNU |      N/A       | N/A                        |
| Equip       | /MENU/EQIPMENU.MNU |      N/A       | N/A                        |
| Status      | /MENU/STATMENU.MNU |      N/A       | N/A                        |
| Change      | /MENU/CHNGMENU.MNU |      N/A       | N/A                        |
| Limit       | /MENU/LIMTMENU.MNU |      N/A       | N/A                        |
| Config      | /MENU/CNFGMENU.MNU |      N/A       | N/A                        |
| Form        | /MENU/FORMMENU.MNU |      0x07      | 0x00 - Make a party of 3   |
|             |                    |                | 0x01 - Split into 3 groups |
|             |                    |                | 0x02 - Split into 2 groups |
| Save        | /MENU/SAVEMENU.MNU |      0x0E      | 0x00                       |
| Name        | /MENU/NAMEMENU.MNU |      0x06      | 0x00 - Cloud               |
|             |                    |                | 0x01 - Barret              |
|             |                    |                | 0x02 - Tifa                |
|             |                    |                | 0x03 - Aerith              |
|             |                    |                | 0x04 - Red XII             |
|             |                    |                | 0x05 - Yuffie              |
|             |                    |                | 0x06 - Cait Sith           |
|             |                    |                | 0x07 - Vincent             |
|             |                    |                | 0x08 - Cid                 |
|             |                    |                | 0x09 - Chocobo             |
| Shop        | /MENU/SHOPMENU.MNU |      0x08      | (0x00-0xFF) Shop Number    |

## Menu dependencies

On the PSX, Menu dependencies are kept in two different directories. The window dressing textures that stay in memory are found in /INIT/WINDOW.BIN and stored as a BIN-GZIP archive. In the MENU directory, some MNU files contain TIM files appended at the end that are displayed when they are loaded. Two of them, PARTYMENU.MNU and FORMMENU.MNU, externally reference TIM files on the disk as they share these resources. SAVEMENU.MNU also externally references the memory card ports.

The PC version has the MNU files internal to the executable and only have external resources. These are kept within the MENU_US.LGP file. The PC version has textures in two different sizes to support the two resolutions the game runs in. The following is a table of the menu resources and where they are located in both the PC and PSX version.

<table>
<thead>
<tr>
<th><p>Picture</p></th>
<th><p>Description</p></th>
<th><p>Low Resolution<br />
PC Filename</p></th>
<th><p>High Resolution<br />
PC Filename</p></th>
<th><p>PSX Location (in<br />
/MENU unless noted)</p></th>
<th><p>TIM Offset</p></th>
</tr>
</thead>
<tbody>
<tr>
<td></td>
<td><p>Cloud Avatar</p></td>
<td><p>CLOUD_L.TEX</p></td>
<td><p>CLOUD.TEX</p></td>
<td><p>CLOUD.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Barret Avatar</p></td>
<td><p>BARRE_L.TEX</p></td>
<td><p>BARRE.TEX</p></td>
<td><p>BARRE.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Tifa Avatar</p></td>
<td><p>TIFA_L.TEX</p></td>
<td><p>TIFA.TEX</p></td>
<td><p>TIFA.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Cloud Avatar</p></td>
<td><p>CLOUD_L.TEX</p></td>
<td><p>CLOUD.TEX</p></td>
<td><p>CLOUD.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Aeris Avatar</p></td>
<td><p>EARITH_L.TEX</p></td>
<td><p>EARITH.TEX</p></td>
<td><p>EARITH.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Red XIII Avatar</p></td>
<td><p>RED_L.TEX</p></td>
<td><p>RED.TEX</p></td>
<td><p>RED.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Yuffie Avatar</p></td>
<td><p>YUFI_L.TEX</p></td>
<td><p>YUFI.TEX</p></td>
<td><p>YUFI.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Cait Sith Avatar</p></td>
<td><p>KETC_L.TEX</p></td>
<td><p>KETC.TEX</p></td>
<td><p>KETC.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Vincent Avatar</p></td>
<td><p>BINS_L.TEX</p></td>
<td><p>BINS.TEX</p></td>
<td><p>BINS.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Cid Avatar</p></td>
<td><p>CIDO_L.TEX</p></td>
<td><p>CIDO.TEX</p></td>
<td><p>CIDO_L.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Young Cloud Avatar</p></td>
<td><p>PCLOUD_L.TEX</p></td>
<td><p>PCLOUD.TEX</p></td>
<td><p>PCLOUD.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Sephiroth Avatar</p></td>
<td><p>PCEFI_L.TEX</p></td>
<td><p>PCEFI.TEX</p></td>
<td><p>PCEFI.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Chocobo Avatar</p></td>
<td><p>CHOCO_L.TEX</p></td>
<td><p>CHOCO.TEX</p></td>
<td><p>CHOCO.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td></td>
<td><p>Placeholder Avatar</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>KALI.TIM</p></td>
<td><p>N/A</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Cloud Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>CLOUD_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>CLOUD.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x1E7C</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Barret Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>BARRE_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>BARRE.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x29A0</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Tifa Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>TIFA_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>TIFA.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x34C4</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Aeris Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>EARITH_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>EARITH.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x3FE8</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Red XIII Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>RED_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>RED.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x4B0C</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Yuffie Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>YUFI_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>YUFI.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x5630</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Cait Sith Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>KETC_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>KETC.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x6154</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Vincent Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>BINS_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>BINS.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x6C78</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Cid Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>CIDO_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>CIDO.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x779C</p></td>
</tr>
<tr>
<td style="background: rgb(230,230,255)"></td>
<td style="background: rgb(230,230,255)"><p>Chocobo Avatar</p></td>
<td style="background: rgb(230,230,255)"><p>CHOCO_L.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>CHOCO.TEX</p></td>
<td style="background: rgb(230,230,255)"><p>NAMEMENU.MNU</p></td>
<td style="background: rgb(230,230,255)"><p>0x82C0</p></td>
</tr>
<tr>
<td></td>
<td><p>Load screen background</p></td>
<td><p>BUSTER.TEX</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x4EDC</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 1</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0xF4F4</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 2</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0xF502</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 3</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0xF8F8</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 4</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0xFCEE</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 5</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x100E4</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 6</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x104DA</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 7</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x108DA</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 8</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x10CC6</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 9</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x110BC</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 10</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x114B2</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 11</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x118A8</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 12</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x11C9E</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 13</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x12094</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 14</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x1248A</p></td>
</tr>
<tr>
<td></td>
<td><p>Save Icon 15</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>SAVEMENU.MNU</p></td>
<td><p>0x12880</p></td>
</tr>
<tr>
<td></td>
<td><p>Coin command</p></td>
<td><p>ZENI.TEX</p></td>
<td><p>ZENI_H.TEX</p></td>
<td><p>ITEMMENU.MNU</p></td>
<td><p>0x3890</p></td>
</tr>
<tr>
<td rowspan="8" style="background: rgb(255,255,255)"></td>
<td rowspan="8" style="background: rgb(255,255,255)"><p>Window Dressings</p></td>
<td><p>BTL_WIN_H.TEX</p></td>
<td><p>BTL_WIN_A_H.TEX</p></td>
<td rowspan="8" style="background: rgb(255,255,255)"><p>/INIT/WINDOW.BIN</p></td>
<td rowspan="8" style="background: rgb(255,255,255)"><p>0x0006</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_B_H.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_C_H.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_D_H.TEX</p></td>
</tr>
<tr>
<td><p>BTL_WIN_L.TEX</p></td>
<td><p>BTL_WIN_A_L.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_B_L.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_C_L.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>BTL_WIN_D_L.TEX</p></td>
</tr>
<tr>
<td rowspan="4" style="background: rgb(255,255,255)"></td>
<td rowspan="4" style="background: rgb(255,255,255)"><p>Menu Font</p></td>
<td><p>USFONT_L.TEX</p></td>
<td><p>USFONT_A_L.TEX</p></td>
<td rowspan="4" style="background: rgb(255,255,255)"><p>/INIT/WINDOW.BIN</p></td>
<td rowspan="4" style="background: rgb(255,255,255)"><p>0x2754</p></td>
</tr>
<tr>
<td></td>
<td><p>USFONT_B_L.TEX</p></td>
</tr>
<tr>
<td><p>USFONT_H.TEX</p></td>
<td><p>USFONT_A_H.TEX</p></td>
</tr>
<tr>
<td></td>
<td><p>USFONT_B_H.TEX</p></td>
</tr>
</tbody>
</table>

## The Save Game format

The save game format is lengthy; as such you can find the save game format in a seperate section [here](Savemap).
