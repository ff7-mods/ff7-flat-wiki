---
title: Code_Map
---

# Code Map

Introduces functions, variables and data related to sound, contained in SCUS_941.63 (game program of US version). Note that all symbol names below are for convenience only.

<table>
<thead>
<tr>
<th><p>PSX Address</p></th>
<th><p>Declaration</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>0x800293D0</p></td>
<td><p>void _AkaoSpuTransferCallback(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x800293F4</p></td>
<td><p>void _AkaoSpuSetTransferCallback(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80029424</p></td>
<td><p>unsigned int _AkaoTransferSamples(const unsigned char *addr, unsigned int size)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x800294A4</p></td>
<td><p>void _AkaoWaitForSpuTransfer(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x800294BC</p></td>
<td><p>void _AkaoReset(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x800297A4</p></td>
<td><p>void AkaoLoadInstrumentSet(const sturct AkaoSampleSet *sampleSet, const struct AkaoInstrumentAttr *instrumentSet)</p></td>
<td><p>Load standard instrument set</p>
<p><em>sampleSet</em>: corresponding to SOUND/INSTR.ALL</p>
<p><em>instrumentSet</em>: corresponding to SOUND/INSTR.DAT</p>
<p>This function is called transparently from 0x8002988C.</p></td>
</tr>
<tr>
<td><p>0x80029818</p></td>
<td><p>void AkaoLoadInstrumentSet2(const sturct AkaoSampleSet *sampleSet, const struct AkaoInstrumentAttr *instrumentSet)</p></td>
<td><p>Load additional instrument set</p>
<p><em>sampleSet</em>: corresponding to SOUND/INSTR2.ALL</p>
<p><em>instrumentSet</em>: corresponding to SOUND/INSTR2.DAT</p></td>
</tr>
<tr>
<td><p>0x8002988C</p></td>
<td><p>void AkaoInitialize(const sturct AkaoSampleSet *sampleSet, const struct AkaoInstrumentAttr *instrumentSet)</p></td>
<td><p>Initialize sound driver and load initial instruments</p>
<p><em>sampleSet</em>: corresponding to SOUND/INSTR.ALL</p>
<p><em>instrumentSet</em>: corresponding to SOUND/INSTR.DAT</p></td>
</tr>
<tr>
<td><p>0x800299C8</p></td>
<td><p>void AkaoDeinitialize(void)</p></td>
<td><p>Deinitialize sound driver</p></td>
</tr>
<tr>
<td><p>0x80029AF0</p></td>
<td><p>void AkaoSetReverbMode(int mode)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80029B78</p></td>
<td><p>void _AkaoTransferSeqBody(const unsigned char *data, int size)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80029C48</p></td>
<td><p>void _AkaoLoadTracks(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002DA30</p></td>
<td><p>void AkaoNewMessage(struct AkaoMessage **ppMessage)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002DA7C</p></td>
<td><p>int AkaoPostMessage(void)</p></td>
<td><p>Post a new command message to the queue (with some wrapped processing)</p>
<p>The message data comes from a global variable at 0x8009A000.</p>
<p>Return value depends on the content of the message data.</p>
<p><strong>Opcode 0x10</strong></p>
<p>Load and start playing new <a href="AKAO_sequence" title="wikilink">AKAO sequence</a></p>
<p>Returns: 0 for success, 1 for already loaded, and -1 for invalid signature</p>
<p><strong>Opcode 0x92</strong></p>
<p>Set value to the condition variable used by Opcode 0xEF.</p></td>
</tr>
<tr>
<td><p>0x8002E1A8</p></td>
<td><p>void _AkaoDispatchMessages(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002E23C</p></td>
<td><p>void _AkaoWriteSpuRegisters(int voiceNum, struct AkaoSpuVoiceAttr *attr)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002E478</p></td>
<td><p>void _AkaoDspOnTick(struct AkaoPlayerTrack *track, struct AkaoPlayer *player, int voiceMask)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002ED34</p></td>
<td><p>void _AkaoCalculateVolumeAndPitch(struct AkaoPlayerTrack *track, int voiceMask, int voiceNum)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002F24C</p></td>
<td><p>void _AkaoCalculateVolumeAndPitch2(struct AkaoPlayerTrack *track, int voiceMask)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002F738</p></td>
<td><p>void _AkaoDspOverlayVoice(struct AkaoPlayerTrack *track, int unknownVoiceMask, int voiceNum)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002F848</p></td>
<td><p>void _AkaoDspMain(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8002FF4C</p></td>
<td><p>void _AkaoSpuNoiseVoice(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80030038</p></td>
<td><p>void _AkaoSpuReverbVoice(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80030148</p></td>
<td><p>void _AkaoSpuPitchLFOVoice(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80030234</p></td>
<td><p>int _AkaoTimerCallback(void)</p></td>
<td><p>Sound callback event that is periodically triggered by root counter 2</p></td>
</tr>
<tr>
<td><p>0x800308D4</p></td>
<td><p>void _AkaoMain(void)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80030E7C</p></td>
<td><p>void _AkaoDispatchVoice(struct AkaoPlayerTrack *track, struct AkaoPlayer *player, int voiceMask)</p></td>
<td><p>Dispatch voice opcodes until the next note or end of track</p></td>
</tr>
<tr>
<td><p>0x80031820</p></td>
<td><p>void AkaoSetInstrument(struct AkaoPlayerTrack *track, unsigned short progNumber)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x800318BC</p></td>
<td><p>int _AkaoReadNextNote(struct AkaoPlayerTrack *track)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80031A70</p></td>
<td><p>int _AkaoFindNextEndPoint(struct AkaoPlayerTrack *track)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80049548</p></td>
<td><p>void (* const MESSAGE_HANDLERS[256])(struct AkaoMessage *)</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80049948</p></td>
<td><p>const unsigned char VOICE_OPCODE_LENGTHS[0x60]</p></td>
<td><p>Length table for voice opcodes 0xa0-0xff</p>
<p>0 for end of track and branches</p></td>
</tr>
<tr>
<td><p>0x80049AA8</p></td>
<td><p>void (* const VOICE_OPCODES[0x60])(struct AkaoPlayerTrack *, struct AkaoPlayer *, int)</p></td>
<td><p>Address table for voice opcodes 0xa0-0xff</p></td>
</tr>
<tr>
<td><p>0x80049C28</p></td>
<td><p>const unsigned short DELTA_TIME_TABLE[11];</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80049C44</p></td>
<td><p>const unsigned short VOLUME_TABLE_L[128]</p></td>
<td><p>See <a href="Opcodes/0xa8aa" title="wikilink">Opcode 0xAA</a> for volume balance calculation</p></td>
</tr>
<tr>
<td><p>0x80049E44</p></td>
<td><p>const unsigned short VOLUME_TABLE_R[128]</p></td>
<td><p>See <a href="Opcodes/0xa8aa" title="wikilink">Opcode 0xAA</a> for volume balance calculation</p></td>
</tr>
<tr>
<td><p>0x8004A5CC</p></td>
<td><p>const short *LFO_FORMS[16]</p></td>
<td></td>
</tr>
<tr>
<td><p>0x8004A60C</p></td>
<td><p>const unsigned char EMPTY_ADPCM[32]</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80063010</p></td>
<td><p>int g_AkaoNumQueuedMessages</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80081DC8</p></td>
<td><p>AkaoMessage g_AkaoMessageQueue[]</p></td>
<td></td>
</tr>
<tr>
<td><p>0x80083580</p></td>
<td><p>unsigned char g_AkaoSeqData[]</p></td>
<td><p>RAM area to load AKAO sequence data</p></td>
</tr>
<tr>
<td><p>0x8009A000</p></td>
<td><p>AkaoMessage g_AkaoMessage</p></td>
<td><p>Message data to be posted. Processed by the function 0x8002DA7C</p></td>
</tr>
</tbody>
</table>

## Runtime Library Functions

### LIBSPU

| PSX Address | Declaration | Description |
|----|----|----|
| 0x80036298 | void SpuInit(void) |  |
| 0x80036FFC | long SpuInitMalloc(long num, char \*top) |  |
| 0x800373AC | long SpuMallocWithStartAddr(unsigned long addr, long size) |  |
| 0x80037964 | unsigned long SpuSetNoiseVoice(long on_off, unsigned long voice_bit) |  |
| 0x80037B90 | long SpuSetNoiseClock(long n_clock) |  |
| 0x80037BE0 | unsigned long SpuRead(unsigned char \*addr, unsigned long size) |  |
| 0x80037C40 | long SpuSetReverb(long on_off) |  |
| 0x80037D90 | long SpuGetReverb(void) |  |
| 0x80037E1C | long SpuSetReverbModeParam(SpuReverbAttr \*attr) |  |
| 0x800387FC | void SpuGetReverbModeParam (SpuReverbAttr \*attr) |  |
| 0x8003884C | long SpuSetReverbDepth(SpuReverbAttr \*attr) |  |
| 0x800388C4 | unsigned long SpuSetReverbVoice(long on_off, unsigned long voice_bit) |  |
| 0x800388E8 | long SpuClearReverbWorkArea(long mode) |  |
| 0x80038A84 | long SpuSetIRQ(long on_off) |  |
| 0x80038BC4 | unsigned long SpuSetIRQAddr(unsigned long addr) |  |
| 0x80038C04 | SpuIRQCallbackProc SpuSetIRQCallback(SpuIRQCallbackProc func) |  |
| 0x80038C6C | void SpuSetKey(long on_off, unsigned long voice_bit) |  |
| 0x80038F04 | unsigned long SpuWrite(unsigned char \*addr, unsigned long size) |  |
| 0x80038F64 | unsigned long SpuSetTransferStartAddr(unsigned long addr) |  |
| 0x80038FB8 | long SpuSetTransferMode(long mode) |  |
| 0x80038FEC | SpuTransferCallbackProc SpuSetTransferCallback(SpuTransferCallbackProc func) |  |
| 0x80039010 | unsigned long SpuSetPitchLFOVoice(long on_off, unsigned long voice_bit) |  |
| 0x80039034 | void SpuSetCommonAttr(SpuCommonAttr \*attr) |  |
| 0x800393C8 | void SpuSetVoiceVolume(int voiceNum, short volL, short volR) |  |
| 0x80039450 | void SpuSetVoiceVolumeAttr(int voiceNum, short volL, short volR, short volModeL, short volModeR) |  |
| 0x800395C8 | void SpuSetVoicePitch(int voiceNum, unsigned short pitch) |  |
| 0x80039644 | void SpuSetVoiceStartAddr(int voiceNum, unsigned long startAddr) |  |
| 0x800396C0 | void SpuSetVoiceLoopStartAddr(int voiceNum, unsigned long lsa) |  |
| 0x8003973C | void SpuSetVoiceDR(int voiceNum, unsigned short DR) |  |
| 0x800397C8 | void SpuSetVoiceSL(int voiceNum, unsigned short SL) |  |
| 0x80039850 | void SpuSetVoiceARAttr(int voiceNum, unsigned short AR, long ARmode) |  |
| 0x800398EC | void SpuSetVoiceSRAttr(int voiceNum, unsigned short SR, long SRmode) |  |
| 0x800399D0 | void SpuSetVoiceRRAttr(int voiceNum, unsigned short RR, long RRmode) |  |

### LIBETC

| PSX Address | Declaration                            | Description |
|-------------|----------------------------------------|-------------|
| 0x8003D0C0  | int ResetCallback(void)                |             |
| 0x8003D150  | int VSyncCallback(void (\*func)(void)) |             |
| 0x8003D1B4  | int StopCallback(void)                 |             |
| 0x8003D214  | int CheckCallback(void)                |             |

### LIBAPI

| PSX Address | Declaration | Description |
|----|----|----|
| 0x800429F0 | void DeliverEvent(unsigned long ev1, unsigned long ev2) |  |
| 0x80042A00 | long OpenEvent(unsigned long desc, long spec, long mode, long (\*func)()) |  |
| 0x80042A10 | long CloseEvent(long event) |  |
| 0x80042A20 | long WaitEvent(long event) |  |
| 0x80042A40 | long EnableEvent(long event) |  |
| 0x80042A50 | long DisableEvent(long event) |  |
| 0x80042BC0 | long SetRCnt(unsigned long spec, unsigned short target, long mode) |  |
| 0x80042C60 | long GetRCnt(unsigned long spec) |  |
| 0x80042C98 | long StartRCnt(unsigned long spec) |  |
| 0x80042CCC | long StopRCnt(unsigned long spec) |  |

# Structures

[struct AkaoInstrumentAttr](INSTRx.DAT)

[struct AkaoSampleSet](INSTRx.ALL)

[struct AkaoSeqHeader, struct AkaoDrumKeyAttr](AKAO_sequence)

`struct AkaoMessage // 36 bytes long`  
`{`  
`  uint16_t opcode;`  
`  uint16_t reserved;`  
`  uint32_t data[8];`  
`};`  
  
`struct AkaoSpuVoiceAttr`  
`{`  
`  uint32_t voice;          // 0x00: voice number`  
`  uint32_t update_flags;   // 0x04: bitset that indicates what SPU registers need to be updated`  
`  uint32_t addr;           // 0x08: waveform data start address (SPU address)`  
`  uint32_t loop_addr;      // 0x0c: loop start address (SPU address)`  
`  uint32_t a_mode;         // 0x10: ADSR: attack mode`  
`  uint32_t s_mode;         // 0x14: ADSR: sustain mode`  
`  uint32_t r_mode          // 0x18: ADSR: release mode`  
`  uint16_t pitch;          // 0x1c: pitch`  
`  uint16_t ar;             // 0x1e: ADSR: attack rate`  
`  uint16_t dr;             // 0x20: ADSR: decay rate`  
`  uint16_t sl;             // 0x22: ADSR: sustain level`  
`  uint16_t sr;             // 0x24: ADSR: sustain rate`  
`  uint16_t rr;             // 0x26: ADSR: release rate`  
`  SpuVolume volume;        // 0x28: volume (left and right)`  
`};`  
  
`struct AkaoPlayer // the music player instance exists at 0x8009A104`  
`{`  
`  uint32_t stereo_mode;                 // 0x00: stereo mode (1: stereo, 4: surround, otherwise: mono)`  
`  uint32_t active_voices;               // 0x04: bitset that indicates the voices currently in use`  
`  uint32_t key_on_voices;               // 0x08: bitset that indicates the voices to key on`  
`  uint32_t keyed_voices;                // 0x0c: bitset that indicates the voices currently keyed on`  
`  uint32_t key_off_voices;              // 0x10: bitset that indicates the voices to key off`  
`  uint32_t saved_active_voices;         // 0x14: unknown voice bitset`  
`  uint32_t tempo;                       // 0x18: tempo (Q16 fixed-point number)`  
`  int32_t tempo_slope;                  // 0x1c: slope of tempo slider (Q16 fixed-point number)`  
`  uint32_t time_counter;                // 0x20: time counter (0x10000 = 1 tick)`  
`  uint32_t overlay_voices;              // 0x24: bitset that indicates the sub-voices used for overlay (opcode 0xF4)`  
`  uint32_t alternate_voices;            // 0x28: bitset that indicates the sub-voices used for alternate voice (opcode 0xF8)`  
`  uint32_t noise_voices;                // 0x2c: bitset that indicates the voices with noise mode enabled`  
`  uint32_t reverb_voices;               // 0x30: bitset that indicates the voices with reverb enabled`  
`  uint32_t pitch_lfo_voices;            // 0x34: bitset that indicates the voices with pitch LFO (frequency modulation) mode enabled`  
`  uint32_t spucnt;                      // 0x38: SPUCNT shadow`  
`  uint32_t reverb_type;                 // 0x3c: reverb type`  
`  uint32_t reverb_depth;                // 0x40: reverb depth (Q16 fixed-point number)`  
`  int32_t reverb_depth_slope;           // 0x44: slope of reverb depth slider (Q16 fixed-point number)`  
`  uint16_t tempo_slide_length;          // 0x48: tempo slide length`  
`  uint16_t song_id;                     // 0x4a: current song id`  
`  uint16_t condition_ack;               // 0x4c: the last matched condition value (opcode 0xEF)`  
`  uint16_t condition;                   // 0x4e: condition variable for dynamic branching according to game status (opcode 0xEF)`  
`  uint16_t reverb_depth_slide_length;   // 0x50: length of reverb depth slide`  
`  uint16_t noise_clock;                 // 0x52: noise clock frequency`  
`  uint16_t field_54;                    // 0x54: unknown (can be altered by opcode 0xF3)`  
`  uint16_t beats_per_measure;           // 0x56: beats per measure`  
`  uint16_t beat;                        // 0x58: current beat`  
`  uint16_t ticks_per_beat;              // 0x5a: ticks per beat`  
`  uint16_t tick;                        // 0x5c: current ticks per beat`  
`  uint16_t measure;                     // 0x5e: current measure`  
`};`  
  
`struct AkaoPlayerTrack // the music player track instances exist at 0x80096608 + (N * 0x108)`  
`{`  
`  uint8_t *addr;                                    // 0x00`  
`  uint8_t *loop_addrs[4];                           // 0x04`  
`  AkaoDrumKeyAttr *drum_addr;                       // 0x14`  
`  int16_t *vibrato_lfo_addr;                        // 0x18`  
`  int16_t *tremolo_lfo_addr;                        // 0x1c`  
`  int16_t *pan_lfo_addr;                            // 0x20`  
`  uint32_t overlay_voice_num;                       // 0x24`  
`  uint32_t alternate_voice_num;                     // 0x28`  
`  uint32_t master_volume;                           // 0x2c`  
`  uint32_t pitch_of_note;                           // 0x30`  
`  int32_t pitch_bend_slide_amplitude;               // 0x34`  
`  uint16_t voice_effect_flags;                      // 0x38`  
`  uint16_t field_3A;                                // 0x3a`  
`  uint16_t field_3C;                                // 0x3c`  
`  uint16_t field_3E;                                // 0x3e`  
`  uint32_t field_40;                                // 0x40`  
`  uint32_t volume;                                  // 0x44`  
`  int32_t volume_slope;                             // 0x48`  
`  int32_t pitch_bend_slope;                         // 0x4c`  
`  uint16_t field_50;                                // 0x50`  
`  uint16_t field_52;                                // 0x52`  
`  uint16_t field_54;                                // 0x54`  
`  uint8_t delta_time_counter;                       // 0x56`  
`  uint8_t gate_time_counter;                        // 0x57`  
`  uint16_t instrument;                              // 0x58`  
`  uint16_t field_5A;                                // 0x5a`  
`  uint16_t volume_slide_length_counter;             // 0x5c`  
`  uint16_t overlay_balance_slide_length_counter;    // 0x5e`  
`  uint16_t pan;                                     // 0x60`  
`  uint16_t pan_slide_length;                        // 0x62`  
`  int16_t pitch_slide_length_counter;               // 0x64`  
`  uint16_t octave;                                  // 0x66`  
`  uint16_t pitch_slide_length;                      // 0x68`  
`  uint16_t previous_note_number;                    // 0x6a`  
`  uint16_t portamento_speed;                        // 0x6c`  
`  uint16_t legato_flags;                            // 0x6e`  
`  uint16_t field_70;                                // 0x70`  
`  uint16_t vibrato_delay;                           // 0x72`  
`  uint16_t vibrato_delay_counter;                   // 0x74`  
`  uint16_t vibrato_rate;                            // 0x76`  
`  uint16_t vibrato_rate_counter;                    // 0x78`  
`  uint16_t vibrato_form;                            // 0x7a`  
`  uint16_t vibrato_max_amplitude;                   // 0x7c`  
`  uint16_t vibrato_depth;                           // 0x7e`  
`  uint16_t vibrato_depth_slide_length_counter;      // 0x80`  
`  int16_t vibrato_depth_slope;                      // 0x82`  
`  uint16_t field_84;                                // 0x84`  
`  uint16_t tremolo_delay;                           // 0x86`  
`  uint16_t tremolo_delay_counter;                   // 0x88`  
`  uint16_t tremolo_rate;                            // 0x8a`  
`  uint16_t tremolo_rate_counter;                    // 0x8c`  
`  uint16_t tremolo_form;                            // 0x8e`  
`  uint16_t tremolo_depth;                           // 0x90`  
`  uint16_t tremolo_depth_slide_length_counter;      // 0x92`  
`  int16_t tremolo_depth_slope;                      // 0x94`  
`  uint16_t field_96;                                // 0x96`  
`  uint16_t pan_lfo_rate;                            // 0x98`  
`  uint16_t pan_lfo_rate_counter;                    // 0x9a`  
`  uint16_t pan_lfo_form;                            // 0x9c`  
`  uint16_t pan_lfo_depth;                           // 0x9e`  
`  uint16_t pan_lfo_depth_slide_length_counter;      // 0xa0`  
`  int16_t pan_lfo_slope;                            // 0xa2`  
`  uint16_t noise_on_off_delay_counter;              // 0xa4`  
`  uint16_t pitchmod_on_off_delay_counter;           // 0xa6`  
`  uint8_t field_A8[16];                             // 0xa8`  
`  uint16_t loop_layer;                              // 0xb8`  
`  uint16_t loop_counts[4];                          // 0xba`  
`  uint16_t previous_delta_time;                     // 0xc2`  
`  uint16_t forced_delta_time;                       // 0xc4`  
`  uint16_t overlay_balance;                         // 0xc6`  
`  int16_t overlay_balance_slope;                    // 0xc8`  
`  int16_t pan_slope;                                // 0xca`  
`  int16_t transpose;                                // 0xcc`  
`  int16_t tuning;                                   // 0xce`  
`  uint16_t note;                                    // 0xd0`  
`  int16_t pitch_slide_amount;                       // 0xd2`  
`  int16_t previous_transpose;                       // 0xd4`  
`  int16_t vibrato_lfo_amplitude;                    // 0xd6`  
`  int16_t tremolo_lfo_amplitude;                    // 0xd8`  
`  int16_t pan_lfo_amplitude;                        // 0xda`  
`  AkaoSpuVoiceAttr spu_attr;                        // 0xdc`  
`};`
