---
title: Savemap
---

### The Savemap

The following is the general save format for the game. This data excludes the header data that differs between the PSX and PC version. (PSX header is 512 Bytes, checksum @ 0x200) (PC header is 9 bytes, checksum @ 0x11) Note: For the *preview* descriptions below, changing these values does not change any in-game values. These are only used so a player can preview the data within the save file when viewing the Save menu.

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th colspan="2" style="text-align: center; background: rgb(204,204,204);"><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x0000</p></td>
<td><p>2(4) bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Checksum (<a href="http://forums.qhimm.com/index.php?topic=4211.msg60545#msg60545">how to generate</a>)<br />
Technically this is a DWord, but the checksum generation method only stores the lower Word.</p></td>
</tr>
<tr>
<td><p>0x0004</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's level</p></td>
</tr>
<tr>
<td rowspan="2"><p>0x0005</p></td>
<td rowspan="2"><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's portrait</p></td>
</tr>
<tr>
<td style="text-align: center;"><p>0x00: Cloud<br />
0x01: Barret<br />
0x02: Tifa<br />
0x03: Aeris<br />
0x04: Red XIII<br />
0x05: Yuffie<br />
0x06: Cait Sith</p></td>
<td style="text-align: center;"><p>0x07: Vincent<br />
0x08: Cid<br />
0x09: Young Cloud<br />
0x0A: Sephiroth<br />
0x0B: Chocobo<br />
0xFF: None</p></td>
</tr>
<tr>
<td><p>0x0006</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: 2nd character's portrait</p></td>
</tr>
<tr>
<td><p>0x0007</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: 3rd character's portrait</p></td>
</tr>
<tr>
<td><p>0x0008</p></td>
<td><p>16 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's name, <a href="FF_Text" title="wikilink">FF Text format</a> , terminated with 0xFF</p></td>
</tr>
<tr>
<td><p>0x0018</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's current HP</p></td>
</tr>
<tr>
<td><p>0x001A</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's max HP</p></td>
</tr>
<tr>
<td><p>0x001C</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's current MP</p></td>
</tr>
<tr>
<td><p>0x001E</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Lead character's max MP</p></td>
</tr>
<tr>
<td><p>0x0020</p></td>
<td><p>4 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Amount of Gil</p></td>
</tr>
<tr>
<td><p>0x0024</p></td>
<td><p>4 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Total number of seconds played</p></td>
</tr>
<tr>
<td><p>0x0028</p></td>
<td><p>32 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong>Save Preview</strong>: Save location, <a href="FF_Text" title="wikilink">FF Text format</a>, terminated with 0xFF</p></td>
</tr>
<tr>
<td><p>0x0048</p></td>
<td><p>3 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>RGB value for upper left corner of window</p></td>
</tr>
<tr>
<td><p>0x004B</p></td>
<td><p>3 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>RGB value for upper right corner of window</p></td>
</tr>
<tr>
<td><p>0x004E</p></td>
<td><p>3 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>RGB value for lower left corner of window</p></td>
</tr>
<tr>
<td><p>0x0051</p></td>
<td><p>3 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>RGB value for lower right corner of window</p></td>
</tr>
<tr>
<td><p>0x0054</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Cloud</p></td>
</tr>
<tr>
<td><p>0x00D8</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Barret</p></td>
</tr>
<tr>
<td><p>0x015C</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Tifa</p></td>
</tr>
<tr>
<td><p>0x01E0</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Aeris's</p></td>
</tr>
<tr>
<td><p>0x0264</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Red XIII</p></td>
</tr>
<tr>
<td><p>0x02E8</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Yuffie</p></td>
</tr>
<tr>
<td><p>0x036C</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Cait Sith (or Young Cloud)</p></td>
</tr>
<tr>
<td><p>0x03F0</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Vincent (or Sephiroth)</p></td>
</tr>
<tr>
<td><p>0x0474</p></td>
<td><p>132 bytes</p></td>
<td colspan="2" style="text-align: center;"><p><strong><a href="#character-record" title="wikilink">Character Record</a></strong>: Cid</p></td>
</tr>
<tr>
<td><p>0x04F8</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Party member in slot 1 [uses same format as character portrait above]</p></td>
</tr>
<tr>
<td><p>0x04F9</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Party member in slot 2</p></td>
</tr>
<tr>
<td><p>0x04FA</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Party member in slot 3</p></td>
</tr>
<tr>
<td><p>0x04FB</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Alignment (Always 0xFF)</p></td>
</tr>
<tr>
<td><p>0x04FC</p></td>
<td><p>640 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Party Item stock, 2 bytes per item, 320 item slots max [See <a href="#save-item-list" title="wikilink">save item list</a> below]</p></td>
</tr>
<tr>
<td><p>0x077C</p></td>
<td><p>800 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Party Materia stock, 4 bytes per materia, 200 materia max [See <a href="#save-materia-list" title="wikilink">save materia list</a> ]</p></td>
</tr>
<tr>
<td><p>0x0A9C</p></td>
<td><p>192 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Materia stolen by Yuffie, 4 bytes per materia, 48 materia max [See <a href="#save-materia-list" title="wikilink">save materia list</a> ]</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0B5C</p></td>
<td style="background: rgb(255,205,154)"><p>32 bytes</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,205,154);"><p>z_3 Unknown (Always 0xFF?)</p></td>
</tr>
<tr>
<td><p>0x0B7C</p></td>
<td><p>4 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Party's Gil amount</p></td>
</tr>
<tr>
<td><p>0x0B80</p></td>
<td><p>4 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Total number of seconds played</p></td>
</tr>
<tr>
<td><p>0x0B84</p></td>
<td><p>4 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Countdown Timer (in seconds)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-bottom: 1px solid #FF9A33"><p>0x0B88</p></td>
<td style="background: rgb(255,205,154); border-bottom: 1px solid #FF9A33"><p>12 bytes</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,205,154); border-bottom: 1px solid #FF9A33;"><p>z_4 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0B88<br />
z_4[0]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>4 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>Used to calculate fractions of seconds (1/65535) of Game timer (0x0B80).<br />
Technically this is a DWord, but only the lower Word is used.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0B8C<br />
z_4[4]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>4 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>Used to calculate fractions of seconds (1/65535) of Countdown timer (0x0B84).<br />
Share the same value with 0x0B88.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0B90<br />
z_4[8]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>4 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>This is set along with Current map value (0x0B94).<br />
If Current module value is 1, this is set to 2.<br />
If Current module value is 3, this is set to 0.<br />
Technically this is a DWord, but only the lower Byte is used.</p></td>
</tr>
<tr>
<td><p>0x0B94</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Current <a href="Engine_basics" title="wikilink">module</a><br />
If value is 1, the game was saved in the field.<br />
If value is 3, the game was saved in the world map.</p></td>
</tr>
<tr>
<td><p>0x0B96</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Current location</p></td>
</tr>
<tr>
<td><p>0x0B98</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Alignment (Always 0x00)</p></td>
</tr>
<tr>
<td><p>0x0B9A</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>X location on Field map (Signed)</p></td>
</tr>
<tr>
<td><p>0x0B9C</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Y location on Field map (Signed)</p></td>
</tr>
<tr>
<td><p>0x0B9E</p></td>
<td><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Triangle Id of player on Field map (Unsigned)</p></td>
</tr>
<tr>
<td><p>0x0BA0</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Direction of Player Model on Field Map(Unsigned)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-bottom: 1px solid #FF9A33"><p>0x0BA1</p></td>
<td style="background: rgb(255,205,154); border-bottom: 1px solid #FF9A33"><p>3 bytes</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,205,154); border-bottom: 1px solid #FF9A33;"><p>z_6 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0BA1<br />
z_6[0]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>1 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>Field Encounter Timer: StepID/Seed (<a href="http://web.archive.org/web/20170518233623/http://forums.qhimm.com/index.php?topic=6431.msg81091#msg81091">[1</a>])</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0BA2<br />
z_6[1]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>1 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>Field Encounter Timer: Offset (<a href="http://web.archive.org/web/20170518233623/http://forums.qhimm.com/index.php?topic=9625.msg191219#msg191219">[2</a>])</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154); border-top: 1px dashed"><p>0x0BA3<br />
z_6[2]</p></td>
<td style="background: rgb(255,255,204); border-top: 1px dashed; border-left: 1px dashed; border-right: 1px dashed"><p>1 byte</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,255,204); border-top: 1px dashed;"><p>Alignment (Always 0x00)</p></td>
</tr>
<tr>
<td style="background: rgb(205,205,154)"><p>0x0BA4</p></td>
<td style="background: rgb(205,205,154)"></td>
<td colspan="2" style="text-align: center; background: rgb(205,205,154);"><p>[BEGINNING OF FIELD SCRIPT MEMORY <a href="#save-memory-bank-1.2f2" title="wikilink">BANK 1 (1/2)</a>]</p></td>
</tr>
<tr>
<td style="background: rgb(205,205,154)"><p>0x0CA4</p></td>
<td style="background: rgb(205,205,154)"></td>
<td colspan="2" style="text-align: center; background: rgb(205,205,154);"><p>[BEGINNING OF FIELD SCRIPT MEMORY <a href="#save-memory-bank-3.2f4" title="wikilink">BANK 2 (3/4)</a>]</p></td>
</tr>
<tr>
<td style="background: rgb(205,205,154)"><p>0x0DA4</p></td>
<td style="background: rgb(205,205,154)"></td>
<td colspan="2" style="text-align: center; background: rgb(205,205,154);"><p>[BEGINNING OF FIELD SCRIPT MEMORY <a href="#save-memory-bank-b.2fc" title="wikilink">BANK 3 (B/C)</a>]</p></td>
</tr>
<tr>
<td style="background: rgb(205,205,154)"><p>0x0EA4</p></td>
<td style="background: rgb(205,205,154)"></td>
<td colspan="2" style="text-align: center; background: rgb(205,205,154);"><p>[BEGINNING OF FIELD SCRIPT MEMORY <a href="#save-memory-bank-d.2fe" title="wikilink">BANK 4 (D/E)</a>]</p></td>
</tr>
<tr>
<td style="background: rgb(205,205,154)"><p>0x0FA4</p></td>
<td style="background: rgb(205,205,154)"></td>
<td colspan="2" style="text-align: center; background: rgb(205,205,154);"><p>[BEGINNING OF FIELD SCRIPT MEMORY <a href="#save-memory-bank-7.2ff" title="wikilink">BANK 5 (7/F)</a>]</p></td>
</tr>
<tr>
<td rowspan="2"><p>0x10A4</p></td>
<td rowspan="2"><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>PHS Locking Mask (1: Locked)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><table>
<tbody>
<tr>
<td style="background: rgb(68,144,205)"><p>LSB</p></td>
<td style="background: rgb(205,205,230)"><p>Cloud</p></td>
<td style="background: rgb(205,205,230)"><p>Barret</p></td>
<td style="background: rgb(205,205,230)"><p>Tifa</p></td>
<td style="background: rgb(205,205,230)"><p>Aeris</p></td>
<td style="background: rgb(205,205,230)"><p>Red</p></td>
<td style="background: rgb(205,205,230)"><p>Yuffie</p></td>
<td style="background: rgb(205,205,230)"><p>Vincent</p></td>
<td style="background: rgb(205,205,230)"><p>Cait</p></td>
<td style="background: rgb(205,205,230)"><p>Cid</p></td>
<td style="background: rgb(68,144,205)"><p>MSB</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr>
<td rowspan="2"><p>0x10A6</p></td>
<td rowspan="2"><p>2 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>PHS Visibility Mask (does not <em>turn off</em> party characters)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><table>
<tbody>
<tr>
<td style="background: rgb(68,144,205)"><p>LSB</p></td>
<td style="background: rgb(205,205,230)"><p>Cloud</p></td>
<td style="background: rgb(205,205,230)"><p>Barret</p></td>
<td style="background: rgb(205,205,230)"><p>Tifa</p></td>
<td style="background: rgb(205,205,230)"><p>Aeris</p></td>
<td style="background: rgb(205,205,230)"><p>Red</p></td>
<td style="background: rgb(205,205,230)"><p>Yuffie</p></td>
<td style="background: rgb(205,205,230)"><p>Vincent</p></td>
<td style="background: rgb(205,205,230)"><p>Cait</p></td>
<td style="background: rgb(205,205,230)"><p>Cid</p></td>
<td style="background: rgb(68,144,205)"><p>MSB</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x10A8</p></td>
<td style="background: rgb(255,205,154)"><p>48 bytes</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,205,154);"><p>z_39 Unknown (Always 0x00?)</p></td>
</tr>
<tr>
<td><p>0x10D8</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Battle Speed (0x00: fastest, 0xFF: slowest)</p></td>
</tr>
<tr>
<td><p>0x10D9</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Battle Message Speed</p></td>
</tr>
<tr>
<td rowspan="5"><p>0x10DA</p></td>
<td rowspan="5"><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>General configuration</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Sound: mono (0x00); stereo (0x01)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Controller: normal (0x00); customize (0x04)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Cursor: initial (0x00); memory (0x10)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>ATB: Active (0x00); Recommended (0x40); Wait (0x80)</p></td>
</tr>
<tr>
<td rowspan="4"><p>0x10DB</p></td>
<td rowspan="4"><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>General configuration (continued)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Camera angle: Auto (0x00); Fix (0x01)</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Magic order: (game crashes if flag set to 0x18 or 0x1C)<br />
"1. restore attack indirect" (0x00)<br />
"2. restore indirect attack" (0x04)<br />
"3. attack indirect restore" (0x08)<br />
"4. attack restore indirect" (0x0C)<br />
"5. indirect restore attack" (0x10)<br />
"6. indirect attack restore" (0x14)<br />
</p></td>
</tr>
<tr>
<td colspan="2" style="text-align: center;"><p>Extra battle window displaying information: Inactive (0x00); Active (0x40)</p></td>
</tr>
<tr>
<td><p>0x10DC</p></td>
<td><p>16 bytes</p></td>
<td colspan="2" style="text-align: center;"><p>Controller Mapping (PSX ONLY)<br />
l2,r2,l1,r1,tri,circle,cross,square,Select,?,?,Start,u,r,d,l<br />
l2,r2,l1,r1,Menu,OK,Cancel,Ext,Help,?,?,Pause,u,r,d,l</p></td>
</tr>
<tr>
<td><p>0x10EC</p></td>
<td><p>1 byte</p></td>
<td colspan="2" style="text-align: center;"><p>Message Speed</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x10ED</p></td>
<td style="background: rgb(255,205,154)"><p>7 bytes</p></td>
<td colspan="2" style="text-align: center; background: rgb(255,205,154);"><p>z_40 Unknown (Always 0x00?)</p></td>
</tr>
</tbody>
</table>

