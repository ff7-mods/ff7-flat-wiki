---
title: 6B_FADE
---

- Opcode: **0x6B**
- Short name: **FADE**
- Long name: Fade

#### Memory layout

| 0x6B | *B1 / B2* | *0 / B3* | *R* | *G* | *B* | *S* | *T* | *A* |
|------|-----------|----------|-----|-----|-----|-----|-----|-----|

#### Arguments

- **const Bit\[4\]** *B1*: Bank to retrieve *R*, or zero if *R* is given as a literal value.
- **const Bit\[4\]** *B2*: Bank to retrieve *G*, or zero if *G* is given as a literal value.
- **const Bit\[4\]** *0*: Zero.
- **const Bit\[4\]** *B3*: Bank to retrieve *B*, or zero if *B* is given as a literal value.
- **const UByte** *R*: Red component value, or address of red value if *B1* is non-zero.
- **const UByte** *G*: Green component value, or address of green value if *B2* is non-zero.
- **const UByte** *B*: Blue component value, or address of blue value if *B3* is non-zero.
- **const UByte** *S*: Speed of fade. Larger numbers indicate faster fades.
- **const UByte** *T*: Type of fade; see table.
- **const UByte** *A*: Adjusts the speed of the fade, based on fade in/out.

#### Description

Fades the screen to the colour specified, either as literal values or values from memory, using the type of fade specified by *T*.

Fades are linear tweens that sit above the field. The from color and to color of the tweens are detailed below. After the tween has completed, the fades also set or do not set a holding color. For example, some fades go from the field colors to a light coloured overlay, but once finish, reset to back to field backgrounds.

The transition fades between fields and menus do not appear to affected by this op code.

The overlay sits infront of field models and background (apart from any special models with KAWAI or SHINE effects). It also sits behind any messages that appear on the screen.

If a FADE (or NFADE) is in progress but another FADE (or NFADE) is called, the current fade is stopped and the new one continues. Both op codes control, what essentially is, a single fade layer, I believe...

*Note: Where colorBlack is mentioned, this essentially means 'transparent', eg you see the field without any overlay*

#### Speed

The speed of the fade is specified by *S*, and is base on:

`   1  -> 240 frames -> 8 secs`  
`   2  -> 120 frames -> 4 secs`  
`   4  -> 60 frames -> 2 secs`  
`   8  -> 30 frames -> 1 secs`  
`   16 -> 15 frames -> 0.5 secs`  
`   32 -> 7.5 frames -> 0.25 secs`

In the table below, I refer to a calculation formula *speedToSeconds* for *S* to seconds is represented as:

`   const speedToSeconds = (speed) => {`  
`       return 8 / Math.pow(2, Math.log2(speed))`  
`   }`

With 'NFADE', the speed calculation is not required, the fade speed *S* represents the frame count for the fade.

#### Adjust

If the type id is odd, the adjust is 0xFF, if even, it is 0x00. Whilst I haven't gone into depth with the adjust, it seemingly affects the wait for (FADEW). If set as per the table below, then the fade will take the time take as above and the FADEW will resolve once completed.

#### Colours

Simple formulas based on the passed *r*, *g*, *b* values:

`   colorBlack    -> rgb(0, 0, 0)`  
`   colorStandard -> rgb(r, g, b)`  
`   colorInverse1 -> rgb(0xFF - r, 0xFF - g, 0xFF - b)`  
`   colorInverse4 -> rgb(4 * (0xFF - r), 4 * (0xFF - g), 4 * (0xFF - b))`

Frame by frame, the tweens will calculate the correct values between the **from** and **to** colours over the period of time of the fade. Eg: FROM rgb(10,10,10) -\> TO rgb(30,20,10) will increase like this:

`   rgb(10,10,10)`  
`   rgb(12,11,10)`  
`   rgb(14,12,10)`  
`   rgb(16,13,10)`  
`   rgb(18,14,10)`  
`   rgb(20,15,10)`  
`   rgb(22,16,10)`  
`   rgb(24,17,10)`  
`   rgb(26,18,10)`  
`   rgb(29,19,10)`  
`   rgb(30,20,10)`

#### Blending Modes

Whilst it seems as though a fade my be a gradual opacity, in FF7, it isn't. Instead it is a blending of colors ontop of each other. Eg: We have a 2 pixel, a dark red one and a dark blue one and an orange overly, we apply it like this:

`   GREEN  rgb( 40, 150, 70) -> BLEND DARK BLUE rgb( 50, 60, 130) ADDITIVE    -> rgb( 90, 210, 200)`  
`   GREEN  rgb( 40, 150, 70) -> BLEND DARK BLUE rgb( 50, 60, 130) SUBTRACTIVE -> rgb(  0, 90,    0)`  
`   ORANGE rgb(255, 130,  0) -> BLEND DARK BLUE rgb( 50, 60, 130) ADDITIVE    -> rgb(255, 190, 130)`  
`   ORANGE rgb(255, 130,  0) -> BLEND DARK BLUE rgb( 50, 60, 130) SUBTRACTIVE -> rgb(205,  70,   0)`

*Note: Values are clamped below 0x00 and above 0xFF*

#### Fade Types - FADE

| ID | Description | Async/Sync | Blending Type | From color | To color | Hold end color after finished | Speed | Adjust (typically) |
|----|----|----|----|----|----|----|----|----|
| 1 | colorInverse4 to field subtractive, hold field | Async, ensure wait for | Subtractive | colorInverse4 | colorBlack | colorBlack | speedToSeconds | 0xFF |
| 2 | field to colorInverse4 subtractive, hold color | Async, ensure wait for | Subtractive | colorBlack | colorInverse4 | colorInverse4 | speedToSeconds | 0x00 |
| 3 | Not in use... |  |  |  |  |  |  |  |
| 4 | instant no wait black, hold black | Instant, no fade | Normal |  | colorBlack | colorBlack | Instant | 0x00 |
| 5 | colorStandard to field additive, hold field | Async, ensure wait for | Additive | colorStandard | colorBlack | colorBlack | speedToSeconds | 0xFF |
| 6 | field to colorStandard additive, hold color | Async, ensure wait for | Normal | colorBlack | colorStandard | colorStandard | speedToSeconds | 0x00 |
| 7 | instant but wait colorInverse1 subtractive, hold field | Async, ensure wait for | Subtractive | colorInverse1 | colorInverse1 | colorBlack | speedToSeconds | 0xFF |
| 8 | instant but wait colorInverse1 subtractive, hold color | Async, ensure wait for | Subtractive | colorInverse1 | colorInverse1 | colorInverse1 | speedToSeconds | 0x00 |
| 9 | instant but wait colorStandard additive, hold field | Async, ensure wait for | Additive | colorStandard | colorStandard | colorBlack | speedToSeconds | 0xFF |
| 10 | instant but wait colorStandard additive, hold color | Async, ensure wait for | Additive | colorStandard | colorStandard | colorStandard | speedToSeconds | 0x00 |

#### Fade Types - NFADE

| ID | Description | Async/Sync | Blending Type | From color | To color | Hold end color after finished | Speed |
|----|----|----|----|----|----|----|----|
| 0 | instant no wait show field, hold field | Instant, no fade | Subtractive |  | colorBlack | colorBlack | Instant |
| 11 | field to colorStandard additive, hold color | Async, ensure wait for | Additive | colorBlack | colorStandard | colorStandard | *S* = frames |
| 12 | field to colorStandard subtractive, hold color | Async, ensure wait for | Subtractive | colorBlack | colorStandard | colorStandard | *S* = frames |
