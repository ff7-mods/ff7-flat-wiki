---
title: FileFormat_FMT
---

Final Fantasy 8's sound effects are stored within two files. The **audio.dat** contains the actual wav files, compressed as 4-bit ADPCM. The **audio.fmt** file is a locator for sounds in the dat.

## FMT File Structure

The FMT is headed by 4 bytes representing the number of sound file headers in the rest of the FMT file, then by a 36 byte header that isn't interesting.

Each sound header (beginning with the first at 0x28) either contains 70 bytes if it represents a valid sound file, or 38 bytes if it's a blank entry (those 38 bytes are all 0x0)

Each sound header representing a valid sound file contains the following structure:

| Offset | Size     | Data                                                                                            |
|--------|----------|-------------------------------------------------------------------------------------------------|
| 0x00   | 4 bytes  | Size of wav file in the dat.                                                                    |
| 0x04   | 4 bytes  | Offset of wav file in the dat.                                                                  |
| 0x08   | 12 bytes | Unknown. If first byte is 0, the other 11 are always 0. Probably some kind of looping metadata. |
| 0x14   | 18 bytes | Microsoft WAVFORMATEX header for the wav file.                                                  |
| 0x26   | 2 bytes  | Samples per block                                                                               |
| 0x28   | 2 bytes  | Number of ADPCM coefficients (used for compression, should always be 7).                        |
| 0x2A   | 28 bytes | Standard Microsoft ADPCMCoefSets.                                                               |
|        |          |                                                                                                 |
