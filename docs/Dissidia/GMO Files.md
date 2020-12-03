---
title: GMO Files
---

[Home](Main%20Page.md) > [Dissidia](Dissidia.md) > GMO Files

<small>Last updated: [Koral][] 14:04, 30 Mar 2009 (EDT)</small>

# GMO Model File

These files contain all the Characters and Location-Map models within
the game.

A complete list of Models referenced by the Filenames can be found here:
\[\[Dissidia/GMO Files/File List\|\[GMO\] File List\]\]

# Format Specifications

<small>Information courtesy of [MrAdults][]</small>

\[GMO\] Files consist of various Chunks defining the type of data they
contain, with no initial hard-coded offsets in the begining of the file.
Each chunk must be parsed seperatly to determine its Type and Size,
either to skip it entirey or attempt to extract the information
contained within.

As such, parsing these \[GMO\] files is a similar mechanism to parsing
generic 3DS files.

## File Header

There is an initial 16-Byte header describing the file as a \[GMO\]:

       0x00   MAGIC = 0x4f 0x4d 0x47 0x2e 0x30 0x30 0x2e 0x31 0x50 0x53 0x50 0x00 0x00 0x00 0x00 
                      "OMG 00 1PSP"

After this comes the first specialised Chunk.

## Chunks

Each Chunk contains an initial local header describing the Type and Size
of the contents to come.

       0x00   SHORT   Chunk-Type
       0x02   SHORT   Size of Chunk-Header
       0x04   LONG    Size of Chunk-Data

A number of Chunk-Types have been discovered, described in detail in the
sections to follow.

### 0x0002 - File Start

This Chunk can be described as the root Chunk containing all Sub-Chunks
within.

### 0x0003 - Sub-File

These Chunks mark the exact nature of the Chunks which follow, and can
be determined by reading the last SHORT of the chunk.

They usually mark Model or Skeletal data, although there may be more
types which are currently undocumented.

Known Values:

-   0x6f6d Models
-   0x305f Skeletal Animations

### 0x0004 - Bone Info

### 0x0005 - Model Surface

### 0x0006 - Mesh

### 0x0007 - Vertex Array

### 0x0008 - Material

### 0x0009 - Texture Reference

### 0x000A - Texture

### 0x000B - Shared Vertex Data

### 0x000F - Texture Animation

### 0x8061 - Mesh Material Info

### 0x8015 - UV Scale and Bias

### 0x8066 - Mesh Index Data

### 0x8081 - Material Texture Blend

### 0x8082 - Material RGBA

### 0x8083 - Material Specularity

  [Koral]: ../../User:Koral.md "wikilink"
  [MrAdults]: http://www.richwhitehouse.com/index.php?postid=34
