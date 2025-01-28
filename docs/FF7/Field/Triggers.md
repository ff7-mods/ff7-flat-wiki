---
title: Triggers
---

# Triggers/Gateways

[1](http://forums.qhimm.com/index.php?topic=4358.msg58674#msg58674) [2](http://forums.qhimm.com/index.php?topic=3247.msg53525#msg53525) and [3](http://forums.qhimm.com/index.php?topic=7129.msg87583#msg87583)

| Offset | Size | Data |
|----|----|----|
| 0 | 9 | Name of field (\0 terminated) |
| 9 | 1 | Control Direction |
| 10 | 2 | Height to focus the camera on the character (0= normal focus, \<0= focus below, \>0= focus above) |
| 12 | 8 | Camera Range |
| 20 | 4 | Unknown (Bg layer 3 & 4 related) |
| 24 | 2 | Background layer 3 animation width (or 1024 if no layer 3) |
| 26 | 2 | Background layer 3 animation height (or 1024) |
| 28 | 2 | Background layer 4 animation width (or 1024) |
| 30 | 2 | Background layer 4 animation height (or 1024) |
| 32 | 24 | Unknown (Bg layer 3 & 4 related) |
| 56 | 12 \* 24 | Gateways |
| 344 | 12 \* 16 | Triggers |
| 536 | 12 | Shown arrows on gateway lines (not present in jp version) |
| 548 | 12 \* 16 | Arrows (not present in jp version) |

## range

`typedef struct {`  
`  S16 left;`  
`  S16 bottom; // maybe top, I dont know/care Its nearly always centred`  
`  S16 right;`  
`  S16 top;    // maybe bottom.`  
`} Range;`

## Vertex

`typedef struct {`  
`  S16 x;`  
`  S16 z;`  
`  S16 y;`  
`} Vertex;`

## Gateways data

For each gateway:

| Offset | Size | Data                       |
|--------|------|----------------------------|
| 0      | 6    | Vertex 1 of exit line      |
| 6      | 6    | Vertex 2 of exit line      |
| 12     | 6    | Destination vertex         |
| 18     | 2    | Field ID                   |
| 20     | 4    | Unknown (four equal bytes) |

## Triggers data

For each trigger:

| Offset | Size | Data                            |
|--------|------|---------------------------------|
| 0      | 6    | Vertex of corner1               |
| 6      | 6    | Vertex of corner2               |
| 12     | 1    | Background group ID (parameter) |
| 13     | 1    | Background frame ID (state)     |
| 14     | 1    | Behavior                        |
| 15     | 1    | Sound ID                        |

### Behavior

behavior can be from 0 to 5:

0 - OnTrigger - ON  
1 - OnTrigger - OFF  
2 - OnTrigger - ON, AwayFromTrigger - OFF  
3 - OnTrigger - OFF, AwayFromTrigger - ON  
4 - OnTrigger - ON, AwayFromTriggerOnPlusSide - OFF  
5 - OnTrigger - OFF, AwayFromTriggerOnPlusSide - ON  

## Shown arrows

For each gateway you can show an arrow. If shown arrow = 1, a red arrow is displayed in the middle of the corresponding gateway line.

## Arrows

This an arrow list to position an arrow where you want.

| Offset | Size | Data                                       |
|--------|------|--------------------------------------------|
| 0      | 4    | Position X (signed)                        |
| 4      | 4    | Position Z (signed)                        |
| 8      | 4    | Position Y (signed)                        |
| 12     | 4    | Arrow type (0= disabled, 1= red, 2= green) |
