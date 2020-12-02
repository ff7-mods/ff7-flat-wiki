---
title: HRC
---

[Home](/Main%20Page.md) > [PSX](/PSX.md) > HRC

## HRC Hierarchy data format

An HRC file is product of the original Playstation Psy-Q 3D development
libraries. They describe the bone hierarchy of a 3D model. Most of the
time they originally start as a plain text file exported from 3D editing
software, or from a 3D file converter. From this they can be "compiled"
into binary form more usable for the PSX.

On the PC version of Final Fantasy 7, a text HRC file is used to define
the skeletal hierarchy of the field models. The Battle Models use the
compiled Format.

But I think that since you read this document, you've got some knowledge
'bout 3D models and skeletons. Let's just start, this format's quite
simple! ^\_^

### HRC file format

Since the HRC files are simple plain-text files, you can open them in
notepad or any other text editor. Here are the first four bones of
"abjb.hrc" (Yuffie's Hierarchy)

`:HEADER_BLOCK 2`  
` :SKELETON sd_yufi_sk`  
` :BONES 24`  
` `  
` hip`  
` root`  
` 2.9662`  
` 1 ABJC `  
` `  
` chest`  
` hip`  
` 4.0621967`  
` 1 ABJE`  
` `  
` head`  
` chest`  
` 5.017107`  
` 1 ACAA `  
` `  
` joint`  
` head`  
` 3.5236073`  
` 0`  
` `  
` ribon_a`  
` joint`  
` 8.52051`  
` 1 ACAF`  
` ....`  
` `

The other bones look the same as the ones listed here. These are the
parts of the file.

#### Header

As most files, also the HRC files have got a kind of header. That are
the first three lines.

`:HEADER_BLOCK 2`

This seems to be a simple "ID". As far as I know, this is the first line
in all HRCs...

`:SKELETON sd_yufi_sk`

This tells you the name of the skeleton, in our example "sd\_yufi\_sk".

`:BONES 24`

Tells you how much bones are stored in this skeleton.

#### Bones

Every bone consist of 4 Lines, which look like this. Let's first take a
look at the lines of the first bone:

<font color="GREEN"> First Line: ("hip")</font>

This is the name of the current bone.

<font color="GREEN">Second Line: ("root")</font>

This is the name of the parent bone. The parent bone must be already
listed above in the skeleton file,or it can be "root" (origin).

<font color="GREEN">Third Line: ("2.9662")</font>

That's the Length of the bone.

<font color="GREEN"> Fourth Line \#1: ("0") </font>

<font color="GREEN">Fourth Line \#2: ("1 ABJC") </font>

<font color="GREEN">Fourth Line \#3: ("2 ABJC ABJD") </font>

This line consist of 2 or more different values. First, there is a
number telling many RSD files are aligned to this model. If it has no
RSD File, the number is 0. If the number is 1, there is a string after
the number telling you the name of the Resource Data File (RSD). The RSD
file tells you which .p Model to use.

There may be even more than 2 RSD Files on 1 Bone, however this has yet
be be seen.

### Notes

There are no bone angles, just bone lengths. The HRC file only contains
hierarchy data. To build a skeleton, animation files are required.
