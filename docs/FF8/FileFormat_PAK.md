---
title: FileFormat_PAK
---

Final Fantasy VIII's movie files are stored within pak files. This is for the CD 2000 version only. Steam 2013 version uses avi files. **publish.pak** contains the message "Published by Square Electronic Arts L.L.C.". **disc1.pak**, **disc2.pak**, **disc3.pak**, and **disc4.pak** hold the rest of the FMV movies.

# PAK File Structure

The PAK file has no header. Each movie usually contains a CAM file and two BINK videos. A PAK file can contain multiple movies. One BINK file is the low res the other is the high res.

| Section         | Description |
|-----------------|-------------|
| CAM - optional  | Camera data |
| BINK - high res | FMV video   |
| BINK - low res  | FMV video   |

### Existing projects you can use to extract the PAK files.

-   <https://github.com/MaKiPL/OpenVIII-monogame/tree/master/PAK%20Extractor>
-   <https://github.com/MaKiPL/FF8-Rinoa-s-Toolset/blob/master/SerahToolkit_SharpGL/FF8_Core/PlayMovie.cs>
-   <https://github.com/Sebanisu/OpenVIII_CPP_WIP/tree/master/src/open_viii/pak>

## BINK files

-   Start with 0x42494B "BIK"
-   More info: <https://wiki.multimedia.cx/index.php/Bink_Container>

## CAM files

-   Each frame is 44 bytes long.

| Offset | Size                         | Description                                       |
|--------|------------------------------|---------------------------------------------------|
| 0      | 3 bytes                      | 0x463850 "F8P"                                    |
| 3      | 3 bytes                      | Unknown                                           |
| 6      | 2 bytes (uint16)             | Approx number of frames. There can be extra data. |
| 8      | 44 bytes \* number of frames | Frame data. Each frame ends with "END"            |

