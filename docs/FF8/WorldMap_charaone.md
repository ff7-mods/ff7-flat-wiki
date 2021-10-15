---
title: WorldMap_charaone
---

by Maki file is different than field [\[ONE](FileFormat_ONE.md) and then again with argument 0x12 having pointer to data as in Wiki in EAX. It's like:

`uint myPointer = charaOneFunction(pointer_to_Chara_section, 0x11...);`  
`charaOneFunction(myPointer, 0x12...);`

## Header

| Offset                                | Length                                       | Description |
|---------------------------------------|----------------------------------------------|-------------|
| 0x00                                  | uint                                         | EOF         |
| 0x04                                  | (TIM\_height \* (TIM\_width \* 4) ) / 2 + 64 | TIM texture |
| \*(this) != x 10 00 00 00 08 00 00 00 | Varies                                       | Chara       |

## Chara

Always 64 bytes length!

UPDATE: Looks like it's 1:1 to MCH: <http://wiki.ffrtt.ru/index.php/FF8/FileFormat_MCH#Model-Data>

| Offset | Length                     | Description                          |
|--------|----------------------------|--------------------------------------|
| 0x00   | uint                       | BoneSectionLength                    |
| 0x04   | uint                       | unknown struct size. Multiply by 8   |
| 0x08   | uint                       | unknown size                         |
| 0x0C   | uint                       | count (used as controller local var) |
| 0x10   | uint                       | unknown                              |
| 0x14   | uint                       | unknown                              |
| 0x18   | uint                       | unknown                              |
| 0x1C   | uint                       | unknown                              |
| 0x20   | uint                       | unknown                              |
| 0x24   | uint                       | unknown                              |
| 0x28   | uint                       | unknown                              |
| 0x2C   | uint                       | unknown                              |
| 0x30   | uint                       | unknown                              |
| 0x24   | uint                       | unknown                              |
| 0x38   | uint                       | Animation section pointer (0x12)     |
| 0x3C   | uint                       | unknown                              |
| 0x40   | BoneSectionLength&lt;&lt;6 | BoneSection                          |

## Animation section (arg4

0x12) ==

| Offset                                                | Length       | Description       |
|-------------------------------------------------------|--------------|-------------------|
| 0x00                                                  | ushort       | countOfAnimations |
| 0x02 + ( entry.Length != 0 ? sizeof(entry\[i-1\] : 0) | sizeof(this) | Animation         |

Animation:

| Offset                                         | Length                        | Description                       |
|------------------------------------------------|-------------------------------|-----------------------------------|
| 0x00                                           | ushort                        | count of animation keypoints      |
| 0x02                                           | ushort                        | count of bones translation frames |
| 0x04 + (entityID \* (countOfBoneRot \* 6) + 6) | 6 + (countOfBoneRotations\*6) | AnimationKeypoint                 |

AnimationKeypoint:

| Offset             | Length | Description          |
|--------------------|--------|----------------------|
| 0x00               | short  | origin X offset      |
| 0x02               | short  | origin Z offset      |
| 0x04               | short  | origin Y (up) offset |
| 0x06 + (boneID\*6) | short  | Bone\[boneID\].RotX  |
| 0x08 + (boneID\*6) | short  | Bone\[boneID\].RotZ  |
| 0x0A + (boneID\*6) | short  | Bone\[boneID\].RotY  |

Case study: First character is Squall in chara.one. Two TIM 8BPP textures. Squall has 8 animations. First animation has one keypoint with 16 bone translations. When moving it plays 2nd animation and has 0x14 keypoints which every have 0x10 bone translations. You can edit origin XYZ offsets for every frame. Due to they way the file is constructed it's not so easy to actually test play other animations.

# source

Example C\# source of file parsing as in OpenVIII (commit from 16/02/1019): <https://github.com/MaKiPL/OpenVIII/blob/db46297fbc7961852e89427927df2e40623266a5/FF8/module_world_debug.cs#L202>

`private static void ReadCharaOne(byte[] charaOneB)`  
`       {`  
`           using (MemoryStream ms = new MemoryStream(charaOneB))`  
`           using (BinaryReader br = new BinaryReader(ms))`  
`           {`  
`               uint eof = br.ReadUInt32();`  
`               TIM2 tim;`  
`               while (ms.CanRead)`  
`                   if (BitConverter.ToUInt16(charaOneB, (int)ms.Position) == 0)`  
`                       ms.Seek(2, SeekOrigin.Current);`  
`                   else if (br.ReadUInt64() == 0x0000000800000010)`  
`                   {`  
`                       ms.Seek(-8, SeekOrigin.Current);`  
`                       tim = new TIM2(charaOneB, (uint)ms.Position);`  
`                       ms.Seek(tim.GetHeight * tim.GetWidth / 2 + 64, SeekOrigin.Current); //i.e. 64*20=1280/2=640 + 64= 704 + eof`  
`                       if (charaOneTextures == null)`  
`                           charaOneTextures = new List<Texture2D[]>();`  
`                       charaOneTextures.Add(new Texture2D[1] { new Texture2D(Memory.graphics.GraphicsDevice, tim.GetWidth, tim.GetHeight, false, SurfaceFormat.Color) });`  
`                       charaOneTextures.Last()[0].SetData(tim.CreateImageBuffer(tim.GetClutColors(0), true));`  
`                   }`  
`                   else //is geometry structure`  
`                   {`  
`                       ms.Seek(-8, SeekOrigin.Current);`  
`                       uint esi10h = BitConverter.ToUInt32(charaOneB, (int)ms.Position + 0x10);`  
`                       uint esi14h = BitConverter.ToUInt32(charaOneB, (int)ms.Position + 0x14);`  
`                       uint u45 = BitConverter.ToUInt32(charaOneB, (int)ms.Position + 56); //+2?`  
`                       uint v29 = BitConverter.ToUInt32(charaOneB, (int)ms.Position) << 6; //bone section?`  
`                       uint d250516c = BitConverter.ToUInt32(charaOneB, (int)ms.Position + 4) * 8; //unk?`  
`                       uint v25 = BitConverter.ToUInt32(charaOneB, (int)ms.Position + 8); //unk size?`  
`                       ms.Seek(u45, SeekOrigin.Current);`  
`                       if (ms.Position > ms.Length)`  
`                           break;`  
`                       ushort countIs = br.ReadUInt16();`  
`                       ushort cEntries = 0;`  
`                       while (countIs != 0/*(cEntries = br.ReadUInt16()) != 0*/)`  
`                       {`  
`                           cEntries = br.ReadUInt16();`  
`                           ushort cBones = br.ReadUInt16();`  
`                           while (cEntries != 0)`  
`                           {`  
`                               Bone testBone = new Bone() { X = br.ReadInt16(), Y = br.ReadInt16(), Z = br.ReadInt16() };`  
`                               Vector3[] myVec = new Vector3[cBones];`  
`                               for (int i = 0; i < cBones; i++)`  
`                                   myVec[i] = new Vector3() { X = br.ReadInt16(), Y = br.ReadUInt16(), Z = br.ReadUInt16() };`  
`                               cEntries--;`  
`                           }`  
`                           countIs--;`  
`                       }`  
`                   }`  
`               return;`  
`           }`  
`}`
