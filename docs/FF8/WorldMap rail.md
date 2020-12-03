---
title: WorldMap rail
---

[Home](../Main%20Page.md) > [FF8](../FF8.md) > WorldMap rail

By MaKiPL

## Info

Rail.obj is a file containing key locations of train movement. It stores
location on world map, and the train automatically rotates, gives power
and calculates needed info (like cargo rotation and etc.) This file
**cannot be LZS compressed**. Doing so makes the game not recognize the
file.

### File scheme

The file is built the similiar way as [World map WMX.obj][]. The engine
is loading animation for specific train every 0x800 bytes (2048).
Always. Animation cannot be larger than 2048, and if is smaller than
2048 bytes, then what's left is filled with 00. One animation frame is
16 bytes. Max animation frame is 127, because 127\*16=2032+16(header).

  
  

| Offset           | Length            | Description               |
|------------------|-------------------|---------------------------|
| 0                | Byte              | Count of animation frames |
| 1                | Byte              | Unknown                   |
| 2                | 2 bytes           | Unknown (Padding?)        |
| 4                | UInt32            | Train Stop offset \#1\*   |
| 8                | UInt32            | Train Stop offset \#2\*   |
| 12               | count \* 16 bytes | Animation frames          |
| 12 + (count\*16) | varies            | Padding / 00              |

-   Train stops are offset to animation frames, in which the train stops
    like (running in the tunnel, or waiting at the station)

### Animation key frame

| Offset | Length           | Description |
|--------|------------------|-------------|
| 0      | 4 Bytes signed\* | X Axis      |
| 4      | 4 Bytes signed\* | Z Axis      |
| 8      | 4 Bytes signed\* | Y Axis      |
| 12     | 4 Bytes          | Unknown     |

-   Location on world map (global) is saved upon 4 bytes. To better
    understand this (and in fact-operate/hack) just convert it to
    decimal. Vars are in big-endian.

00 00 FE FF is far west. FF FF 01 00 is far east.

  [World map WMX.obj]: WorldMap%20wmx.md "wikilink"
