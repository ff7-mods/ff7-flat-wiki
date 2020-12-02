---
title: Opcodes
---

[Home](/ff7-flat-wiki/Main%20Page.md) > [FF7](/ff7-flat-wiki/FF7.md) > [WorldMap Module](/ff7-flat-wiki/FF7/WorldMap%20Module.md) > [Script](/ff7-flat-wiki/FF7/WorldMap%20Module/Script.md) > Opcodes

## Stack Operations: Arithmetic

[`015`` ``push`` ``neg`][]  
[`017`` ``push`` ``logicnot`][]  
[`018`` ``push`` ``distance`` ``from`` ``active`` ``entity`` ``to`` ``point`][]  
[`019`` ``push`` ``distance`` ``from`` ``active`` ``entity`` ``to`` ``entity`` ``by`` ``model`` ``id`][]  
[`01b`` ``push`` ``unknown`][]  
[`030`` ``push`` ``mul`][]  
[`040`` ``push`` ``add`][]  
[`041`` ``push`` ``sub`][]  
[`050`` ``push`` ``shl`][]  
[`051`` ``push`` ``shr`][]  
[`060`` ``push`` ``less`][]  
[`061`` ``push`` ``greater`][]  
[`062`` ``push`` ``lessequal`][]  
[`063`` ``push`` ``greaterequal`][]  
[`070`` ``push`` ``equal`][]  
[`080`` ``push`` ``and`][]  
[`0a0`` ``push`` ``or`][]  
[`0b0`` ``push`` ``logicand`][]  
[`0c0`` ``push`` ``logicor`][]  
[`0e0`` ``write`` ``bank`][]

## Stack Operations: Data Sources

[`100`` ``reset`` ``stack`][]  
[`110`` ``push`` ``constant`][]  
[`114`` ``push`` ``bit`` ``from`` ``bank0`][]  
[`117`` ``push`` ``special`][]  
[`118`` ``push`` ``byte`` ``from`` ``bank0`][]  
[`119`` ``push`` ``byte`` ``from`` ``bank1`][]  
[`11b`` ``push`` ``special`][`117`` ``push`` ``special`]  
[`11c`` ``push`` ``word`` ``from`` ``bank0`][]  
[`11d`` ``push`` ``word`` ``from`` ``bank1`][]  
[`11f`` ``push`` ``special`][`117`` ``push`` ``special`]

## Flow Control

[`200`` ``jump`][]  
[`201`` ``jump`` ``if`` ``false`][]  
[`203`` ``return`][]  
[`204`` ``run`` ``function`][]

## System Operations

