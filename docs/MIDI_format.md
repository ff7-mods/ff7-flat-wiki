---
title: MIDI_format
---

[Home](index.md) > MIDI format

# Standard MIDI File (SMF) Format

The <B>Standard MIDI File</B> (SMF) is a file format used to store MIDI data (plus some other kinds of data typically needed by a sequencer.

This format stores the standard MIDI messages (ie, status bytes with appropriate data bytes) plus a time-stamp for each message (ie, a series of bytes that represent how many clock pulses to wait before "playing" the event). The format also allows saving information about tempo, time and key signatures, the names of tracks and patterns, and other information typically needed by a sequencer. One SMF can store information for numerous patterns and tracks so that any sequencer can preserve these structures when loading the file.

<B><FONT COLOR=RED>NOTE:</FONT></B> A <B>track</B> usually is analogous to one musical part, such as a Trumpet part. A <B>pattern</B> would be analogous to all of the musical parts (ie, Trumpet, Drums, Piano, etc) for one song.

The format was designed to be generic so that the most important data can be read by all sequencers. Think of a MIDI file as a musical version of an ASCII text file (except that the MIDI file contains binary data), and the various sequencer programs as text editors all capable of reading that file. But, unlike ASCII, MIDI file format saves data in <B>chunks</B> (ie, groups of bytes preceded by an ID and size) which can be parsed, loaded, skipped, etc. Therefore, SMF format is flexible enough for a particular sequencer to store its own proprietary, "extra" data in such a way that another sequencer won't be confused when loading the file and can safely ignore this extra stuff that it doesn't need. For example, maybe a sequencer wants to save a "flag byte" that indicates whether the user has turned on an audible metronome click. The sequencer can save this flag byte in such a way that another sequencer can skip this byte without having to understand what that byte is for. In the future, the SMF format can also be extended to include new "official" chunks that all sequencer programs may elect to load and use. This can be done without making old data files obsolete, nor making old sequencers no longer able to load the new files. So, the format is designed to be extensible in a backwardly compatible way.

Of course, SMF files may be used by other MIDI software than just sequencers. Since SMF files can store any and all types of MIDI messages, including System Exclusive messages, they may be used to store/load data by all kinds of MIDI software, such as a Patch Editor that wants to save some System Exclusive messages it received from a MIDI module. (The "timestamp" for each message may be irrelevant to such a Patch Editor. But it's easily ignored for programs that don't really need it).

In conclusion, any software that saves or loads MIDI data should use SMF format for its data files.

## Chunks

Data is always saved within a <B>chunk</B>. There can be many chunks inside of a MIDI file.

Each chunk can be a different size (and likely will be). A chunk's size is how many (8-bit) bytes are contained in the chunk.

The data bytes in a chunk are typically related in some way. For example, all of the bytes in one chunk may be for one particular sequencer track. The bytes for another sequencer track may be put in a different chunk. So, a chunk is simply a group of related bytes.

Each chunk must begin with a 4 character (ie, 4 ascii bytes) <B>ID</B> which tells what "type" of chunk this is.

The next 4 bytes must form a 32-bit length (ie, size) of the chunk.

<U>All chunks must begin with these two fields</U> (ie, 8 bytes), which are referred to as the <B>chunk header</B>.

Here's what a chunk's header looks like if you defined it in C: <c> struct CHUNK\_HEADER {

`  char             ID[4];`  
`  unsigned long    Length; `

}; </c> <B><FONT COLOR=RED>NOTE:</FONT></B> The <B>Length</B> does not include the 8 byte chunk header. It simply tells you how many bytes of data are in the chunk <U>following this header</U>.

And here's an example chunk header (with bytes expressed in hex) if you examined it with a hex editor:

`4D 54 68 64 00 00 00 06`

Note that the first 4 bytes make up the ascii ID of <B>MThd</B> (ie, the first four bytes are the ascii values for 'M', 'T', 'h', and 'd'). The next 4 bytes tell us that there should be 6 more data bytes in the chunk (and after that we should find the next chunk header or the end of the file).

### MThd Chunk

The MThd header has an ID of <B>MThd</B>, and a Length of <B>6</B>.

Let's examine the 6 data bytes (which follow the MThd header) in an MThd chunk.

The first two data bytes tell the <B>Format</B> (which I prefer to call "type"). There are actually 3 different types (ie, formats) of MIDI files. A type of 0 means that the file contains one single track containing midi data on possibly all 16 midi channels. If your sequencer sorts/stores all of its midi data in one single block of memory with the data in the order that it's "played", then it should read/write this type. A type of 1 means that the file contains one or more simultaneous (ie, all start from an assumed time of 0) tracks, perhaps each on a single midi channel. Together, all of these tracks are considered one sequence or pattern. If your sequencer separates its midi data (i.e. tracks) into different blocks of memory but plays them back simultaneously (ie, as one "pattern"), it will read/write this type. A type of 2 means that the file contains one or more sequentially independant single-track patterns. If your sequencer separates its midi data into different blocks of memory, but plays only one block at a time (ie, each block is considered a different "excerpt" or "song"), then it will read/write this type.

The next 2 bytes tell how many tracks are stored in the file, <B>NumTracks</B>. Of course, for format type 0, this is always 1. For the other 2 types, there can be numerous tracks.

The last two bytes indicate how many Pulses (i.e. clocks) Per Quarter Note (abbreviated as PPQN) resolution the time-stamps are based upon, <B>Division</B>. For example, if your sequencer has 96 ppqn, this field would be (in hex):

`00 60`

<B><FONT COLOR=RED>NOTE:</FONT></B> The 4 bytes that make up the <B>Length</B> are stored in (Motorola) "Big Endian" byte order, not (Intel) "Little Endian" reverse byte order. (ie, The 06 is the fourth byte instead of the first of the four).

In fact, all MIDI files begin with the above <B>MThd header</B> (and that's how you know that it's a MIDI file).

Alternately, if the first byte of Division is negative, then this represents the division of a second that the time-stamps are based upon. The first byte will be -24, -25, -29, or -30, corresponding to the 4 SMPTE standards representing frames per second. The second byte (a positive number) is the resolution within a frame (ie, subframe). Typical values may be 4 (MIDI Time Code), 8, 10, 80 (SMPTE bit resolution), or 100.

You can specify millisecond-based timing by the data bytes of -25 and 40 subframes.

Here's what an MThd chunk looks like if you defined it in C:

<c> struct MTHD\_CHUNK {

`  /* Here's the 8 byte header that all chunks must have */`  
`  char           ID[4];  /* This will be 'M','T','h','d' */`  
`  unsigned long  Length; /* This will be 6 */`

`  /* Here are the 6 bytes */`  
`  unsigned short Format;`  
`  unsigned short NumTracks;`  
`  unsigned short Division;`

}; </c>

And here's an example of a complete MThd chunk (with header) if you examined it in a hex editor:

    4D 54 68 64     MThd ID
    00 00 00 06     Length of the MThd chunk is always 6.
    00 01           The Format type is 1.
    00 02           There are 2 MTrk chunks in this file.
    E7 28           Each increment of delta-time represents a millisecond.

### MTrk Chunk

After the MThd chunk, you should find an <B>MTrk chunk</B>, as this is the only other currently defined chunk. (If you find some other chunk ID, it must be proprietary to some other program, so skip it by ignoring the following data bytes indicated by the chunk's Length).

An MTrk chunk contains all of the midi data (with timing bytes), plus optional non-midi data for <U>one track</U>. Obviously, you should encounter as many MTrk chunks in the file as the MThd chunk's NumTracks field indicated.

The MTrk header begins with the ID of <b>MTrk</B>, followed by the Length (ie, number of data bytes for this track). The Length will likely be different for each track. (After all, a track containing the violin part for a Bach concerto will likely contain more data than a track containing a simple 2 bar drum beat).

Here's what an MTrk chunk looks like if you defined it in C: <c> struct MTRK\_CHUNK {

`  /* Here's the 8 byte header that all chunks must have */`  
`  char           ID[4];   /* This will be 'M','T','r','k' */`  
`  unsigned long  Length;  /* This will be the actual size of Data[] */`

`  /* Here are the data bytes */`  
`  unsigned char  Data[];  /* Its actual size is Data[Length] */`

}; </c>

#### Variable Quantities

Think of a track in the MIDI file in the same way that you normally think of a track in a sequencer. A sequencer track contains a series of <B>events</B>. For example, the first event in the track may be to sound a middle C note. The second event may be to sound the E above middle C. These two events may both happen at the same time. The third event may be to release the middle C note. This event may happen a few musical beats after the first two events (ie, the middle C note is held down for a few musical beats). Each event has a "time" when it must occur, and the events are arranged within a "chunk" of memory in the order that they occur.

In a MIDI file, an event's "time" precedes the data bytes that make up that event itself. In other words, the bytes that make up the event's time-stamp come first. A given event's time-stamp is referenced from the previous event. For example, if the first event occurs 4 clocks after the start of play, then its "delta-time" is 04. If the next event occurs simultaneously with that first event, its time is 00. So, a delta-time is the duration (in clocks) between an event and the preceding event.

<B><FONT COLOR=RED>NOTE:</FONT></B> Since all tracks start with an assumed time of 0, the first event's delta-time is referenced from 0.

A delta-time is stored as a series of bytes which is called a <B>variable length quantity</B>. Only the first 7 bits of each byte is significant (right-justified; sort of like an ASCII byte). So, if you have a 32-bit delta-time, you have to unpack it into a series of 7-bit bytes (ie, as if you were going to transmit it over midi in a SYSEX message). Of course, you will have a variable number of bytes depending upon your delta-time. To indicate which is the last byte of the series, you leave bit \#7 clear. In all of the preceding bytes, you set bit \#7. So, if a delta-time is between 0-127, it can be represented as one byte. The largest delta-time allowed is 0FFFFFFF, which translates to 4 bytes variable length. Here are examples of delta-times as 32-bit values, and the variable length quantities that they translate to:

     NUMBER        VARIABLE QUANTITY
    00000000              00
    00000040              40
    0000007F              7F
    00000080             81 00
    00002000             C0 00
    00003FFF             FF 7F
    00004000           81 80 00
    00100000           C0 80 00
    001FFFFF           FF FF 7F
    00200000          81 80 80 00
    08000000          C0 80 80 00
    0FFFFFFF          FF FF FF 7F

Here are some C routines to read and write variable length quantities such as delta-times. With <B>WriteVarLen()</B>, you pass a 32-bit value (ie, unsigned long) and it spits out the correct series of bytes to a file. <B>ReadVarLen()</B> reads a series of bytes from a file until it reaches the last byte of a variable length quantity, and returns a 32-bit value.

<c> void WriteVarLen(register unsigned long value) {

`  register unsigned long buffer;`  
`  buffer = value & 0x7F;`

`  while ( (value >>= 7) )`  
`  {`  
`    buffer <<= 8;`  
`    buffer |= ((value & 0x7F) | 0x80);`  
`  }`

`  while (TRUE)`  
`  {`  
`     putc(buffer,outfile);`  
`     if (buffer & 0x80)`  
`         buffer >>= 8;`  
`     else`  
`         break;`  
`  }`

}

unsigned long ReadVarLen() {

`   register unsigned long value;`  
`   register unsigned char c;`

`   if ( (value = getc(infile)) & 0x80 )`  
`   {`  
`      value &= 0x7F;`  
`      do`  
`      {`  
`        value = (value << 7) + ((c = getc(infile)) & 0x7F);`  
`      } while (c & 0x80);`  
`   }`

`   return(value);`

} </c>

<B><FONT COLOR=RED>NOTE:</FONT></B> The concept of variable length quantities (ie, breaking up a large value into a series of bytes) is used with other fields in a MIDI file besides delta-times, as you'll see later.

For those not writing in C, you may benefit from a psuedo-code explanation of the above routines. In pseudo-code, ReadVarLen() is:

1.  Initialize the variable which will hold the value. Set it to 0. We'll call this variable 'result'.
2.  Read the next byte of the Variable Length quantity from the MIDI file.
3.  Shift all of the bits in 'result' 7 places to the left. (ie, Multiply 'result' by 128).
4.  Logically OR 'result' with the byte that was read in, but first mask off bit \#7 of the byte. (ie, AND the byte with hexadecimal 7F before you OR with 'result'. But make sure you save the original value of the byte for the test in the next step).
5.  Test if bit \#7 of the byte is set. (ie, Is the byte AND hexadecimal 80 equal to hexadecimal 80)? If so, loop back to step \#2. Otherwise, you're done, and 'result' now has the appropriate value.

In pseudo code, WriteVarLen() could be:

1.  Assume that you have a variable named 'result' which contains the value to write out as a Variable Length Quantity.
2.  Declare an array which can contain 4 numbers. We'll call this variable 'array'. Initialize a variable named 'count' to 0.
3.  Is 'result' less than 128? If so, skip to step \#8.
4.  Take the value 'result' AND with hexadecimal 7F, and OR with hexadecimal 80, and store it in 'count' element of 'array'. (ie, The first time through the loop, this gets stored in the first element of 'array'). NOTE: Don't alter the value of 'result' itself.
5.  Increment 'count' by 1.
6.  Shift all bits in 'result' 7 places to the right. (This can be done by dividing by 128).
7.  Loop back to step \#3.
8.  Take the value 'result' AND with hexadecimal 7F, and store it in 'count' element of 'array'.
9.  Increment 'count' by 1.
10. Write out the values stored in 'array'. Start with the last element stored above, and finish with the first element stored. (ie, Write them out in reverse order so that the first element of 'array' gets written to the MIDI file last). NOTE: The variable 'count' tells you how many total bytes to write. It also can be used as an index into the array (if you subtract one from it, and keep writing out bytes until it is -1).

#### Events in an MTrk

An MTrk can contain [MIDI events](http://www.borg.com/~jglatt/tech/midispec.htm) and non-MIDI events (ie, events that contain data such as tempo settings, track names, etc).

The first (1 to 4) byte(s) in an MTrk will be the first event's delta-time as a variable length quantity. The next data byte is actually the first byte of that event itself. I'll refer to this as the event's <B>Status</B>. For [MIDI events](http://www.borg.com/~jglatt/tech/midispec.htm), this will be the actual MIDI Status byte (or the first midi data byte if running status). For example, if the byte is hex 90, then this event is a <B>Note-On</B> upon midi channel 0. If for example, the byte was hex 23, you'd have to recall the previous event's status (ie, midi running status). Obviously, the first MIDI event in the MTrk <U>must</U> have a status byte. After a midi status byte comes its 1 or 2 data bytes (depending upon the status - some MIDI messages only have 1 subsequent data byte). After that you'll find the next event's delta time (as a variable quantity), etc.

------------------------------------------------------------------------

<CENTER>

<FONT COLOR=RED><B>SYSEX events</B></FONT>

</CENTER>

SYSEX (system exclusive) events (status = F0) are a special case because a SYSEX event can be any length. After the F0 status (which is always stored -- no running status here), you'll find yet another series of variable length bytes. Combine them with ReadVarLen() and you'll come up with a 32-bit value that tells you how many more bytes follow which make up this SYSEX event. This length doesn't include the F0 status.

For example, consider the following SYSEX MIDI message:

`F0 7F 7F 04 01 7F 7F F7`

This would be stored in a MIDI file as the following series of bytes (minus the delta-time bytes which would precede it):

`F0 07 7F 7F 04 01 7F 7F F7`

The 07 above is the variable length quantity (which happens to fit in just one byte for this example). It indicates that there are seven, following bytes that comprise this SYSEX message.

Really oddball midi units send a system exclusive message as a series of small "packets" (with a time delay inbetween transmission of each packet). The first packet begins with an F0, but it doesn't end with an F7. The subsequent packets don't start with an F0 nor end with F7. The last packet doesn't start with an F0, but does end with the F7. So, between the first packet's opening F0 and the last packet's closing F7, there's 1 SYSEX message there. (Note: only extremely poor designs, such as the crap marketed by Casio exhibit such horrid behavior). Of course, since a delay is needed inbetween each packet, you need to store each packet as a separate event with its own time in the MTrk. Also, you need some way of knowing which events shouldn't begin with an F0 (ie, all of them except the first packet). So, the MIDI file redefines a midi status of F7 (normally used as an end mark for SYSEX packets) as a way to indicate an event that doesn't begin with F0. If such an event follows an F0 event, then it's assumed that the F7 event is the second "packet" of a series. In this context, it's referred to as a SYSEX CONTINUATION event. Just like the F0 type of event, it has a variable length followed by data bytes. On the other hand, the F7 event could be used to store MIDI REALTIME or MIDI COMMON messages. In this case, after the variable length bytes, you should expect to find a MIDI Status byte of F1, F2, F3, F6, F8, FA, FB, FC, or FE. (Note that you wouldn't find any such bytes inside of a SYSEX CONTINUATION event). When used in this manner, the F7 event is referred to as an ESCAPED event.

------------------------------------------------------------------------

<CENTER>

<FONT COLOR=RED><B>Non-MIDI events</B></FONT>

</CENTER>

A status of FF is reserved to indicate a special non-MIDI event. (Note that FF is used in MIDI to mean "reset", so it wouldn't be all that useful to store in a data file. Therefore, the MIDI file arbitrarily redefines the use of this status). After the FF status byte is another byte that tells you what <B>Type</B> of non-MIDI event it is. It's sort of like a second status byte. Then after this byte is another byte(s -- a variable length quantity again) that tells how many more data bytes follow in this event (ie, its Length). This Length doesn't include the FF, Type byte, nor the Length byte. These special, non-MIDI events are called <B>Meta-Events</B>, and most are optional unless otherwise noted. The section of this online book entitled "Meta-Events" lists the currently defined Meta-Events. Note that unless otherwise mentioned, more than one of these events can be placed in an MTrk (even the same Meta-Event) at any delta-time. (Just like all midi events, Meta-Events have a delta-time from the previous event regardless of what type of event that may be. So, you can freely intermix MIDI and Meta events).

#### Meta-Events in an MTrk

------------------------------------------------------------------------

##### Sequence Number

`FF 00 02 `<I><FONT COLOR=RED><B>`ss ss`</B></FONT></I>

or...

`FF 00 00`

This optional event must occur at the beginning of a MTrk (ie, before any non-zero delta-times and before any midi events). It specifies the sequence number. The two data bytes <I><FONT COLOR=RED><B>ss ss</B></FONT></I>, are that number which corresponds to the <B>MIDI Cue</B> message. In a format 2 MIDI file, this number identifies each "pattern" (ie, Mtrk) so that a "song" sequence can use the MIDI Cue message to refer to patterns.

If the <I><FONT COLOR=RED><B>ss ss</B></FONT></I> numbers are omitted (ie, the second form shown above), then the MTrk's location in the file is used. (ie, The first MTrk chunk is sequence number 0. The second MTrk is sequence number 1. Etc).

In format 0 or 1, which contain only one "pattern" (even though format 1 contains several MTrks), this event is placed in only the first MTrk. So, a group of format 0 or 1 files with different sequence numbers can comprise a "song collection".

There can be only one of these events per MTrk chunk in a Format 2. There can be only one of these events in a Format 0 or 1, and it must be in the first MTrk.

------------------------------------------------------------------------

##### Text

`FF 01 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

Any amount of text (amount of bytes = <I><FONT COLOR=GREEN><B>len</B></FONT></I>) for any purpose. It's best to put this event at the beginning of an MTrk. Although this text could be used for any purpose, there are other text-based Meta-Events for such things as orchestration, lyrics, track name, etc. This event is primarily used to add "comments" to a MIDI file which a program would be expected to ignore when loading that file.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Copyright

`FF 02 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

A copyright message. It's best to put this event at the beginning of an MTrk.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Sequence/Track Name

`FF 03 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The name of the sequence or track. It's best to put this event at the beginning of an MTrk.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Instrument

`FF 04 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The name of the instrument (ie, MIDI module) being used to play the track. This may be different than the Sequence/Track Name. For example, maybe the name of your sequence (ie, Mtrk) is "Butterfly", but since the track is played upon a Roland S-770, you may also include an Instrument Name of "Roland S-770".

It's best to put one (or more) of this event at the beginning of an MTrk to provide the user with identification of what instrument(s) is playing the track. Usually, the instruments (ie, patches, tones, banks, etc) are setup on the audio devices via <B>MIDI Program Change</B> and <B>MIDI Bank Select Controller</B> events within the MTrk. So, this event exists merely to provide the user with visual feedback of what instruments are used for a track.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Lyric

`FF 05 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

A song lyric which occurs on a given beat. A single Lyric MetaEvent should contain only one syllable.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Marker

`FF 06 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The text for a marker which occurs on a given beat. Marker events might be used to denote a loop start and loop end (ie, where the sequence loops back to a previous event).

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Cue Point

`FF 07 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The text for a cue point which occurs on a given beat. A Cue Point might be used to denote where a WAVE (ie, sampled sound) file starts playing, for example, where the <I><FONT COLOR=RED><B>text</B></FONT></I> would be the WAVE's filename.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Program (Patch) Name

`FF 08 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The name of the program (ie, patch) used to play the MTrk. This may be different than the Sequence/Track Name. For example, maybe the name of your sequence (ie, Mtrk) is "Butterfly", but since the track is played upon an electric piano patch, you may also include a Program Name of "ELECTRIC PIANO".

Usually, the instruments (ie, patches, tones, banks, etc) are setup on the audio devices via <B>MIDI Program Change</B> and <B>MIDI Bank Select Controller</B> events within the MTrk. So, this event exists merely to provide the user with visual feedback of what particular patch is used for a track. But it can also give a hint to intelligent software if patch remapping needs to be done. For example, if the MIDI file was created on a non-General MIDI instrument, then the <B>MIDI Program Change</B> event will likely contain the wrong value when played on a General MIDI instrument. Intelligent software can use the Program Name event to look up the correct value for the <B>MIDI Program Change</B> event.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### Device (Port) Name

`FF 09 `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`text`</B></FONT></I>

The name of the MIDI device (port) where the track is routed. This replaces the "MIDI Port" Meta-Event which some sequencers formally used to route MIDI tracks to various MIDI ports (in order to support more than 16 MIDI channels).

For example, assume that you have a MIDI interface that has 4 MIDI output ports. They are listed as "MIDI Out 1", "MIDI Out 2", "MIDI Out 3", and "MIDI Out 4". If you wished a particular MTrk to use "MIDI Out 1" then you would put a Port Name Meta-event at the beginning of the MTrk, with "MIDI Out 1" as the <I><FONT COLOR=RED><B>text</B></FONT></I>.

All MIDI events that occur in the MTrk, after a given Port Name event, will be routed to that port.

In a format 0 MIDI file, it would be permissible to have numerous Port Name events intermixed with MIDI events, so that the one MTrk could address numerous ports. But that would likely make the MIDI file much larger than it need be. The Port Name event is useful primarily in format 1 MIDI files, where each MTrk gets routed to one particular port.

Note that <B>len</B> could be a series of bytes since it is expressed as a variable length quantity.

------------------------------------------------------------------------

##### End of Track

`FF 2F 00`

This event is <u>not</u> optional. It must be the last event in every MTrk. It's used as a definitive marking of the end of an MTrk. Only 1 per MTrk.

------------------------------------------------------------------------

##### Tempo

`FF 51 03 `<I><FONT COLOR=RED><B>`tt tt tt`</B></FONT></I>

Indicates a tempo change. The 3 data bytes of <B>tt tt tt</B> are the tempo in microseconds per quarter note. In other words, the microsecond tempo value tells you how long each one of your sequencer's "quarter notes" should be. For example, if you have the 3 bytes of 07 A1 20, then each quarter note should be 0x07A120 (or 500,000) microseconds long.

So, the MIDI file format expresses tempo as "the amount of time (ie, microseconds) per quarter note".

<B><FONT COLOR=RED>NOTE:</FONT></B> If there are no tempo events in a MIDI file, then the tempo is assumed to be 120 BPM

In a format 0 file, the tempo changes are scattered throughout the one MTrk. In format 1, the very first MTrk should consist of only the tempo (and time signature) events so that it could be read by some device capable of generating a "tempo map". It is best not to place MIDI events in this MTrk. In format 2, each MTrk should begin with at least one initial tempo (and time signature) event.

------------------------------------------------------------------------

##### SMPTE Offset

`FF 54 05 `<I><FONT COLOR=RED><B>`hr mn se fr ff`</B></FONT></I>

Designates the SMPTE start time (hours, minutes, seconds, frames, subframes) of the MTrk. It should be at the start of the MTrk. The hour should not be encoded with the SMPTE format as it is in <B>MIDI Time Code</B>. In a format 1 file, the SMPTE OFFSET must be stored with the tempo map (ie, the first MTrk), and has no meaning in any other MTrk. The <FONT COLOR=RED><B>ff</B></FONT> field contains fractional frames in 100ths of a frame, even in SMPTE based MTrks which specify a different frame subdivision for delta-times (ie, different from the subframe setting in the MThd).

------------------------------------------------------------------------

##### Time Signature

`FF 58 04 `<I><FONT COLOR=RED><B>`nn dd cc bb`</B></FONT></I>

Time signature is expressed as 4 numbers. <I><FONT COLOR=RED><B>nn</B></FONT></I> and <I><FONT COLOR=RED><B>dd</B></FONT></I> represent the "numerator" and "denominator" of the signature as notated on sheet music. The denominator is a negative power of 2: 2 = quarter note, 3 = eighth, etc.

The <I><FONT COLOR=RED><B>cc</B></FONT></I> expresses the number of MIDI clocks in a metronome click.

The <I><FONT COLOR=RED><B>bb</B></FONT></I> parameter expresses the number of notated 32nd notes in a MIDI quarter note (24 MIDI clocks). This event allows a program to relate what MIDI thinks of as a quarter, to something entirely different.

For example, 6/8 time with a metronome click every 3 eighth notes and 24 clocks per quarter note would be the following event:

`FF 58 04 06 03 18 08`

<B><FONT COLOR=RED>NOTE:</FONT></B> If there are no time signature events in a MIDI file, then the time signature is assumed to be 4/4.

In a format 0 file, the time signatures changes are scattered throughout the one MTrk. In format 1, the very first MTrk should consist of only the time signature (and tempo) events so that it could be read by some device capable of generating a "tempo map". It is best not to place MIDI events in this MTrk. In format 2, each MTrk should begin with at least one initial time signature (and tempo) event.

------------------------------------------------------------------------

##### Key Signature

`FF 59 02 `<I><FONT COLOR=RED><B>`sf mi`</B></FONT></I>

<I><FONT COLOR=RED><B>sf</B></FONT></I> = -7 for 7 flats, -1 for 1 flat, etc, 0 for key of c, 1 for 1 sharp, etc.

<I><FONT COLOR=RED><B>mi</B></FONT></I> = 0 for major, 1 for minor

------------------------------------------------------------------------

##### Proprietary Event

`FF 7F `<I><FONT COLOR=GREEN><B>`len`</B></FONT></I>` `<I><FONT COLOR=RED><B>`data`</B></FONT></I>

This can be used by a program to store proprietary data. The first byte(s) should be a unique ID of some sort so that a program can identity whether the event belongs to it, or to some other program. A 4 character (ie, ascii) ID is recommended for such.

Note that <I><FONT COLOR=GREEN><B>len</B></FONT></I> could be a series of bytes since it is expressed as a variable length quantity.
