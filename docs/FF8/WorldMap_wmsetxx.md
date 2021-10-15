---
title: WorldMap_wmsetxx
---

## Info

WMSETxx.obj (where xx may refer to gr,us,it,fr,sp) is a multi-data world map file containing many core functions and 3D objects. This file contains almost everything: sounds, scripts, dialogs, texts, textures, models- all contained in one file. Main differences between en/it/gr/sp/fr are localized dialogs, so next sections have different offsets. Offsets before this are all the same. [Wmset.obj](WorldMap_wmset.md) is probably never used in-game and is leftover. Dialogs in lang-en/wmset.obj are in english, but the file is different from wmsetus.obj.

## General structure

WMSETxx.obj is made from 48 sections. File starts with header, that has 48\*4 bytes. Every offset is 4 bytes long.

| Offset        | Length  | Description      |
|---------------|---------|------------------|
| 0             | 4 bytes | Section 1        |
| SectNmbr \* 4 | 4 bytes | Section SectNmbr |

The last section is offset 188.

### Section 1: World map encounter data supplier

| Offset             | Length  | Description                            |
|--------------------|---------|----------------------------------------|
| 0                  | 4 bytes | FileSize (this+4)                      |
| 4 + (entryID \* 4) | 4 bytes | EncounterIdSupplierDataProvider\_Entry |

**EncounterIdSupplierDataProvider\_Entry**:

| Offset | Length | Description |
|--------|--------|-------------|
| 0      | Byte   | regionID    |
| 1      | Byte   | groundID    |
| 2      | Byte   | ESI\*       |
| 3      | Byte   | unused      |

-   ESI is the name of the register that holds the third byte parameter of section1. It is used later to determine the encounter. When the character makes a step on worldmap, the game loops through whole section1 data and tests:

if the character is walking on groundID and regionID, if yes, then ESI is our multiplier to section4 containing encounters. Example entry:

00 06 00 00:

