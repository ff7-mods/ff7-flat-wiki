---
title: WorldMapCamera
---

By MaKiPL. :\*

## Camera detail

Camera on world map is set to look-at target. Look at target is Squall, that is read from chara.one in world.fs file.

As the camera is look-at, then it works and moves on "logic" sphere. Memory in FF8 is static. Camera memory starts soon after last face indice layout is hold. Is after 3-4 unknown NULL bytes.

### Camera build

Remember! Values are **little-endian**!

Physical camera location/translation:

| Offset | Static memory address | Default or medium value    | Type of value          | Description                                                                                     |
|--------|-----------------------|----------------------------|------------------------|-------------------------------------------------------------------------------------------------|
| 0      | 0x0203ECF8            | 0                          | short (2 bytes signed) | Camera Y axis translation. Camera.Location.Y = (Squall.Location + THIS);                        |
| 2      | 0x0203ECFA            | AB FE                      | short (2 bytes signed) | Camera X axis translation. Camera.Location.X = (Squall.Location.X + THIS);                      |
| 4      | 0x0203ECFC            | 00 E4 / 00 E0              | short (2 bytes signed) | Distance between camera and look-at-target (physical)                                           |
| 8      | 0x0203ED00            | \~FF 92                    | uint16                 | Operates camera tangent Y axis position. This is: hacking this to bird-fly view or like in RPG  |
| 10     | 0x0203ED02            | ranges from 00 00 to 0F FF | 12 bit                 | Operates camera tangent Z axis position. This is: the same as rotating camera in-game           |
| 12     | 0x0203ED04            | 00 00 (FF 0F max)          | 12 bit                 | Camera root rotation. For up-side down example. 9-12th bit is irrelevant. (1111 1111 xxxx 1111) |
| 40     | 0x0203ED2C            | 0                          | bool                   | RESET CAMERA                                                                                    |

Others:

| Static memory address | Default or medium value | Type of value | Description                                                            |
|-----------------------|-------------------------|---------------|------------------------------------------------------------------------|
| 0x01CA92E4            | 1024/640                | uint16        | Logical camera zoom - Takes physical camera and applies logical zoom\* |

Logical zoom, for FF8 they're fixed values:

-   640 - when camera mode is set to far
-   1024 - when camera mode is set to near

These zoom is operated, when you in-game set the camera near-far preferences. (F default in Steam release)

## Camera OPCODE

PRESENTED OPCODE'S ARE FOR STEAM RELEASE! If no opcode for variable above, then this variable is mostly fixed and is not changed on world map itself. (This is for example static vars).

### Camera logical zoom

`FF8_EN.exe+5D7FA - mov [eax*4+FF8_EN.exe+18A927C],ecx`

### Tangent Y

`FF8_EN.exe+15901F - add word ptr [FF8_EN.exe+1C3ED00],-10`  
`FF8_EN.exe+15900F - add word ptr [FF8_EN.exe+1C3ED00],10`  
`FF8_EN.exe+1584EA - add word ptr [FF8_EN.exe+1C3ED00],04`  
`FF8_EN.exe+15902C - mov [FF8_EN.exe+1C3ED00],ax`  
`FF8_EN.exe+15848D - mov [FF8_EN.exe+1C3ED00],ax`  
`FF8_EN.exe+1584C4 - mov [FF8_EN.exe+1C3ED00],dx`

-   ADD applies tick to smooth camera going down logic
-   MOV applies camera going up and additional operations

### Tangent X

`FF8_EN.exe+158676 - add [FF8_EN.exe+1C3ED02],ax`  
`FF8_EN.exe+15873E - add [FF8_EN.exe+1C3ED02],ax`  
`FF8_EN.exe+15871A - add [FF8_EN.exe+1C3ED02],ax`  
`FF8_EN.exe+158936 - mov [ecx+0A],ax`

-   First ADD is applied on regular translation. The one that user can rotate in-game mainly
-   Second ADD is applied on translations when character is going eg. right, and camera is set to front
-   Third ADD is applied when Squall has moved enough in one direction, so the camera is rotated hardly
-   Additional MOV is to finally check and correct camera rotation
