---
title: AKAO_sequence
---

## Introduction

AKAO sequence is the most complicated part of the FF7 sound system. ("AKAO" is the signature string, which implies that the sound format has developed by Square Enix sound programmer Minoru Akao.)

AKAO sequence is similar to MIDI sequence - it's custom tracker format for playing sequence sound, well tuned specially for PSX.

The sequence data can be found in all FF7 game modules: Field, Battle, Worldmap and in minigames.

All files with exension \*.SND are AKAO.

- **MINI/ASERI2.SND** - Battle Arena theme
- **MINI/SENSUI.SND** - used in Submarine minigame
- **ENEMY6/OVER2.SND** - game over sequence
- **ENEMY6/FAN2.SND** - battle win "fanfare" sequence
- **MOVIE/OVER2.SND** - same game over sequence, don't know, why to duplicate data

Other AKAO sequences are hard-wired in other files.

## File Structure

### Header (size: 16 bytes)

`struct AkaoSeqHeader`  
`{`  
`  static const uint8_t magic[4];  // "AKAO" C-string`  
`  uint16_t id;                    // song ID, used for playing sequence`  
`  uint16_t length;                // data length - sizeof(header)`  
`  uint16_t reverb_type;           // reverb type (range from 0 to 9)`  
`  struct AkaoTimeStamp timestamp; // creation time`  
`};`  
  
`struct AkaoTimeStamp`  
`{`  
`  uint8_t year_bcd;               // year (in binary coded decimal)`  
`  uint8_t month_bcd;              // month (in binary coded decimal, between 0x01 - 0x12)`  
`  uint8_t day_bcd;                // day (in binary coded decimal, between 0x01 - 0x31)`  
`  uint8_t hours_bcd;              // hours (in binary coded decimal, between 0x00 - 0x23)`  
`  uint8_t minutes_bcd;            // minutes (in binary coded decimal, between 0x00 - 0x59)`  
`  uint8_t seconds_bcd;            // seconds (in binary coded decimal, between 0x00 - 0x59)`  
`};`

### Channel Info (size: 4 bytes + 2 bytes \* <channels count>)

`struct AkaoChannelInfo`  
`{`  
`  uint32_t mask;                         // represents bitmask of used channels in this song`  
`  uint16_t start_offsets[num_channels];  // offsets to channel opcode data`  
`};`

`int num_channels = 0;`  
`while (int bit = 0; bit < 24; bit++)`  
`  if ((info.mask & 0xFFFFFF) & (1 << bit)) != 0)`  
`    num_channels++;`

First there is 32-bit number (offset 0x10), which represents bitmask of used channels in this song.

After this bitmask, there is <channels count> offsets to channel opcode data counting from current offset. Each offsets is a relative offset based on the address \*next to\* the offset itself. (This is a general rule for early versions of AKAO to interpret relative offsets.)

### Channel Commands \[AKAO Opcodes\]

For every channels in an AKAO sequence, there is a set of commands to perform. This is similar to Field opcodes. Here I will call this sound commands "opcodes". Every opcode has its own number of arguments (from no-arguments, to 3 arguments).

### Drum Instrument Map Table

When a song uses a drum kit with [opcode 0xEC](Opcodes/0xeced), a drum instrument map table will be placed at the end of the sequence. The table determines the instrument, channel volume and pan for each keys.

The table consists of a repetition of 5-byte items.

`struct AkaoDrumKeyAttr`  
`{`  
`  uint8_t instrument;   // corresponding to opcode 0xA1`  
`  uint8_t key;          // note number when playing the drum note`  
`  uint16_t volume;      // corresponding to opcode 0xA8 (lower 8bit is a fractional part of the volume)`  
`  uint8_t pan;          // corresponding to opcode 0xAA`  
`}`

## Example (Home-Created AKAO Sequence):

### Header

**41 4b 41 4f** - AKAO string

**34 12** - song ID: 0x1234

**16 00** - data length 0x16 in hex or 22 in decimal

**04 00** - reverb type: 4 (large studio)

**96 12 18 22 46 28** - created at 1996-12-18 22:46:28

### Channel Info

**01 00 00 00** - this indicates, that used only one channel

**00 00** - offset to first channel opcodes: in our example 0x00 means that next to this offset is opcodes for first channel

### Channel Commands

**e8 a8 66** - sets tempo, parameter 0x66a8

**ea 00 50** - sets reverb depth

**a8 55** - load sample 0x55 from INSTR.ALL to channel

**aa 40** - sets channel volume

