---
title: LGP_format
---

### LGP Archive format for PC by [Ficedula](../User:Ficedula)

This section explains how the LGP archives from FF7 PC are constructed. If you're looking for a tool that already manages LGP archives, try [Ficedula](../User:Ficedula)'s [LGP Editor](http://sylphds.net/f2k3/index.html).

Essentially the LGP file is split up into four (maybe less, depending on how you count it) sections.

1.  File header/Table of contents
2.  CRC code
3.  Actual data
4.  File terminator

#### Section 1: File Header

This contains two parts: A header of fixed size, then the table of contents.

The first item is 12 bytes containing the file creator. This is a standard string, except it is "rightaligned". In other words the blank space comes before the actual text, not after. In FF7 it's always "SQUARESOFT" preceded by two nulls to make it 12 bytes. The only other thing you might see is the header "FICEDULA-LGP", which I use to indicate a file is an LGP \*patch\* one of my programs has constructed, not a complete archive.

Next is a four-byte integer saying how many files the archive contains.

Following this is the table of contents (TOC): One entry per file.

Each entry in the TOC has the following structure:

<table>
<thead>
<tr>
<th><p>Offset</p></th>
<th><p>Length</p></th>
</tr>
</thead>
<tbody>
<tr>
<td><p>20 bytes</p></td>
<td><p>Null terminated string, giving filename</p></td>
</tr>
<tr>
<td><p>4 byte integer</p></td>
<td><p>Position in this file where data starts for the file</p></td>
</tr>
<tr>
<td><p>1 byte</p></td>
<td style="background: rgb(255,255,204)"><p>Some sort of check code. File attributes? Normally seems to be<br />
14 but it does vary.</p></td>
</tr>
<tr>
<td><p>2 byte short</p></td>
<td style="background: rgb(255,255,204)"><p>Something to do with duplicate file names. If a name is unique it is 0, otherwise it is assigned a value based on existing duplicates. (Hard to explain)</p></td>
</tr>
</tbody>
</table>

#### Section 2: Section formerly designated as "CRC Code"

This section is 3600 bytes. It is 30 sets of 30 entries containing two 16-bit words each (30 x 30 x 2 x 2 = 3600)

The sets contain file-group information which is based on the first two letters of each file name.

The first letter, minus the value for ascii 'a' (0x61) is the index of the set to which the file belongs.

The second letter, minus the value for ascii ' ' ' (0x60) is the index of the entry within the set. Since the second letter in all of the file names is ascii 'a' or greater, it means that the lowest entry index is 1, so the first entry (at index 0) in every group is always zero (0x0000).

Each entry is two words.

The first word is the 1-based index of the directory entry for the first file in the set.

The second word is the number of files in the set, most of which are 0x003c (60). There are a few entries after the bulk which have fewer entries.

The meaning of these sets and why they're divided in this manner is yet to be determined.

There is one 16-bit word with the value of 0 (0x0000) at the end of this data which may belong to this section or the next.

#### Section 3: Actual Data

The data from the files. However it's not that simple: the TOC doesn't list how long each file is (somewhat useful). It's done here. The offset in the TOC is actually the position of yet another file header. Format is:

|   Size   | Description                             |
|:--------:|-----------------------------------------|
| 20 bytes | Null terminated string, giving filename |
| 4 bytes  | File length                             |
|  Varies  | The file data itself                    |

#### Section 4: Terminator

After the last piece of data comes the file descriptor. This is a simple string, except instead of being null-terminated it's terminated by the end of the file. It's "FINAL FANTASY 7" for all archives, except LGP patches, where it's "LGP PATCH FILE".

#### Notes

The game is remarkably flexible about LGP archives. So long as the TOC and the CRC data is intact it'll accept just about anything.

- Example 1: The filename in the TOC and in the actual file header don't have to match. It only checks the TOC.
- Example 2: You can point two entries in the TOC at the same data and it works.
- Example 3: You can have ANY junk in the data section so long as all the TOC entries point to a valid file header. Not every piece of data has to be "accounted" for by the TOC. There can be data not used.

[LGP Editor](http://www.ficedula.com/) uses this to its advantage in the Advanced Editor. If you want to replace a file in an LGP archive with your own copy, it just puts the file on the end of the LGP, writes a new file terminator, and updates the TOC to point at the new file. It even lets you link two TOC entries to the same data or have "inactive" files in the archive that aren't referenced by any TOC entry.

I don't know whether the file terminator has to be intact, but for safety's sake my editor preserves it. The CRC must be present and correct. Also, if you're replacing an archive with you're own custom version make sure it has filenames in the TOC matching the ones in the old one.

The game doesn't check archive sizes as long as all filenames are present. So if you want, you could replace an archive containing 95 files with a 98-file archive, so long as 95 of those 98 names matched those present in the original 95-file archive. (However there's no point in doing this when the game won't use any files other than the 95 it's expecting to find).

There are reports on [Qhimm's board](http://forums.qhimm.com/) that once you've altered an archive and the game refuses to read it, it won't ever read it until you reinstall - even if you fix the problem/restore from a backup. The idea was generally scorned and ignored, but I'll mention it because something like that happened to me. No solid conclusion can be drawn here.

Sometimes, there are data "gaps" in the file that don't appear to be referenced by any file - even by an inactive file. If you're only using the TOC method to get at files (the easy way) then you won't notice this anyway. However, if you're stepping through the file header by header, even reading the unused ones, this can cause problems. If you use my program to update a file with one that's smaller than the original (can happen) then it writes it in, but leaves a gap after it (of course). However, to help you out, after the end of the file, it writes a 4 byte integer saying how much more space to skip over to reach the next file header. This really doesn't affect many things - only tools (like my Advanced LGP Editor) that bypass the TOC to construct their own file lists. FF7 never notices a thing.

### Useful downloads

Below there are links to known programs that are capable to edit LGP archives:

- [LGP Tools](http://www.sylphds.net/f2k3/programs/lgptools/lgptools160.zip) - with an Advanced LGP Editor allowing edit archive thoughoutly
- [Emerald](http://elentor.com/Projetos/FF7-Tools/Extracting/Emerald.zip) - has mass extracting/repacking function
- [Unmass](http://mirex.mypage.sk/index.php?selected=1#Unmass) - general file extractor with LGP archives support
