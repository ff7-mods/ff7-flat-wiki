---
title: Camera_Matrix
---

### Section 2: Camera Matrix ([Kero](../../User:Kero)

This is yet to be completely understand, I am pretty sure that this is not exactly trash, since it is based on at least 300 changes of field files. It was pretty nasty, as you can imagine, first divide sections of field file, load section 2 into hexedit, change byte, save section 2, run .bat file that complete new field file with new section 2 and compress it. After that I always had to use ficedula lgp tools, awful, I am definitely going to program command line program for this, in gui i had to alway on original field file, click, replace, click instead of just adding line to .bat file. After that run ff7.exe, go to destinated location and observe what happened.

I am working on program to load walkmesh along with camera matrix. I am pretty sure about vectors, after all, they are all same length and they are orthogonal, but i could misinterpret order of them, position of center is little uncertain and resize factor too. The program should help me to figure out these thing.

#### Description of section 2 (field file): Camera

The goal of this section is to define camera matrix. In fact it seems pretty simple. For camera matrix, you need vector for axis x, vector for axis y, vector for axis z and position of camera in world space. Vectors for axis x,y,z are defined in world space and in camera space are normally united.

Example: You have axis x defined as vector (0.176,-0.512,0.840) but that is in world space. In camera space it is just (1,0,0).

\- Every offset is relative here, 00 is at the start of section 2 (after length indicator). - This will will be in the left handed coordinated system; x-axis from left to right, y-axis from bottom to top, z-axis from near to far. - In here, I am changing signs so these vectors should be correct for file loaded right from section 5 walkmesh. While in walkmesh you don't change any signs, here I am changing them, so they will fit and if you use this article with unchanged values for walkmesh, you should get right image, same as in ff7. (FIXME: not yet true)

This is an overview the camera data format.

#### Section 2 Format

| Offset | Size    | Description              |
|--------|---------|--------------------------|
| 0x00   | 6 bytes | Camera Vector X axis     |
| 0x06   | 6 bytes | Camera Vector Y axis     |
| 0x0C   | 6 bytes | Camera Vector Z axis     |
| 0x12   | 2 bytes | Camera Vector Z.z (copy) |
| 0x14   | 4 bytes | Camera Space X position  |
| 0x18   | 4 bytes | Camera Space Y position  |
| 0x1C   | 4 bytes | Camera Space Z position  |
| 0x20   | 4 bytes | *Blank*                  |
| 0x24   | 2 bytes | Zoom                     |

There may be multiple cameras in a single file, in that case (mds5_1, blinst_1...) this data structure (sizeof=38 bytes) is repeated several times, and there is no indication of the count of cameras, except the size of the section.

How to get vectors for the axis:

Vectors are stored right at the beginning of section 2.

`typedef struct {`  
`   S16 x;`  
`   S16 y;`  
`   S16 z;`  
`} vector3s;`

You will load first vector for axis x (from offset 0 to 5), for axis y (6 to 11) and axis z (12-17). These values are in fixed point with multiply constant 4096. Length of vectors x,y and z is always 4096 (first vecsize is for x, then y and last z), thats make out multiplication constant. These vectors are also always orthogonormal, as you can see in ORTO 1-2 (1=x,2-y,3=z) ORTO U-Vis scalar product of U and V. As you can see, very near zero (first value is without division of multi constant). Now you have three vectors, but they are not looking in correct direction, you have to change some signs. For each vector change sign of y and z values. Now these vectors should point in correct direction, same as in FF7.

I am now assuming that you have vectors for axises loaded, each component of each vector was divided by 4096 (don't forget to store it in float) and you changed signs for component y and z. After vectors is one S16 number (from offset 18 to 19), same as z component of vector for z axis.

Now you want to have position of center of the camera matrix. Get three S32 numbers for position of center (x from 20 to 23, y from 24-27 and z from 28-31). These number are not position of center in worlds pace, but they are position of center of camera space, defined in space, where position of center is in 0,0,0 and axis for vectors are the ones you read, but have opposite signs. You get center of camera matrix like this:

`// vx,vy,vz are axis you read, divided, y,z signs changed`  
`// (tx,ty,tz) is position of camera matrix in world space`  
`// ox,oy,oz are S32 numbers you read from offset 20 to 31`  
`tx = -(ox*vx.x + oy*vy.x + oz*vz.x);`  
`ty = -(ox*vx.y + oy*vy.y + oz*vz.y);`  
`tz = -(ox*vx.z + oy*vy.z + oz*vz.z);`

After this is just blank U32 number, seems always zero and last, but not least the zoom (36-37) (don't know whether Signed or Unsigned). The bigger resize number, the bigger the model and walkmesh.