[`300`` ``load`` ``model`][]  
[`302`` ``set`` ``player`` ``entity`][]  
[`303`` ``set`` ``active`` ``entity`` ``movespeed`][]  
[`304`` ``set`` ``active`` ``entity`` ``direction`` ``&`` ``facing`][]  
[`305`` ``set`` ``wait`` ``frames`][]  
[`306`` ``wait?`][]  
[`307`` ``set`` ``control`` ``lock`][]  
[`308`` ``set`` ``active`` ``entity`` ``mesh`` ``coordinates`][]  
[`309`` ``set`` ``active`` ``entity`` ``coordinates`` ``in`` ``mesh`][]  
[`30a`` ``set`` ``active`` ``entity`` ``vertical`` ``speed`][]  
[`30b`` ``set`` ``active`` ``entity`` ``y`` ``offset`][]  
[`30c`` ``enter`` ``vehicle?`][]  
[`30d`` ``stop`` ``entity`][]  
[`30e`` ``active`` ``entity`` ``play`` ``animation`][]  
[`310`` ``set`` ``active`` ``point`][]  
[`311`` ``set`` ``point`` ``mesh`` ``coordinates`][]  
[`312`` ``set`` ``point`` ``coordinates`` ``in`` ``mesh`][]  
[`313`` ``set`` ``point`` ``terrain`` ``BGR`][]  
[`314`` ``set`` ``point`` ``dropoff`` ``parameters`][]  
[`315`` ``set`` ``point`` ``sky`` ``top`` ``BGR`][]  
[`316`` ``set`` ``point`` ``sky`` ``bottom`` ``BGR`][]  
[`317`` ``trigger`` ``battle`][]  
[`318`` ``enter`` ``field`` ``scene`][]  
[`319`` ``set`` ``map`` ``options`][]  
[`31b`` ``noop`][]  
[`31c`` ``unknown`][]  
[`31d`` ``play`` ``sound`` ``effect`][]  
[`31f`` ``set`` ``camera`` ``rotation`` ``speed`][]  
[`320`` ``unknown`][]  
[`321`` ``unknown`][]  
[`324`` ``set`` ``window`` ``dimensions`][]  
[`325`` ``set`` ``window`` ``message`][]  
[`326`` ``set`` ``window`` ``prompt`][]  
[`327`` ``wait`` ``for`` ``prompt`` ``acknowledge?`][]  
[`328`` ``set`` ``active`` ``entity`` ``direction`][]  
[`329`` ``unknown`][]  
[`32a`` ``unknown`][]  
[`32b`` ``set`` ``battle`` ``lock`][]  
[`32c`` ``set`` ``window`` ``parameters`][]  
[`32d`` ``wait`` ``for`` ``window`` ``ready`][]  
[`32e`` ``wait`` ``for`` ``message`` ``acknowledge`][]  
[`32f`` ``set`` ``player`` ``direction`][]  
[`330`` ``set`` ``active`` ``entity`][]  
[`331`` ``exit`` ``vehicle`][]  
[`332`` ``unknown`][]  
[`333`` ``rotate`` ``current`` ``entity`` ``to`` ``model`][]  
[`334`` ``wait`` ``for`` ``function`][]  
[`336`` ``set`` ``active`` ``entity`` ``movespeed`` ``(honor`` ``walkmesh)`][]  
[`339`` ``hide`` ``active`` ``entity`` ``model`][]  
[`33a`` ``set`` ``active`` ``entity`` ``vertical`` ``speed`` ``2`][]  
[`33b`` ``fade`` ``out?`][]  
[`33c`` ``set`` ``field`` ``entry`` ``point?`][]  
[`33d`` ``set`` ``field`` ``entry`` ``point2?`][]  
[`33e`` ``play`` ``music`][]  
[`347`` ``move`` ``active`` ``entity`` ``to`` ``entity`` ``by`` ``model`` ``id?`][]  
[`348`` ``fade`` ``in?`][]  
[`349`` ``set`` ``world`` ``progress`][]  
[`34a`` ``unknown`][]  
[`34b`` ``set`` ``chocobo`` ``type`][]  
[`34c`` ``set`` ``submarine`` ``color`][]  
[`34d`` ``show`` ``animation`` ``layer`][]  
[`34e`` ``hide`` ``animation`` ``layer`][]  
[`34f`` ``set`` ``active`` ``entity`` ``y`` ``position`][]  
[`350`` ``set`` ``meteor`` ``texture`` ``on/off`][]  
[`351`` ``set`` ``music`` ``volume`][]  
[`352`` ``shake`` ``camera`` ``on/off`][]  
[`353`` ``unknown`][]  
[`354`` ``unknown`][]  
[`355`` ``set`` ``battle`` ``countdown`` ``timer`][]

  [`015`` ``push`` ``neg`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/015.md
    "wikilink"
  [`017`` ``push`` ``logicnot`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/017.md
    "wikilink"
  [`018`` ``push`` ``distance`` ``from`` ``active`` ``entity`` ``to`` ``point`]:
    FF7/WorldMap_Module/Script/Opcodes/018 "wikilink"
  [`019`` ``push`` ``distance`` ``from`` ``active`` ``entity`` ``to`` ``entity`` ``by`` ``model`` ``id`]:
    FF7/WorldMap_Module/Script/Opcodes/019 "wikilink"
  [`01b`` ``push`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/01b.md
    "wikilink"
  [`030`` ``push`` ``mul`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/030.md
    "wikilink"
  [`040`` ``push`` ``add`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/040.md
    "wikilink"
  [`041`` ``push`` ``sub`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/041.md
    "wikilink"
  [`050`` ``push`` ``shl`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/050.md
    "wikilink"
  [`051`` ``push`` ``shr`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/051.md
    "wikilink"
  [`060`` ``push`` ``less`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/060.md
    "wikilink"
  [`061`` ``push`` ``greater`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/061.md
    "wikilink"
  [`062`` ``push`` ``lessequal`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/062.md
    "wikilink"
  [`063`` ``push`` ``greaterequal`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/063.md
    "wikilink"
  [`070`` ``push`` ``equal`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/070.md
    "wikilink"
  [`080`` ``push`` ``and`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/080.md
    "wikilink"
  [`0a0`` ``push`` ``or`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/0a0.md
    "wikilink"
  [`0b0`` ``push`` ``logicand`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/0b0.md
    "wikilink"
  [`0c0`` ``push`` ``logicor`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/0c0.md
    "wikilink"
  [`0e0`` ``write`` ``bank`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/0e0.md
    "wikilink"
  [`100`` ``reset`` ``stack`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/100.md
    "wikilink"
  [`110`` ``push`` ``constant`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/110.md
    "wikilink"
  [`114`` ``push`` ``bit`` ``from`` ``bank0`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/114.md
    "wikilink"
  [`117`` ``push`` ``special`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/117.md
    "wikilink"
  [`118`` ``push`` ``byte`` ``from`` ``bank0`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/118.md
    "wikilink"
  [`119`` ``push`` ``byte`` ``from`` ``bank1`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/119.md
    "wikilink"
  [`11c`` ``push`` ``word`` ``from`` ``bank0`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/11c.md
    "wikilink"
  [`11d`` ``push`` ``word`` ``from`` ``bank1`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/11d.md
    "wikilink"
  [`200`` ``jump`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/200.md "wikilink"
  [`201`` ``jump`` ``if`` ``false`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/201.md
    "wikilink"
  [`203`` ``return`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/203.md "wikilink"
  [`204`` ``run`` ``function`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/204.md
    "wikilink"
  [`300`` ``load`` ``model`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/300.md
    "wikilink"
  [`302`` ``set`` ``player`` ``entity`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/302.md
    "wikilink"
  [`303`` ``set`` ``active`` ``entity`` ``movespeed`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/303.md
    "wikilink"
  [`304`` ``set`` ``active`` ``entity`` ``direction`` ``&`` ``facing`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/304.md
    "wikilink"
  [`305`` ``set`` ``wait`` ``frames`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/305.md
    "wikilink"
  [`306`` ``wait?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/306.md "wikilink"
  [`307`` ``set`` ``control`` ``lock`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/307.md
    "wikilink"
  [`308`` ``set`` ``active`` ``entity`` ``mesh`` ``coordinates`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/308.md
    "wikilink"
  [`309`` ``set`` ``active`` ``entity`` ``coordinates`` ``in`` ``mesh`]:
    FF7/WorldMap_Module/Script/Opcodes/309 "wikilink"
  [`30a`` ``set`` ``active`` ``entity`` ``vertical`` ``speed`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/30a.md
    "wikilink"
  [`30b`` ``set`` ``active`` ``entity`` ``y`` ``offset`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/30b.md
    "wikilink"
  [`30c`` ``enter`` ``vehicle?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/30c.md
    "wikilink"
  [`30d`` ``stop`` ``entity`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/30d.md
    "wikilink"
  [`30e`` ``active`` ``entity`` ``play`` ``animation`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/30e.md
    "wikilink"
  [`310`` ``set`` ``active`` ``point`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/310.md
    "wikilink"
  [`311`` ``set`` ``point`` ``mesh`` ``coordinates`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/311.md
    "wikilink"
  [`312`` ``set`` ``point`` ``coordinates`` ``in`` ``mesh`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/312.md
    "wikilink"
  [`313`` ``set`` ``point`` ``terrain`` ``BGR`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/313.md
    "wikilink"
  [`314`` ``set`` ``point`` ``dropoff`` ``parameters`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/314.md
    "wikilink"
  [`315`` ``set`` ``point`` ``sky`` ``top`` ``BGR`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/315.md
    "wikilink"
  [`316`` ``set`` ``point`` ``sky`` ``bottom`` ``BGR`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/316.md
    "wikilink"
  [`317`` ``trigger`` ``battle`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/317.md
    "wikilink"
  [`318`` ``enter`` ``field`` ``scene`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/318.md
    "wikilink"
  [`319`` ``set`` ``map`` ``options`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/319.md
    "wikilink"
  [`31b`` ``noop`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/31b.md "wikilink"
  [`31c`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/31c.md "wikilink"
  [`31d`` ``play`` ``sound`` ``effect`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/31d.md
    "wikilink"
  [`31f`` ``set`` ``camera`` ``rotation`` ``speed`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/31f.md
    "wikilink"
  [`320`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/320.md "wikilink"
  [`321`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/321.md "wikilink"
  [`324`` ``set`` ``window`` ``dimensions`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/324.md
    "wikilink"
  [`325`` ``set`` ``window`` ``message`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/325.md
    "wikilink"
  [`326`` ``set`` ``window`` ``prompt`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/326.md
    "wikilink"
  [`327`` ``wait`` ``for`` ``prompt`` ``acknowledge?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/327.md
    "wikilink"
  [`328`` ``set`` ``active`` ``entity`` ``direction`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/328.md
    "wikilink"
  [`329`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/329.md "wikilink"
  [`32a`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32a.md "wikilink"
  [`32b`` ``set`` ``battle`` ``lock`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32b.md
    "wikilink"
  [`32c`` ``set`` ``window`` ``parameters`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32c.md
    "wikilink"
  [`32d`` ``wait`` ``for`` ``window`` ``ready`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32d.md
    "wikilink"
  [`32e`` ``wait`` ``for`` ``message`` ``acknowledge`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32e.md
    "wikilink"
  [`32f`` ``set`` ``player`` ``direction`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/32f.md
    "wikilink"
  [`330`` ``set`` ``active`` ``entity`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/330.md
    "wikilink"
  [`331`` ``exit`` ``vehicle`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/331.md
    "wikilink"
  [`332`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/332.md "wikilink"
  [`333`` ``rotate`` ``current`` ``entity`` ``to`` ``model`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/333.md
    "wikilink"
  [`334`` ``wait`` ``for`` ``function`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/334.md
    "wikilink"
  [`336`` ``set`` ``active`` ``entity`` ``movespeed`` ``(honor`` ``walkmesh)`]:
    FF7/WorldMap_Module/Script/Opcodes/336 "wikilink"
  [`339`` ``hide`` ``active`` ``entity`` ``model`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/339.md
    "wikilink"
  [`33a`` ``set`` ``active`` ``entity`` ``vertical`` ``speed`` ``2`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/33a.md
    "wikilink"
  [`33b`` ``fade`` ``out?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/33b.md
    "wikilink"
  [`33c`` ``set`` ``field`` ``entry`` ``point?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/33c.md
    "wikilink"
  [`33d`` ``set`` ``field`` ``entry`` ``point2?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/33d.md
    "wikilink"
  [`33e`` ``play`` ``music`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/33e.md
    "wikilink"
  [`347`` ``move`` ``active`` ``entity`` ``to`` ``entity`` ``by`` ``model`` ``id?`]:
    FF7/WorldMap_Module/Script/Opcodes/347 "wikilink"
  [`348`` ``fade`` ``in?`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/348.md
    "wikilink"
  [`349`` ``set`` ``world`` ``progress`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/349.md
    "wikilink"
  [`34a`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34a.md "wikilink"
  [`34b`` ``set`` ``chocobo`` ``type`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34b.md
    "wikilink"
  [`34c`` ``set`` ``submarine`` ``color`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34c.md
    "wikilink"
  [`34d`` ``show`` ``animation`` ``layer`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34d.md
    "wikilink"
  [`34e`` ``hide`` ``animation`` ``layer`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34e.md
    "wikilink"
  [`34f`` ``set`` ``active`` ``entity`` ``y`` ``position`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/34f.md
    "wikilink"
  [`350`` ``set`` ``meteor`` ``texture`` ``on/off`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/350.md
    "wikilink"
  [`351`` ``set`` ``music`` ``volume`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/351.md
    "wikilink"
  [`352`` ``shake`` ``camera`` ``on/off`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/352.md
    "wikilink"
  [`353`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/353.md "wikilink"
  [`354`` ``unknown`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/354.md "wikilink"
  [`355`` ``set`` ``battle`` ``countdown`` ``timer`]: /ff7-flat-wiki/FF7/WorldMap%20Module/Script/Opcodes/355.md
    "wikilink"