Extra info by Kaspar: The number of frames is always equal to the "approx number" above + 1 (therefore we can consider that approx number as the last frame index if we start counting from 0 ). The only exception to this is disc03\_04 wich contains 3 extra frame data (wich is probably pointless since the whole file contains blank camera animation anyway.

Each Frame data sector is structured this way:

| Offset | Size    | Description                          |
|--------|---------|--------------------------------------|
| 0      | 6 bytes | Camera Vector X axis                 |
| 6      | 6 bytes | Camera Vector Y axis                 |
| 12     | 6 bytes | Camera Vector Z axis                 |
| 18     | 2 bytes | Camera Vector Z.z (copy)             |
| 20     | 4 bytes | Camera Space X position              |
| 24     | 4 bytes | Camera Space Y position              |
| 28     | 4 bytes | Camera Space Z position              |
| 32     | 2 bytes | Camera Pan X                         |
| 34     | 2 bytes | Camera Pan Y                         |
| 36     | 2 bytes | Zoom                                 |
| 38     | 2 bytes | Zoom (Repeated)                      |
| 40     | 1 byte  | Render Mode ('08','10','11' or '50') |
| 41     | 3 bytes | "END" marker                         |

The 4 Render mode seems to be these :

`   -8 ('08') = render characters over FMV and masks meshes over characters (hiding/masking them)`

`   -16('10') = render characters over FMV (not masked)`

`   -17('11') = don't render characters over FMV`

`   -80('50) = End Transition? (not sure what's this exactly but for sure the character are not rendered with this on)`

the 80 mode (when used) is active for the last 4 frame only and seems like it's not used when the fmv transition to the field at the end (eg. attack on Dollet landing or Galbadia Garden intro)

The camera data is really similar to the Field one contained in the .CA files.

Thanks to TrueOdin that bringed them to my attention it looks like beta PC version for FF7 had some cam files too but they were slightly different:

-each frame sector is 40byte size with no 'END' marker

-there is no header so if you want to know the frame count you have to divide the filesize by 40

-Zoom is not repeated

The structure for FF7 .cam sector is something like this :

| Offset | Size    | Description                                 |
|--------|---------|---------------------------------------------|
| 0      | 6 bytes | Camera Vector X axis                        |
| 6      | 6 bytes | Camera Vector Y axis                        |
| 12     | 6 bytes | Camera Vector Z axis                        |
| 18     | 2 bytes | Camera Vector Z.z (copy)                    |
| 20     | 4 bytes | Camera Space X position                     |
| 24     | 4 bytes | Camera Space Y position                     |
| 28     | 4 bytes | Camera Space Z position                     |
| 32     | 2 bytes | Camera Pan X                                |
| 34     | 2 bytes | Camera Pan Y                                |
| 36     | 2 bytes | Zoom                                        |
| 38     | 2 bytes | Unknown (Xx Repeated? not sure, need check) |

If someone is willing to create a ff7 wiki page for this feel free to move this last part there.

## Pak File Details

The filenames are based on the 2013 name scheme. I am using **h** suffix for high res and **l** suffix for low res. Disc numbers go from 0-3. And 4 being for extra videos not fmv related.

##### disc1.pak

| FileName        | Frames | Offset   | Size     | Type |
|-----------------|--------|----------|----------|------|
| disc00\_00.cam  | 326    | 0        | 14352    | F8P  |
| disc00\_00h.bik | 326    | 3810     | 5759124  | BIK  |
| disc00\_00l.bik | 326    | 5818a4   | 2498748  | BIK  |
| disc00\_01.cam  | 199    | 7e3960   | 8764     | F8P  |
| disc00\_01h.bik | 205    | 7e5b9c   | 3572420  | BIK  |
| disc00\_01l.bik | 205    | b4de60   | 1522312  | BIK  |
| disc00\_02.cam  | 161    | cc18e8   | 7092     | F8P  |
| disc00\_02h.bik | 161    | cc349c   | 2805776  | BIK  |
| disc00\_02l.bik | 161    | f704ac   | 1410720  | BIK  |
| disc00\_03.cam  | 1100   | 10c8b4c  | 48408    | F8P  |
| disc00\_03h.bik | 1100   | 10d4864  | 19654004 | BIK  |
| disc00\_03l.bik | 1100   | 2392dd8  | 8597316  | BIK  |
| disc00\_04.cam  | 215    | 2bc5d1c  | 9468     | F8P  |
| disc00\_04h.bik | 215    | 2bc8218  | 3778948  | BIK  |
| disc00\_04l.bik | 215    | 2f62b9c  | 1628944  | BIK  |
| disc00\_05.cam  | 1114   | 30f06ac  | 49024    | F8P  |
| disc00\_05h.bik | 1114   | 30fc62c  | 20063552 | BIK  |
| disc00\_05l.bik | 1114   | 441eb6c  | 8923620  | BIK  |
| disc00\_06.cam  | 41     | 4ca1550  | 1812     | F8P  |
| disc00\_06h.bik | 41     | 4ca1c64  | 757108   | BIK  |
| disc00\_06l.bik | 41     | 4d5a9d8  | 347236   | BIK  |
| disc00\_07.cam  | 1084   | 4daf63c  | 47704    | F8P  |
| disc00\_07h.bik | 1084   | 4dbb094  | 19696056 | BIK  |
| disc00\_07l.bik | 1084   | 6083a4c  | 8855428  | BIK  |
| disc00\_08.cam  | 324    | 68f59d0  | 14264    | F8P  |
| disc00\_08h.bik | 324    | 68f9188  | 4736972  | BIK  |
| disc00\_08l.bik | 324    | 6d7d954  | 2073440  | BIK  |
| disc00\_09.cam  | 1391   | 6f77cb4  | 61212    | F8P  |
| disc00\_09h.bik | 1391   | 6f86bd0  | 24180228 | BIK  |
| disc00\_09l.bik | 1391   | 86961d4  | 10270268 | BIK  |
| disc00\_10.cam  | 393    | 9061810  | 17300    | F8P  |
| disc00\_10h.bik | 393    | 9065ba4  | 7195820  | BIK  |
| disc00\_10l.bik | 393    | 9742850  | 3265804  | BIK  |
| disc00\_11.cam  | 465    | 9a5fd5c  | 20468    | F8P  |
| disc00\_11h.bik | 465    | 9a64d50  | 8496456  | BIK  |
| disc00\_11l.bik | 465    | a27f298  | 3846440  | BIK  |
| disc00\_12.cam  | 45     | a62a3c0  | 1988     | F8P  |
| disc00\_12h.bik | 45     | a62ab84  | 752040   | BIK  |
| disc00\_12l.bik | 45     | a6e252c  | 300964   | BIK  |
| disc00\_13.cam  | 15     | a72bcd0  | 668      | F8P  |
| disc00\_13h.bik | 15     | a72bf6c  | 249788   | BIK  |
| disc00\_13l.bik | 15     | a768f28  | 99988    | BIK  |
| disc00\_14.cam  | 360    | a7815bc  | 15848    | F8P  |
| disc00\_14h.bik | 360    | a7853a4  | 6369460  | BIK  |
| disc00\_14l.bik | 360    | ad98458  | 2769344  | BIK  |
| disc00\_15.cam  | 300    | b03c618  | 13208    | F8P  |
| disc00\_15h.bik | 300    | b03f9b0  | 5236916  | BIK  |
| disc00\_15l.bik | 300    | b53e264  | 2236992  | BIK  |
| disc00\_16.cam  | 150    | b7604a4  | 6608     | F8P  |
| disc00\_16h.bik | 150    | b761e74  | 2776716  | BIK  |
| disc00\_16l.bik | 150    | ba07d00  | 1276724  | BIK  |
| disc00\_17.cam  | 890    | bb3f834  | 39168    | F8P  |
| disc00\_17h.bik | 890    | bb49134  | 15823644 | BIK  |
| disc00\_17l.bik | 890    | ca60450  | 8111120  | BIK  |
| disc00\_18.cam  | 191    | d21c860  | 8412     | F8P  |
| disc00\_18h.bik | 192    | d21e93c  | 3436444  | BIK  |
| disc00\_18l.bik | 192    | d5658d8  | 1772548  | BIK  |
| disc00\_19.cam  | 121    | d7164dc  | 5332     | F8P  |
| disc00\_19h.bik | 121    | d7179b0  | 2155424  | BIK  |
| disc00\_19l.bik | 121    | d925d50  | 944536   | BIK  |
| disc00\_20.cam  | 401    | da0c6e8  | 17652    | F8P  |
| disc00\_20h.bik | 401    | da10bdc  | 7142436  | BIK  |
| disc00\_20l.bik | 401    | e0e0800  | 3132744  | BIK  |
| disc00\_21.cam  | 829    | e3dd548  | 36484    | F8P  |
| disc00\_21h.bik | 829    | e3e63cc  | 14983636 | BIK  |
| disc00\_21l.bik | 829    | f2305a0  | 6743692  | BIK  |
| disc00\_22.cam  | 141    | f89ec2c  | 6212     | F8P  |
| disc00\_22h.bik | 141    | f8a0470  | 2585084  | BIK  |
| disc00\_22l.bik | 141    | fb1766c  | 1175040  | BIK  |
| disc00\_23.cam  | 550    | fc3646c  | 24208    | F8P  |
| disc00\_23h.bik | 550    | fc3c2fc  | 9986472  | BIK  |
| disc00\_23l.bik | 550    | 105c24a4 | 4486592  | BIK  |
| disc00\_24.cam  | 575    | 10a09a64 | 25308    | F8P  |
| disc00\_24h.bik | 575    | 10a0fd40 | 10441380 | BIK  |
| disc00\_24l.bik | 575    | 11404fe4 | 4692084  | BIK  |
| disc00\_25.cam  | 130    | 1187e858 | 5728     | F8P  |
| disc00\_25h.bik | 130    | 1187feb8 | 2438880  | BIK  |
| disc00\_25l.bik | 130    | 11ad3598 | 1140268  | BIK  |
| disc00\_26.cam  | 101    | 11be9bc4 | 4452     | F8P  |
| disc00\_26h.bik | 101    | 11bead28 | 1792576  | BIK  |
| disc00\_26l.bik | 101    | 11da0768 | 783064   | BIK  |
| disc00\_27.cam  | 306    | 11e5fa40 | 13472    | F8P  |
| disc00\_27h.bik | 306    | 11e62ee0 | 5574568  | BIK  |
| disc00\_27l.bik | 306    | 123b3e88 | 2513668  | BIK  |
| disc00\_28.cam  | 432    | 1261998c | 19016    | F8P  |
| disc00\_28h.bik | 432    | 1261e3d4 | 7643824  | BIK  |
| disc00\_28l.bik | 432    | 12d68684 | 3323692  | BIK  |
| disc00\_29.cam  | 750    | 13093db0 | 33008    | F8P  |
| disc00\_29h.bik | 750    | 1309bea0 | 13517424 | BIK  |
| disc00\_29l.bik | 750    | 13d80110 | 6015936  | BIK  |
| disc00\_30.cam  | 2897   | 1433ccd0 | 127476   | F8P  |
| disc00\_30h.bik | 2925   | 1435bec4 | 49898052 | BIK  |
| disc00\_30l.bik | 2925   | 172f2108 | 22289504 | BIK  |

##### disc2.pak

| FileName        | Frames | Offset  | Size     | Type |
|-----------------|--------|---------|----------|------|
| disc01\_00.cam  | 453    | 0       | 19940    | F8P  |
| disc01\_00h.bik | 453    | 4de4    | 8128812  | BIK  |
| disc01\_00l.bik | 453    | 7c5710  | 3597828  | BIK  |
| disc01\_01.cam  | 278    | b33d14  | 12240    | F8P  |
| disc01\_01h.bik | 278    | b36ce4  | 4869600  | BIK  |
| disc01\_01l.bik | 278    | fdbac4  | 2060252  | BIK  |
| disc01\_02.cam  | 330    | 11d2aa0 | 14528    | F8P  |
| disc01\_02h.bik | 330    | 11d6360 | 5962524  | BIK  |
| disc01\_02l.bik | 330    | 1785e7c | 2662428  | BIK  |
| disc01\_03.cam  | 450    | 1a0fe98 | 19808    | F8P  |
| disc01\_03h.bik | 450    | 1a14bf8 | 8227052  | BIK  |
| disc01\_03l.bik | 450    | 21ed4e4 | 3724748  | BIK  |
| disc01\_04.cam  | 168    | 257aab0 | 7400     | F8P  |
| disc01\_04h.bik | 168    | 257c798 | 3036032  | BIK  |
| disc01\_04l.bik | 168    | 2861b18 | 1356172  | BIK  |
| disc01\_05.cam  | 219    | 29acca4 | 9644     | F8P  |
| disc01\_05h.bik | 219    | 29af250 | 4033920  | BIK  |
| disc01\_05l.bik | 219    | 2d87fd0 | 1843800  | BIK  |
| disc01\_06.cam  | 104    | 2f4a228 | 4584     | F8P  |
| disc01\_06h.bik | 104    | 2f4b410 | 1894044  | BIK  |
| disc01\_06l.bik | 104    | 3119aac | 853980   | BIK  |
| disc01\_07.cam  | 160    | 31ea288 | 7048     | F8P  |
| disc01\_07h.bik | 160    | 31ebe10 | 2909428  | BIK  |
| disc01\_07l.bik | 160    | 34b2304 | 1309396  | BIK  |
| disc01\_08.cam  | 381    | 35f1dd8 | 16772    | F8P  |
| disc01\_08h.bik | 381    | 35f5f5c | 6936652  | BIK  |
| disc01\_08l.bik | 381    | 3c937a8 | 3126604  | BIK  |
| disc01\_09.cam  | 226    | 3f8ecf4 | 9952     | F8P  |
| disc01\_09h.bik | 226    | 3f913d4 | 4177224  | BIK  |
| disc01\_09l.bik | 226    | 438d11c | 1917924  | BIK  |
| disc01\_10.cam  | 416    | 4561500 | 18312    | F8P  |
| disc01\_10h.bik | 416    | 4565c88 | 7604492  | BIK  |
| disc01\_10l.bik | 416    | 4ca6594 | 3444452  | BIK  |
| disc01\_11.cam  | 603    | 4fef478 | 26540    | F8P  |
| disc01\_11h.bik | 603    | 4ff5c24 | 10981628 | BIK  |
| disc01\_11l.bik | 603    | 5a6ed20 | 4951152  | BIK  |
| disc01\_12.cam  | 335    | 5f27990 | 14748    | F8P  |
| disc01\_12h.bik | 335    | 5f2b32c | 6173264  | BIK  |
| disc01\_12l.bik | 335    | 650e57c | 2823184  | BIK  |
| disc01\_13.cam  | 381    | 67bf98c | 16772    | F8P  |
| disc01\_13h.bik | 381    | 67c3b10 | 6843600  | BIK  |
| disc01\_13l.bik | 381    | 6e4a7e0 | 3034044  | BIK  |
| disc01\_14.cam  | 531    | 712f39c | 23372    | F8P  |
| disc01\_14h.bik | 531    | 7134ee8 | 9498260  | BIK  |
| disc01\_14l.bik | 531    | 7a43d7c | 4188788  | BIK  |
| disc01\_15.cam  | 120    | 7e427f0 | 5288     | F8P  |
| disc01\_15h.bik | 120    | 7e43c98 | 2224344  | BIK  |
| disc01\_15l.bik | 120    | 8062d70 | 1024412  | BIK  |
| disc01\_16.cam  | 149    | 815cf0c | 6564     | F8P  |
| disc01\_16h.bik | 149    | 815e8b0 | 2754272  | BIK  |
| disc01\_16l.bik | 149    | 83fef90 | 1264204  | BIK  |
| disc01\_17.cam  | 150    | 85339dc | 6608     | F8P  |
| disc01\_17h.bik | 150    | 85353ac | 2722300  | BIK  |
| disc01\_17l.bik | 150    | 87cdda8 | 1221752  | BIK  |
| disc01\_18.cam  | 255    | 88f8220 | 11228    | F8P  |
| disc01\_18h.bik | 255    | 88fadfc | 4656768  | BIK  |
| disc01\_18l.bik | 255    | 8d6bc7c | 2106780  | BIK  |
| disc01\_19.cam  | 428    | 8f6e218 | 18840    | F8P  |
| disc01\_19h.bik | 428    | 8f72bb0 | 7841392  | BIK  |
| disc01\_19l.bik | 428    | 96ed220 | 3561280  | BIK  |
| disc01\_20.cam  | 150    | 9a52960 | 6608     | F8P  |
| disc01\_20h.bik | 150    | 9a54330 | 2667756  | BIK  |
| disc01\_20l.bik | 150    | 9cdf81c | 1168116  | BIK  |
| disc01\_21.cam  | 75     | 9dfcb10 | 3308     | F8P  |
| disc01\_21h.bik | 75     | 9dfd7fc | 1396348  | BIK  |
| disc01\_21l.bik | 75     | 9f52678 | 646296   | BIK  |
| disc01\_22.cam  | 120    | 9ff0310 | 5288     | F8P  |
| disc01\_22h.bik | 120    | 9ff17b8 | 2132696  | BIK  |
| disc01\_22l.bik | 120    | a1fa290 | 932544   | BIK  |
| disc01\_23.cam  | 285    | a2ddd50 | 12548    | F8P  |
| disc01\_23h.bik | 285    | a2e0e54 | 5164156  | BIK  |
| disc01\_23l.bik | 285    | a7cdad0 | 2314168  | BIK  |
| disc01\_24.cam  | 330    | aa02a88 | 14528    | F8P  |
| disc01\_24h.bik | 330    | aa06348 | 6084528  | BIK  |
| disc01\_24l.bik | 330    | afd3af8 | 2784636  | BIK  |
| disc01\_25.cam  | 300    | b27b874 | 13208    | F8P  |
| disc01\_25h.bik | 300    | b27ec0c | 5413124  | BIK  |
| disc01\_25l.bik | 300    | b7a8510 | 2413380  | BIK  |
| disc01\_26.cam  | 120    | b9f5854 | 5288     | F8P  |
| disc01\_26h.bik | 120    | b9f6cfc | 2180104  | BIK  |
| disc01\_26l.bik | 120    | bc0b104 | 980208   | BIK  |
| disc01\_27.cam  | 75     | bcfa5f4 | 3308     | F8P  |
| disc01\_27h.bik | 75     | bcfb2e0 | 1345552  | BIK  |
| disc01\_27l.bik | 75     | be43af0 | 595492   | BIK  |
| disc01\_28.cam  | 120    | bed5114 | 5288     | F8P  |
| disc01\_28h.bik | 120    | bed65bc | 2180512  | BIK  |
| disc01\_28l.bik | 120    | c0eab5c | 980596   | BIK  |
| disc01\_29.cam  | 692    | c1da1d0 | 30456    | F8P  |
| disc01\_29h.bik | 692    | c1e18c8 | 12448828 | BIK  |
| disc01\_29l.bik | 692    | cdc0d04 | 5528956  | BIK  |
| disc01\_30.cam  | 120    | d306a80 | 5288     | F8P  |
| disc01\_30h.bik | 120    | d307f28 | 2194876  | BIK  |
| disc01\_30l.bik | 120    | d51fce4 | 994700   | BIK  |
| disc01\_31.cam  | 135    | d612a70 | 5948     | F8P  |
| disc01\_31h.bik | 135    | d6141ac | 2480668  | BIK  |
| disc01\_31l.bik | 135    | d871bc8 | 1130648  | BIK  |
| disc01\_32.cam  | 327    | d985c60 | 14396    | F8P  |
| disc01\_32h.bik | 327    | d98949c | 5902052  | BIK  |
| disc01\_32l.bik | 327    | df2a380 | 2628608  | BIK  |
| disc01\_33.cam  | 1186   | e1abf80 | 52192    | F8P  |
| disc01\_33h.bik | 1186   | e1b8b60 | 21305376 | BIK  |
| disc01\_33l.bik | 1186   | f60a380 | 9445316  | BIK  |

##### disc3.pak

| FileName        | Frames | Offset  | Size     | Type |
|-----------------|--------|---------|----------|------|
| disc02\_00.cam  | 197    | 0       | 8676     | F8P  |
| disc02\_00h.bik | 197    | 21e4    | 3641072  | BIK  |
| disc02\_00l.bik | 197    | 37b0d4  | 1670856  | BIK  |
| disc02\_01.cam  | 472    | 512f9c  | 20776    | F8P  |
| disc02\_01h.bik | 472    | 5180c4  | 8222124  | BIK  |
| disc02\_01l.bik | 472    | cef670  | 3725124  | BIK  |
| disc02\_02.cam  | 105    | 107cdb4 | 4628     | F8P  |
| disc02\_02h.bik | 105    | 107dfc8 | 1970280  | BIK  |
| disc02\_02l.bik | 105    | 125f030 | 919644   | BIK  |
| disc02\_03.cam  | 105    | 133f88c | 4628     | F8P  |
| disc02\_03h.bik | 105    | 1340aa0 | 1958900  | BIK  |
| disc02\_03l.bik | 105    | 151ee94 | 909292   | BIK  |
| disc02\_04.cam  | 106    | 15fce80 | 4672     | F8P  |
| disc02\_04h.bik | 106    | 15fe0c0 | 1887824  | BIK  |
| disc02\_04l.bik | 106    | 17caf10 | 827636   | BIK  |
| disc02\_05.cam  | 106    | 1895004 | 4672     | F8P  |
| disc02\_05h.bik | 106    | 1896244 | 1887052  | BIK  |
| disc02\_05l.bik | 106    | 1a62d90 | 827048   | BIK  |
| disc02\_06.cam  | 110    | 1b2cc38 | 4848     | F8P  |
| disc02\_06h.bik | 110    | 1b2df28 | 2008528  | BIK  |
| disc02\_06l.bik | 110    | 1d184f8 | 908540   | BIK  |
| disc02\_07.cam  | 300    | 1df61f4 | 13208    | F8P  |
| disc02\_07h.bik | 300    | 1df958c | 5197180  | BIK  |
| disc02\_07l.bik | 300    | 22ee308 | 2299856  | BIK  |
| disc02\_08.cam  | 75     | 251fad8 | 3308     | F8P  |
| disc02\_08h.bik | 75     | 25207c4 | 1331060  | BIK  |
| disc02\_08l.bik | 75     | 2665738 | 580980   | BIK  |
| disc02\_09.cam  | 728    | 26f34ac | 32040    | F8P  |
| disc02\_09h.bik | 728    | 26fb1d4 | 13015424 | BIK  |
| disc02\_09l.bik | 728    | 3364b54 | 5734772  | BIK  |
| disc02\_10.cam  | 120    | 38dccc8 | 5288     | F8P  |
| disc02\_10h.bik | 120    | 38de170 | 2201640  | BIK  |
| disc02\_10l.bik | 120    | 3af7998 | 1001672  | BIK  |
| disc02\_11.cam  | 315    | 3bec260 | 13868    | F8P  |
| disc02\_11h.bik | 315    | 3bef88c | 5698360  | BIK  |
| disc02\_11l.bik | 315    | 415ebc4 | 2548364  | BIK  |
| disc02\_12.cam  | 226    | 43cce50 | 9952     | F8P  |
| disc02\_12h.bik | 226    | 43cf530 | 4078040  | BIK  |
| disc02\_12l.bik | 226    | 47b2f08 | 1818104  | BIK  |
| disc02\_13.cam  | 611    | 496ed00 | 26892    | F8P  |
| disc02\_13h.bik | 611    | 497560c | 10918000 | BIK  |
| disc02\_13l.bik | 611    | 53dee7c | 4793772  | BIK  |
| disc02\_14.cam  | 105    | 5871428 | 4628     | F8P  |
| disc02\_14h.bik | 105    | 587263c | 1924220  | BIK  |
| disc02\_14l.bik | 105    | 5a482b8 | 874880   | BIK  |
| disc02\_15.cam  | 255    | 5b1dc38 | 11228    | F8P  |
| disc02\_15h.bik | 255    | 5b20814 | 4525952  | BIK  |
| disc02\_15l.bik | 255    | 5f71794 | 2026736  | BIK  |
| disc02\_16.cam  | 233    | 6160484 | 10260    | F8P  |
| disc02\_16h.bik | 233    | 6162c98 | 4248316  | BIK  |
| disc02\_16l.bik | 233    | 656ff94 | 1918400  | BIK  |
| disc02\_17.cam  | 90     | 6744554 | 3968     | F8P  |
| disc02\_17h.bik | 90     | 67454d4 | 1628548  | BIK  |
| disc02\_17l.bik | 90     | 68d2e58 | 728508   | BIK  |
| disc02\_18.cam  | 90     | 6984c14 | 3968     | F8P  |
| disc02\_18h.bik | 90     | 6985b94 | 1614036  | BIK  |
| disc02\_18l.bik | 90     | 6b0fc68 | 714012   | BIK  |
| disc02\_19.cam  | 162    | 6bbe184 | 7136     | F8P  |
| disc02\_19h.bik | 162    | 6bbfd64 | 2733948  | BIK  |
| disc02\_19l.bik | 162    | 6e5b4e0 | 1195420  | BIK  |
| disc02\_20.cam  | 275    | 6f7f27c | 12108    | F8P  |
| disc02\_20h.bik | 275    | 6f821c8 | 4904472  | BIK  |
| disc02\_20l.bik | 275    | 742f7e0 | 2154376  | BIK  |
| disc02\_21.cam  | 280    | 763d768 | 12328    | F8P  |
| disc02\_21h.bik | 280    | 7640790 | 4514208  | BIK  |
| disc02\_21l.bik | 280    | 7a8e930 | 1987908  | BIK  |
| disc02\_22.cam  | 90     | 7c73e74 | 3968     | F8P  |
| disc02\_22h.bik | 90     | 7c74df4 | 1650640  | BIK  |
| disc02\_22l.bik | 90     | 7e07dc4 | 750740   | BIK  |
| disc02\_23.cam  | 200    | 7ebf258 | 8808     | F8P  |
| disc02\_23h.bik | 200    | 7ec14c0 | 3558312  | BIK  |
| disc02\_23l.bik | 200    | 8226068 | 1558340  | BIK  |
| disc02\_24.cam  | 600    | 83a27ac | 26408    | F8P  |
| disc02\_24h.bik | 600    | 83a8ed4 | 10585392 | BIK  |
| disc02\_24l.bik | 600    | 8dc1404 | 4585408  | BIK  |
| disc02\_25.cam  | 30     | 9220bc4 | 1328     | F8P  |
| disc02\_25h.bik | 30     | 92210f4 | 559944   | BIK  |
| disc02\_25l.bik | 30     | 92a9c3c | 256904   | BIK  |
| disc02\_26.cam  | 410    | 92e87c4 | 18048    | F8P  |
| disc02\_26h.bik | 410    | 92ece44 | 7479808  | BIK  |
| disc02\_26l.bik | 410    | 9a0f044 | 3401948  | BIK  |
| disc02\_27.cam  | 130    | 9d4d920 | 5728     | F8P  |
| disc02\_27h.bik | 130    | 9d4ef80 | 2423808  | BIK  |
| disc02\_27l.bik | 130    | 9f9eb80 | 1123796  | BIK  |
| disc02\_28.cam  | 376    | a0b1154 | 16552    | F8P  |
| disc02\_28h.bik | 376    | a0b51fc | 6874028  | BIK  |
| disc02\_28l.bik | 376    | a7435a8 | 3114128  | BIK  |
| disc02\_29.cam  | 395    | aa3ba38 | 17388    | F8P  |
| disc02\_29h.bik | 395    | aa3fe24 | 7284036  | BIK  |
| disc02\_29l.bik | 395    | b132368 | 3334088  | BIK  |
| disc02\_30.cam  | 625    | b460330 | 27508    | F8P  |
| disc02\_30h.bik | 625    | b466ea4 | 11211932 | BIK  |
| disc02\_30l.bik | 625    | bf18340 | 4961628  | BIK  |
| disc02\_31.cam  | 995    | c3d389c | 43788    | F8P  |
| disc02\_31h.bik | 995    | c3de3a8 | 17959496 | BIK  |
| disc02\_31l.bik | 995    | d4fedf0 | 8009592  | BIK  |

##### disc4.pak

| FileName        | Frames | Offset   | Size      | Type |
|-----------------|--------|----------|-----------|------|
| disc03\_00.cam  | 390    | 0        | 17168     | F8P  |
| disc03\_00h.bik | 390    | 4310     | 7076980   | BIK  |
| disc03\_00l.bik | 390    | 6c3f84   | 3177212   | BIK  |
| disc03\_01.cam  | 1260   | 9cba80   | 55448     | F8P  |
| disc03\_01h.bik | 1260   | 9d9318   | 22713736  | BIK  |
| disc03\_01l.bik | 1260   | 1f828a0  | 10113788  | BIK  |
| disc03\_02.cam  | 285    | 2927b9c  | 12548     | F8P  |
| disc03\_02h.bik | 285    | 292aca0  | 5103348   | BIK  |
| disc03\_02l.bik | 285    | 2e08b94  | 2252028   | BIK  |
| disc03\_03.cam  | 225    | 302e890  | 9908      | F8P  |
| disc03\_03h.bik | 225    | 3030f44  | 4064732   | BIK  |
| disc03\_03l.bik | 225    | 3411520  | 1814904   | BIK  |
| disc03\_04.cam  | 4348   | 35cc698  | 191320    | F8P  |
| disc03\_04h.bik | 4345   | 35fb1f0  | 75274524  | BIK  |
| disc03\_04l.bik | 4345   | 7dc4b0c  | 32520396  | BIK  |
| disc03\_05.cam  | 3065   | 9cc83d8  | 134868    | F8P  |
| disc03\_05h.bik | 3065   | 9ce92ac  | 28030204  | BIK  |
| disc03\_05l.bik | 3065   | b7a47a8  | 15064748  | BIK  |
| disc03\_06.cam  | 7091   | c602654  | 312012    | F8P  |
| disc03\_06h.bik | 7091   | c64e920  | 124325396 | BIK  |
| disc03\_06l.bik | 7091   | 13cdf734 | 55224860  | BIK  |

##### publish.pak

| FileName        | Frames | Offset | Size   | Type |
|-----------------|--------|--------|--------|------|
| disc04\_00h.bik | 117    | 0      | 196276 | BIK  |
| disc04\_00l.bik | 117    | 2feb4  | 86240  | BIK  |