**c2** - turns on reverb effect

**a1 0c** - sets volume pan

**c8** - sets loop point

**66** - 0x66 % 11 = 3 (3 means to take 3rd number from play length table), 0x66 / 11 = 9 (9 means to take pitch\[9\] from loaded instrument record index)

**ca** - returns to saved loop point with opcode c8

This example plays Chocobo "Whoo-Hoo" (instrument number 0x55) repeatedly.

## Sound Opcode List

<table>
<thead>
<tr>
<th><p>Opcode</p></th>
<th><p>Summary</p></th>
<th><p>Length</p></th>
<th><p>Operands</p></th>
<th><p>Note</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p><a href="Opcodes/0x0099" title="wikilink">0x00-0x99</a></p></td>
<td><p>Note, Tie, Rest</p></td>
<td><p>1</p></td>
<td></td>
<td><p>The opcode indicates the note key and length. The note will be keyed off 2 ticks before the next note.</p></td>
</tr>
<tr>
<td><p>0x9A-0x9F</p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xA0</a></p></td>
<td><p>Finish Channel</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa1" title="wikilink">0xA1</a></p></td>
<td><p>Load Instrument</p></td>
<td><p>2</p></td>
<td><p>instrument: byte (0-127)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0x0099" title="wikilink">0xA2</a></p></td>
<td><p>Overwrite Next Note Length</p></td>
<td><p>2</p></td>
<td><p>length: byte</p></td>
<td><p>Ignores the regular length (delta-time) of the next note and overwrites it with the specified length.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa8aa" title="wikilink">0xA3</a></p></td>
<td><p>Channel Master Volume</p></td>
<td><p>2</p></td>
<td><p>volume: byte (0-127)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa4" title="wikilink">0xA4</a></p></td>
<td><p>Pitch Bend Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, semitones: signed byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa5" title="wikilink">0xA5</a></p></td>
<td><p>Set Octave</p></td>
<td><p>2</p></td>
<td><p>octave: byte (0-15)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa5" title="wikilink">0xA6</a></p></td>
<td><p>Increase Octave</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa5" title="wikilink">0xA7</a></p></td>
<td><p>Decrease Octave</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa8aa" title="wikilink">0xA8</a></p></td>
<td><p>Channel Volume</p></td>
<td><p>2</p></td>
<td><p>volume: byte (0-127)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa9" title="wikilink">0xA9</a></p></td>
<td><p>Channel Volume Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, volume: byte (0-127)</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa8aa" title="wikilink">0xAA</a></p></td>
<td><p>Channel Pan</p></td>
<td><p>2</p></td>
<td><p>pan: byte (0-127)</p></td>
<td><p>64 is the center.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xab" title="wikilink">0xAB</a></p></td>
<td><p>Channel Pan Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, pan: byte (0-127)</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xac" title="wikilink">0xAC</a></p></td>
<td><p>Noise Clock Frequency</p></td>
<td><p>2</p></td>
<td><p>clock: byte (0x00-0x3f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xAD</a></p></td>
<td><p>ADSR: Attack Rate</p></td>
<td><p>2</p></td>
<td><p>attack_rate: byte (0x00-0x7f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xAE</a></p></td>
<td><p>ADSR: Decay Rate</p></td>
<td><p>2</p></td>
<td><p>decay_rate: byte (0x00-0x0f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xAF</a></p></td>
<td><p>ADSR: Sustain Level</p></td>
<td><p>2</p></td>
<td><p>sustain_level: byte (0x00-0x0f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xB0</a></p></td>
<td><p>ADSR: Decay Rate &amp; Sustain Level</p></td>
<td><p>3</p></td>
<td><p>decay_rate: byte (0x00-0x0f), sustain_level: byte (0x00-0x0f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xB1</a></p></td>
<td><p>ADSR: Sustain Rate</p></td>
<td><p>2</p></td>
<td><p>sustain_rate: byte (0x00-0x7f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xB2</a></p></td>
<td><p>ADSR: Release Rate</p></td>
<td><p>2</p></td>
<td><p>release_rate: byte (0x00-0x1f)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xB3</a></p></td>
<td><p>ADSR: Reset ADSR</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb4b5" title="wikilink">0xB4</a></p></td>
<td><p>Vibrato (Channel Pitch LFO)</p></td>
<td><p>4</p></td>
<td><p>delay: byte, rate: byte, type: byte (0-15)</p></td>
<td><p>When <code>rate</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb4b5" title="wikilink">0xB5</a></p></td>
<td><p>Vibrato Depth</p></td>
<td><p>2</p></td>
<td><p>depth: byte</p></td>
<td><p>The most significant bit of the <code>depth</code> determines the amplitude range.</p>
<p>When it is 0, the range is up to about ± 50 cents (amplitude is 15/256 compared with range type 1).</p>
<p>When it is 1, the range is up to about ± 700 cents.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb4b5" title="wikilink">0xB6</a></p></td>
<td><p>Turn Off Vibrato</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xB7</a></p></td>
<td><p>ADSR: Attack Mode</p></td>
<td><p>2</p></td>
<td><p>attack_mode: byte (1 or 5)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb8b9" title="wikilink">0xB8</a></p></td>
<td><p>Tremolo (Channel Volume LFO)</p></td>
<td><p>4</p></td>
<td><p>delay: byte, rate: byte, type: byte (0-15)</p></td>
<td><p>When <code>rate</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb8b9" title="wikilink">0xB9</a></p></td>
<td><p>Tremolo Depth</p></td>
<td><p>2</p></td>
<td><p>depth: byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xb8b9" title="wikilink">0xBA</a></p></td>
<td><p>Turn Off Tremolo</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/ADSR" title="wikilink">0xBB</a></p></td>
<td><p>ADSR: Sustain Mode</p></td>
<td><p>2</p></td>
<td><p>sustain_mode: byte (1, 3, 5 or 7)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xbcbd" title="wikilink">0xBC</a></p></td>
<td><p>Channel Pan LFO</p></td>
<td><p>3</p></td>
<td><p>rate: byte, type: byte (0-15)</p></td>
<td><p>When <code>rate</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xbcbd" title="wikilink">0xBD</a></p></td>
<td><p>Channel Pan LFO Depth</p></td>
<td><p>2</p></td>
<td><p>depth: byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xbcbd" title="wikilink">0xBE</a></p></td>
<td><p>Turn Off Channel Pan LFO</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xbf" title="wikilink">0xBF</a></p></td>
<td><p>ADSR: Release Mode</p></td>
<td><p>2</p></td>
<td><p>release_mode: byte (3 or 7)</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc0c1" title="wikilink">0xC0</a></p></td>
<td><p>Channel Transpose (Absolute)</p></td>
<td><p>2</p></td>
<td><p>semitones: signed byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc0c1" title="wikilink">0xC1</a></p></td>
<td><p>Channel Transpose (Relative)</p></td>
<td><p>2</p></td>
<td><p>semitones: signed byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc2c3" title="wikilink">0xC2</a></p></td>
<td><p>Turn On Reverb</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc2c3" title="wikilink">0xC3</a></p></td>
<td><p>Turn Off Reverb</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc4c5" title="wikilink">0xC4</a></p></td>
<td><p>Turn On Noise</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc4c5" title="wikilink">0xC5</a></p></td>
<td><p>Turn Off Noise</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc6c7" title="wikilink">0xC6</a></p></td>
<td><p>Turn On Frequency Modulation</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc6c7" title="wikilink">0xC7</a></p></td>
<td><p>Turn Off Frequency Modulation</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc8c9" title="wikilink">0xC8</a></p></td>
<td><p>Loop Point</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Remember the current offset as a loop point and increase the nesting level of the loop.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc8c9" title="wikilink">0xC9</a></p></td>
<td><p>Return to Loop Point Up to N Times</p></td>
<td><p>2</p></td>
<td><p>times: byte</p></td>
<td><p>On the Nth repeat, this instruction will end the current loop by decrementing the nesting level of the loop. Otherwise, it will increment the loop counter and return to the loop point. When <code>times</code> is 0, it will be translated to 256 times.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xc8c9" title="wikilink">0xCA</a></p></td>
<td><p>Return to Loop Point</p></td>
<td><p>1</p></td>
<td></td>
<td><p>This instruction will increment the loop counter.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xcb" title="wikilink">0xCB</a></p></td>
<td><p>Reset Sound Effects</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Reset sound effects such as noise, frequency modulation, reverb, overlay voice and alternate voice.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xcccd" title="wikilink">0xCC</a></p></td>
<td><p>Turn On Legato</p></td>
<td><p>1</p></td>
<td></td>
<td><p>This instruction will stop the regular key on and key off performance of the subsequent notes and update the pitch only.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xcccd" title="wikilink">0xCD</a></p></td>
<td><p>Turn Off Legato</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xcecf" title="wikilink">0xCE</a></p></td>
<td><p>Turn On Noise and Toggle Noise On/Off after a Period of Time</p></td>
<td><p>2</p></td>
<td><p>delay: byte</p></td>
<td><p>When <code>delay</code> is 0, it will be translated to 257 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xcecf" title="wikilink">0xCF</a></p></td>
<td><p>Toggle Noise On/Off after a Period of Time</p></td>
<td><p>2</p></td>
<td><p>delay: byte</p></td>
<td><p>When <code>delay</code> is 0, it will be translated to 257 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd0d1" title="wikilink">0xD0</a></p></td>
<td><p>Turn On Full-Length Note Mode</p></td>
<td><p>1</p></td>
<td></td>
<td><p>This instruction will stop the regular key off performance of the subsequent notes.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd0d1" title="wikilink">0xD1</a></p></td>
<td><p>Turn Off Full-Length Note Mode</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd2d3" title="wikilink">0xD2</a></p></td>
<td><p>Turn On Frequency Modulation and Toggle Frequency Modulation On/Off after a Period of Time</p></td>
<td><p>2</p></td>
<td><p>delay: byte</p></td>
<td><p>When <code>delay</code> is 0, it will be translated to 257 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd2d3" title="wikilink">0xD3</a></p></td>
<td><p>Toggle Frequency Modulation On/Off after a Period of Time</p></td>
<td><p>2</p></td>
<td><p>delay: byte</p></td>
<td><p>When <code>delay</code> is 0, it will be translated to 257 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd4d5" title="wikilink">0xD4</a></p></td>
<td><p>Turn On Playback Rate Side Chain</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Duplicate and use the playback frequency of the previous voice channel.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd4d5" title="wikilink">0xD5</a></p></td>
<td><p>Turn Off Playback Rate Side Chain</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd6d7" title="wikilink">0xD6</a></p></td>
<td><p>Turn On Pitch-Volume Side Chain</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Multiply the playback frequency of the previous voice channel to the output volume. Lower pitch will make the volume smaller.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd6d7" title="wikilink">0xD7</a></p></td>
<td><p>Turn Off Pitch-Volume Side Chain</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd8d9" title="wikilink">0xD8</a></p></td>
<td><p>Channel Fine Tuning (Absolute)</p></td>
<td><p>2</p></td>
<td><p>amount: signed byte</p></td>
<td><p>The pitch can be changed in the range of one octave above and below. The <code>amount</code> is the multiplicand for the playback frequency, not a log-based parameter like cents. For example, when the <code>amount</code> is 127, the pitch will be multiplied by 127/128 (about +1 octave). Negative value ​​will lower the pitch.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xd8d9" title="wikilink">0xD9</a></p></td>
<td><p>Channel Fine Tuning (Relative)</p></td>
<td><p>2</p></td>
<td><p>amount: signed byte</p></td>
<td><p>The <code>amount</code> will be added to the current tuning amount.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xdadb" title="wikilink">0xDA</a></p></td>
<td><p>Turn On Portamento</p></td>
<td><p>2</p></td>
<td><p>speed: byte</p></td>
<td><p>When <code>speed</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xdadb" title="wikilink">0xDB</a></p></td>
<td><p>Turn Off Portamento</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0x0099" title="wikilink">0xDC</a></p></td>
<td><p>Fix Note Length</p></td>
<td><p>2</p></td>
<td><p>length_to_add: signed byte</p></td>
<td><p>Ignore the regular length (delta-time) of subsequent notes and set to the fixed length. The <code>length_to_add</code> parameter will be added to the current length value. (the initial value is 0)</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xdd" title="wikilink">0xDD</a></p></td>
<td><p>Vibrato Depth Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, depth: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xde" title="wikilink">0xDE</a></p></td>
<td><p>Tremolo Depth Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, depth: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xdf" title="wikilink">0xDF</a></p></td>
<td><p>Channel Pan LFO Depth Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, depth: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xE0-0xE7</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe8e9" title="wikilink">0xE8</a></p></td>
<td><p>Tempo</p></td>
<td><p>3</p></td>
<td><p>tempo: uint16 |bpm = tempo / 214.998204 (approximate) More strictly, <code>bpm = 60.0 / (48 * (65536.0 / tempo) * (0x44E8 / (33868800.0 / 8)))</code></p>
<p>Note that this coefficient is different from other games with PlayStation AKAO.</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe8e9" title="wikilink">0xE9</a></p></td>
<td><p>Tempo Slide</p></td>
<td><p>4</p></td>
<td><p>length: byte, tempo: uint16</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xeaeb" title="wikilink">0xEA</a></p></td>
<td><p>Reverb Depth</p></td>
<td><p>3</p></td>
<td><p>depth: uint16</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xeaeb" title="wikilink">0xEB</a></p></td>
<td><p>Reverb Depth Slide</p></td>
<td><p>4</p></td>
<td><p>length: byte, depth: uint16</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xeced" title="wikilink">0xEC</a></p></td>
<td><p>Turn On Drum Mode</p></td>
<td><p>3</p></td>
<td><p>drum_map_offset: signed int16</p></td>
<td><p>The <code>drum_map_offset</code> is a relative offset pointing to the drum instrument map table, which determines the instrument for each keys.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xeced" title="wikilink">0xED</a></p></td>
<td><p>Turn Off Drum Mode</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xee" title="wikilink">0xEE</a></p></td>
<td><p>Unconditional Jump</p></td>
<td><p>3</p></td>
<td><p>destination_offset: signed int16</p></td>
<td><p>This instruction can be used to make an infinite loop.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xef" title="wikilink">0xEF</a></p></td>
<td><p>CPU-Conditional Jump</p></td>
<td><p>4</p></td>
<td><p>condition: byte, destination_offset: signed int16</p></td>
<td><p>Jump if the condition variable matches <code>condition</code>. The value of the condition variable can be set from the game program.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf0f1" title="wikilink">0xF0</a></p></td>
<td><p>Jump on the Nth Repeat</p></td>
<td><p>4</p></td>
<td><p>times: byte, destination_offset: signed int16</p></td>
<td><p>When <code>times</code> is 0, it will be translated to 256 times.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf0f1" title="wikilink">0xF1</a></p></td>
<td><p>Break the Loop on the Nth Repeat</p></td>
<td><p>4</p></td>
<td><p>times: byte, destination_offset: signed int16</p></td>
<td><p>Unlike 0xF0, this instruction will end the current loop by decrementing the nesting level of the loop. When <code>times</code> is 0, it will be translated to 256 times.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa1" title="wikilink">0xF2</a></p></td>
<td><p>Load Instrument (No Attack Sample)</p></td>
<td><p>2</p></td>
<td><p>instrument: byte</p></td>
<td><p>Unlike 0xA1, the sample before the loop point is replaced by a short, silence sample.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf3" title="wikilink">0xF3</a></p></td>
<td><p>Unknown</p></td>
<td><p>1</p></td>
<td></td>
<td><p>There is no actual use in music.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf4f5" title="wikilink">0xF4</a></p></td>
<td><p>Turn On Overlay Voice</p></td>
<td><p>3</p></td>
<td><p>instrument: byte, instrument2: byte</p></td>
<td><p>Play the same melody by different instruments on two voice channels. A free voice channel is required to work. Note that the two channels share the playback rate, and the pitch is not calculated for each instruments. Used in the song "Anxious Heart".</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf4f5" title="wikilink">0xF5</a></p></td>
<td><p>Turn Off Overlay Voice</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf4f5" title="wikilink">0xF6</a></p></td>
<td><p>Overlay Volume Balance</p></td>
<td><p>2</p></td>
<td><p>balance: byte (0-127)</p></td>
<td><p>When the balance is 0, the volume of the primary voice will be 100% (127/128) of original and that of the secondary voice will be 0%. 127 is the opposite.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf4f5" title="wikilink">0xF7</a></p></td>
<td><p>Overlay Volume Balance Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, balance: byte (0-127)</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf8f9" title="wikilink">0xF8</a></p></td>
<td><p>Turn On Alternate Voice</p></td>
<td><p>2</p></td>
<td><p>release_rate: byte (0x00-0x1f)</p></td>
<td><p>This instruction allows subsequent notes to be played on two alternating channels. At the same time, the ADSR release rate will be set to the specified value. A free voice channel is required to work. Check "Opening - Bombing Mission", "Tifa's Theme" and "Fortress of the Condor" for actual usage.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf8f9" title="wikilink">0xF9</a></p></td>
<td><p>Turn Off Alternate Voice</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFA-0xFC</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfd" title="wikilink">0xFD</a></p></td>
<td><p>Time Signature</p></td>
<td><p>3</p></td>
<td><p>ticks_per_beat: byte, beats_per_measure: byte</p></td>
<td><p>Note that two parameters can be 0. This pattern is used for initialization.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe" title="wikilink">0xFE</a></p></td>
<td><p>Measure Number</p></td>
<td><p>3</p></td>
<td><p>measure: short</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFF</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
</tbody>
</table>
