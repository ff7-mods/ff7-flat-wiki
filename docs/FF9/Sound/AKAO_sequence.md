---
title: AKAO_sequence
---

## Introduction

AKAO sequence is similar to MIDI sequence - it's custom tracker format for playing sequence sound, well tuned specially for PSX.

## File Structure

### Header (size: 64 bytes)

`struct AkaoSeqHeader`  
`{`  
`  static const uint8_t magic[4];  // "AKAO" C-string`  
`  uint16_t id;                    // song ID, used for playing sequence`  
`  uint16_t length;                // data length (including this header)`  
`  uint16_t reverb_type;           // reverb type (range from 0 to 9)`  
`  uint8_t field_0A[6];`  
`  uint32_t field_10;`  
`  uint16_t sample_set_id;         // associated sample set ID`  
`  uint16_t field_12;`  
`  uint32_t field_14;`  
`  uint32_t field_18;`  
`  uint32_t field_1C;`  
`  uint32_t mask;                  // represents bitmask of used channels in this song`  
`  uint32_t field_24;`  
`  uint32_t field_28;`  
`  uint32_t field_2C;`  
`  uint32_t instrument_map_offset; // relative offset to custom instrument map (0 if unused)`  
`  uint32_t drum_map_offset;       // relative offset to custom drum map (0 if unused)`  
`  uint32_t field_38;`  
`  uint32_t field_3C;`  
`};`

### Channel Offsets (size: 2 bytes \* <channels count>)

`struct AkaoChannelInfo`  
`{`  
`  uint32_t start_offsets[num_channels];  // offsets to channel opcode data`  
`};`

`AkaoSeqHeader *header;`  
`int num_channels = 0;`  
`while (int bit = 0; bit < 32; bit++)`  
`  if (info.mask & (1 << bit)) != 0)`  
`    num_channels++;`

There is <channels count> offsets to channel opcode data counting from current offset. Each offsets is a relative offset based on the address the offset itself.

### Channel Commands \[AKAO Opcodes\]

For every channels in an AKAO sequence, there is a set of commands to perform. This is similar to Field opcodes. Here I will call this sound commands "opcodes". Every opcode has its own number of arguments.

### Custom Instrument Map Table

When a song uses custom instruments with [opcode 0xFE 0x14](Opcodes/0xfe14), a custom instrument map table will be placed after the end of AKAO opcode sequence.

This table consists of a collection of zones representing performance settings for a particular key range. A zone is an 8-byte item, and an instrument can have one or more regions.

`struct AkaoInstrumentZoneAttr`  
`{`  
`  uint8_t instrument;   // corresponding to opcode 0xA1`  
`  uint8_t low_key;      // lowest key (in note number)`  
`  uint8_t high_key;     // highest key (in note number)`  
`  uint8_t ar;           // ADSR: attack rate (0-127)`  
`  uint8_t sr;           // ADSR: sustain rate (0-127)`  
`  uint8_t s_mode;       // ADSR: sustain mode (1: linear increase, 3: linear decrease, 5: exponential increase, 7: exponential decrease)`  
`  uint8_t rr;           // ADSR: release rate (0-31)`  
`  uint8_t volume;       // adjust the note volume to n/128 of the original volume (0 will keep the original volume)`  
`}`

\- Zones must be ordered from low key to high key - The final zone of the instrument must be a terminator filled with 0s (more precisely, a zone with ADSR sustain mode of 0 is considered a terminator)

### Drum Instrument Map Table

When a song uses a drum kit with [opcode 0xFE 0x04](Opcodes/0xfe04), a drum instrument map table will be placed at the end of the sequence. The table determines the instrument, channel volume and pan for each keys.

The table consists of a repetition of 8-byte items.

