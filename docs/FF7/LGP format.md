---
title: LGP format
---

[Home](../Main%20Page.md) > [FF7](../FF7.md) > LGP format

### LGP Archive format for PC by [Ficedula][]

This section explains how the LGP archives from FF7 PC are constructed.
If you're looking for a tool that already manages LGP archives, try
[Ficedula][]'s [LGP Editor][].

Essentially the LGP file is split up into four (maybe less, depending on
how you count it) sections.

1.  File header/Table of contents
2.  CRC code
3.  Actual data
4.  File terminator

#### Section 1: File Header

This contains two parts: A header of fixed size, then the table of
contents.

The first item is 12 bytes containing the file creator. This is a
standard string, except it is "rightaligned". In other words the blank
space comes before the actual text, not after. In FF7 it's always
"SQUARESOFT" preceded by two nulls to make it 12 bytes. The only other
thing you might see is the header "FICEDULA-LGP", which I use to
indicate a file is an LGP \*patch\* one of my programs has constructed,
not a complete archive.

Next is a four-byte integer saying how many files the archive contains.

Following this is the table of contents (TOC): One entry per file.

Each entry in the TOC has the following structure:

<table>
<thead>
<tr class="header">
<th><p>Offset</p></th>
<th><p>Length</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>20 bytes</p></td>
<td><p>Null terminated string, giving filename</p></td>
</tr>
<tr class="even">
<td><p>4 byte integer</p></td>
<td><p>Position in this file where data starts for the file</p></td>
</tr>
<tr class="odd">
<td><p>1 byte</p></td>
<td><p>Some sort of check code. File attributes? Normally seems to be<br />
14 but it does vary.</p></td>
</tr>
<tr class="even">
<td><p>2 byte short</p></td>
<td><p>Something to do with duplicate file names. If a name is unique it is 0, otherwise it is assigned a value based on existing duplicates. (Hard to explain)</p></td>
</tr>
</tbody>
</table>

#### Section 2: CRC Code

This code is used to validate the LGP archive. The bad news is I have no
idea how to make it (I've figured out how to decode it, ie. find out
whether the archive is valid, but I can't create my own). The good news
is you don't need to! The only thing this CRC is based on is the number
of files in the archive (maybe the filenames too, haven't checked that).
Anyway, the TOC is the only thing this check relates to. So if you're
replicating an archive from FF7 for use in the game with the same number
of files and filenames you can just copy the CRC section from an
existing file.

Normally it's 3602 bytes long (one archive may be different, possibly
MAGIC.LGP). Anyway, one normally-safe way of calculating the CRC size is
to find the end of the TOC and the beginning of the first file. Anything
in between is probably CRC code (this is not guaranteed to work. It
works with "official" archives but editors - such as [LGP Editor][1] -
can alter the TOC to achieve extra things).

#### Section 3: Actual Data

The data from the files. However it's not that simple: the TOC doesn't
list how long each file is (somewhat useful). It's done here. The offset
in the TOC is actually the position of yet another file header. Format
is:

|   Size   | Description                             |
|:--------:|-----------------------------------------|
| 20 bytes | Null terminated string, giving filename |
| 4 bytes  | File length                             |
|  Varies  | The file data itself                    |

#### Section 4: Terminator

After the last piece of data comes the file descriptor. This is a simple
string, except instead of being null-terminated it's terminated by the
end of the file. It's "FINAL FANTASY 7" for all archives, except LGP
patches, where it's "LGP PATCH FILE".

#### Notes

The game is remarkably flexible about LGP archives. So long as the TOC
and the CRC data is intact it'll accept just about anything.

-   Example 1: The filename in the TOC and in the actual file header
    don't have to match. It only checks the TOC.
-   Example 2: You can point two entries in the TOC at the same data and
    it works.
-   Example 3: You can have ANY junk in the data section so long as all
    the TOC entries point to a valid file header. Not every piece of
    data has to be "accounted" for by the TOC. There can be data not
    used.

[LGP Editor][1] uses this to its advantage in the Advanced Editor. If
you want to replace a file in an LGP archive with your own copy, it just
puts the file on the end of the LGP, writes a new file terminator, and
updates the TOC to point at the new file. It even lets you link two TOC
entries to the same data or have "inactive" files in the archive that
aren't referenced by any TOC entry.

I don't know whether the file terminator has to be intact, but for
safety's sake my editor preserves it. The CRC must be present and
correct. Also, if you're replacing an archive with you're own custom
version make sure it has filenames in the TOC matching the ones in the
old one.

The game doesn't check archive sizes as long as all filenames are
present. So if you want, you could replace an archive containing 95
files with a 98-file archive, so long as 95 of those 98 names matched
those present in the original 95-file archive. (However there's no point
in doing this when the game won't use any files other than the 95 it's
expecting to find).

There are reports on [Qhimm's board][] that once you've altered an
archive and the game refuses to read it, it won't ever read it until you
reinstall - even if you fix the problem/restore from a backup. The idea
was generally scorned and ignored, but I'll mention it because something
like that happened to me. No solid conclusion can be drawn here.

Sometimes, there are data "gaps" in the file that don't appear to be
referenced by any file - even by an inactive file. If you're only using
the TOC method to get at files (the easy way) then you won't notice this
anyway. However, if you're stepping through the file header by header,
even reading the unused ones, this can cause problems. If you use my
program to update a file with one that's smaller than the original (can
happen) then it writes it in, but leaves a gap after it (of course).
However, to help you out, after the end of the file, it writes a 4 byte
integer saying how much more space to skip over to reach the next file
header. This really doesn't affect many things - only tools (like my
Advanced LGP Editor) that bypass the TOC to construct their own file
lists. FF7 never notices a thing.

### Useful downloads

Below there are links to known programs that are capable to edit LGP
archives:

-   [LGP Tools][] - with an Advanced LGP Editor allowing edit archive
    thoughoutly
-   [Emerald][] - has mass extracting/repacking function
-   [Unmass][] - general file extractor with LGP archives support

  [Ficedula]: ../User:Ficedula.md "wikilink"
  [LGP Editor]: http://sylphds.net/f2k3/index.html
  [1]: http://www.ficedula.com/
  [Qhimm's board]: http://forums.qhimm.com/
  [LGP Tools]: http://www.sylphds.net/f2k3/programs/lgptools/lgptools160.zip
  [Emerald]: http://elentor.com/Projetos/FF7-Tools/Extracting/Emerald.zip
  [Unmass]: http://mirex.mypage.sk/index.php?selected=1#Unmass
