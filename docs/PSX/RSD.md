---
title: RSD
---

[Home](../Main%20Page.md.md) > [PSX](../PSX.md) > RSD

## RSD resource data format

An RSD file is product of the original Playstation Psy-Q 3D development
libraries. They are often expoted by 3D modelers when converting from an
LWO or DXF file to something more understandable by the PSX. It is in
ascii, making it easy to edit by hand. When a 3D editor does an export,
four text files are actually created, .rsd, .ply, .mat, and .grp. These
can then be "compiled" into a binary .rsd file for the PSX.

In the PC version of Final Fantasy 7, the text .rsd file is used while
the other files were "compiled" into [Polygon(.p)][] format.

The following example is "acaa.rsd", the RSD File for Yuffie's Head:

`@RSD940102`  
` # Output by SGI RSD fileset library libRsdObj.`  
` PLY=ACAB.PLY`  
` MAT=ACAB.MAT`  
` GRP=ACAB.GRP`  
` # Texture files`  
` NTEX=3`  
` TEX[0]=ACAC.TIM`  
` TEX[1]=ACAD.TIM `  
` TEX[2]=ACAE.TIM`  
` `

The first line is an ID. It is always the following.

`@RSD940102`

The number, 940102, is a date. January 2nd, 1994. This was created with
one of the first SGI workstations for PSX development.

The Second line is a comment. Every line beginning with "\#" is ignored
by the engine.

`# Output by SGI RSD fileset library libRsdObj.`

The next lines tell you the Polygon Mesh File for this model.

`PLY=ACAB.PLY`

This is the Material File for this Model.

`MAT=ACAB.MAT`

The Group file..

`GRP=ACAB.GRP`

On FF7PC, these files were compiled into a [Polygon(.p)][] file, but
with the same four leter filename.

The next line is telling how many textures this model uses. Usually it
is 0, and there are no more lines. However, in our example it is 3, and
there are 3 textures in here.

`NTEX=3`

In the last section you can see an array telling you the filenames for
the textures. However, if you want to have the "real" filename, you'll
have to replace "TIM" by "TEX""ACAC.TIM" --&gt; "ACAC.TEX"

`TEX[x]=y`

  [Polygon(.p)]: ../FF7/P.md "wikilink"
