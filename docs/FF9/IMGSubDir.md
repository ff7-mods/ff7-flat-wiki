---
title: IMGSubDir
---

[Home](../Main%20Page.md.md) > [FF9](../FF9.md) > IMGSubDir

# Sub Directory Information

The sub directories consist of a file list structure and then actual
file data.

## Sub Directory: File List Structure

The infomation is formated as 2 WORDS + 1 DWORD \* the file count from
the root directory. With as many as 300 + files this accounts for 1 to 2
sectors for a subdirectory section. The first sector information may be
considered the END sector of the directory information, it is likely
this is how it is used by the game kernel.

|      Name       | Type  | Description                           |
|:---------------:|:-----:|:--------------------------------------|
| File Identifier | WORD  | File ID for loading.                  |
|     Unknown     | WORD  | Possibly File Type.                   |
|  First Sector   | DWORD | This is the first sector of the file. |
|                 |       |                                       |

## File Size information

This is determined expostfacto. It is not included with the file list.
First you load the file directory structure (1 + sectors). The next step
is to find the file you wish to know the size of (IE 0 to FileCount-1 in
the file structure array). Take the first sector of the next file in the
array (only if it's not the last file) and subtract the first sector of
the file you wish the size of, the result is the number of sectors the
file ocupies within the image. The last file is a bit different you need
the sector of the next sub directory file list and subtract from that
the first sector of the file you wish the size of.

## Source Code

    typedef struct
    {
       unsigned int Flags;
       unsigned int FirstSector;
    }
    FF9_SubDirectoryFileInfo;

    unsigned int FileSize(void *FileData, int FileN, int FileCount)
    {
       if(FileN < (FileCount-1))
       {
          
       }
    }
