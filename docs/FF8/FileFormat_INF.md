---
title: FileFormat_INF
---

By myst6re.

# Gateways/Triggers

| Offset | Size     | Data                                                                                  |
|--------|----------|---------------------------------------------------------------------------------------|
| 0      | 9        | Name of field (\\0 terminated)                                                        |
| 9      | 1        | Control Direction                                                                     |
| 10     | 6        | Unknown                                                                               |
| 16     | 2        | Like [\[PVP](FileFormat_PVP.md)\] value                                   |
| 18     | 2        | Height to focus the camera on the character (0= Focus on the feet, 200= normal focus) |
| 20     | 8\*8     | Camera Ranges                                                                         |
| 84     | 2\*8     | Screen Ranges                                                                         |
| 100    | 32 \* 12 | Gateways                                                                              |
| 384    | 16 \* 12 | Triggers                                                                              |

## Range data

Gives the limits of the camera when moving.

`typedef struct {`  
`   qint16 top;`  
`   qint16 bottom;`  
`   qint16 right;`  
`   qint16 left;`  
`} Range;`

### Camera Range

Each range corresponds to a background layer.

### Screen Range

Always (0, 224, 320, 0) twice. The first range change the screen resolution, the second seems to do nothing.

## Gateways data

Passage between fields.  
For each gateway:

| Offset | Size   | Data                                |
|--------|--------|-------------------------------------|
| 0      | 6      | Vertex 1 of exit line (maybe x,z,y) |
| 6      | 6      | Vertex 2 of exit line (maybe x,z,y) |
| 12     | 6      | Destination vertex                  |
| 18     | 2      | Field ID (or 0x7FFF if unused gate) |
| 20     | 4 \* 2 | Unknown (or 0x7FFF)                 |
| 28     | 4      | Unknown (four equal bytes)          |

## Triggers data

Doors interactions.  
For each trigger:

| Offset | Size | Data              |
|--------|------|-------------------|
| 0      | 6    | Vertex of corner1 |
| 6      | 6    | Vertex of corner2 |
| 12     | 1    | Door ID (or 0xFF) |
| 13     | 3    | *Blank*           |

# Old formats

In the PC version, you can sometimes see older versions of this format, there are three that are more similar to the format of [Final Fantasy VII](../FF7/Field/Triggers.md).

## 672 bytes format

The first Unknown data are 4 bytes and there is no PVP field.

## 576 bytes format

Same as 672 bytes format + the first Unknown data in Gateways are not present (like FF7).

## 504 bytes format

Same as 576 bytes format + There is only one camera range and no screen range.
