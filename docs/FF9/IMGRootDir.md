---
title: IMGRootDir
---

# Root Directory

The first sector of FF9.IMG contains a root directory of information with sector locations for subdirectories and the sector of the first file in that subdirectory.

note: [sector](glossary/sector) hereon refers to a 2048 byte chunk of the file keep this in mind when 'deciphering' information.

## Root Directory Header

The root directory begins with the following header format

| Name | Units/Size | Description |
|:--:|:--:|:---|
| Signature | char\[4\] | 'FF9'\0 (signature to indicate it's an FF9 data file likely) |
| unknown | DWORD | No information available at this time |
| Directory Count | DWORD | This contains the number of directories in the FF9.IMG file. |
| unknown | DWORD | No information available at this time |
|  |  |  |

## Root Directory Entries

Following the Root Directory header are the entries for the subdirectories.

| Name | Units/Size | Description |
|:--:|:--:|:---|
| Type | DWORD | The type of subdirectory this is |
| File Count | DWORD | This gives the number of files within the subdirectory. |
| Directory Information Sector | DWORD | Sector that contains the directory information (IE file sector list). |
| First File Sector | DWORD | This points to the sector of the first file (for fast reference?) |
|  |  |  |

Directory Types

| Number | Description                                                  |
|:------:|:-------------------------------------------------------------|
|  0x02  | Normal subdirectory contains normal files.                   |
|  0x03  | Heirarchical directory.                                      |
|  0x04  | Not a directory but indicates the end of the directory list. |
|        |                                                              |
