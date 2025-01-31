---
title: 5E_SHAKE
---

- Opcode: **0x5E**
- Short name: **SHAKE**
- Long name: Shake Camera

#### Memory layout

| 0xA8 | *U1* | *U2* | *T* | *xA* | *xF* | *vA* | *vF* |
|------|------|------|-----|------|------|------|------|

#### Arguments

- **const Short** *U1*: Bank to retrieve X-coordinate, or zero if it is specified as a literal value
- **const Short** *U2*: Bank to retrieve Y-coordinate, or zero if it is specified as a literal value
- **const Short** *xA*: The amplitude or how far the 'bounce' is on the x axis
- **const Short** *xF*: The time taken for each tween moment between 'bounces' on the x axis
- **const Short** *yA*: The amplitude or how far the 'bounce' is on the y axis
- **const Short** *yF*: The time taken for each tween moment between 'bounces' on the y axis

#### Description

The current camera movement through standard op codes (eg, [SCR2DC](FF7/Field/Script/Opcodes/66_SCR2DC "wikilink"), [SCRLA](63_SCRLA) and player movement. This camera movement remains unaffected by the SHAKE command. Instead a SHAKE adds an additional X & Y offset to the existing camera when it is running. When it is not running, the shake value is functionally equivalent to *{x:0, y:0}*.

SHAKE is async.

SHAKE commands (with the exception of type 0 -\> which resets the stop the shake) are a chain of tweens. If a shake command has been executed, the current movement (tween) continues until it finished, but the next tween it's the existing queue is not applied. Instead, the new SHAKE commands are queued and subsequently run instead.

All tweens are executed with quadratic in and out easing.

Each tween on each axis is made up of an amplitude (how far the bounce goes) and a time (how long it takes). The SHAKE sets the amplitude and time for each axis independently. The calculation of the next axis position also is independent, eg, if X time frame is 30 and the Y time frame is 50, in a period of 150 frames, X bounces 5 times, and Y bounces 3 times.

There is also a level of randomness applied on the movements so that are always the same size. The following list are roughly the first 30 'random' amplitude factors. *Note: If you halve the amplitude and multiply by the below factor, you get the rough pixel distance.*

`  const steps = [`  
`       -1, 1.14, -1.34, 0.61, -0.49, 0.64, -0.25, 0.47, -1.20, -0.01,`  
`       1.14, -0.86, 0.81, -0.58, 0.68, -1.31, 0.44, -0.91, 0.03, -0.97,`  
`       1.25, -0.76, 0.48, -0.99, 1.34, -0.85, 0.55, -0.65, 0.07, -0.83`  
`  ]`

The type 0 SHAKE resets the camera back to *{x:0, y:0}*. It waits for the current tween to finish as usual, breaks the chain and adds a tween back to {x:0, y:0}. The time frame taken is the larger of the two **xF** and **yF** values.

#### SHAKE Types

There are 4 tween types as determined by the **T** value:

*Note: N/A = Not applicable, can be any value, doesn't affect functionality*

| Type | Description | Axes | xA | xF | yA | yF |
|----|----|----|----|----|----|----|
| 0 | Stop SHAKE and reset camera | X & Y | N/A | N/A Must be \>0 | N/A | N/A Must be \>0 |
| 1 | SHAKE X axis only | X | Must be \>0 | Must be \>0 | N/A | N/A |
| 2 | SHAKE Y axis only | Y | N/A | N/A | Must be \>0 | Must be \>0 |
| 3 | SHAKE X & Y axis | X & Y | Must be \>0 | Must be \>0 | Must be \>0 | Must be \>0 |