## Save Memory Bank 1/2

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x0BA4<br />
<em>B[1][0]</em></p></td>
<td><p>2 byte</p></td>
<td><p>Main progress variable</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BA6<br />
<em>B[1][2]</em><br />
z_7[0]</p></td>
<td><p>1 Byte</p></td>
<td><p>Yuffie's Initial Level (z_7 Unknown) Byte value before Yuffie join the team: 0x00.<br />
(If byte's value is changed, then you can't fight Yuffie, so she can't be obtained).<br />
Yuffie's Initial Level only is set when she already join the team.<br />
Credit to <a href="../Savemap" title="wikilink">(NFITC1)</a></p></td>
</tr>
<tr>
<td><p>0x0BA7<br />
<em>B[1][3]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Aeris' current love points</p></td>
</tr>
<tr>
<td><p>0x0BA8<br />
<em>B[1][4]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Tifa's current love points</p></td>
</tr>
<tr>
<td><p>0x0BA9<br />
<em>B[1][5]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Yuffie's current love points</p></td>
</tr>
<tr>
<td><p>0x0BAA<br />
<em>B[1][6]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Barret's current love points</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BAB<br />
<em>B[1][7]</em></p></td>
<td style="background: rgb(255,205,154)"><p>17 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_8 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BAB<br />
<em>B[1][7]</em><br />
z_8[0]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>1<sup>st</sup> temp party member char ID placeholder<br />
This is used to store the player's party configuration before they are overridden for a special event that requires a specific character setup using GTPYE. {elm/first/s1}<br />
The player's original party configuration can then be set back to its original setup using SPTYE. {elminn_2/ballet/s11}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BAC<br />
<em>B[1][8]</em><br />
z_8[1]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>2<sup>nd</sup> temp party member char ID placeholder<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BAD<br />
<em>B[1][9]</em><br />
z_8[2]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>3<sup>ed</sup> temp party member char ID placeholder<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BAE<br />
<em>B[1][10]</em><br />
z_8[3]</p></td>
<td style="background: rgb(255,205,154)"><p>6 byte</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB4<br />
<em>B[1][16]</em><br />
z_8[9]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Game Timer Hours</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB5<br />
<em>B[1][17]</em><br />
z_8[10]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Game Timer Minutes</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB6<br />
<em>B[1][18]</em><br />
z_8[11]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Game Timer Seconds</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB7<br />
<em>B[1][19]</em><br />
z_8[12]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Game Timer Frames. From 0x00 to ~0x21 in one sec.(33 FPS?)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB8<br />
<em>B[1][20]</em><br />
z_8[13]</p></td>
<td style="background: rgb(254,254,255)"><p>1 bytes</p></td>
<td style="background: rgb(254,254,255)"><p>Countdown Timer Hours</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BB9<br />
<em>B[1][21]</em><br />
z_8[14]</p></td>
<td style="background: rgb(254,254,255)"><p>1 bytes</p></td>
<td style="background: rgb(254,254,255)"><p>Countdown Timer Minutes</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BBA<br />
<em>B[1][22]</em><br />
z_8[15]</p></td>
<td style="background: rgb(254,254,255)"><p>1 bytes</p></td>
<td style="background: rgb(254,254,255)"><p>Countdown Timer Seconds</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BBB<br />
<em>B[1][23]</em><br />
z_8[16]</p></td>
<td style="background: rgb(254,254,255)"><p>1 bytes</p></td>
<td style="background: rgb(254,254,255)"><p>Countdown Timer Frames. From 0 to 30 (dec) in one sec.</p></td>
</tr>
<tr>
<td><p>0x0BBC<br />
<em>B[1][24]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Number of battles fought</p></td>
</tr>
<tr>
<td><p>0x0BBE<br />
<em>B[1][26]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Number of escapes</p></td>
</tr>
<tr>
<td rowspan="2"><p>0x0BC0<br />
<em>B[1][28]</em></p></td>
<td rowspan="2"><p>2 bytes</p></td>
<td><p>Menu Visiblity Mask (Quit not affected)</p></td>
</tr>
<tr>
<td><table>
<tbody>
<tr>
<td style="background: rgb(68,144,205)"><p>LSB</p></td>
<td style="background: rgb(205,205,230)"><p>item</p></td>
<td style="background: rgb(205,205,230)"><p>magic</p></td>
<td style="background: rgb(205,205,230)"><p>materia</p></td>
<td style="background: rgb(205,205,230)"><p>equip</p></td>
<td style="background: rgb(205,205,230)"><p>status</p></td>
<td style="background: rgb(205,205,230)"><p>order</p></td>
<td style="background: rgb(205,205,230)"><p>limit</p></td>
<td style="background: rgb(205,205,230)"><p>config</p></td>
<td style="background: rgb(205,205,230)"><p>PHS</p></td>
<td style="background: rgb(205,205,230)"><p>save</p></td>
<td style="background: rgb(68,144,205)"><p>MSB</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr>
<td rowspan="2"><p>0x0BC2<br />
<em>B[1][30]</em><br />
</p></td>
<td rowspan="2"><p>2 bytes</p></td>
<td><p>Menu Locking Mask (1: Locked) (Quit not affected)</p></td>
</tr>
<tr>
<td><table>
<tbody>
<tr>
<td style="background: rgb(68,144,205)"><p>LSB</p></td>
<td style="background: rgb(205,205,230)"><p>item</p></td>
<td style="background: rgb(205,205,230)"><p>magic</p></td>
<td style="background: rgb(205,205,230)"><p>materia</p></td>
<td style="background: rgb(205,205,230)"><p>equip</p></td>
<td style="background: rgb(205,205,230)"><p>status</p></td>
<td style="background: rgb(205,205,230)"><p>order</p></td>
<td style="background: rgb(205,205,230)"><p>limit</p></td>
<td style="background: rgb(205,205,230)"><p>config</p></td>
<td style="background: rgb(205,205,230)"><p>PHS</p></td>
<td style="background: rgb(205,205,230)"><p>save</p></td>
<td style="background: rgb(68,144,205)"><p>MSB</p></td>
</tr>
</tbody>
</table></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BC4<br />
<em>B[1][32]</em></p></td>
<td style="background: rgb(255,205,154)"><p>16 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_9 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BC4<br />
<em>B[1][32]</em><br />
z_9[0]</p></td>
<td style="background: rgb(255,205,154)"><p>4 byte</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BC8<br />
<em>B[1][36]</em><br />
z_9[4]</p></td>
<td><p>1 byte</p></td>
<td><p>Field Items, Sector 7 Train Graveyard<br />
Item bit mask (<a href="../Bit_numbering" title="wikilink">LBS</a>) (applied when you pick them up).<br />
Bit=0(Item on the floor), Bit=1(Item Picked Up).<br />
0x01: Hi-Potion.(mds7st1|Barrel 1)<br />
0x02: Echo Screen.(mds7st1|Barrel 2)<br />
0x04: Potion.(mds7st2|Floor 2)<br />
0x08: Ether.(mds7st2|Floor 3)<br />
0x10: Hi-Potion.(mds7st1|Roof Train 1)<br />
0x20: Potion.(mds7st1|Inside Train 2)<br />
0x40: Potion.(mds7st1|Floor 1)<br />
0x80: Hi-Potion.(mds7st2|Roof Train 2)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BC9<br />
<em>B[1][37]</em><br />
z_9[5]</p></td>
<td><p>1 byte</p></td>
<td><p>Field Items<br />
0x01: Elixir {hyou8_2/tr00/s1}<br />
0x02: Potion {hyou5_1/tr00/s1}<br />
0x04: Safety Bit {hyou5_3/trbox/s1}<br />
0x08: Mind Source {hyou2/trbox/s1}<br />
0x10: Sneak Glove {mkt_w/event/s1}<br />
0x20: Premium Heart {mkt_ia/event/s3}{mkt_ia/line00/s4}<br />
0x40: Unused<br />
0x80: Unused<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BCA<br />
<em>B[1][38]</em><br />
z_9[6]</p></td>
<td style="background: rgb(255,205,154)"><p>10 byte</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td><p>0x0BD4<br />
<em>B[1][48]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Item bit mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you pick them up). Field Item / Materia<br />
Bit=0(Item on the floor), Bit=1(Item Picked Up).<br />
0x01: Potion {md8_3/p/s1}<br />
0x02: Potion + Phoenix Down {ealin_2/zu/s1}<br />
0x04: Ether {eals_1/p/s1}<br />
0x08: Cover Materia {eals_1/mp/s1}<br />
0x10: Choco-Mog Summon {farm/dancer/s1}<br />
0x20: Sense Materia {mds6_22/mat/s1}<br />
0x40: Ramuh Summon {crcin_2/mat/s1}<br />
0x80: Mythril Key Item {zz1/m1/s1}<br />
</p></td>
</tr>
<tr>
<td><p>0x0BD5<br />
<em>B[1][49]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Materia Cave / Northern Cave (Item bit mask)<br />
0x01: Mime Materia {zz5/l1,l2,l3,l4/s1}<br />
0x02: HP&lt;-&gt;MP Materia {zz6/mat/s1}<br />
0x04: Quadra Magic Materia {zz7/l1,l2,l3,l4/s1}<br />
0x08: Knights of the Round Summon {zz8/l1,l2,l3,l4/s1}<br />
0x10: Elixir {las3_1/hako1/s1}{las4_0/cid/s1}<br />
0x20: X-Potion {las3_1/hako2/s1}<br />
0x40: Turbo Ether {las3_2/hako1/s1}{las4_0/tifa/s1}{las4_0/cait/s1}<br />
0x80: Vaccine {las3_2/hako2/s1}{las4_0/yufi/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BD6<br />
<em>B[1][50]</em></p></td>
<td style="background: rgb(255,205,154)"><p>14 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_10 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BD6<br />
<em>B[1][50]</em><br />
z_10[0]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items Northern Cave<br />
0x01: Magic Counter Materia {las3_2/mat/s1}<br />
0x02: Speed Source {las3_3/hako1/s1}{las4_0/red/s1}<br />
0x04: Turbo Ether {las3_3/hako2/s1}<br />
0x08: X-Potion {las3_3/hako3/s1}<br />
0x10: Mega All {las3_3/mat/s3}{las4_0/vincent/s1}<br />
0x20: Luck Source {las4_1/hako1/s1}<br />
0x40: Remedy {las3_1/hako3/s1}{las4_0/ballet/s1}<br />
0x80: Bolt Ring {zz1/m1/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BD7<br />
<em>B[1][51]</em><br />
z_10[1]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items<br />
0x01: Gold Armlet {zz2/m/s8}<br />
0x02: Great Gospel {zz2/m/s7}<br />
0x04: Shooting Coaster prize Umbrella {jetin1/dic/s0}<br />
0x08: Shooting Coaster prize Flayer {jetin1/dic/s0}<br />
0x10: Death Penalty + Chaos {zz4/buki/s1}<br />
0x20: Elixir {ghotin_2/reizo/s1}<br />
0x40: Enemy Skill animation displayed {zz3/mat/s3}<br />
0x80: Enemy Skill {zz3/mat/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BD8<br />
<em>B[1][52]</em><br />
z_10[2]</p></td>
<td style="background: rgb(255,255,204)"><p>4 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BDC<br />
<em>B[1][56]</em><br />
z_10[6]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items, Sector 7 Wall Market and Shinra HQ<br />
Item bit mask (<a href="../Bit_numbering" title="wikilink">LBS</a>) (applied when you pick them up).<br />
Bit=0(Item on the floor), Bit=1(Item Picked Up).<br />
0x01: Ether.(Corneo's masion basement floor) {colne_4/TAKARA/s1}<br />
0x02: Hyper.(Corneo's masion corneo 's bedroom floor) {colne_6/TAKARA/s1}<br />
0x04: Phoenix Down (Corneo's masion 2nd floor right room) {colne_3/TAKARA/s1}<br />
0x08: Elixir at Shinra HQ stairs {blinst_2/TAKARA/s1}<br />
0x10: Unused<br />
0x20: Magic Source {cosmin7/TAKARA/s1}<br />
0x40: First Midgar Part Key Item {blin65_1/PARTA/s1}<br />
0x80: Second Midgar Part at Shinra HQ {blin65_1/PARTB/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BDD<br />
<em>B[1][57]</em><br />
z_10[7]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items, Shinra HQ<br />
Item bit mask (<a href="../Bit_numbering" title="wikilink">LBS</a>) (applied when you pick them up).<br />
Bit=0(Item on the floor), Bit=1(Item Picked Up).<br />
0x01: Third Midgar Part Key Item {blin65_1/PARTC/s1}<br />
0x02: Fourth Midgar Part Key Item {blin65_1/PARTD/s1}<br />
0x04: Fifth Midgar Part Key Item {blin65_1/PARTE/s1}<br />
0x08: Keycard 66 Key Item {blin65_1/TAKARA/s1}<br />
0x10: All Materia {shpin_2/TAKARAA/s1}<br />
0x20: Ether {shpin_2/TAKARAB/s1}<br />
0x40: Wind Slash {shpin_3/TAKARA/s1}<br />
0x80: Fairy Ring {gidun_4/TAKARAA/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BDE<br />
<em>B[1][58]</em><br />
z_10[8]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items<br />
0x01: X-Potion {gidun_4/TAKARAB/s1}<br />
0x02: Added Effect Materia {gidun_1/TAKARAA/s1}<br />
0x04: Black M-phone {gidun_2/TAKARAA/s1}<br />
0x08: Ether {gidun_2/TAKARAB/s1}<br />
0x10: Elixir {cosmin6/TAKARA/s1}<br />
0x20: HP Absorb Materia {hideway3/TAKARA/s4}<br />
0x40: Magic Shuriken {hideway1/TAKARA/s4}<br />
0x80: Hairpin {hideway2/TAKARA/s4}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BDF<br />
<em>B[1][59]</em><br />
z_10[9]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>Field Items<br />
0x01: Keycard 62 Key Item {blin61/ZAKOA/s1}<br />
0x02: MP Absorb Materia {uta_im/TAKARAA/s1}<br />
0x04: Swift Bolt {uttmpin4/TAKARAA/s1}<br />
0x08: Elixir {uttmpin4/TAKARAB/s1}<br />
0x10: Pile Bunker {blin2_i/TAKARAA/s1}<br />
0x20: Master Fist {blin2_i/TAKARAB/s1}<br />
0x40: Behemoth Horn {blinst_2/TAKARB/s1}<br />
0x80: Full Cure Materia {cosmin7/TAKARAA/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BE0<br />
<em>B[1][60]</em><br />
z_10[10]</p></td>
<td style="background: rgb(255,255,204)"><p>4 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td><p>0x0BE4<br />
<em>B[1][64]</em></p></td>
<td><p>8 bytes</p></td>
<td><p>Key items [see Key Item List]</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BEC<br />
<em>B[1][72]</em></p></td>
<td style="background: rgb(255,205,154)"><p>8 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_11 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BEC<br />
<em>B[1][72]</em><br />
z_11[0]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252"><p>Northern Cave - Progress (TODO: more info)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BED<br />
<em>B[1][73]</em><br />
z_11[1]</p></td>
<td style="background: rgb(255,205,154)"><p>1 byte</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BEE<br />
<em>B[1][74]</em><br />
z_11[2]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave - Progress (TODO: more info)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BEF<br />
<em>B[1][75]</em><br />
z_11[3]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Items mask, Chocobo Farm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Activated right after getting Choco-Mog{farm/mat/s1}(Is set by kernel, not from Field) (See 0x0BD4[4])<br />
0x02: Activated right after getting Enemy Skill {blin68_2/mtr/s1}(Is set by kernel, not from Field) (See 0x0FC6[2])<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BF0<br />
<em>B[1][76]</em><br />
z_11[4]</p></td>
<td style="background: rgb(255,205,154)"><p>4 byte</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown (Always 0x00?)<br />
</p></td>
</tr>
<tr>
<td><p>0x0BF4<br />
<em>B[1][80]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Aeris battle love points</p></td>
</tr>
<tr>
<td><p>0x0BF5<br />
<em>B[1][81]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Tifa battle love points</p></td>
</tr>
<tr>
<td><p>0x0BF6<br />
<em>B[1][82]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Yuffie battle love points</p></td>
</tr>
<tr>
<td><p>0x0BF7<br />
<em>B[1][83]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Barret battle love points</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BF8<br />
<em>B[1][84]</em></p></td>
<td style="background: rgb(255,205,154)"><p>1 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_12 Unknown</p></td>
</tr>
<tr>
<td><p>0x0BF9<br />
<em>B[1][85]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Rating for Penned Chocobo Number 1 (01: Wonderful -&gt; 08: Worst)</p></td>
</tr>
<tr>
<td><p>0x0BFA<br />
<em>B[1][86]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Rating for Penned Chocobo Number 2</p></td>
</tr>
<tr>
<td><p>0x0BFB<br />
<em>B[1][87]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Rating for Penned Chocobo Number 3</p></td>
</tr>
<tr>
<td><p>0x0BFC<br />
<em>B[1][88]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Rating for Penned Chocobo Number 4</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0BFD<br />
<em>B[1][89]</em></p></td>
<td style="background: rgb(255,205,154)"><p>2 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_13 Unknown</p></td>
</tr>
<tr>
<td><p>0x0BFF<br />
<em>B[1][91]</em></p></td>
<td><p>3 bytes</p></td>
<td><p>Ultimate Weapon's remaining HP</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C02<br />
<em>B[1][94]</em></p></td>
<td style="background: rgb(255,205,154)"><p>28 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_14 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C02<br />
<em>B[1][94]</em><br />
z_14[0]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave, bit mask<br />
0x01: Set if Dragon Zombie has used Pandora's Box<br />
0x02: Unknown<br />
0x04: Northern Cave - Progress (TODO: more info)<br />
0x08: Unknown<br />
0x10: Unknown<br />
0x20: Northern Cave - Bizarro Sephiroth Battle Progress: Second time you switch between party groups in battle change to 0xE0.<br />
0x40: Northern Cave - Bizarro Sephiroth Battle Progress: First time you switch between party groups in battle change to 0xC0.<br />
0x80: Northern Cave - Bizarro Sephiroth Battle Progress: Set to 0x80 on Bizarro Sephiroth battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C14<br />
<em>B[1][112]</em><br />
z_14[18]</p></td>
<td style="background: rgb(225,236,252)"><p>2 bytes</p></td>
<td style="background: rgb(225,236,252)"><p>Current Battle Points (Battle Square)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C18<br />
<em>B[1][116]</em><br />
z_14[22]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Current Number of Battles Won (Battle Square)</p></td>
</tr>
<tr>
<td><p>0x0C1E<br />
<em>B[1][122]</em></p></td>
<td><p>1 bytes</p></td>
<td><p>Needs more research. (bit=0: show tutorial. bit=1: hide tutorial.)<br />
0x01: Junnon Parade (Jump to map junone22) {junonr1/evl0/s3}<br />
0x02: Space Animation displayed {rcktin7/space/s3}<br />
0x04: Grey Submarine Tutorial already seen?<br />
0x08: Forgotten City Animation displayed {loslake1/ev1/s3}<br />
0x10: unknown<br />
0x20: Snow Area Tutorial already seen?<br />
0x40: Display Field Help<br />
0x80: Bizarro Sephiroth Battle, set if main group is currently fighting.<br />
</p></td>
</tr>
<tr>
<td><p>0x0C1F<br />
<em>B[1][123]</em></p></td>
<td><p>1 bytes</p></td>
<td><p>Weapons Killed<br />
0x01: Ultimate Weapon killed (enables Special Battles at Battle Sq) {COLOIN1/s2/s1}<br />
0x04: Ultima Weapon's HP &lt; 20,000<br />
0x08: Ruby Weapon<br />
0x10: Emerald Weapon</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C20<br />
<em>B[1][124]</em></p></td>
<td style="background: rgb(255,205,154)"><p>4 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_15 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C20<br />
<em>B[1][124]</em><br />
z_15[0]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Which Chocobo was taken out from the stable.<br />
00 / 01 - 06 Which stable's Chocobo was taken out. The stable is displayed empty, but still occupied. 00: Chocobo can be taken out even if another Chocobo is exist on world map. - (* Glitch) Not 00: Chocobo cannot be taken out even if no Chocobo is exist on world map.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C21<br />
<em>B[1][125]</em><br />
z_15[1]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Riding off wild chocobo dialog options.<br />
0x01 Enter direction to Chocobo Farm &amp; Show send/release Wild Chocobo option when riding off. ON: Right of ranch / Show option OFF: In front of cage / Hide option Set to "ON" after buying chocobo stable.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C22<br />
<em>B[1][126]</em><br />
z_15[2]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo display value on world map (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Bit=0(Disabled), Bit=1(Enabled).<br />
Ex: Wild Chocobo (0x01) + Black Chocobo (0x20) = Byte value 0x21<br />
0x01: Caught wild chocobo<br />
0x02: Riding Chocobo<br />
0x04: Yellow<br />
0x08: Green<br />
0x10: Blue<br />
0x20: Black<br />
0x40: Gold<br />
0x80: None?<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C23<br />
<em>B[1][127]</em><br />
z_15[3]</p></td>
<td><p>1 byte</p></td>
<td><p>Vehicle display value on world map (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Note: if disk is different than 1, buggy is invisible.<br />
Bit=0(Disabled), Bit=1(Enabled).<br />
Ex: Buggy (0x01) + Tiny Bronco (0x04) = Byte value 0x05<br />
Byte value 0x00: None<br />
0x01: Buggy<br />
0x02: Buggy (bit=1:Driving it | bit=0: Don't)<br />
0x04: Tiny Bronco<br />
0x08: Unknown/Unused<br />
0x10: Highwind<br />
0x20: Highwind (bit=1: Flying in the sky | bit=0: On the ground)<br />
0x40: Unknown/Unused<br />
0x80: Unknown/Unused<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C24<br />
<em>B[1][128]</em></p></td>
<td style="background: rgb(255,205,154)"><p>97 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_16 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C24<br />
<em>B[1][128]</em><br />
z_16[0]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask, Corel (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Barret talks about his hometown before enter the Ropeway for first time {ROPEST[1][1-Main][49]}<br />
0x02: Free rest in corel inn {NCOINN[0][0-Main][5]}<br />
0x04: Villagers rebuke Barret {NCOREL[13][1][3]}<br />
0x08:<br />
0x10:<br />
0x20: If you couldn't stop the train {NCOREL2[5][2][4]}<br />
0x40: Huge Materia Key Item {NOREL3[1][0-Main][7]}<br />
0x80: Ultima Materia {NCOREL2[2][4][26]}{NCOREL3[24][4][20]}{NCOIN2[8][1][25]}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C25<br />
<em>B[1][129]</em><br />
z_16[1]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Priscilla Warnings (Reset after read): "It gets deeper the farther you go..." or (High Voltage through tower base) {UJUNON2/cloud/s12}<br />
0x02: Oldman: "Young man, do CPR!" {UJUNON4/oldm1/s3}<br />
0x04: Free rest: "You all must be tired. If you want to get some rest, stay here." {JUMIN/drctr/s0}<br />
0x08: Talk with oldm1 about seeing "a man with a black cape" {UJUNON1/cloud/s10}<br />
0x10: Priscilla: "It gets deeper the farther you go..." {UJUNON2/cloud/s12}<br />
0x20: Tifa: "No...it was 5 years ago" {JUMIN/tifa/s9}<br />
0x40: Cloud: "Hey</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C26<br />
<em>B[1][130]</em><br />
z_16[2]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: man1: "It's dangerous, please don't go!" if you choose "I'm still going" {SNOW/man1/s3}<br />
0x02: Snowboard Key Item {SNMIN1/board/s1}<br />
0x04: If you choose to kick Shinra Soldier's butt {SNOW/SINRAH1,SINRAH2,SINRAH3/s2}<br />
0x08: Elena punch Cloud {SNOW/man1/s3}{SNOW/irena/s11}<br />
0x10: Cloud wake-up in Gast home after beeing punched {SNMAYOR/drctr/s0}<br />
0x20: The boy gives you his snowboard {SNMIN1/boy/s1}<br />
0x40: Glacier Map Key Item {SNMIN2/dscvmap/s4}<br />
0x80: First time you do Snowboard {SNOW/playgam/s2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C27<br />
<em>B[1][131]</em><br />
z_16[3]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: If you succeed climbing (to the top, not the cave, just before crater_1 map) {GAIA_32/ladd5/s4}<br />
0x02: If you Push-over the rock {GAIIN_2/icerock/s1}<br />
0x04: Ice Pillar 1 down {GAIIN_5/turara1/s3}<br />
0x08: Ice Pillar 2 down {GAIIN_5/turara2/s3}<br />
0x10: Ice Pillar 3 down {GAIIN_5/turara3/s3}<br />
0x20: Ice Pillar 4 down {GAIIN_5/turara4/s3}<br />
0x40: First time you enter Holzoff's house(2nd room) / If you collaps at the Great Glacier {HOLU_2/drctr/s0}<br />
0x80: History about Yamski and mini Cliff tutorial {HOLU_1/drctr/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C28<br />
<em>B[1][132]</em><br />
z_16[4]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: First time you enter GAIAFOOT map talk {GAIAFOOT/drctr/s0}<br />
0x02:<br />
0x04: Tifa ask you take her with you {CRATER_2/drctr/s0}<br />
0x08: Rufus finds the crater {TRNAD_2/hikutei/s2}<br />
0x10: Sephiroth: "This is the end...for all of you" then his body vanish {TRNAD_4/discver/s2}<br />
0x20:<br />
0x40: Sephiroth illusion Nibelheim{WOA_3/gonivl1,gonivl2,gonivl3/s2}<br />
0x80: First time cloud enter map crater_1 and talk about meteor and the crater {CRATER_1/drctr/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C29<br />
<em>B[1][133]</em><br />
z_16[5]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask, Whirlwind Maze (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: If you give the Black Materia to Barret {TRNAD_1/ballet/s1}<br />
0x02: If you give the Black Materia to {TRNAD_1/red/s1}<br />
0x04: Entrust the Black Materia {TRNAD_1/ballet/s1}<br />
0x08: Tifa tells you need to cross when the wind is calm {WOA_1/setume3/s2}<br />
0x10: 12 Black Cape man down {TRNAD_3/drctr/s0}<br />
0x20: Black Cape man down {WOA_1/drctr/s0}<br />
0x40: Black Cape man down {CRATER_1/blkdown/s4}<br />
0x80: Black Cape man jump off {TRNAD_2/drctr/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C2A<br />
<em>B[1][134]</em><br />
z_16[6]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask, Whirlwind Maze (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Cloud: "What happened to this town? It's so run-down" {UJUNON1/drctr/s0}<br />
0x02: If you have taken the Glacier Map before he offers you to, man3: "What nerve! You already tore down the map."<br />
0x04: Screen shake then Random Battle{GAIIN_6/drctr/s0}<br />
0x08: Shiva Summon in Priscilla's house {PRISILA/sivamt/s1}<br />
0x10: Black Cape man: "Ughâ¦ Errgaahh</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C2B<br />
<em>B[1][135]</em><br />
z_16[7]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Field mask, Whirlwind Maze (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Cid regets about gaving the Huge Materia to the Shinra {NCOREL/worry/s2}<br />
0x02: After Barret finish talking about his hometown history then enters the ropeway {ROPEST/ad/S3}<br />
0x04: Cid tell Prisila they have found Cloud {PRISILA/prisl/s1}<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C44<br />
<em>B[1][160]</em><br />
z_16[32]</p></td>
<td><p>1 byte</p></td>
<td><p>Progress items, Wallmarket (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Bit=0(Item not obtained), Bit=1(Item obtained).<br />
0x01: Cologne at Wallmarket {mktpb/woman2/s1}<br />
0x02: Flower Cologne at Wallmarket {mktpb/woman2/s1}<br />
0x04: Sexy Cologne at Wallmarket {mktpb/woman2/s1}<br />
0x08: Wig at Wallmarket {mkt_mens}<br />
0x10: Dyed Wig at Wallmarket {mkt_mens}<br />
0x20: Blonde Wig at Wallmarket {mkt_mens}<br />
0x40: Pharmacy coupon at Wallmarket {mkt_s2/line01/s3}<br />
0x80: Obtained any Wig at Wallmarket {mkt_mens/event/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C45<br />
<em>B[1][161]</em><br />
z_16[33]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Progress items, Wallmarket (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Bit=0(Item not obtained), Bit=1(Item obtained).<br />
0x01: Girl at Honey Bee Inn put make-up on cloud, poor result (result is random) {onna2/girl1/s3}<br />
0x02: Girl at Honey Bee Inn put make-up on cloud, averange result (result is random) {onna2/girl1/s3}<br />
0x04: Girl at Honey Bee Inn put make-up on cloud, best result (result is random) {onna2/girl1/s3}<br />
0x08: Obtaining the dress at Wallmarket {mkt_s1/event/s2}<br />
0x10: Dress selected (clean/soft,shiny/shimmers) {mktpb/oldm3/s1}<br />
0x20: Cotton Dress [0xCA] {mktpb/oldm3/s1}<br />
0x40: Satin Dress [0xAA] {mktpb/oldm3/s1}<br />
0x80: Silk Dress [0x9A] {mktpb/oldm3/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C46<br />
<em>B[1][162]</em><br />
z_16[34]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Progress items, Wallmarket (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Bit=0(Item not obtained), Bit=1(Item obtained).<br />
0x01: Disinfectant at Wallmarket {mkt_s3/tensyu}<br />
0x02: Deodorant at Wallmarket {mkt_s3/tensyu}<br />
0x04: Digestive at Wallmarket {mkt_s3/tensyu}<br />
0x08: Materia shop owner ask you to get something from the inn vending machine {MKT_M/tensyu/s1}<br />
0x10: 200 gil Item at vending machine in Wallmarket {mktinn/cloud/s4}<br />
0x20: 100 gil Item at vending machine in Wallmarket {mktinn/cloud/s4}<br />
0x40: 50 gil Item at vending machine in Wallmarket {mktinn/cloud/s4}<br />
0x80: Boutique owner's son ask you to bring his father back from bar {mkt_s1/man1/s8}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C47<br />
<em>B[1][163]</em><br />
z_16[35]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Ms. Cloud Bauty level (Don Corneo choice) (0 to 25 Points)<br />
1 Point: Cotton Dress, Wig, Glass Tiara, Cologne, Poor Make-Up<br />
3 Points: Satin Dress, Dyed Wig, Ruby Tiara, Flower Cologne, Averange Make-Up<br />
5 Points: Silk Dress, Blonde Wig, Diamond Tiara, Sexy Cologne, Best Make-Up<br />
Unfinished Calc Script for this items (Not taken into account by point calc):<br />
Lingerie (Should be +1), Mystery panties (+3), Bikini briefs (+5)<br />
2 to 11 Points: Choose Tifa<br />
12 to 18 Points: Choose Aerith<br />
19 or more Points: Choose Cloud<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C48<br />
<em>B[1][164]</em><br />
z_16[36]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Field Objects, Sector 7 Train Graveyard (<a href="../Bit_numbering" title="wikilink">LBS</a>) (so far)<br />
Bit=0(Original Position), Bit=1(Moved).<br />
0x01: Train 1 Position. {mds7st2}<br />
0x02: Train 2 Position. {mds7st2}<br />
0x04: Train 3 Position. {mds7st2}<br />
0x08, 0x10, 0x20, 0x40, 0x80: Unused<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C49<br />
<em>B[1][165]</em><br />
z_16[37]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Field Items, Sector 7 Wall Market<br />
Items bit mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)<br />
0x01: Cloud see the first battery holder and figured out the idea of using a battery there... {wcrimb_1}<br />
0x02: First battery applied up the wall of Wallmarket(0x02){wcrimb_1}<br />
0x04: Second battery applied up the wall of Wallmarket(0x04){wcrimb_1}<br />
0x08:<br />
0x10: Third battery applied and Ether obtained up the wall of Wallmarket (0x10){wcrimb_2}<br />
0x20: Battery (Gun shop batery pack 1/3){MKT_W/oyaji02/s1}<br />
0x40: Battery (Gun shop batery pack 2/3){MKT_W/oyaji02/s1}<br />
0x80: Battery (Gun shop batery pack 3/3){MKT_W/oyaji02/s1}<br />
Note: all 3 batteries get at same time.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4A<br />
<em>B[1][166]</em><br />
z_16[38]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Number of Fort Condor Battles Fought<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4B<br />
<em>B[1][167]</em><br />
z_16[39]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Number of Fort Condor Battles Won<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4C<br />
<em>B[1][168]</em><br />
z_16[40]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress, Fort Condor<br />
0x01: Oldman sited ask your help to protect the Condor [0x01] {convil_1/event/s13}<br />
0x02: If 0x01 &amp;Cloud join them to fight Shinra [0x03] {convil_1/cloud/s18}<br />
0x04: If 0x02 &amp; you talk him again: [0x07] {convil_1/event/s15}<br />
A) He tells you he already talk to the store owners to sell you items.<br />
B) He let you rest for free.<br />
0x08: When set they tell you that there are no more shinra troops to fight[0x0F] {convil_2/event/s4}<br />
0x10: Banished from Fort Condor after loosing the Huge Materia Boss Fight: Party talk {convil_2/event/s11}--&gt;{condor2/init/s0}--&gt;{condor2/event/s3}<br />
0x20: Phoenix Materia (Then Condor fly) {convil_4/ph_mat/s1}<br />
0x40: Condor Born movie() {convil_2/event/s11}<br />
0x80: Banished from Fort Condor after loosing the Huge Materia Boss Fight: Cutted rope {convil_2/event/s11}--&gt;{condor2/init/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4D<br />
<em>B[1][169]</em><br />
z_16[41]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Battle Rank (Battle difficulty), Fort Condor<br />
01: Rank 1 (Battles 1-3)<br />
02: Rank 2 (Battles 4-6)<br />
03: Rank 3 (Battles 7-9)<br />
04: Rank 4 (Battles 10-12)<br />
05: Rank 5 (Battles 13+)<br />
06: Rank 6 (Huge Materia battle)<br />
The Battle Rank set the number of enemies. Fire Catapults enabled from Rank 2, and Tristoners from Rank 3.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4E<br />
<em>B[1][170]</em><br />
z_16[42]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Number of Allies left, Fort Condor<br />
The number of surviving allies units. (The ones that you give in exchange for gil)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C4F<br />
<em>B[1][171]</em><br />
z_16[43]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Number of Enemies killed, Fort Condor<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C50<br />
<em>B[1][172]</em><br />
z_16[44]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Battle result, Fort Condor<br />
00: If you win the battle<br />
01: If you lose the battle</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C51<br />
<em>B[1][173]</em><br />
z_16[45]</p></td>
<td style="background: rgb(225,236,252)"><p>2 bytes</p></td>
<td style="background: rgb(225,236,252)"><p>Game Progres Temp Var, Fort Condor {convil_4/mihari/s1}<br />
When the battle ends, the Game Progres Var (0x0BA4) is copied to this Var.<br />
Is used to check the progresion diff to trigger the new attack event.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C53<br />
<em>B[1][175]</em><br />
z_16[47]</p></td>
<td style="background: rgb(225,236,252)"><p>1 bytes</p></td>
<td style="background: rgb(225,236,252)"><p>Number of Enemies left alive in the battle field, Fort Condor<br />
Set by kernel, not referenced by the field script.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C54<br />
<em>B[1][176]</em><br />
z_16[48]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress, Fort Condor<br />
00: No battle<br />
01: Normal Battle<br />
03: Final Boss Battle<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C55<br />
<em>B[1][177]</em><br />
z_16[49]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress &amp; Battle Reward, Fort Condor<br />
0x01: Condor Progress {convil_1/jijii/s1}<br />
0x02: Condor Progress {convil_1/mihari/s1}{convil_2/mihari/s1}{convil_4/ph_mat/s1}<br />
0x04: Condor Progress {convil_1/event/s19}<br />
0x08: Condor Progress {convil_2/mihari/s1}<br />
0x10: "Received "Magic Comb"!" {convil_2/itemget/s1}<br />
0x20: "Received "Peace Ring"!" {convil_2/itemget/s1}<br />
0x40: "Received "Megalixir"!" {convil_2/itemget/s1}<br />
0x80: "Received "Super Ball"!" {convil_2/itemget/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C56<br />
<em>B[1][178]</em><br />
z_16[50]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress, Fort Condor<br />
0x01:<br />
0x02: If you ever entered the {condor1} map<br />
0x04: If you are inside the Fort<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C57<br />
<em>B[1][179]</em><br />
z_16[51]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Battle modifier linked with 0x0C4D, Fort Condor<br />
0x01: If 0x0C4D &gt;= 2 is set to 1 {convil_2/event/s7}<br />
0x02: If 0x0C4D &gt;= 3 is set to 1 {convil_2/event/s7}<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C58<br />
<em>B[1][180]</em><br />
z_16[52]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Fort Condor Funds</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C5A<br />
<em>B[1][182]</em><br />
z_16[54]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Number of Fort Condor Battles Lost<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C5B<br />
<em>B[1][183]</em><br />
z_16[55]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Speaking to the children near the wall of Wallmarket(0x01)<br />
0x02: Speaking to the children near the wall of Wallmarket(0x02)<br />
0x04: Conversation of children on top of the wall of Wallmarket(0x04)<br />
0x08: Speaking to the child by the pipe in Wallmarket (0x08)<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C5C<br />
<em>B[1][184]</em><br />
z_16[56]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Handle the map jumps to MOVE_S(670),MOVE_I,MOVE_F,MOVE_R,MOVE_U,MOVE_D, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C5D<br />
<em>B[1][185]</em><br />
z_16[57]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress, Great Glacier<br />
0x01: To know if you came from the snowboard course (0=YES,1=NO), if so display the land event: "...So where did we land?..."{hyou2/event/s1}, "We've jumped pretty far..." {hyou3/event/s5}<br />
0x02: To know if you came from the Glacier Map Screen, if so restore your position and set this bit to 0 {hyou1/init/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C5E<br />
<em>B[1][186]</em><br />
z_16[58]</p></td>
<td style="background: rgb(225,236,252)"><p>2 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud MAPID, is used to know where to send you after seeing the Glacier Map, Great Glacier {hyoumap/init/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C60<br />
<em>B[1][188]</em><br />
z_16[60]</p></td>
<td style="background: rgb(225,236,252)"><p>2 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud position (X) right before you use the map, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C62<br />
<em>B[1][190]</em><br />
z_16[62]</p></td>
<td style="background: rgb(225,236,252)"><p>2 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud position (Y) right before you use the map, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C64<br />
<em>B[1][192]</em><br />
z_16[64]</p></td>
<td style="background: rgb(225,236,252)"><p>2 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud position (Z) right before you use the map, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C66<br />
<em>B[1][194]</em><br />
z_16[66]</p></td>
<td style="background: rgb(225,236,252)"><p>2 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud position (triangle ID) right before you use the map, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C68<br />
<em>B[1][196]</em><br />
z_16[68]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Store Cloud direction right before you use the map, then restore it from it, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C69<br />
<em>B[1][197]</em><br />
z_16[69]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Is set to 1 when cloud pass-out, Great Glacier<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C6A<br />
<em>B[1][198]</em><br />
z_16[70]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Cloud Pass-out Counter, Great Glacier<br />
First time you jump to HOLU_1(687), then to HOLU_2(688)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C6B<br />
<em>B[1][199]</em><br />
z_16[71]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Progress &amp; Field item mask, Great Glacier<br />
0x01: When you touch the hot spring (used to get Alexander Summon) {hyou10/event/s3}---&gt;{hyou10/cloud/s4,s5}<br />
0x02: If you ever have spoken to snoww {hyou12/snoww/s1}<br />
0x04: If you lose the battle against the Snow woman (snoww)<br />
0x08: If you win the battle against the Snow woman<br />
0x10: Received "Alexander" Materia{hyou13_2/mt/s1}<br />
0x20: Received "Added Cut" Materia {MOVE_d/mt/s1}<br />
0x40: Received "All" Materia {hyou12/mt/s1}<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C74<br />
<em>B[1][208]</em><br />
z_16[80]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Used to save user anwser in the debugroom {BLACKBG7/leave/s1} before Jump to map blin70_4 (No269)<br />
00: Set along with GameProgress = 0<br />
00: Set along with GameProgress = 1566<br />
00: Set along with GameProgress = 1572<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C75<br />
<em>B[1][209]</em><br />
z_16[81]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Unknown is set to 0 in Wall Market {MRKT2/mapinit/s0}</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C84<br />
<em>B[1][224]</em><br />
z_16[96]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Keeps track of which Shinra floors are unlocked (By picking keycards). Values still unknown.(255 all doors opened when set manualy)</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0C85<br />
<em>B[1][225]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Mission 1st reactor flags.<br />
0x01: elevator on top floor.<br />
0x08: 1st door opened.<br />
0x10: 2nd door opened.<br />
0x20: Jessie free from stuck.<br />
0x40: bomb set.<br />
0x80: set if time is out for gameover check.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0C86<br />
<em>B[1][226]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Mission 1st reactor flags.<br />
0x02: elevator door opened.<br />
0x04: scrolled at map init to show reactor.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0C87<br />
<em>B[1][227]</em></p></td>
<td style="background: rgb(255,205,154)"><p>29/45 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_17 Unknown[0-28] First 29 bytes of 45 (ENDS AT 0x0CB3 16 Bytes into next bank)</p></td>
</tr>
</tbody>
</table>

## Save Memory Bank 3/4

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CA4<br />
<em>B[3][0]</em></p></td>
<td style="background: rgb(255,205,154)"><p>16/45 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_17 Unknown[29-44] Last 16 bytes of 45</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CAD<br />
<em>B[3][9]</em><br />
z_17[9]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>1<sup>st</sup> party member char ID mirror.<small> Is a mirror of 0x04F8 (set from field module).</small><br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CAE<br />
<em>B[3][10]</em><br />
z_17[10]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>2<sup>nd</sup> party member char ID mirror.<small> Is a mirror of 0x04F9 (set from field module).</small><br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CAF<br />
<em>B[3][11]</em><br />
z_17[11]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>3<sup>ed</sup> party member char ID mirror.<small> Is a mirror of 0x04FA (set from field module).</small><br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0CB4<br />
<em>B[3][16]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Aeris In Church progression (document this better)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CB5<br />
<em>B[3][17]</em></p></td>
<td style="background: rgb(255,205,154)"><p>49 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_18 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0CE6<br />
<em>B[3][66]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Escape from 1st reactor progress.<br />
0x01: after scroll at start of map MD8_2 (maybe unneded).<br />
0x02: after people panic on MD8_3 is over to never show it again.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CE7<br />
<em>B[3][67]</em></p></td>
<td style="background: rgb(255,205,154)"><p>7 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_19 Unknown</p></td>
</tr>
<tr>
<td><p>0x0CEE<br />
<em>B[3][74]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Party GP (0-10000)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CF0<br />
<em>B[3][76]</em></p></td>
<td style="background: rgb(255,205,154)"><p>12 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_20 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CF0<br />
<em>B[3][76]</em><br />
z_20[0]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Chocobo Race - Times you lose (Only on Corel Prision Race){crcin/esto/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CF3<br />
<em>B[3][79]</em><br />
z_20[3]</p></td>
<td style="background: rgb(255,205,154)"><p>1 Byte</p></td>
<td style="background: rgb(255,205,154)"><p>Battle Square Special Dialog Progression {0x00 init, 0x10 :no text, 0xF0:new special fight}</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CF4<br />
<em>B[3][80]</em><br />
z_20[4] &amp; Z_20[5]</p></td>
<td style="background: rgb(255,255,204)"><p>2 Bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Battle Square Battle Points</p></td>
</tr>
<tr>
<td><p>0x0CFC<br />
<em>B[3][88]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Number of chocobo stables owned</p></td>
</tr>
<tr>
<td><p>0x0CFD<br />
<em>B[3][89]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Number of occupied stables</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0CFE<br />
<em>B[3][90]</em></p></td>
<td style="background: rgb(225,236,252)"><p>1 Byte</p></td>
<td style="background: rgb(225,236,252)"><p>Choco Bill dialogs mask 0x01: If you talk him after meteor get summoned (only showed once) {FRMIN/jijii/s1}<br />
0x02: If he offers you to rent Chocobo Stables (only showed once) {FRMIN/jijii/s1}<br />
</p></td>
</tr>
<tr>
<td><p>0x0CFF<br />
<em>B[3][91]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Chocobo Stables Occupied Mask. LSB 1 2 3 4 5 6 x x MSB Stable #) Chocobo's in stables. 1=0ccupied</p></td>
</tr>
<tr>
<td><p>0x0D00<br />
<em>B[3][92]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Chocobos who can't mate LSB 1 2 3 4 5 6 x x MSB (Stable #).The Chocobo Was Just Born or has Recently Mated.1=can't mate</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D01<br />
<em>B[3][93]</em></p></td>
<td style="background: rgb(255,205,154)"><p>40 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_22 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D13<br />
<em>B[3][111]</em><br />
z_22[18]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Aeris flower quest progress.<br />
0x01: if we buy flower from Aeris.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D23<br />
<em>B[3][127]</em><br />
z_22[34]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Current room in TUNNEL_1. From 1 to 6. If less then 1 then we go to TUNNEL_3. If 6 then to TUNNEL_2. Used instead of duplicating tunnel rooms. Start room set during mission 5 reactor train minigame.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D24<br />
<em>B[3][128]</em><br />
z_22[35]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Kalm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak to someone).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08: Spoke to the child in the house next to the Inn<br />
0x10: Freed the dog in a house<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D26<br />
<em>B[3][130]</em><br />
z_22[37]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Reactor under the plate (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Speaking with Biggs(0x01)<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D27<br />
<em>B[3][131]</em><br />
z_22[38]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Reactor under the plate (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Speaking with Jesse(0x01)<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td><p>0x0D29<br />
<em>B[3][133]</em></p></td>
<td><p>1 Byte</p></td>
<td><p>Yuffie can be found in the forests? (LSB only) others used?</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D2A<br />
<em>B[3][134]</em></p></td>
<td style="background: rgb(255,205,154)"><p>28 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_23 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D44<br />
<em>B[3][160]</em><br />
z_23[26]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Reactor under the plate (<a href="../Bit_numbering" title="wikilink">LBS</a>).<br />
Bit=0(NOT Activated/Received/Spoken to), Bit=1(Activated/Received/Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10: Aerith on roof event ends<br />
0x20:<br />
0x40: Turbo Ether {MIN51_2}<br />
0x80: Aerith on roof event starts<br />
</p></td>
</tr>
<tr>
<td><p>0x0D46<br />
<em>B[3][162]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Don's Mission Progress (more needed here)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D47<br />
<em>B[3][163]</em></p></td>
<td style="background: rgb(255,205,154)"><p>31 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_24 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D47<br />
<em>B[3][163]</em><br />
z_24[0]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08: Elevator event at shinra HQ(0x08)<br />
0x10: First conversation while climbing Shinra HQ stairs(0x10)<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D49<br />
<em>B[3][165]</em><br />
z_24[2]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80: Second conversation while climbing Shinra HQ stairs(0x80)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D4A<br />
<em>B[3][166]</em><br />
z_24[3]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Third conversation while climbing Shinra HQ stairs (0x01)<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D4C<br />
<em>B[3][168]</em><br />
z_24[5]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Braking in Shinra HQ scene (0x01)<br />
0x02: Taking out the guards and obtaining keycard 60(0x02)<br />
0x04: Taking everyone out the first floor in Shinra HQ(0x04)<br />
0x08: Speaking to the couple in the shop at Shinra HQ(0x08)<br />
0x10: Speaking to the shop seller in Shinra HQ(0x10)<br />
0x20: Approaching Shinra HQ and conversation at the front door scene(0x20)<br />
0x40: Approaching Shinra HQ and conversation at the front door scene(0x40)<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D50<br />
<em>B[3][172]</em><br />
z_24[9]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Item on floor), Bit=1(Item taken).<br />
0x01: Phoenix down from locker at floor 64 (0x01)<br />
0x02: Ether from locker at floor 64(0x02)<br />
0x04:<br />
0x08:<br />
0x10: Exiting elevator FMV at floor 60(0x10)<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D52<br />
<em>B[3][174]</em><br />
z_24[11]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Bits kept for the doors at floor 63, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Door opened), Bit=1(Door closed).<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D55<br />
<em>B[3][177]</em><br />
z_24[14]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Item mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Item on floor), Bit=1(Item taken).<br />
0x01:<br />
0x02: Coupon C from Shinra HQ(0x02)<br />
0x04: Coupon C from Shinra HQ(0x04)<br />
0x08: Coupon B from Shinra HQ(0x08)<br />
0x10: Speaking to the machine at floor 63(0x10)<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D56<br />
<em>B[3][178]</em><br />
z_24[15]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Bits kept for some events on floor 63, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(Really needs to be investigated).<br />
Bit=0(Door opened), Bit=1(Door closed).<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D57<br />
<em>B[3][179]</em><br />
z_24[16]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Hitting vending machine at floor 64(0x01)<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D58<br />
<em>B[3][180]</em><br />
z_24[17]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08: Placing midgar fifth part(0x08)<br />
0x10: Placing midgar fourth part(0x10)<br />
0x20: Placing midgar third part(0x20)<br />
0x40: Placing midgar second part(0x40)<br />
0x80: Placing midgar first part(0x80)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D59<br />
<em>B[3][181]</em><br />
z_24[18]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01: Midgar model lights up at floor 65<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80: Last conversation with floor 63 machine<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D5D<br />
<em>B[3][185]</em><br />
z_24[22]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, Shinra HQ (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20: Retrieving coupons (must know the order)(0x20)<br />
0x40: Retrieving coupons (must know the order)(0x40)<br />
0x80: Retrieving coupons (must know the order)(0x80)<br />
</p></td>
</tr>
<tr>
<td><p>0x0D66<br />
<em>B[3][194]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Turtle Paradise Flyers Seen LSB 1 2 3 4 5 6 x x MSB (flyer#) 1=seen 0x01: Sector 7 Slums<br />
0x02: 1st Floor Shinra Building<br />
0x04: Gold Saucer - Ghost Hotel<br />
0x08: Cosmo Canyon - Inn 2nd Floor<br />
0x10: Cosmo Canyon - Near Shop<br />
0x20: Wutai In Front of Trap Room<br />
0x40: Wutai - In Front of Turtle Paradise<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D67<br />
<em>B[3][195]</em></p></td>
<td style="background: rgb(255,205,154)"><p>12 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_25 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D67<br />
<em>B[3][195]</em><br />
z_25[0]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Conversations mask<br />
0x01: Cait Sith Leaves, and tell you that "The Sister Ray's not this way" {SINBIL_1/KETLINE/s5}<br />
0x02: Don Corneo's mansion first time you talk to DOORMAN {colne_1/DOORMAN/s1}<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D68<br />
<em>B[3][196]</em><br />
z_25[1]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Cloud Lv just before Jenova Synthesis battle start.<br />
Used as lv placeholder for Jenova Synthesis Boost formula.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D69<br />
<em>B[3][197]</em><br />
z_25[2]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Barret Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6A<br />
<em>B[3][198]</em><br />
z_25[3]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Tifa Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6B<br />
<em>B[3][199]</em><br />
z_25[4]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Red XII Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6C<br />
<em>B[3][200]</em><br />
z_25[5]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Yuffie Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6D<br />
<em>B[3][201]</em><br />
z_25[6]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Cait Sith Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6E<br />
<em>B[3][202]</em><br />
z_25[7]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Vincent Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D6F<br />
<em>B[3][203]</em><br />
z_25[8]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Northern Cave: Cid Lv just before Jenova Synthesis battle start.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D70<br />
<em>B[3][204]</em><br />
z_25[9]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Bizarro Sephiroth Fight Number of Groups<br />
01: 1 Group. First time you enter the map{LASTMAP/directr/s0}<br />
02: 2 Groups {LASTMAP/AD3/s3}<br />
03: 3 Groups {LASTMAP/AD3/s3}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D71<br />
<em>B[3][205]</em><br />
z_25[10]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Bizarro Sephiroth Fight, some progress value<br />
00: {LASTMAP/BAT/s4,s5}<br />
01: {LASTMAP/BAT/s4}<br />
02: {LASTMAP/BAT/s4}<br />
03: {LASTMAP/BAT/s5}<br />
04: {LASTMAP/BAT/s5}<br />
05: {LASTMAP/BAT/s5}<br />
06: {LASTMAP/BAT/s5}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D72<br />
<em>B[3][206]</em><br />
z_25[11]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Great Glacier Snowboard, taken path (Set the exit location where you land) {hyou1/event/s1}<br />
0x01: Left both times: Forest HYOU2<br />
0x02: Right both times: Outside Frostbite cave HYOU3<br />
0x04: Left right: Main gate HYOU1<br />
0x08: Right then left: Single tree HYOU7<br />
</p></td>
</tr>
<tr>
<td><p>0x0D73<br />
<em>B[3][207]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Yuffie Regulary. Has the character entered the party regulary? For example Yuffie further appears in the forest if this option is off.<br />
0x6E: Yes; 0x6F: No</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D74<br />
<em>B[3][208]</em></p></td>
<td style="background: rgb(255,205,154)"><p>15 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_26 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D74<br />
<em>B[3][208]</em><br />
z_26[0]</p></td>
<td style="background: rgb(255,163,0)"><p>1 byte</p></td>
<td style="background: rgb(255,163,0)"><p>MDS7PLR1 event flags.<br />
0x01: when everyone run to hideout.<br />
0x02: when talk to man to view pillar to call. This will run special event script when return to this map. Remove this bit after script is called.<br />
0x04: when Barret return to map and call us again.<br />
0x08: after return to this map after seeing pillar.<br />
0x10: after talking to right soldier twice (before mission in 5th reactor).<br />
0x20:<br />
0x40:<br />
0x80:</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D75<br />
<em>B[3][209]</em><br />
z_26[1]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: Right after enter s7 bar MAP[0xA1]<br />
0x02: After 7th heaven initial scene[0xFF]or[0xBF] if bit 6 is 0<br />
0x04: Tifa get out the bar[0xA5]?<br />
0x08: Scene ends and barret wait outside bar[0xAD]<br />
0x10: Barret talk before enter the bar[0xFD]or[0xBD] if bit 6 is 0<br />
0x20: Right after enter s7 bar MAP[0xA1]<br />
0x40: Girl talk about reactor explotion[0xED]<br />
0x80: Right after enter s7 bar MAP[0xA1]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D76<br />
<em>B[3][210]</em><br />
z_26[2]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: After you wake up in the Hideout[0x03]<br />
0x02: After you wake up in the Hideout[0x03]<br />
0x04: Unknown[0x00]?<br />
0x08: Unknown[0x00]<br />
0x10: Avalache member continue running to s7 train station and Villagers are arround Avalache team [0x51]{mds7}<br />
0x20: Unknown it become 1 seconds after 0x0D76[4] is set [0x51]{mds7}<br />
0x40: Unknown[0x00]<br />
0x80: Unknown[0x00]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D77<br />
<em>B[3][211]</em><br />
z_26[3]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: Tell tifa did fight w/ barret (1) didn't fight (0)[0x05]or[0x04] if not<br />
0x02: Unknown[0x00]<br />
0x04: Auto tifa talk about fight w/ barret[0x04]<br />
0x08: Unknown[0x00]<br />
0x10: Unknown[0x00]<br />
0x20: Unknown[0x00]<br />
0x40: Unknown[0x00]<br />
0x80: Unknown[0x00]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D78<br />
<em>B[3][212]</em><br />
z_26[4]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: Barret chages in bar (set w/ z_26[1] state #2)[0x03]<br />
0x02: Barret chages in bar (set w/ z_26[1] state #2)[0x03]<br />
0x04: After we have talked to tifa[0x07]<br />
0x08: Set to 1 if we choose no drink when talking to tifa[0x0F]<br />
0x10: Set to 1 if we choose strong drink talking ot tifa[0x17]<br />
0x20: Unknown[0x00]<br />
0x40: Unknown[0x00]<br />
0x80: Unknown[0x00]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D79<br />
<em>B[3][213]</em><br />
z_26[5]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: set to 1 when tifa calls the machine down after you 1st talk down stairs, never gets unset[0x03]<br />
0x02: 1 if elevator is in hide out (pinball machine)[0x02]<br />
0x04: After you wake up in the Hideout[0x1F]<br />
0x08: After you wake up in the Hideout[0x1F]<br />
0x10: After you wake up in the Hideout[0x1F]<br />
0x20: Unknown[0x00]<br />
0x40: After giving Barret the materia tutorial[0x5D]<br />
0x80: Unknown[0x00]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D7A<br />
<em>B[3][214]</em><br />
z_26[6]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Conversations mask, MDS7 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Not spoken to), Bit=1(Spoken to). The value inside [] is the hex value of the entire byte.<br />
Start sector 7 slums [0x00]<br />
0x01: After hide out 1st talk[0x03]<br />
0x02: After hide out 1st talk[0x03]<br />
0x04: second part of talk tifa enter in scene[0x07]<br />
0x08: After you wake up in the Hideout[0x6F]<br />
0x10: Unknown[0x00]<br />
0x20: After you wake up in the Hideout[0x6F]<br />
0x40: After you wake up in the Hideout[0x6F]<br />
0x80: After you get out the Hideout and talk to tifa [0xEF]<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D7B<br />
<em>B[3][215]</em><br />
z_26[7]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Training room at sector 5 (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you speak).<br />
Bit=0(Item on floor), Bit=1(Item taken).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10: All materia after taking ether(0x10)<br />
0x20: Ether chest that falls from ceiling(0x20)<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D7C<br />
<em>B[3][216]</em><br />
z_26[8]</p></td>
<td style="background: rgb(255,163,0)"><p>1 byte</p></td>
<td style="background: rgb(255,163,0)"><p>MDS7ST3 event flags.<br />
0x01: when everyone start run to hideout.<br />
0x02: when trainman tells you about war (3 talk).<br />
0x04: when pair on station agreed with each other.<br />
0x08: when Jessie, Biggs and Wedge run into train.<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0D83<br />
<em>B[3][223]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Midgard train flags.<br />
0x01: when we talk to Biggs on way to sector 7.<br />
0x02: when we talk to Wedge twice on way to sector 7.<br />
0x04: when talk to Jessie, before look at map.<br />
0x10: this bit is checked on ROOTMAP, though it doesn't use ingame.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D84<br />
<em>B[3][224]</em></p></td>
<td style="background: rgb(255,205,154)"><p>32/64 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_27 Unknown[0-31] First 32 bytes of 64 (ENDS AT 0x0DC3 32 Bytes into next bank)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0D90<br />
<em>B[3][236]</em><br />
z_27[12]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Event flags inside Junon.<br />
0x01:<br />
0x02:<br />
0x04: Junon Soldiers running through the city after the parade.<br />
0x08:<br />
0x10:<br />
0x20: Enemy Skill materia<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
</tbody>
</table>

## Save Memory Bank B/C

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DA4<br />
<em>B[11][0]</em></p></td>
<td style="background: rgb(255,205,154)"><p>32/64 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_27 Unknown[32-63] Last 32 bytes of 64</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DA4<br />
<em>B[11][0]</em><br />
z_27[32]</p></td>
<td style="background: rgb(205,230,230)"><p>6 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race - Chocobo Name (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DAA<br />
<em>B[11][6]</em><br />
z_27[38]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G1) - Jockey<br />
00: Cloud<br />
01: Tifa<br />
02: Cid<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DAB<br />
<em>B[11][7]</em><br />
z_27[39]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G1) - Course<br />
00: Long course<br />
01: Short course<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DAC<br />
<em>B[11][8]</em><br />
z_27[40]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G1) - Bet Selection Screen<br />
00: Enabled {crcin_1/esto}<br />
01: Disabled {crcin_2/esto}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DAD<br />
<em>B[11][9]</em><br />
z_27[41]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G1) - ???<br />
00: All others times but<br />
01: When you race by talking to ester in {crcin_1/esto}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DAE<br />
<em>B[11][10]</em><br />
z_27[42]</p></td>
<td style="background: rgb(205,230,230)"><p>2 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Sprint Speed<br />
Value = 4500 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB0<br />
<em>B[11][12]</em><br />
z_27[44]</p></td>
<td style="background: rgb(205,230,230)"><p>2 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Speed<br />
Value = 3500 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB2<br />
<em>B[11][14]</em><br />
z_27[46]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Acceleration<br />
Value = 70 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB3<br />
<em>B[11][15]</em><br />
z_27[47]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Cooperation<br />
Value = 100 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB4<br />
<em>B[11][16]</em><br />
z_27[48]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Intelligence<br />
Value = 100 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB5<br />
<em>B[11][17]</em><br />
z_27[49]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Type (Yellow, Green, Blue, Black, Gold)<br />
Value = 0 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB6<br />
<em>B[11][18]</em><br />
z_27[50]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Personality<br />
Value = 0 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB7<br />
<em>B[11][19]</em><br />
z_27[51]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - ???<br />
05: When you race by talking to ester in {crcin_2/esto}<br />
07: All others times {crcin_1/esto}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB8<br />
<em>B[11][20]</em><br />
z_27[52]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - ???<br />
Value = 1 (ALWAYS) {crcin_1/crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DB9<br />
<em>B[11][21]</em><br />
z_27[53]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - ???<br />
Value = 0 (ALWAYS) {crcin_1/crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DBA<br />
<em>B[11][22]</em><br />
z_27[54]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Joe/TEIOH Chalenge<br />
00: No<br />
01: Yes<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DBB<br />
<em>B[11][23]</em><br />
z_27[55]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Selected Rank<br />
00: Class C<br />
01: Class B<br />
02: Class A<br />
03: Class S<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DBC<br />
<em>B[11][24]</em><br />
z_27[56]</p></td>
<td style="background: rgb(205,230,230)"><p>1 byte</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race - ???<br />
Random 0/15{crcin_1/esto}<br />
0: All others times</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DBD<br />
<em>B[11][25]</em><br />
z_27[57]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Chocobo Race - Finish Place (0 to 5)<br />
Set to 0xFF on the elevator {GLDELEV/dic/s0}<br />
Used only when you must race to get out the desert prision. After winning the race and before exit the map is set to 0xFF and never change again. {crcin/esto/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DBE<br />
<em>B[11][26]</em><br />
z_27[58]</p></td>
<td style="background: rgb(205,230,230)"><p>2 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G2) - Stamina<br />
Value = 6000 {crcin_2}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0DC0<br />
<em>B[11][28]</em><br />
z_27[60]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race(G1) - Winning Prize<br />
00 = 500GP | "Received "Sprint Shoes"<br />
01 = 300GP | "Received "Counter Attack" Materia</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0DC4<br />
<em>B[11][32]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 1 [See Below for <a href="#chocobo-record" title="wikilink">Chocobo Slot format</a>]</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0DD4<br />
<em>B[11][48]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 2</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0DE4<br />
<em>B[11][64]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 3</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0DF4<br />
<em>B[11][80]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 4 [Slot 5 and 6 are located at 0x1084 - 0x10A3]</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E04<br />
<em>B[11][96]</em></p></td>
<td style="background: rgb(255,205,154)"><p>13 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_28 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E0C<br />
<em>B[11][104]</em><br />
z_28[8]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Change on Final Battle<br />
<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08: Final Battle<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E0E<br />
<em>B[11][106]</em><br />
z_28[10]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Yuffie Stolen Materia Quest - Disabled party members {YUFY1/YUFI}<br />
(Bit mask is set just before stolen materia been restored, to know what chars must be reactivated.)<br />
0x01: Unused<br />
0x02: Barret<br />
0x04: Tifa<br />
0x08: Red XIII<br />
0x10: Cait Sith<br />
0x20: Cid<br />
0x40: Vincent<br />
0x80: Aeris<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E0F<br />
<em>B[11][107]</em><br />
z_28[11]</p></td>
<td style="background: rgb(205,230,230)"><p>2 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>G-Bike Minigame Last Score {GAMES_2/dic}</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E11<br />
<em>B[11][109]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 Bytes</p></td>
<td style="background: rgb(255,255,204)"><p>G-Bike Minigame High Score</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E13<br />
<em>B[11][111]</em></p></td>
<td style="background: rgb(255,205,154)"><p>1 Byte</p></td>
<td style="background: rgb(255,205,154)"><p>UnSaved Snowboard Mini Game Temp Var.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E14<br />
<em>B[11][112]</em></p></td>
<td style="background: rgb(255,255,204)"><p>4 Bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Fastest Time For Snowboard Beginner Course. Format: MMSSTTT0 90 27 36 02 in the file is a time of 2'36"279 (value is 32bit int so will become 02362790 when read )</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E18<br />
<em>B[11][116]</em></p></td>
<td style="background: rgb(255,255,204)"><p>4 Bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Fastest Time For Snowboard Expert Course. See Beginner Course for more info</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E1C<br />
<em>B[11][120]</em></p></td>
<td style="background: rgb(255,255,204)"><p>4 Bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Fastest Time For Snowboard Crazy Course. See Beginner Course for more info</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E20<br />
<em>B[11][124]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 Byte</p></td>
<td style="background: rgb(255,255,204)"><p>HighScore For Snowboard Beginner Course</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E21<br />
<em>B[11][125]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 Byte</p></td>
<td style="background: rgb(255,255,204)"><p>HighScore For Snowboard Expert Course</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E22<br />
<em>B[11][126]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 Byte</p></td>
<td style="background: rgb(255,255,204)"><p>HighScore For Snowboard Crazy Course</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E23<br />
<em>B[11][127]</em></p></td>
<td style="background: rgb(255,205,154)"><p>1 Byte</p></td>
<td style="background: rgb(255,205,154)"><p>UnSaved Snowboard Mini Game Temp Var</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E24<br />
<em>B[11][128]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>2nd rank at RollerCoaster Shooter</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0E26<br />
<em>B[11][130]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>3rd rank at RollerCoaster Shooter</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E28<br />
<em>B[11][132]</em></p></td>
<td style="background: rgb(255,205,154)"><p>17 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_29 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E28<br />
<em>B[11][132]</em><br />
z_29[0]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Mythril Side Quest/Chocobo Sage Side Quest<br />
0x01: Talked to the Weapon Seller about the Keystone, Temple of the Ancients, DIO, etc {zz2/m/s4}<br />
0x02: Chocobo Sage when he finish all remembering stuff {zz3/dic/s0}<br />
0x04: Unused<br />
0x08: Old man: "Large Materia needs high level Materia." {zz1/m1/s1}<br />
0x10: Mythril given to the Weapon Seller {zz2/m/s1}<br />
0x20: Chocobo Sage if you ask him "What about that Chocobo?" {zz3/m1/s1}<br />
0x40: Chocobo Sage every time he remember something new about Chocobos is set to 1, and when you tell that back to Chole reset to 0. {zz3/m1/s1}{FRCYO/kodomo/s1}<br />
0x80: First time you talk to Chole after meeting Chocobo Sage {FRCYO/kodomo/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E29<br />
<em>B[11][133]</em><br />
z_29[1]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo Sage Side Quest - Progression Variable 01: First time you talk to Chocobo Sage<br />
02,03,04: About Blue/Green Chocobo<br />
05: About Black Chocobo<br />
06,07,08: About Gold Chocobo<br />
09,10: About Zeio Nuts</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2A<br />
<em>B[11][134]</em><br />
z_29[2]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Number of battles to reach in order to unlock the next part of the Chocobo breeding tutorial</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2C<br />
<em>B[11][136]</em><br />
z_29[4]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Sage Side Quest - Part of the random number of battles formula<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2D<br />
<em>B[11][137]</em><br />
z_29[5]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Unused?<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2E<br />
<em>B[11][138]</em><br />
z_29[6]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race / Others<br />
0x01: Set to 1 the first time you talk to Ester to race and Ride your own Chocobo {crcin_1/esto/s1}<br />
0x02: Set to 1 just before Chocobo Race Engine be launched {crcin_1/esto/s1}<br />
Set to 0 when you receive the price or lose. {crcin_1/dic/s0}<br />
0x04: Set to 1 just before your first time race (Ester say "Yeahh but jockeys can't buy tickets.")<br />
Then after been activated the next races (she say: "Good Luck! Take care!") {crcin_1/esto/s1}<br />
0x08: After beating Mog's House and receive 30GP from the guy {GAMES_2/kabe/s1}<br />
0x10: If you win 9 races to enter Rank S {crcin_1/esto/s1}<br />
0x20: If you win 19 races with the same chocobo to receive Sprint Shoes, Cat's Bell, Precious Watch, Chocobracelet, and Counter Attack Materia. {crcin_1/esto/s1}<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2F<br />
<em>B[11][139]</em><br />
z_29[7]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Chocobo Race - Selected Chocobo Stable Position (0 to 5)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E30<br />
<em>B[11][140]</em><br />
z_29[8]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Unused?<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2E<br />
<em>B[11][138]</em><br />
z_29[6]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Northern Cave<br />
0x01: Bottom of Northern Cave talk {las4_0/dic/s0}<br />
0x02: Set to 1 when you enter the map "las3_3" comming from map "las4_1" {las3_3/dic/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E2F<br />
<em>B[11][139]</em><br />
z_29[7]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Northern Cave<br />
0x01: Bottom of Northern Cave talk {las4_0/dic/s0}<br />
0x02: Set to 1 when you enter the map "las3_3" comming from map "las4_1" {las3_3/dic/s0}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E30<br />
<em>B[11][140]</em><br />
z_29[8]</p></td>
<td style="background: rgb(205,230,230)"><p>1 bytes</p></td>
<td style="background: rgb(205,230,230)"><p>Northern Cave - Received items from party in the last talk<br />
0x01: Barret {las4_0/ballet/s1}<br />
0x02: Tifa {las4_0/tifa/s1}<br />
0x04: RedXIII {las4_0/red/s1}<br />
0x08: Cid {las4_0/cid/s1}<br />
0x10: Cait Sith {las4_0/cait/s1}<br />
0x20: Yuffi {las4_0/yufi/s1}<br />
0x40: Vincent {las4_0/vincent/s1}<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E33<br />
<em>B[11][143]</em><br />
z_29[11]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Lucrecia's Cave sidequest Progression Variable</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E35<br />
<em>B[11][145]</em><br />
z_29[13]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Lucrecia's Cave sidequest:<br />
Number of battles to get past in order to unlock Chaos &amp; Death Penalty</p></td>
</tr>
<tr>
<td><p>0x0E39<br />
<em>B[11][149]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>1st rank at RollerCoaster Shooter</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0E3C<br />
<em>B[11][152]</em></p></td>
<td style="background: rgb(255,205,154)"><p>105 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_30 Unknown</p></td>
</tr>
</tbody>
</table>

## Save Memory Bank D/E

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x0EA4<br />
<em>B[13][0]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Which game-play Disc is needed</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EA5<br />
<em>B[13][1]</em></p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>z_31 Tifa's House 0x01: Final Heaven {niv_ti2/piano/s1}<br />
0x02: Cloud played the piano in the flashback {niv_ti2/molody/s2}<br />
0x04: Elemental Materia {niv_ti2/piano/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EA6<br />
<em>B[13][2]</em></p></td>
<td style="background: rgb(255,205,154)"><p>1 Byte</p></td>
<td style="background: rgb(255,205,154)"><p>Start Of Bombing Mission (0x14=Yes, 0x56=No)<br />
Northern Cave - Progress (TODO: more info) 0x94</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EA7<br />
<em>B[13][3]</em></p></td>
<td style="background: rgb(255,205,154)"><p>3 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_32 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EA7<br />
<em>B[13][3]</em><br />
z_32[0]</p></td>
<td style="background: rgb(255,205,154)"><p>1 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>Northern Cave - Progress (TODO: more info)</p></td>
</tr>
<tr>
<td><p>0x0EAA<br />
<em>B[13][6]</em></p></td>
<td><p>2 Bytes</p></td>
<td><p>Step counter. Used in great glacier to count the steps until passing out and resetted whenever you enter it. Value to pass out = 544</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EAC<br />
<em>B[13][8]</em></p></td>
<td style="background: rgb(255,205,154)"><p>22 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_33 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0EC2<br />
<em>B[13][30]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Field pointers mask (hand over party leader's head + red and green arrows)<br />
0x00: Inactive<br />
0x02: Active</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EC3<br />
<em>B[13][31]</em></p></td>
<td style="background: rgb(255,205,154)"><p>1 byte</p></td>
<td style="background: rgb(255,205,154)"><p>z_34 Unknown. <del>If you have max materias in your equipment it is set to non-zero (needs to be confirmed)</del> FALSE! (By Ss4).</p></td>
</tr>
<tr>
<td><p>0x0EC4<br />
<em>B[13][32]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 1 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0ECA<br />
<em>B[13][38]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 2 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0ED0<br />
<em>B[13][44]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 3 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0ED6<br />
<em>B[13][50]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 4 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0EDC<br />
<em>B[13][56]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 5 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0EE2<br />
<em>B[13][62]</em></p></td>
<td><p>6 bytes</p></td>
<td><p>Name of Chocobo 6 (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td><p>0x0EE8<br />
<em>B[13][68]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 1</p></td>
</tr>
<tr>
<td><p>0x0EEA<br />
<em>B[13][70]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 2</p></td>
</tr>
<tr>
<td><p>0x0EEC<br />
<em>B[13][72]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 3</p></td>
</tr>
<tr>
<td><p>0x0EEE<br />
<em>B[13][74]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 4</p></td>
</tr>
<tr>
<td><p>0x0EF0<br />
<em>B[13][76]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 5</p></td>
</tr>
<tr>
<td><p>0x0EF2<br />
<em>B[13][78]</em></p></td>
<td><p>2 bytes</p></td>
<td><p>Stamina of Chocobo 6</p></td>
</tr>
<tr>
<td><p>0x0EF4<br />
<em>B[13][80]</em></p></td>
<td><p>1 byte</p></td>
<td><p>Vincent Regularly/Change Submarine Color. (Bit-mask)<br />
0x01:<br />
0x02:<br />
0x04: Vincent Regulary. Has the character entered the party regularly? Byte value (Yes:[0xFF]; No:[0xFB])(NEEDS TO BE CHECKED)<br />
0x08: Gray Submarine (bit = 1)/ Red Submarine (bit = 0) (Liked with 0x0EF6[2])<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EF5<br />
<em>B[13][81]</em></p></td>
<td style="background: rgb(255,205,154)"><p>23 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_35 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EF6<br />
<em>B[13][82]</em><br />
z_35[1]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Vehicle Submarine<br />
0x01:<br />
0x02:<br />
0x04: Grey Submarine Ignored / Red Submarine bit = 1 (Linked with 0x0EF4[3])<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EFD<br />
<em>B[13][89]</em><br />
z_35[8]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Northern Cave - Yuffie Split up path</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0EFF<br />
<em>B[13][91]</em><br />
z_35[10]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Save flag.<br />
0x02: set when we in save (menu or point? please check) and unset when out<br />
Other byte values: 0x10, 0x12, 0x51</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F04<br />
<em>B[13][96]</em><br />
z_35[22]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Northern Cave - Progress (TODO: more info)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F05<br />
<em>B[13][97]</em><br />
z_35[23]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Northern Cave - Progress (TODO: more info)</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F0C<br />
<em>B[13][104]</em></p></td>
<td style="background: rgb(255,255,204)"><p>24 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Name of location (<a href="FF_Text" title="wikilink">FF Text format</a>)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F24<br />
<em>B[13][128]</em></p></td>
<td style="background: rgb(255,205,154)"><p>5 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_36 Unknown</p></td>
</tr>
<tr>
<td><p>0x0F29<br />
<em>B[13][133]</em></p></td>
<td><p>1 bytes</p></td>
<td><p>Save on the world map - Tutorial seen (To be Checked)<br />
0x3B: Seen<br />
0x33: Not Seen</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F2A<br />
<em>B[13][134]</em></p></td>
<td style="background: rgb(255,205,154)"><p>50 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_37 Unknown</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F2A<br />
<em>B[13][134]</em><br />
z_37[0]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Needs more research. 0x01:<br />
0x02:<br />
0x04: Red Submarine Tutorial<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F2B<br />
<em>B[13][135]</em><br />
z_37[1]</p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>0x20<br />
<em>B[13][-3716]</em>: World map Ruby Weapon form. bit=0: Small Form (before first encounter). bit=1: Big Form (after first encounter).</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F3A<br />
<em>B[13][150]</em><br />
z_37[16]</p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Rand number between 0,1,2. Is set when you change field map. ex: enter a town.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F5C<br />
<em>B[13][184]</em></p></td>
<td style="background: rgb(255,255,204)"><p>3 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Party leader's coordinates on world map:<br />
Party leader X position on the world map (X coord). Value from 0 up to 295000<br />
000000: 0x000000<br />
065535: 0xFFFF00 | 065536: 0x000001<br />
131071: 0xFFFF01 | 131072: 0x000002<br />
196607: 0xFFFF02 | 196608: 0x000003<br />
262143: 0xFFFF03 | 262144: 0x000004<br />
295000: 0x588004</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F5F<br />
<em>B[13][187]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Party leader viewing direction angle on the world map. Value from 0 up to 255 to cover 0 - 359Â°<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F60<br />
<em>B[13][188]</em></p></td>
<td style="background: rgb(255,255,204)"><p>3 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Party leader Y position on the world map (Y coord). Value from 1 up to 230000<br />
000001: 0x01003C<br />
065535: 0xFFFF3C | 065536: 0x00003D<br />
131071: 0xFFFF3D | 131072: 0x00003E<br />
196607: 0xFFFF3E | 196608: 0x00003F<br />
230000: 0x70823F</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F63<br />
<em>B[13][191]</em></p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Party leader Z altitude on the world map (Z coord). Input value from -128 up to 127 are allowed (0 = Mean Sea Level)</p></td>
</tr>
<tr>
<td><p>0x0F64<br />
<em>B[13][192]</em></p></td>
<td><p>8 bytes</p></td>
<td><p>Caught Wild Chocobo's coordinates on world map</p></td>
</tr>
<tr>
<td><p>0x0F6C<br />
<em>B[13][200]</em></p></td>
<td><p>8 bytes</p></td>
<td><p>Tiny Bronco/Chocobo's coordinates on world map</p></td>
</tr>
<tr>
<td><p>0x0F74<br />
<em>B[13][208]</em></p></td>
<td><p>8 bytes</p></td>
<td><p>Buggy/Highwind's coordinates on world map</p></td>
</tr>
<tr>
<td><p>0x0F7C<br />
<em>B[13][216]</em></p></td>
<td><p>8 bytes</p></td>
<td><p>Submarine/???'s coordinates on world map</p></td>
</tr>
<tr>
<td><p>0x0F84<br />
<em>B[13][224]</em></p></td>
<td><p>8 bytes | Diamond=&gt;Ultimate=&gt;Ruby Weapon's coordinates on world map (ruby is bound To the desert)</p></td>
<td></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F8C<br />
<em>B[13][232]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>1<sup>st</sup> Snow Pole X Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F8E<br />
<em>B[13][234]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>1<sup>st</sup> Snow Pole Y Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F90<br />
<em>B[13][236]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>2<sup>nd</sup> Snow Pole X Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F92<br />
<em>B[13][238]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>2<sup>nd</sup> Snow Pole Y Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F94<br />
<em>B[13][240]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>3<sup>ed</sup> Snow Pole X Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x0F96<br />
<em>B[13][242]</em></p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>3<sup>ed</sup> Snow Pole Y Coordinate.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F98<br />
<em>B[13][244]</em></p></td>
<td style="background: rgb(255,205,154)"><p>12/236 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>z_38 Unknown[0-11] First 12 bytes of 236 (ENDS AT 0x1083 224 Bytes into next bank)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F9C<br />
<em>B[13][248]</em><br />
z_38[4]</p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Angle of the world. The viewing direction of the camera onto the world map. For top-view (ca. 45Â°) this value should be 0.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F9D<br />
<em>B[13][249]</em><br />
z_38[5]</p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Top-view (ca. 45Â°). Determines the camera's position.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F9C<br />
<em>B[13][248]</em><br />
z_38[4]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Camera angle and rotation of normal world map.<br />
00 00 - FF 0F: Map rotation angle. xx yx: if y &gt; 0, y will be changed to 0. (Source: Asa. Data Collision)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0F9F<br />
<em>B[13][251]</em><br />
z_38[6]</p></td>
<td style="background: rgb(255,255,204)"><p>2 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Snow Pole Number/Where address will be overwritten by next pole (cycling 00, 01, 02, 00, 01, 02... )<br />
00: 1st pole address<br />
01: 2nd pole address<br />
02: 3rd pole address</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FA0<br />
<em>B[13][252]</em><br />
z_38[8]</p></td>
<td><p>1 bytes</p></td>
<td><p>Wild Chocobo Type.<br />
Value is set when Chocobo is caught and used after Chocobo is sent to cage.<br />
Index is the byte's value and not the bit-mask.<br />
0x00: Chocobo not displayed in cage<br />
0x01: Wonderful<br />
0x02: Great<br />
0x03: Good<br />
0x04: Fair<br />
0x05: Average<br />
0x06: Poor<br />
0x07: Bad<br />
0x08: Terrible<br />
Over 08 = Choco Billy's rating window not displayed</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FA1<br />
<em>B[13][253]</em><br />
z_38[9]</p></td>
<td style="background: rgb(255,255,204)"><p>1 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Riding Byte.<br />
Index is the byte's value and not the bit-mask.<br />
0x00: On foot.<br />
0x03: Highwind<br />
0x04: Wild Chocobo (Liked with 0x0C22[0])<br />
0x0D: Submarine<br />
0x13: Chocobo (Liked with 0x0C22[1/7]. 0x0C22: 0x04=Yellow, ..., 0x40=Gold)<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FA3<br />
<em>B[13][255]</em><br />
z_38[11]</p></td>
<td style="background: rgb(255,205,154)"><p>1 bytes</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown. It seems this value is mixture of Number of Snow Poles, Party direction and walking steps or coordinates. Value will be ignored when loading slot.</p></td>
</tr>
</tbody>
</table>

## Save Memory Bank 7/F

<table>
<caption><strong>Table 1: FF7 Save Slot</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FA4<br />
<em>B[7][0]</em></p></td>
<td style="background: rgb(255,205,154)"><p>224/236 Bytes</p></td>
<td style="background: rgb(255,205,154)"><p>Unknown z_38[12-235] Last 224 bytes of 236</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FA6<br />
<em>B[7][2]</em><br />
z_38[14]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>World map camera &amp; map display<br />
Add two values (one from camera, one from map) and set this byte.<br />
Camera: Aerial(00); Closeup(20)<br />
Map: Off(80); Small(00); Large(40)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FAB<br />
<em>B[7][7]</em><br />
z_38[19]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>If not 0x00, game crashes</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FC4<br />
<em>B[7][32]</em><br />
z_38[44]</p></td>
<td><p>2 bytes</p></td>
<td><p>Fields items mask.<br />
0x0001: first potion on MD1STIN.<br />
0x0002: second potion on MD1STIN.<br />
0x0004: potion at NMKIN3.<br />
0x0008: phoenix down on NKMIN1.</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FC6<br />
<em>B[7][34]</em><br />
z_38[46]</p></td>
<td style="background: rgb(225,236,252)"><p>1 byte</p></td>
<td style="background: rgb(225,236,252)"><p>Items mask, Chocobo Farm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Destruct Materia Animation displayed {sininb42/mtr/s3}<br />
0x02: Destruct Materia {sininb42/mtr/s1}<br />
0x04: Enemy Skill {blin68_2/mtr/s1} (See 0x0BEF[1])<br />
0x08: Enemy Skill Animation (Drop after battle) {blin68_2/mtr/s3}<br />
0x10: Odin Materia {sinin2_1/mtr/s1}<br />
0x20: Odin Materia Animation displayed {sinin2_1/mtr/s3}<br />
0x40: Counter Materia {nvdun1/mtr/s1}<br />
0x80: Magic Plus Materia {sandun_1/mtr/s1}<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FF1<br />
<em>B[7][77]</em><br />
z_38[89]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>On Buggy vehicle. Specifies if a character is on a Buggy. Only if a Buggy is present.<br />
0x0E: On; 0x0C: Off</p></td>
</tr>
<tr>
<td><p>0x0FF4<br />
<em>B[7][80]</em><br />
z_38[92]</p></td>
<td><p>1 byte</p></td>
<td><p>Items mask, Mythril Mine (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: 4sbwy_6 - Tent<br />
0x02: 4sbwy_3 - Potion<br />
0x04: 4sbwy_1 - Ether<br />
0x08: psdun_3 - Ether<br />
0x10: psdun_4 - Hi-Potion<br />
0x20: psdun_4 - Elixir<br />
0x40: psdun_3 - Long Range materia<br />
0x80: gnmk - Titan Materia<br />
</p></td>
</tr>
<tr>
<td><p>0x0FF5<br />
<em>B[7][81]</em><br />
z_38[93]</p></td>
<td><p>1 byte</p></td>
<td><p>Items mask, (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: elmin2_2 - Ether<br />
0x02: losin1 - Comet Materia<br />
0x04: gonjun1 - Deathblow Materia<br />
0x08: q_4 - Hades Materia<br />
0x10: q_4 - Outsider<br />
0x20: q_3 - Escourt Guard<br />
0x40: q_3 - Conformer<br />
0x80: q_4 - Spirit Lance<br />
</p></td>
</tr>
<tr>
<td><p>0x0FF6<br />
<em>B[7][82]</em><br />
z_38[94]</p></td>
<td><p>1 byte</p></td>
<td><p>Items mask, (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: q_1 - Heaven's Cloud<br />
0x02: q_3 - Megalixir<br />
0x04: q_4 - Megalixir<br />
0x08: losinn - Elixir<br />
0x10: losin2 - Guard Source<br />
0x20: losin3 - Magic Source<br />
0x40: las1_2 las4_0 - Elixir<br />
0x80: las1_2 las4_0 - Mystle<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FF9<br />
<em>B[7][85]</em><br />
z_38[97]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Kalm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Hidden Ether in the second floor of a house<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FFB<br />
<em>B[7][87]</em><br />
z_38[99]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Kalm Traveler rewards visibility (each bit set back to 0 when picked up)<br />
Guide Book (0x01); Master Command(0x02); Master Magic (0x04); Master Summon (0x08); Gold Chocobo (0x10)</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FFC<br />
<em>B[7][88]</em><br />
z_38[100]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Kalm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Peacemaker in a house<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10:<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FFD<br />
<em>B[7][89]</em><br />
z_38[101]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Kalm (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01:<br />
0x02: Hidden Ether from house next to the Inn<br />
0x04:<br />
0x08: Guard Source<br />
0x10: Hidden Ether<br />
0x20:<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x0FFE<br />
<em>B[7][90]</em><br />
z_38[102]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Mythril Mine (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01:<br />
0x02:<br />
0x04:<br />
0x08:<br />
0x10: Mind Source<br />
0x20: Tent<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1004<br />
<em>B[7][96]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>1<sup>st</sup> party member char ID in Group 1. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1005<br />
<em>B[7][97]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>2<sup>nd</sup> party member char ID in Group 1. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1006<br />
<em>B[7][98]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>3<sup>ed</sup> party member char ID in Group 1. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1007<br />
<em>B[7][99]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>1<sup>st</sup> party member char ID in Group 2. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1008<br />
<em>B[7][100]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>2<sup>nd</sup> party member char ID in Group 2. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1009<br />
<em>B[7][101]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>3<sup>ed</sup> party member char ID in Group 2. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x100A<br />
<em>B[7][102]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>1<sup>st</sup> party member char ID in Group 3. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x100B<br />
<em>B[7][103]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>2<sup>nd</sup> party member char ID in Group 3. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x100C<br />
<em>B[7][104]</em><br />
z_38[]</p></td>
<td style="background: rgb(254,254,255)"><p>1 byte</p></td>
<td style="background: rgb(254,254,255)"><p>3<sup>ed</sup> party member char ID in Group 3. Final Boss Battle: Bizarro Sephiroth.<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x101E<br />
<em>B[7][122]</em><br />
z_38[134]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Items mask, Junon (<a href="../Bit_numbering" title="wikilink">LBS</a>)(applied when you take the item).<br />
Bit=0(Item in field), Bit=1(Item taken).<br />
0x01: Mind Source<br />
0x02: Power Source<br />
0x04: Guard Source<br />
0x08:<br />
0x10: 1/35 Soldier<br />
0x20: Luck Source<br />
0x40:<br />
0x80:<br />
</p></td>
</tr>
<tr>
<td style="background: rgb(255,205,154)"><p>0x1030<br />
<em>B[7][140]</em><br />
z_38[152]</p></td>
<td style="background: rgb(255,255,204)"><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Field screen rain switch (non-zero to turn on rain effect)</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x1084<br />
<em>B[7][224]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 5</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x1094<br />
<em>B[7][240]</em></p></td>
<td style="background: rgb(255,255,204)"><p>16 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Chocobo slot 6</p></td>
</tr>
</tbody>
</table>

## Character Record

<table>
<caption><strong>Table 2: Character Record</strong></caption>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x00</p></td>
<td><p>1 byte</p></td>
<td><p>Character ID - Ignored If Not Cait / Vincent???</p></td>
</tr>
<tr>
<td><p>0x01</p></td>
<td><p>1 byte</p></td>
<td><p>Level (1-99)</p></td>
</tr>
<tr>
<td><p>0x02</p></td>
<td><p>1 byte</p></td>
<td><p>Strength (0-255)</p></td>
</tr>
<tr>
<td><p>0x03</p></td>
<td><p>1 byte</p></td>
<td><p>Vitality (0-255)</p></td>
</tr>
<tr>
<td><p>0x04</p></td>
<td><p>1 byte</p></td>
<td><p>Magic (0-255)</p></td>
</tr>
<tr>
<td><p>0x05</p></td>
<td><p>1 byte</p></td>
<td><p>Spirit (0-255)</p></td>
</tr>
<tr>
<td><p>0x06</p></td>
<td><p>1 byte</p></td>
<td><p>Dexterity (0-255)</p></td>
</tr>
<tr>
<td><p>0x07</p></td>
<td><p>1 byte</p></td>
<td><p>Luck (0-255)</p></td>
</tr>
<tr>
<td><p>0x08</p></td>
<td><p>1 byte</p></td>
<td><p>Strength Bonus (Power Sources used)</p></td>
</tr>
<tr>
<td><p>0x09</p></td>
<td><p>1 byte</p></td>
<td><p>Vitality Bonus (Guard Sources used)</p></td>
</tr>
<tr>
<td><p>0x0A</p></td>
<td><p>1 byte</p></td>
<td><p>Magic Bonus (Magic Sources used)</p></td>
</tr>
<tr>
<td><p>0x0B</p></td>
<td><p>1 byte</p></td>
<td><p>Spirit Bonus (Mind Sources used)</p></td>
</tr>
<tr>
<td><p>0x0C</p></td>
<td><p>1 byte</p></td>
<td><p>Dexterity Bonus (Speed Sources used)</p></td>
</tr>
<tr>
<td><p>0x0D</p></td>
<td><p>1 byte</p></td>
<td><p>Luck Bonus (Luck Sources used)</p></td>
</tr>
<tr>
<td><p>0x0E</p></td>
<td><p>1 byte</p></td>
<td><p>Current limit level (1-4)</p></td>
</tr>
<tr>
<td><p>0x0F</p></td>
<td><p>1 byte</p></td>
<td><p>Current limit bar (0xFF = limit break)</p></td>
</tr>
<tr>
<td><p>0x10</p></td>
<td><p>12 bytes</p></td>
<td><p>Name (<a href="FF_Text" title="wikilink">FF Text</a> format) Game's Naming Boxes Cap you At 9 Chars</p></td>
</tr>
<tr>
<td><p>0x1C</p></td>
<td><p>1 byte</p></td>
<td><p>Equipped weapon</p></td>
</tr>
<tr>
<td><p>0x1D</p></td>
<td><p>1 byte</p></td>
<td><p>Equipped armor</p></td>
</tr>
<tr>
<td><p>0x1E</p></td>
<td><p>1 byte</p></td>
<td><p>Equipped accessory</p></td>
</tr>
<tr>
<td><p>0x1F</p></td>
<td><p>1 byte</p></td>
<td><p>Character flags - 0x10-Sadness, 0x20-Fury</p></td>
</tr>
<tr>
<td><p>0x20</p></td>
<td><p>1 byte</p></td>
<td><p>Char order - 0xFF-Normal, 0xFE-Back row</p></td>
</tr>
<tr>
<td><p>0x21</p></td>
<td><p>1 byte</p></td>
<td><p>Level progress bar (0-63) Games Gui Hides Values &lt;4, 4-63 are visible as "progress"</p></td>
</tr>
<tr>
<td><p>0x22</p></td>
<td><p>2 bytes</p></td>
<td><p>Learned limit skills<br />
0x0001: Limit Lv. 1-1<br />
0x0002: Limit Lv. 1-2<br />
<small>0x0004: Always 0 (reserved bit or spacer/breaker/end of limit)</small><br />
0x0008: Limit Lv. 2-1<br />
0x0010: Limit Lv. 2-2<br />
<small>0x0020: Always 0 (reserved bit or spacer/breaker/end of limit)</small><br />
0x0040: Limit Lv. 3-1<br />
0x0080: Limit Lv. 3-2<br />
<small>0x0100: Always 0 (reserved bit or spacer/breaker/end of limit)</small><br />
0x0200: Limit Lv. 4<br />
</p></td>
</tr>
<tr>
<td><p>0x24</p></td>
<td><p>2 bytes</p></td>
<td><p>Number of kills</p></td>
</tr>
<tr>
<td><p>0x26</p></td>
<td><p>2 bytes</p></td>
<td><p>Times limit 1-1 has been used</p></td>
</tr>
<tr>
<td><p>0x28</p></td>
<td><p>2 bytes</p></td>
<td><p>Times limit 2-1 has been used</p></td>
</tr>
<tr>
<td><p>0x2A</p></td>
<td><p>2 bytes</p></td>
<td><p>Times limit 3-1 has been used</p></td>
</tr>
<tr>
<td><p>0x2C</p></td>
<td><p>2 bytes</p></td>
<td><p>Current HP</p></td>
</tr>
<tr>
<td><p>0x2E</p></td>
<td><p>2 bytes</p></td>
<td><p>Base HP (before materia alterations)</p></td>
</tr>
<tr>
<td><p>0x30</p></td>
<td><p>2 bytes</p></td>
<td><p>Current MP</p></td>
</tr>
<tr>
<td><p>0x32</p></td>
<td><p>2 bytes</p></td>
<td><p>Base MP (before materia alterations)</p></td>
</tr>
<tr>
<td style="background: rgb(255,255,204)"><p>0x34</p></td>
<td style="background: rgb(255,255,204)"><p>4 bytes</p></td>
<td style="background: rgb(255,255,204)"><p>Unknown</p></td>
</tr>
<tr>
<td><p>0x38</p></td>
<td><p>2 bytes</p></td>
<td><p>Maximum HP (after materia alterations)</p></td>
</tr>
<tr>
<td><p>0x3A</p></td>
<td><p>2 bytes</p></td>
<td><p>Maximum MP (after materia alterations)</p></td>
</tr>
<tr>
<td><p>0x3C</p></td>
<td><p>4 bytes</p></td>
<td><p>Current EXP</p></td>
</tr>
<tr>
<td><p>0x40</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 1</p></td>
</tr>
<tr>
<td><p>0x44</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 2</p></td>
</tr>
<tr>
<td><p>0x48</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 3</p></td>
</tr>
<tr>
<td><p>0x4C</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 4</p></td>
</tr>
<tr>
<td><p>0x50</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 5</p></td>
</tr>
<tr>
<td><p>0x54</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 6</p></td>
</tr>
<tr>
<td><p>0x58</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 7</p></td>
</tr>
<tr>
<td><p>0x5C</p></td>
<td><p>4 bytes</p></td>
<td><p>Weapon materia slot number 8</p></td>
</tr>
<tr>
<td><p>0x60</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 1</p></td>
</tr>
<tr>
<td><p>0x64</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 2</p></td>
</tr>
<tr>
<td><p>0x68</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 3</p></td>
</tr>
<tr>
<td><p>0x6C</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 4</p></td>
</tr>
<tr>
<td><p>0x70</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 5</p></td>
</tr>
<tr>
<td><p>0x74</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 6</p></td>
</tr>
<tr>
<td><p>0x78</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 7</p></td>
</tr>
<tr>
<td><p>0x7C</p></td>
<td><p>4 bytes</p></td>
<td><p>Armor materia slot number 8</p></td>
</tr>
<tr>
<td><p>0x80</p></td>
<td><p>4 bytes</p></td>
<td><p>EXP to next level</p></td>
</tr>
</tbody>
</table>

## Chocobo Record

| Offset | Length  | Description                             |
|--------|---------|-----------------------------------------|
| 0x0    | 2 bytes | Sprint Speed                            |
| 0x2    | 2 bytes | Max Sprint Speed                        |
| 0x4    | 2 bytes | Speed                                   |
| 0x6    | 2 bytes | Max Speed                               |
| 0x8    | 1 byte  | Acceleration                            |
| 0x9    | 1 byte  | Cooperation                             |
| 0xA    | 1 byte  | Intelligence                            |
| 0xB    | 1 byte  | Personality                             |
| 0xC    | 1 byte  | Pcount (?)                              |
| 0xD    | 1 byte  | Number of races won                     |
| 0xE    | 1 byte  | 1: female)                              |
| 0xF    | 1 byte  | Type (Yellow, Green, Blue, Black, Gold) |

**Table 3: Chocobo Record**

## Save Item List

Each item in the item list is stored as a word value with the quantity, expressed as a 7-bit value, concatenated with the item's index, expressed as a 9-bit value between the range of 0-320. In Binary: QQQQQQQXXXXXXXXX Where X is the index and Q is the quantity. There are a total of 320 item slots in the save map and a total of 320 objects that are stored there, some of which are dummy items. The objects are indexed like this:  
Indexes 0 - 127: Items  
Indexes 128 - 255: Weapons  
Indexes 256 - 287: Armors  
Indexes 288 - 319: Accessories  
Quantity is limited (by the menu mechanics) to 99 since there are only two characters available in the item menu to show quantity. A Graphical "glitch" occurs in the ten's digit when quantity exceeds that number. The menu only checks the current quantity to determine if the value can increase and the quantity will not decrease unless an item is used or sold. Forcing the quantity to exceed 99 does not have any side effect with most versions of the game. The Japanese PSX version(BISLPS-00700) is the only version with a problem when you exceed a quantity of 99 for an item. This version will experience an error during battles when you have more then 99 of an item.

## Save Materia List

Materia is stored as a single-byte ID followed by the amount of AP on that instance of Materia stored as an unsigned 24-bit integer.eskill materia does not use the ap value, but instead the 24 bits as switches for each skill that can be learned. For every materia ap =0xFFFFFF when mastered

| ID   | Name             | Type         |
|------|------------------|--------------|
| 0x00 | MP Plus          | Independent  |
| 0x01 | HP Plus          | Independent  |
| 0x02 | Speed Plus       | Independent  |
| 0x03 | Magic Plus       | Independent  |
| 0x04 | Luck Plus        | Independent  |
| 0x05 | EXP Plus         | Independent  |
| 0x06 | Gil Plus         | Independent  |
| 0x07 | Enemy Away       | Independent  |
| 0x08 | Enemy Lure       | Independent  |
| 0x09 | Chocobo Lure     | Independent  |
| 0x0B | Long Range       | Independent  |
| 0x0C | Mega All         | Independent  |
| 0x0D | Counter Attack   | Independent  |
| 0x0E | Slash-All        | Command      |
| 0x0F | Double Cut       | Command      |
| 0x0A | Pre-emptive      | Independent  |
| 0x10 | Cover            | Independent  |
| 0x11 | Underwater       | Independent  |
| 0x12 | HP \<-\> MP      | Independent  |
| 0x13 | W-Magic          | Command      |
| 0x14 | W-Summon         | Command      |
| 0x15 | W-Item           | Command      |
| 0x16 | Unknown          | Placeholder? |
| 0x17 | All              | Support      |
| 0x18 | Counter          | Support      |
| 0x19 | Magic Counter    | Support      |
| 0x1A | MP Turbo         | Support      |
| 0x1B | MP Absorb        | Support      |
| 0x1C | HP Absorb        | Support      |
| 0x1D | Elemental        | Support      |
| 0x1E | Added Effect     | Support      |
| 0x1F | Sneak Attack     | Support      |
| 0x20 | Final Attack     | Support      |
| 0x21 | Added Cut        | Support      |
| 0x22 | Steal As Well    | Support      |
| 0x23 | Quadra Magic     | Support      |
| 0x24 | Steal            | Command      |
| 0x25 | Sense            | Command      |
| 0x26 | Unknown          | Placeholder? |
| 0x27 | Throw            | Command      |
| 0x28 | Morph            | Command      |
| 0x29 | Deathblow        | Command      |
| 0x2A | Manipulate       | Command      |
| 0x2B | Mime             | Command      |
| 0x2C | Enemy Skill      | Command      |
| 0x2D | Unknown          | Placeholder? |
| 0x2E | Unknown          | Placeholder? |
| 0x2F | Unknown          | Placeholder? |
| 0x30 | Master Command   | Command      |
| 0x31 | Fire             | Magic        |
| 0x32 | Ice              | Magic        |
| 0x33 | Earth            | Magic        |
| 0x34 | Lightning        | Magic        |
| 0x35 | Restore          | Magic        |
| 0x36 | Heal             | Magic        |
| 0x37 | Revive           | Magic        |
| 0x38 | Seal             | Magic        |
| 0x39 | Mystify          | Magic        |
| 0x3A | Transform        | Magic        |
| 0x3B | Exit             | Magic        |
| 0x3C | Poison           | Magic        |
| 0x3D | Demi             | Magic        |
| 0x3E | Barrier          | Magic        |
| 0x3F | Unknown          | Placeholder? |
| 0x40 | Comet            | Magic        |
| 0x41 | Time             | Magic        |
| 0x42 | Unknown          | Placeholder? |
| 0x43 | Unknown          | Placeholder? |
| 0x44 | Destruct         | Magic        |
| 0x45 | Contain          | Magic        |
| 0x46 | FullCure         | Magic        |
| 0x47 | Shield           | Magic        |
| 0x48 | Ultima           | Magic        |
| 0x49 | Master Magic     | Magic        |
| 0x4A | Choco/Mog        | Summon       |
| 0x4B | Shiva            | Summon       |
| 0x4C | Ifrit            | Summon       |
| 0x4D | Ramuh            | Summon       |
| 0x4E | Titan            | Summon       |
| 0x4F | Odin             | Summon       |
| 0x50 | Leviathan        | Summon       |
| 0x51 | Bahamut          | Summon       |
| 0x52 | Kujata           | Summon       |
| 0x53 | Alexander        | Summon       |
| 0x54 | Phoenix          | Summon       |
| 0x55 | Neo Bahamut      | Summon       |
| 0x56 | Hades            | Summon       |
| 0x57 | Typhoon          | Summon       |
| 0x58 | Bahamut ZERO     | Summon       |
| 0x59 | Knights of Round | Summon       |
| 0x5A | Master Summon    | Summon       |
| 0xFF | Empty Slot       | NONE         |

**Table 1: Materia List (PC)**

## Key Item List

Key Items are stored in Bank 1 of the Savemap, one bit for each item. Bit ON - party has the item.

<table>
<caption><strong>Table 1: Key Items List</strong></caption>
<thead>
<tr>
<th><p>Variable</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x0BE4<br />
Var 64</p></td>
<td><p>0x01: Cotton Dress<br />
0x02: Satin Dress<br />
0x04: Silk Dress<br />
0x08: Wig<br />
0x10: Dyed Wig<br />
0x20: Blonde Wig<br />
0x40: Glass Tiara<br />
0x80: Ruby Tiara</p></td>
</tr>
<tr>
<td><p>0x0BE5<br />
Var 65</p></td>
<td><p>0x01: Diamond Tiara<br />
0x02: Cologne<br />
0x04: Flower cologne<br />
0x08: Sexy Cologne<br />
0x10: Member's Card<br />
0x20: Lingerie<br />
0x40: Mystery panties<br />
0x80: Bikini briefs</p></td>
</tr>
<tr>
<td><p>0x0BE6<br />
Var 66</p></td>
<td><p>0x01: Pharmacy Coupon<br />
0x02: Disinfectant<br />
0x04: Deodorant<br />
0x08: Digestive<br />
0x10: Huge Materia (Fort Condor)<br />
0x20: Huge Materia (Corel)<br />
0x40: Huge Materia (Underwater)<br />
0x80: Huge Materia (rocket)</p></td>
</tr>
<tr>
<td><p>0x0BE7<br />
Var 67</p></td>
<td><p>0x01: Key to Ancients<br />
0x02: Letter to a Daughter<br />
0x04: Letter to a Wife<br />
0x08: Lunar Harp<br />
0x10: Basement Key<br />
0x20: Key to Sector 5<br />
0x40: Keycard 60<br />
0x80: Keycard 62</p></td>
</tr>
<tr>
<td><p>0x0BE8<br />
Var 68</p></td>
<td><p>0x01: Keycard 65<br />
0x02: Keycard 66<br />
0x04: Keycard 68<br />
0x08: Midgar parts<br />
0x10: Midgar parts<br />
0x20: Midgar parts<br />
0x40: Midgar parts<br />
0x80: Midgar parts</p></td>
</tr>
<tr>
<td><p>0x0BE9<br />
Var 69</p></td>
<td><p>0x01: PHS<br />
0x02: Gold Ticket<br />
0x04: Keystone<br />
0x08: Leviathan Scales<br />
0x10: Glacier Map<br />
0x20: A Coupon<br />
0x40: B Coupon<br />
0x80: C Coupon</p></td>
</tr>
<tr>
<td><p>0x0BEA<br />
Var 70</p></td>
<td><p>0x01: Black Materia<br />
0x02: Mythril<br />
0x04: Snowboard</p></td>
</tr>
</tbody>
</table>

## KERNEL.BIN Section 4 Entry

During game initialization, section 4 from KERNEL.BIN is decompressed and copied into RAM. This is all the initial values and structure for most of the Save, excluding the header data and the tail of the last bank (0x0054 to 0x0B93).

## Documentation Notes & Format

Format: Bit mask: Bit description \[Hex byte value\] {Field Keyword}  
Example: 0x04: Set to 1 if we choose no drink when talking to tifa. \[0x0F\] {MDS7PB_1}  
Bit mask: Is the bit position number in hex. Bit7(0x80)\|Bit6(0x40)\|Bit5(0x20)\|Bit4(0x10)\|Bit3(0x08)\|Bit2(0x04)\|Bit1(0x02)\|Bit0(0x01)

Note: We use [LBS 0](../Bit_numbering) bit numbering.

Bit description: What bit does.

Hex byte value: The Byte's value in hex when the bit change.(optional)

Field Keyword: Field name code.
