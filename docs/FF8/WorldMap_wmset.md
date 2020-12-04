---
title: WorldMap_wmset
---

## File general info

Please reefer to [WmsetXX.obj](WorldMap_wmsetxx.md) for more specific info.

## Models section

Researched by: Vehek (http://forums.qhimm.com/index.php?topic=13799.msg193791\#msg193791)

`struct`  
`{`  
`u16 triangle_count;`  
`u16 quad_count;`  
`u16 texture_page;`  
`u16 vertex_count;`  
`triangle triangleData[triangle_count];`  
`quad quadData[quad_count];`  
`vertex verticeData[vertex_count];`  
`} model`

`struct`  
`{`  
`u8 vertexIndices[3];`  
`u8 semitransp; //Sets semitransparency if bit 0x01 is set`  
`u8 texcoords1[2];`  
`u8 texcoords2[2];`  
`u8 texcoords3[2];`  
`u16 CLUT_ID;`  
`} triangle`

`struct`  
`{`  
`u8 vertexIndices[4];`  
`u8 texcoords1[2];`  
`u8 texcoords2[2];`  
`u8 texcoords3[2];`  
`u8 texcoords4[2];`  
`u16 CLUT_ID;`  
`u8 semitransp;//Sets semitransparency if bit 0x01 is set`  
`u8 unknown`  
`} quad`

`struct`  
`{`  
`s16 coordinates[3];`  
`u16 unknown;`  
`}vertex`

## Generic Wmset.obj models offsets

GAME USES wmsetXX.obj file instead of THIS. This is list with models offsets FYI:

`15612`  
`18980`  
`19376`  
`20940`  
`21256`  
`22820`  
`23136`  
`24100`  
`24336`  
`24492`  
`26088`  
`27700`  
`29288`  
`29444`  
`31140`  
`33172`  
`36484`  
`36880`  
`38320`  
`39712`  
`41144`  
`42604`  
`43904`  
`44884`  
`45968`  
`49360`  
`55100`  
`60808`  
`65588`  
`66640`  
`67036`  
`67896`  
`68388`

Texture offsets for above models, where index 0 is the first model listed here, and 32 is the last one (68388).

`           switch(index)`  
`           {`  
`               case 0:`  
`                   return 413048;`  
`               case 1:`  
`                   return 429980;`  
`               case 2:`  
`                   return 446912;`  
`               case 3:`  
`                   return 451076;`  
`               case 4:`  
`                   return 453192;`  
`               case 5:`  
`                   return 457356;`  
`               case 6:`  
`                   return 459472;`  
`               case 7:`  
`                   return 463636;`  
`               case 8:`  
`                   return 465752;`  
`               case 9:`  
`                   return 467868;`  
`               case 10:`  
`                   return 470016;`  
`               case 11:`  
`                   return 472164;`  
`               case 12:`  
`                   return 474312;`  
`               case 13:`  
`                   return 474508;`  
`               case 14:`  
`                   return 478768;`  
`               case 15:`  
`                   return 483028;`  
`               case 16:`  
`                   return 491384;`  
`               case 17:`  
`                   return 499740;`  
`               case 18:`  
`                   return 501888;`  
`               case 19:`  
`                   return 504036;`  
`               case 20:`  
`                   return 506184;`  
`               case 21:`  
`                   return 508332;`  
`               case 22:`  
`                   return 510480;`  
`               case 23:`  
`                   return 512628;`  
`               case 24:`  
`                   return 514776;`  
`               case 25:`  
`                   return 523132;`  
`               case 26:`  
`                   return 531488;`  
`               case 27:`  
`                   return 539844;`  
`               case 28:`  
`                   return 548200;`  
`               case 29:`  
`                   return 550316;`  
`               case 30:`  
`                   return 551440;`  
`               case 31:`  
`                   return 551636;`  
`               case 32:`  
`                   return 552728;`  
`               default:`  
`                   return 0; //For compiler`  
`           }`