`struct AkaoDrumKeyAttr`  
`{`  
`  uint8_t instrument;   // corresponding to opcode 0xA1`  
`  uint8_t key;          // note number when playing the drum note`  
`  uint8_t ar;           // ADSR: attack rate (0-127)`  
`  uint8_t sr;           // ADSR: sustain rate (0-127)`  
`  uint8_t s_mode;       // ADSR: sustain mode (1: linear increase, 3: linear decrease, 5: exponential increase, 7: exponential decrease)`  
`  uint8_t rr;           // ADSR: release rate (0-31)`  
`  uint8_t volume;       // adjust the percussion volume to n/128 of the original volume (0 will keep the original volume)`  
`  uint8_t pan : 7;      // corresponding to opcode 0xAA`  
`  uint8_t reverb : 1;   // reverb on/off (0: off, 1: on)`  
`}`

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
<td><p>The opcode indicates the note key and length.</p></td>
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
<td><p><a href="Opcodes/0xe0" title="wikilink">0xE0</a></p></td>
<td><p>Unknown</p></td>
<td><p>1</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe1" title="wikilink">0xE1</a></p></td>
<td><p>Unknown</p></td>
<td><p>2</p></td>
<td><p>value: byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe2" title="wikilink">0xE2</a></p></td>
<td><p>Unknown</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Clears the effect of opcode 0xE1</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe3" title="wikilink">0xE3</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe4" title="wikilink">0xE4</a></p></td>
<td><p>Vibrato Rate Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, rate: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe5" title="wikilink">0xE5</a></p></td>
<td><p>Tremolo Rate Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, rate: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xe6" title="wikilink">0xE6</a></p></td>
<td><p>Channel Pan LFO Rate Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, rate: byte</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xE7-0xEF</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>1</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xf0fd" title="wikilink">0xF0-0xFD</a></p></td>
<td><p>Note, Tie, Rest with Length</p></td>
<td><p>2</p></td>
<td><p>length: byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe00" title="wikilink">0xFE 0x00</a></p></td>
<td><p>Tempo</p></td>
<td><p>4</p></td>
<td><p>tempo: uint16 |bpm = tempo / 218.453333 (approximate) More strictly, <code>bpm = 60.0 / (48 * (65536.0 / tempo) * (0x43D1 / (33868800.0 / 8)))</code></p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe00" title="wikilink">0xFE 0x01</a></p></td>
<td><p>Tempo Slide</p></td>
<td><p>5</p></td>
<td><p>length: byte, tempo: uint16</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe02" title="wikilink">0xFE 0x02</a></p></td>
<td><p>Reverb Depth</p></td>
<td><p>4</p></td>
<td><p>depth: uint16</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe02" title="wikilink">0xFE 0x03</a></p></td>
<td><p>Reverb Depth Slide</p></td>
<td><p>5</p></td>
<td><p>length: byte, depth: uint16</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe04" title="wikilink">0xFE 0x04</a></p></td>
<td><p>Turn On Drum Mode</p></td>
<td><p>2</p></td>
<td></td>
<td><p>The drum map offset is recorded in the file header.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe04" title="wikilink">0xFE 0x05</a></p></td>
<td><p>Turn Off Drum Mode</p></td>
<td><p>2</p></td>
<td></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe06" title="wikilink">0xFE 0x06</a></p></td>
<td><p>Unconditional Jump</p></td>
<td><p>4</p></td>
<td><p>destination_offset: signed int16</p></td>
<td><p>This instruction can be used to make an infinite loop.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe07" title="wikilink">0xFE 0x07</a></p></td>
<td><p>CPU-Conditional Jump</p></td>
<td><p>5</p></td>
<td><p>condition: byte, destination_offset: signed int16</p></td>
<td><p>Jump if the condition variable matches <code>condition</code>. The value of the condition variable can be set from the game program.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe08" title="wikilink">0xFE 0x08</a></p></td>
<td><p>Jump on the Nth Repeat</p></td>
<td><p>5</p></td>
<td><p>times: byte, destination_offset: signed int16</p></td>
<td><p>When <code>times</code> is 0, it will be translated to 256 times.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe08" title="wikilink">0xFE 0x09</a></p></td>
<td><p>Break the Loop on the Nth Repeat</p></td>
<td><p>5</p></td>
<td><p>times: byte, destination_offset: signed int16</p></td>
<td><p>Unlike 0xF0, this instruction will end the current loop by decrementing the nesting level of the loop. When <code>times</code> is 0, it will be translated to 256 times.</p></td>
</tr>
<tr>
<td><p><a href="../../FF7/PSX/Sound/Opcodes/0xa1" title="wikilink">0xFE 0x0A</a></p></td>
<td><p>Load Instrument (No Attack Sample)</p></td>
<td><p>3</p></td>
<td><p>instrument: byte</p></td>
<td><p>Unlike 0xA1, the sample before the loop point is replaced by a short, silence sample.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe0b" title="wikilink">0xFE 0x0B</a></p></td>
<td><p>Unknown</p></td>
<td><p>6</p></td>
<td><p>offset: signed int16, offset2: signed int16</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFE 0x0C-0x0D</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe0e" title="wikilink">0xFE 0x0E</a></p></td>
<td><p>Pattern</p></td>
<td><p>4</p></td>
<td><p>destination_offset: signed int16</p></td>
<td><p>Remember the return address and jump to the specified location. It cannot be nested.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe0f" title="wikilink">0xFE 0x0F</a></p></td>
<td><p>End Pattern</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Return from opcode 0xFE 0x0E.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe10" title="wikilink">0xFE 0x10</a></p></td>
<td><p>Allocate Reserved Voices</p></td>
<td><p>3</p></td>
<td><p>count: byte</p></td>
<td><p>Reserve the specified <code>count</code> of hardware voices. Reserved voices will not be used unless explicitly specified in opcode 0xFE 0x1D.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe10" title="wikilink">0xFE 0x11</a></p></td>
<td><p>Free Reserved Voices</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Set the count of reserved voices to 0.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa3" title="wikilink">0xFE 0x12</a></p></td>
<td><p>Channel Master Volume Slide</p></td>
<td><p>3</p></td>
<td><p>length: byte, volume: byte (0-127)</p></td>
<td><p>When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFE 0x13</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe14" title="wikilink">0xFE 0x14</a></p></td>
<td><p>Load Custom Instrument (Key-Split Instrument)</p></td>
<td><p>3</p></td>
<td><p>instrument: byte</p></td>
<td><p>The custom instrument number corresponds to the custom instrument map pointed from the file header. Note that the number is different from the regular sample number used in opcode 0xA1.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe15" title="wikilink">0xFE 0x15</a></p></td>
<td><p>Time Signature</p></td>
<td><p>4</p></td>
<td><p>ticks_per_beat: byte, beats_per_measure: byte</p></td>
<td><p>Note that two parameters can be 0. This pattern is used for initialization.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe16" title="wikilink">0xFE 0x16</a></p></td>
<td><p>Measure Number</p></td>
<td><p>3</p></td>
<td><p>measure: byte</p></td>
<td></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFE 0x17-0x18</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa9" title="wikilink">0xFE 0x19</a></p></td>
<td><p>Channel Volume Slide Per Note On</p></td>
<td><p>4</p></td>
<td><p>length: byte, volume: byte (0-127)</p></td>
<td><p>Applies volume slide (opcode 0xA9) for each notes. When <code>length</code> is 0, it will be translated to 256 ticks.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe1a" title="wikilink">0xFE 0x1A</a></p></td>
<td><p>Unknown</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Turn something on.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe1b" title="wikilink">0xFE 0x1B</a></p></td>
<td><p>Unknown</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Clears the effect of opcode 0xFE 0x1A.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe1c" title="wikilink">0xFE 0x1C</a></p></td>
<td><p>Unknown</p></td>
<td><p>3</p></td>
<td><p>value: byte</p></td>
<td><p>Obsoleted opcode? As far as I learned from the assembly code, it probably does nothing.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe1d" title="wikilink">0xFE 0x1D</a></p></td>
<td><p>Use Reserved Voices</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Allow using the reserved voices to play the sound of the current track. If they are all used, the remaining voices will instead be used normally.</p>
<p>Use opcode <a href="Opcodes/0xfe10" title="wikilink">0xFE 0x10</a> to allocate reserved voices.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xfe1e" title="wikilink">0xFE 0x1E</a></p></td>
<td><p>Use No Reserved Voices</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Disable the effect of opcode 0xFE 0x1D.</p></td>
</tr>
<tr>
<td><p><a href="Opcodes/0xa0" title="wikilink">0xFE 0x1F</a></p></td>
<td><p>Unimplemented</p></td>
<td><p>2</p></td>
<td></td>
<td><p>Code-referenced to 0xA0. Should not be used.</p></td>
</tr>
<tr>
<td><p>0xFE 0x20-0xFF</p></td>
<td><p>Unimplemented (Out of Range)</p></td>
<td><p>n/a</p></td>
<td></td>
<td><p>Do not use.</p></td>
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
