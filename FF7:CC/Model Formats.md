---
title: Model Formats
---

[Home](Main%20Page.md) > [FF7:CC](FF7:CC.md) > Model Formats

<small>[Koral][] 16:59, 29 Mar 2009 (EDT)</small>

# Known FF7:CC Model Formats

-   \[\[FF7:CC/Model Formats\#exp Format\|\[!\] (exp) Format\]\]

Note that the Vertices must decoded in accordance with the PSP-GPU
specifications, detailed below.

# PSP Vertex Decoding and Rendering

<small>Stub -- lots of info, may require a new page entirely devoted to
this</small>

TODO

## exp Format

\[!\] files contain all the information neccessary to correctly render
and animate any 3D geometry on the PSP.

Each \[!\]-File contains multiple Models and Textures to represent a
single entity to render, additionally storing skeletal heirarchy and
animation data chunks.

These files include

-   [TYPE-0][] Characters, Monsters, NPCs and various prop Models
-   [TYPE-1][] Location Map Models

### File Structure

    File Header: 0x80 bytes [128 bytes]

       0x00   magic " !' " [0x0 0x0 0x0 0x0 0x21 0x27 0x00 0x00]

       0x0A   SHORT: number of Models in VERTEX-CHUNK
       0x0E   SHORT: number of Textures in TEXTURE-CHUNK

       0x10   DWORD: offset to [unknown chunk 1]

       0x14   DWORD: offset to VERTEX Chunk start
       0x1C   DWORD: offset to TEXTURE Chunk start

       0x34   DWORD: offset to [unknown chunk 2] 
       0x3C   DWORD: offset to [unknown chunk 3]
       0x40   DWORD: offset to [unknown chunk 4]
       0x48   DWORD: offset to [unknown chunk 5]

    [Unknown Chunk 1] 

       multiple 32-byte chunks 
       ?

    VERTEX Chunk

       For each Model, 8-bytes per entry: (the count is located at 0x0A in File Header)

           0x00   DWORD: Texture-ID of the texture to use (zero based)
           0x04   DWORD: offset to Vertex-data start for this Model
       
       Model Vertex Data:
     
           0x00   DWORD: TYPE of data [see notes]
           0x04   beginning of PSP-Encoded vertex data [see notes]

The \*TYPE\* value determines how to parse the vertex-data which
follows, and known values are:

-   00 - Used for Characters, Monsters, Props, etc
-   01 - Used for Location-Maps

See the section on PSP-GPU for more information on parsing the vertices.

    TEXTURE Chunk

       For each Texture, 16-bytes per entry: (the count is located at 0x0E in File Header)

            0x00   SHORT: image Width
            0x02   SHORT: image Height
            0x04   DWORD: Interlacing Mode [see notes]
            0x08   DWORD: offset to PALLETE-data start
            0x0C   DWORD: offset to PIXEL-data start

       PALLETE data:

            [see notes]

       PIXEL data:

            [see notes]

The PIXEL and PALLETE data are as per the [\[TEX][1]\] format

    [Unknown Chunks]
       ?

## exp TYPE-0 Models

These files use Skin-Weighted vertices exclusively, representing all the
**Characters, Monsters, NPCs** and **small Event-specific props** shown
throughout the game.

This is a complete list of the RAW files corresponding to the in-game
entity:

    2162 Zack - Soldier 1st Class
    2163 Zack - after Angeal's death
    2164 Zack - Soldier 2nd Class
    2165 Zack at the beach
    2166 Angeal
    2167 Angeal's clone (Hound form)
    2168 Angeal w/ wing
    2169 Sephiroth
    2170 Genesis 
    2171 Genesis w/ wing
    2172 Genesis being degenerated
    2173 Genesis's clone w/o mask
    2174 Lazard 
    2175 Lazard in Angeal form
    2176 Tseng
    2177 Cissnei
    2178 Cissnei at the beach
    2179 Hojo
    2180 Hollander 
    2181 Hollander at the last stage of degeneration 
    2182 Aerith
    2183 Cloud - the infantry man
    2184 Cloud in Soldier 1st class uniform
    2185 Infantry man - the captain
    2186 Infantry man
    2187 Soldier 2nd Class
    2188 Soldier 3rd Class
    2189 Gillian
    2190 Reno
    2191 Rude
    2192 Tifa
    2193-2194 Angeal and Zack with weird shadow on faces (actually, the 2 Soldiers in the Epilogue)
    2195 Researcher 
    2196 Man in suite
    2197 Woman in suite
    2198 Man
    2199 Woman in suite
    2200 Boy
    2201 Girl
    2202 Man
    2203 Woman
    2204 Man
    2205 Wutai warrior
    2207 Spriggan
    2208 Thunderbird
    2209 One eye
    2210 Angeal's clone (One eye)
    2212 Angeal's clone (Sahagin form)
    2214 Angeal's clone (Hound form)
    2215 worm
    2216 Stinger
    2218 Flying machine
    2219 Bomb
    2220 Griffon
    2221 Angeal's clone (Griffon form)
    2222 Demon
    2223-2224 Genesis's clone w/o wing
    2225 Genesis's clone w/ wing
    2227 Genesis's clone
    2228 Genesisâ€™s clone being degenerated
    2229 Sweeper (machine)
    2230 Tarantula (machine)
    2231-2232 Tank
    2234-2235 Wutai's giant monster
    2236 Ifrit
    2237 Bahamuth
    2238 Fury Bahamuth
    2239 Angeal Penance
    2240 Genesis Avatar
    2246 Chair
    2250 Truck
    2252 Aerith
    2253 Sephiroth
    2254 Zack - Soldier 2nd Class
    2255 Angeal
    2256 Genesis
    2257 Mask of Genesis's clone
    2259 Needle machine
    2260 Chain machine 
    2261 Missile machine
    2262 Sweeper (machine)
    2263 Wutai's giant monster
    2264 Thunderbird
    2265 Hound
    2267 Dual horns
    2368-2370 Saucer (machine)
    2371-2372 Alert Head (small machine w/ armour)
    2373-2274 Drill machine 
    2275 Tarantula (machine)
    2276 Support machine
    2277 Bug
    2280 Sephiroth
    2281 Genesis's clone (Predator)
    2282 Tseng
    2283 Sephiroth
    2284 Zack - Soldier 1st Class
    2285 Zack - after Angeal's death
    2288 Man
    2289 Woman
    2290 Boy
    2291 Girl
    2292 Angeal w/ wing
    2293 Angeal
    2294 Zack - Soldier 2nd Class
    2295 Genesis's clone
    2296 Genesisâ€™s clone being degenerated
    2297-2298 Genesis's clone (Predator)
    2300 Files
    2304 Lazard
    2305 Lazard in Angeal form
    2306 Cissnei
    2307 Genesis w/ wing
    2308 Helicopter
    2309 Genesis being degenerated
    2310 Angeal clone (Sahagin form)
    2311 Cloud - the infantry man
    2316 Heel
    2317-2318 Wutai warrior
    2320 Hornets (bees)
    2321 Death Claw
    2322 Mover
    2324 Dorky face
    2325 Hungry
    2327-2328 Grangalan
    2329 Chocobo
    2330 Magic pot
    2331-2333 Tonberry
    2334 CaithSith
    2335 Hollander
    2336 Motorcycle
    2337 Angeal w/ wing
    2341 Infantry man (the captain)
    2343 Sweeper (machine)
    2345 Genesisâ€™s clone w/o wing
    2346 Genesisâ€™s clone w/ wing
    2347 Man
    2348 Woman (the shopkeeper)
    2349 Boy (the little thief)
    2352 Woman
    2353 Boy
    2356 Woman
    2357-2358 Boy
    2359 Juice-can
    2361 Book (cyan)
    2362 Dumbapple
    2363 Book (magenta)
    2366 Wutai warrior
    2367 Genesis's clone (Infantry man form)
    2368 Shinra rocket
    2369 Cissnei at the beach
    2370-2371 Genesis's clone (Infantry man form)
    2372 Genesisâ€™s clone (Predator)
    2373 Moogle
    2374 Zack at the beach
    2375 Rooms
    2376 Normal Behemoth
    2377 King Behemoth (golden)
    2378 Cloud in Soldier 1st class uniform
    2379 Genesisâ€™s clone (Dominator)
    2380 Hollander at the last stage of degeneration 
    2382 Worm
    2383 Dual horns
    2384 Item box
    2394 Jenova
    2398 The monster in tube
    2399-2401 Genesisâ€™s clone (Shadow scythe/knight/mage)
    2402 Camera
    2405 Top floor
    2406 Path?
    2407 some kind of machine
    2408 Hollander at the last stage of degeneration
    2410-2411 Genesis at the last stage of degeneration
    2412 Wutai warrior
    2414 Tarantula
    2415 Sahagin
    2416 Stinger
    2418 Spriggan 
    2419 Alert Head (small machine w/ armour)
    2420 Hound
    2421 Demon
    2422 Dorky face 
    2424 Death Claw
    2425 One eye
    2426 Bug
    2427 Bowl?
    2428 Water pot
    2429 Strong box
    2430 Golden Coin?
    2431 Minerva (The Goddess)
    2432 Malboro
    2434 Black woman in suite
    2435 Black man in suite
    2436 Yuffie
    2438 Documentation?
    2439 Statue
    2440 Hollander's bag
    2441 Plain? 
    2444 Genesisâ€™s clone (Dominator)
    2443 The monster in tube like
    2444 Genesisâ€™s clone w/ wing
    2445-2447 Flower Wagon
    2448 Sniper
    2449 Truck
    2450 Barrel
    2451 Helicopter
    2453 Potion
    2454 Helicopter
    2455 Worm
    2456-2457 Zack's last moment

<small> -- [SilverWings][] </small>

## exp TYPE-1 Models

<small>Stub -- incomplete</small>

These files contain static geometry with initial bounding-box data
preceeding the vertex data, and usually represent all the **Location Map
models** to render within the game.

  [Koral]: User:Koral.md "wikilink"
  [TYPE-0]: FF7:CC/Model%20Formats.md#exp%20TYPE-0%20Models "wikilink"
  [TYPE-1]: FF7:CC/Model%20Formats.md#exp%20TYPE-1%20Models "wikilink"
  [1]: FF7:CC/Image%20Formats.md#TEX%20Format "wikilink"
  [SilverWings]: http://forums.qhimm.com/index.php?action=profile;u=3658