If Squall is in region = 0 and walks on ground with ID 6 (as far as I remember it's Balamb Plains or forest) then get encounters from section4 that start at 0\*8; Other example:

04 1B 24 00:

If Squall is in region = 4 and walks on ground with ID 0x1B, then get encounters from section4 that starts at 0x24\*8 = 288

That way the engine can play encounter based on place you are, because if you're walking on Balamb beach, then engine should play encounter with beach, not snow plains. That's why if you change the for one map portion you can totally erase encounters in this region, because in example region 4 that may be Centra regions does not contain any BalambPlains, so there is no entry in section1 and therefore the engine finds the region encounters, but doesn't find the encounter entries for BalambPlainsGround in Centra ruins (this is totally an example).

### Section 2: World map Regions

Nothing much to write here. 32x24 world map. Just open it via hexEditor. It's just bitmap (you can even convert bytes to image and mini worldmap will show) Every single byte is regionID used for example in section1 for encounters.

### Section 3: World Map Encounters Flags

One byte per encounter group in section 4. Always 0 on railways/roads, always 12 on forests, 128 on Island closest to Hell/Heaven, 3 in Galbadia Desert (day and night) and 2 for everything else.

### Section 4: World Map Encounters

| Offset             | Length   | Description                               |
|--------------------|----------|-------------------------------------------|
| section1.ESI \* 16 | 16 bytes | 2 \* 8 bytes of encounters from scene.out |

It's as simple as that: Squall makes step on worldmap, game gets Squall position and tests it with section2 containing region, then loops through section1 and tests groundID and regionID to find ESI multiplier, if random number generates battle, then game gets to section4 using ESI determined earlier with Squall step on world map and plays randomly one of the eight encounters (because one ESI/encounterEntry is 16 bytes, where first four words are the most common, other 2 medium and last 2 rarest)

### Section 5: UNUSED Encounter Flags (after Lunar Cry)

Unused in-game

One byte (always 8 here) per encounter group in section 6. Analog to section 3, but for Lunar Cry encounters.

### Section 6: World Map Encounters (after Lunar Cry)

Same format as Section 4, but only with Lunar Cry encounters. You can use the section 1 to obtain ground, this way: search in section 1 for region == 10 (Esthar), and substract 80 from the esi value, you will obtain the correct esi for the section 6.

### Section 7-8: roads, train track, bridge

Related with Section 39. Maybe scripts in section 8. (like sections 10, 12 and 32)

Script format (ScriptsCount must be guessed):

| Offset                | Length                | Description                                                         |
|-----------------------|-----------------------|---------------------------------------------------------------------|
| 0                     | 4 \* ScriptsCount + 4 | List of script positions, not always sorted (ended with 0x00000000) |
| 4 \* ScriptsCount + 4 | Varies + 4            | Scripts data (ended with 0x00000000)                                |

In script data you have 4-bytes opcodes, the first byte is the identifier, and the last two bytes are the parameter (the second byte is always 0xFF). Scripts always start with 0x01 opcode, and finish with 0x16 opcode. There is always one 0x04 opcode inside. For now most is unknown, I only understood that 0x2B opcode refer to scene ID in its parameter (you can find UFO, Koyo-K and Lac Obel battles in Section 32).

### Section 9: UNKNOWN

### Section 10-11: UNKNOWN (Related to Squall model)

Maybe scripts in section 10. (like sections 8, 12 and 32)

### Section 12-13: UNKNOWN

Maybe scripts in section 12. (like sections 8, 10 and 32)

### Section 14: Side quests texts/tialogs

This section provides dialogs on world map used in side quests.

This section starts with header pointing to **relative** offsets to dialog/text portions.

Dumped data from wmsetus.obj:

`…+-1 Airstation5 … 7  Get off…YesNo5 + 7  Get off…YesNo5 - 7  Get off…YesNo”Bound for 5 4 7“Pay 4111 Gil to rideDon't ride”`  
`Bound for 5 3 7“Pay 4111 Gil to rideDon't ride”Bound for 5 ! 7“Pay 4111 Gil to rideDon't ride7 ”You don't have enough money“`  
`Selphie ”C'mon?  To the 5Missile Base7?“ n Soldier”Give it up“ n Soldier”I'm busy“ n Soldier”There's no way you're getting `  
`through?“ n Soldier”This is our duty“ n Soldier”Just like always“ n Soldier”How 'bout a date…“Found a draw point?But no one `  
`can drawFound a draw point?Nothing thereFound a draw point? foundCan't carry anymoreYou do not have DrawWho will draw…Don't `  
`draw  stocked 1+-=*&??()·.71Out of/  …?3  7remaining …YesNo#‘2 How to drive 7          4!Back  7!Forward          6!Get on`  
`:off Steer with directional button 1!Change POV2 Garden Controls 7          4!Back  7!Forward  5!To cockpit          6!Get on`  
`:off Steer with directional button 1!Change POV2 How to ride a Chocobo 7 6!Get off Run with directional button 1!Change POV2`  
` Spaceship Controls 7          4!Back  7!Forward  5!To cockpit          6!Get on:off Directional button to go up:down:steer 1!`  
`Change POV)This place looksfamiliar·It looks abandonedand run=down”Huh?…“Nida”The gauge is going berserk?…“)Shouldn't be getting`  
` off·This must be Obel LakeThrow a rockTry hummingIt's Obel LakeThrow a rockTry hummingA black shadow rose to the surfaceThrow`  
` a rockTry humming againThe black shadow disappearedThe rock sank .The rock skipped once . .The rock skipped twice . . .The `  
`rock skipped 4 times . . . .The rock skipped 5 times . . . . .The rock skipped 6 times . . . . . .The rock skipped 7 times . `  
`. . . . .The rock skippedmany many timesBlack Shadow”Hello human  What a lovely tune“A black shadow rose to the surface”Hello?“)`  
`There's something large there·”Thanks for speaking to me again?“”Umm“”Can you do me a favor…“)What is it·)I don't want to hear `  
`it·”It's my friend Mr Monkey Can you find him for me…“”Please“”“”Mr Monkey should be in a forest somewhere Keep walking around `  
`and I'm sure you'll find him“”Oh yeah do you know what…“”Oh yeah“”What a beautiful day“”I wonder what it means…“”Mysterious `  
`writing on the rock“”Mr Monkey had a rock like this I think“”Take a break at the railroad bridge“”Take some time off at Eldbeak`  
` Peninsula“”I bet it's a wonderful place“Relayed the whereabouts of Mr Monkey”Thank you?“There's the monkey?Throw a rockSing”`  
`You suck?“The monkey disappeared into the forestThe monkey told you off and disappeared into the forest”Ahhh?  Darn it? `  
`Y=You're just a big loser?  I'm able to skip the rock as many times as I want? So there? Ha=Ha? Loser? Dork? Idiot? Your mom `  
`wears combat boots?“”OUCH? D=Darn it? You're gonna pay for that?“The monkey threw a rock at you and ran?Upon inspecting the `  
`rockit looks man=made andhas some carving on itYou found the monkey”You big dork???“Almost?The monkey ran awayWhat's this?…You`  
` found a piece of rock by your footIt looks man=made andhas some carving on itBut it was just a rockA bird is warming an egg`  
`Check it outLeave it aloneIt seems that the birdwent to go look for foodYou found a piece of rock thereNothing there1  `  
`S T S L R M 1  U R H A E O 1  R E A I D R 1  E A S N P D 1  S T S L R M 71  U R H A E O 71  R E A I D R 71  E A S N P D 7”`  
`At the beach in 2 something special washes ashore at times“”You'll find something on an island east of 4 too“”There's also `  
`something on top of a mountain with a lake and cavern“”Back in the day south of here there used to be a small but beautiful `  
`village surrounded by deep forests Everyone lived a happy life there“There is a stone pillarIf you look closelythere's something`  
` written on it”TRETIMEASUREAT MINOFFDEISLE“)…·Found 9?Found L?Found ?Found 1?That sound disappeared into the lakeThere are many`  
` multicoloredrocks with faces all over the placeThe black=faced rock tells you sternly”The treasure is probably in the direction`  
` of the North Star“The white=faced rock tells you coldly”It's east“The white=faced rock tells you coldly”It's west“The white=`  
`faced rock tells you coldly”It's south“The white=faced rock tells you coldly”It's north“The red=faced rock tells you angrily”`  
`The blue one's a liar?“The red=faced rock tells you angrily”The treasure's to the east?“The red=faced rock tells you angrily”`  
`The treasure's to the west?“The red=faced rock tells you angrily”The treasure's to the south?“The red=faced rock tells you angrily`  
`”The treasure's to the north?“The red=faced rock tells you angrily”The treasure's not here?“The blue=faced rock whispers”`  
`I don't know where the treasure is“The blue=faced rock whispers”People call us ‘The Liar Rocks'“The blue=faced rock whispers”`  
`Some of us just repeat the same thing“The blue=faced rock whispers”Some of us just talk nonsense“The blue=faced whispers”`  
`Some of us just say the opposite of what we mean“This place just has rubble lying among the grassAbsolutely nothing)`  
`Is thispart of something…·)Seems like the same rock     I picked up before·)This must be all of them·”This must be all the rocks““`  
`If he's not around perhaps he took a train towards Dollet…“)I remember now This is Edea's house I get the feeling there's something`  
`nearby Something hugenearby·`

### Section 15: NULL

4 Bytes NULL

### Section 16: World map objects data

| Offset                   | Length  | Description                                |
|--------------------------|---------|--------------------------------------------|
| 0                        | 4 bytes | Relative offset to Model structure (below) |
| Various                  | 4 bytes | '00 00 00 00' - offset list end            |
| Offset pointed by header | Various | Models (see below)                         |

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

### Section 17-19: UNKNOWN

UNKNOWN

### Section 20: UNKNOWN

Bunch of AKAO frames headers packed

### Section 21: AKAO

Starts with AKAO header

### Section 22-28: NULL

4 Bytes NULL

### Section 29: World map "water block"

Section 29 is a duplicate segment from "full" water block (not segment!) used in world map (wmx.obj).

#### Usage

<s>Whenever landing or entering ragnarok, the engine does not load segments from wmx.obj until the transition is done.</s> Whenever transforming viewport at certain speed, the engine can't keep up with loading the new segments/blocks. The areas that are not loaded but should be rendered in the same time are filled with this block. This can be seen when the camera view is set so that it rotates during ragnarok entering/exiting transition or placing character to different area.

### Section 30: NULL

4 Bytes NULL

### Section 31: UNKNOWN

UNKNOWN

### Section 32: Text- Location names

This section provides location names (probably for Ragnarok landing?)

This section starts with header pointing to **relative** offsets to dialog/text portions.

Dumped data from wmsetus.obj:

`?2344 Forest  Garden  Garden: Station!9Missile Base7WinhillEdea's House%:`  
`51 Seaside Station1 City1: AirstationLunatic Pandora Laboratory=1`  
`Sorceress MemorialTears' Point1 Seaside Station=Tears' PointTears' `  
`PointLunatic Pandora Laboratory1:Airstation1 Sorceress Memorial`

### Section 33-34: Light related

UNKNOWN

### Section 35: World Map draw points

| Offset                    | Length | Description       |
|---------------------------|--------|-------------------|
| 0x00                      | 0x2C   | UNUSED            |
| 0x2C + (thisEntryID \* 4) | DWORD  | DrawPointVariable |

**DrawPointVariable**:

| Offset | Length | Description   |
|--------|--------|---------------|
| 0x00   | BYTE   | World block X |
| 0x01   | BYTE   | World block Y |
| 0x02   | WORD   | Magic ID      |

Magic contained in world map draw point: (ID is: section35 magic entry+0x80 \[add 1 to be correct with list below\])

`   129 0 1 Cure`  
`   130 0 1 Esuna`  
`   131 0 1 Thunder`  
`   132 0 1 Fira`  
`   133 0 1 Thundara`  
`   134 0 1 Blizzara`  
`   135 0 1 Blizzard`  
`   136 0 1 Fire`  
`   137 0 1 Cure`  
`   138 0 1 Water`  
`   139 0 1 Cura`  
`   140 0 1 Esuna`  
`   141 0 1 Scan`  
`   142 0 1 Shell`  
`   143 0 1 Haste`  
`   144 0 1 Aero`  
`   145 0 1 Bio`  
`   146 0 1 Life`  
`   147 0 1 Demi`  
`   148 0 1 Protect `  
`   149 0 1 Holy `  
`   150 0 1 Thundaga`  
`   151 0 1 Stop`  
`   152 0 1 Firaga`  
`   153 0 1 Regen`  
`   154 0 1 Blizzaga`  
`   155 0 1 Confuse`  
`   156 0 1 Flare`  
`   157 0 1 Dispel`  
`   158 0 1 Slow`  
`   159 0 1 Quake`  
`   160 0 1 Curaga`  
`   161 0 1 Tornado`  
`   162 0 0 Full-Life`  
`   163 0 1 Reflect`  
`   164 0 0 Aura`  
`   165 0 0 Quake`  
`   166 0 1 Double`  
`   167 0 1 Break`  
`   168 0 0 Meteor`  
`   169 0 0 Ultima`  
`   170 0 0 Triple`  
`   171 0 1 Confuse`  
`   172 0 1 Blind`  
`   173 1 1 Quake`  
`   174 0 1 Sleep`  
`   175 0 1 Silence`  
`   176 1 1 Flare`  
`   177 0 1 Death`  
`   178 0 1 Drain`  
`   179 1 1 Pain`  
`   180 0 1 Berserk`  
`   181 0 1 Float`  
`   182 0 1 Zombie`  
`   183 0 1 Meltdown`  
`   184 1 0 Ultima`  
`   185 1 1 Tornado`  
`   186 1 1 Quake`  
`   187 1 1 Meteor`  
`   188 1 1 Holy`  
`   189 1 1 Flare`  
`   190 1 1 Aura`  
`   191 1 1 Ultima`  
`   192 1 1 Triple`  
`   193 1 1 Full-Life`  
`   194 1 1 Tornado`  
`   195 1 1 Quake`  
`   196 1 1 Meteor`  
`   197 1 1 Holy`  
`   198 1 1 Flare`  
`   199 1 1 Aura`  
`   200 1 1 Ultima`  
`   201 1 1 Triple`  
`   202 1 1 Full-Life`  
`   203 1 1 Tornado`  
`   204 1 1 Quake`  
`   205 1 1 Meteor`  
`   206 1 1 Holy`  
`   207 1 1 Flare`  
`   208 1 1 Aura`  
`   209 1 1 Ultima`  
`   210 1 1 Triple`  
`   211 1 1 Full-Life`  
`   212 1 1 Ultima`  
`   213 1 1 Meteor`  
`   214 1 1 Holy`  
`   215 1 1 Flare`  
`   216 1 1 Aura`  
`   217 1 1 Ultima`  
`   218 1 1 Triple`  
`   219 1 1 Full-Life`  
`   220 1 1 Meteor`  
`   221 1 1 Holy`  
`   222 1 1 Triple`  
`   223 1 1 Aura`  
`   224 1 1 Ultima`  
`   225 1 1 Triple`  
`   226 1 1 Full-Life`  
`   227 1 1 Meteor`  
`   228 1 1 Holy`  
`   229 1 1 Flare`  
`   230 1 1 Aura`  
`   231 1 1 Ultima`  
`   232 1 1 Triple`  
`   233 1 1 Full-Life`  
`   234 1 1 Meteor`  
`   235 1 1 Triple`  
`   236 1 1 Flare`  
`   237 1 1 Aura`  
`   238 1 1 Ultima`  
`   239 1 1 Triple`  
`   240 1 1 Full-Life`  
`   241 1 1 Meteor`  
`   242 1 1 Holy`  
`   243 1 1 Flare`  
`   244 1 1 Aura`  
`   245 1 1 Ultima`  
`   246 0 1 Blizzard`  
`   247 0 1 Cure`  
`   248 1 1 Dispel`  
`   249 1 1 Confuse`  
`   250 0 0 Meteor`  
`   251 0 0 Double`  
`   252 0 0 Aura`  
`   253 0 0 Holy`  
`   254 0 0 Flare`  
`   255 0 0 Ultima`  
`   256 1 1 Scan`

Halfer: X = rowBlockAmount, which is 4 times segment amount so 4 \* 32 = 128 or 0x80. The last bit tells which row of the two we are on, first or second. The range of top row is from 0x00 - 0x7F and second row's 0x80 - 0xFF.

Y is incremented whenever X goes over 0xFF.

### Section 36-37: UNKNOWN

Maybe scripts in section 37. (like sections 8, 10 and 12)

### Section 38: World map textures archive

This section starts with header pointing to **relative** offsets to .TIM textures. When engine reads offset as 0 (00 00 00 00) then ends reading offsets (so 0 is end of offset list). This is one of the larger sections in file. THIS section is responsible for 1/2 world map textures (Those are really used in-game). There is 36 textures inside as of original release. Also, sea, beach and special effects texture is present.

| Offset                   | Length  | Description                     |
|--------------------------|---------|---------------------------------|
| 0                        | 4 bytes | Relative offset to texture      |
| Various (144 originally) | 4 bytes | '00 00 00 00' - offset list end |
| Offset pointed by header | Various | .TIM texture (10 00 00 00 08)   |

### Section 39: Textures - roads, train track, bridge

This section starts with header pointing to **relative** offsets to .TIM textures. When engine reads offset as 0 (00 00 00 00) then ends reading offsets (so 0 is end of offset list). THIS section is responsible for train track textures, road textures, bridge train track texture (the one that gets through FH).

| Offset                   | Length  | Description                     |
|--------------------------|---------|---------------------------------|
| 0                        | 4 bytes | Relative offset to texture      |
| Various (52 originally)  | 4 bytes | '00 00 00 00' - offset list end |
| Offset pointed by header | Various | .TIM texture (10 00 00 00 08)   |

### Section 40: One world map texture/NULL

This section starts with header pointing to **relative** offsets to only one .TIM texture. This is the first texture that is in [texl.obj](WorldMap_texl.md) or wmsetxx.obj/Section 38.

| Offset        | Length                           | Description                     |
|---------------|----------------------------------|---------------------------------|
| 0             | 4 bytes                          | Relative offset to texture      |
| 4             | 4 bytes                          | '00 00 00 00' - offset list end |
| 8             | Various (16384 originally)       | .TIM texture (10 00 00 00 08)   |
| After Texture | Next offset-(header+TIM texture) | NULL data                       |

### Section 41: UNKNOWN

UNKNOWN

### Section 42: Vehicle and object textures

This section starts with header pointing to **relative** offsets to .TIM textures. When engine reads offset as 0 (00 00 00 00) then ends reading offsets (so 0 is end of offset list). THIS section is responsible for vehicles, world map objects textures (Balamb mobile, Galbadia mobile, Balamb halo ring, cactuar statue, lunatic pandora...)

| Offset                   | Length  | Description                     |
|--------------------------|---------|---------------------------------|
| 0                        | 4 bytes | Relative offset to texture      |
| Various (132 originally) | 4 bytes | '00 00 00 00' - offset list end |
| Offset pointed by header | Various | .TIM texture (10 00 00 00 08)   |

### Section 43: Sound/music related

Starts with AKAO

### Section 44: Music related

Starts with AKAO

### Section 45-48: Sound/music related

Starts with AKAO
