---
title: Pointers
---

By MaKiPL.

FF8 engine reads [Battle Stage files](../FileFormat_X.md)

**Here's the list:**

`private static uint GetCameraPointer()`  
`       {`  
`           int[] _x5D4 = {4,5,9,12,13,14,15,21,22,23,24,26,`  
`           29,32,33,34,35,36,39,40,50,53,55,61,62,63,64,65,66,67,68,69,70,`  
`           71,72,73,75,78,82,83,85,86,87,88,89,90,91,94,96,97,98,99,100,105,`  
`           106,121,122,123,124,125,126,127,135,138,141,144,145,148,149,150,`  
`           151,158,160};`  
`           int[] _x5D8 = {`  
`           0,1,2,3,6,7,10,11,17,18,25,27,28,38,41,42,43,47,49,57,58,59,60,74,`  
`           76,77,80,81,84,93,95,101,102,103,104,109,110,111,112,113,114,115,116,`  
`           117,118,119,120,128,129,130,131,132,133,134,139,140,143,146,152,153,154,`  
`           155,156,159,161,162};`  
`           int _5d4 = _x5D4.Count(x => x== Memory.encounters[Memory.battle_encounter].bScenario);`  
`           int _5d8 = _x5D8.Count(x => x == Memory.encounters[Memory.battle_encounter].bScenario);`  
`           if (_5d4 > 0) return 0x5D4;`  
`           if (_5d8 > 0) return 0x5D8;`  
`           switch (Memory.encounters[Memory.battle_encounter].bScenario)`  
`           {`  
`               case 8:`  
`               case 48:`  
`               case 79:`  
`                   return 0x618;`  
`               case 16:`  
`                   return 0x628;`  
`               case 19:`  
`                   return 0x644;`  
`               case 20:`  
`                   return 0x61c;`  
`               case 30:`  
`               case 31:`  
`                   return 0x934;`  
`               case 37:`  
`                   return 0xcc0;`  
`               case 44:`  
`               case 45:`  
`               case 46:`  
`                   return 0x9A4;`  
`               case 51:`  
`               case 52:`  
`               case 107:`  
`               case 108:`  
`                   return 0x600;`  
`               case 54:`  
`               case 56:`  
`                   return 0x620;`  
`               case 92:`  
`                   return 0x83c;`  
`               case 136:`  
`                   return 0x5fc;`  
`               case 137:`  
`                   return 0xFDC; //That one is really giant, what is it? //It's a witch stage, worth to see at MIPS`  
`               case 142:`  
`                   return 0x183C; //That one won! xD //It's a final battle`  
`               case 147:`  
`                   return 0xa0c;`  
`               case 157:`  
`                   return 0x638;`  
`           }`  
`           throw new Exception("0xFFF, unknown pointer!");`  
`       }`
