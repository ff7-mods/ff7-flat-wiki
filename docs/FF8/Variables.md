---
title: Variables
---

By [Shard](../User:Shard.md).

Game variables can be accessed using the PSHM family of script functions, and can be written to by using the POPM family of functions. Which one you use depends on the size of the variable. The variables are all stored in save files, with the save block starting at address 0xD10 on uncompressed PC saves. The parameter to access a variable in the game scripts is basically the offset from this point in the variable block. For example, getting main story progress (word 256, which is word 0x100 in hex) just gets the two bytes starting at address 0xD10 + 0x100 = 0xE10. The varmap is continuous in memory while the game is running as well. In the en-US version of the original and SE releases (and likely most other versions), the varblock begins at 0x18fe9b8. You can use this [Cheat Engine Table](https://www.mediafire.com/?ucolf65ewq1yoty) to track them as you play.

Items in grey are unused by field scripts (some of them may be used in battle scripts).

| Var type    | Var Number  | Description                                                                                                                                                             |
|-------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Byte        | 0-3         | unused in fields (always "FF-8")                                                                                                                                        |
| Long        | 4           | Steps (used to generate random encounters)                                                                                                                              |
| Long        | 8           | Payslip                                                                                                                                                                 |
| Byte        | 12-15       | unused in fields                                                                                                                                                        |
| Signed Word | 16          | SeeD rank points?                                                                                                                                                       |
| Byte        | 18-19       | unused in fields                                                                                                                                                        |
| Long        | 20          | Battles won. (Fun fact: this affects the basketball shot in Trabia.)                                                                                                    |
| Byte        | 24-25       | unused in fields                                                                                                                                                        |
| Word        | 26          | Battles escaped.                                                                                                                                                        |
| Word        | 28          | Enemies killed by Squall                                                                                                                                                |
| Word        | 30          | Enemies killed by Zell                                                                                                                                                  |
| Word        | 32          | Enemies killed by Irvine                                                                                                                                                |
| Word        | 34          | Enemies killed by Quistis                                                                                                                                               |
| Word        | 36          | Enemies killed by Rinoa                                                                                                                                                 |
| Word        | 38          | Enemies killed by Selphie                                                                                                                                               |
| Word        | 40          | Enemies killed by Seifer                                                                                                                                                |
| Word        | 42          | Enemies killed by Edea                                                                                                                                                  |
| Word        | 44          | Squall death count                                                                                                                                                      |
| Word        | 46          | Zell death count                                                                                                                                                        |
| Word        | 48          | Irvine death count                                                                                                                                                      |
| Word        | 50          | Quistis death count                                                                                                                                                     |
| Word        | 52          | Rinoa death count                                                                                                                                                       |
| Word        | 54          | Selphie death count                                                                                                                                                     |
| Word        | 56          | Seifer death count                                                                                                                                                      |
| Word        | 58          | Edea death count                                                                                                                                                        |
| Byte        | 60-67       | unused in fields                                                                                                                                                        |
| Long        | 68          | Enemies killed                                                                                                                                                          |
| Long        | 72          | Amount of Gil the party currently has                                                                                                                                   |
| Long        | 76          | Amount of Gil Laguna's party has                                                                                                                                        |
| Long        | 80          | Counts the number of frames since the current movie started playing.                                                                                                    |
| Word        | 84          | Last area visited.                                                                                                                                                      |
| Signed Byte | 86          | Current car rent.                                                                                                                                                       |
| Signed Byte | 87          | Built-in engine variable. No idea what it does. Scripts always check if it's equal to 0 or 10. Related to music.                                                        |
| Signed Byte | 88          | Built-in engine variable. Used exclusively on save points. Never written to with field scripts. Related to Siren's Move-Find ability.                                   |
| Byte        | 89-103      | unused in fields                                                                                                                                                        |
| Long        | 104         | Seems related to SARALYDISPON/SARALYON/MUSICLOAD/PHSPOWER opcodes                                                                                                       |
| Long        | 108         | Music related                                                                                                                                                           |
| Long        | 112         | unused in fields                                                                                                                                                        |
| Byte        | 116-147     | Draw points in field                                                                                                                                                    |
| Byte        | 148-179     | Draw points in worldmap                                                                                                                                                 |
| Byte        | 180-255     | unused in fields                                                                                                                                                        |
| Word        | 256         | Main Story quest progress.                                                                                                                                              |
| Byte        | 258         | not investigated                                                                                                                                                        |
| Byte        | 259-260     | unused in fields                                                                                                                                                        |
| Byte        | 261         | not investigated                                                                                                                                                        |
| Byte        | 262-263     | unused in fields                                                                                                                                                        |
| Byte        | 264         | not investigated                                                                                                                                                        |
| Byte        | 265         | not investigated                                                                                                                                                        |
| Byte        | 266         | World map version? (3=Esthar locations unlocked)                                                                                                                        |
| Byte        | 267         | unused in fields                                                                                                                                                        |
| Byte        | 268         | not investigated                                                                                                                                                        |
| Byte        | 269         | not investigated                                                                                                                                                        |
| Byte        | 270         | not investigated                                                                                                                                                        |
| Byte        | 271         | unused in fields                                                                                                                                                        |
| Byte        | 272-299     | SO MANY F\*\*\*ING CARD GAME VARIABLES                                                                                                                                  |
| Byte        | 300         | Card Queen re-cards.                                                                                                                                                    |
| Byte        | 301-303     | unused in fields                                                                                                                                                        |
| Byte        | 304-305     | Timber Maniacs issues found.                                                                                                                                            |
| Byte        | 306-319     | Reserved for Hacktuar / FF8Voice                                                                                                                                        |
| Byte        | 320-332     | Ultimecia Gallery related (pictures viewed?)                                                                                                                            |
| Byte        | 333         | Ultimecia Armory chest flags                                                                                                                                            |
| Byte        | 334         | Ultimecia Castle seals. See [SEALEDOFF](Field/Script/Opcodes/159_SEALEDOFF.md) for details.                                                                 |
| Byte        | 335         | Card related                                                                                                                                                            |
| Byte        | 336         | Deling City bus related                                                                                                                                                 |
| Byte        | 338-340     | Deling Sewer gates opened                                                                                                                                               |
| Byte        | 341         | Does lots of things.<sub>5</sub>                                                                                                                                        |
| Byte        | 342         | Deling City bus system                                                                                                                                                  |
| Byte        | 343         | G-Garden door/event flags.                                                                                                                                              |
| Byte        | 344         | B-Garden / G-Garden event flags (during GvG)                                                                                                                            |
| Byte        | 345         | G-Garden door/event flags.                                                                                                                                              |
| Byte        | 346-349     | FH Instrument (346 Zell, 347 Irvine, 348 Selphie, 349 Quistis)                                                                                                          |
| Word        | 350-356     | Health Bars (Garden mech fight)                                                                                                                                         |
| Byte        | 358         | Space station talk flags, Centra ruins related (beat odin?).                                                                                                            |
| Byte        | 359         | Centra ruins related (beat odin?).                                                                                                                                      |
| Long        | 360         | Choice of FH music.                                                                                                                                                     |
| Byte        | 364-368     | Randomly generated code for Centra Ruins.                                                                                                                               |
| Byte        | 369-370     | Ultimecia Castle flags                                                                                                                                                  |
| Byte        | 371         | unused in fields                                                                                                                                                        |
| Byte        | 372-376     | Ultimecia boss/timer/item flags                                                                                                                                         |
| Byte        | 377         | Ultimecia organ note controller                                                                                                                                         |
| Byte        | 378         | Centra Ruins timer (controls blackout messages from Odin)                                                                                                               |
| Byte        | 379         | unused in fields                                                                                                                                                        |
| Word        | 380         | Squall health during mech fight.                                                                                                                                        |
| Byte        | 382-383     | unused in fields                                                                                                                                                        |
| Byte        | 384         | Something about Laguna's time periods and GFs.                                                                                                                          |
| Byte        | 385         | Laguna dialogue in pub. Only the +2 bit is ever set. Don't change the +1 bit.                                                                                           |
| Byte        | 387         | Winhill progress?                                                                                                                                                       |
| Byte        | 388         | Timber Maniacs HQ talk flags (main lobby)                                                                                                                               |
| Byte        | 389         | Timber Maniacs HQ talk flags (office room)                                                                                                                              |
| Byte        | 390         | Edea talk flags at her house                                                                                                                                            |
| Byte        | 391         | Laguna talk flags (in his office, disc 3)                                                                                                                               |
| Byte        | 392         | unknown (used in Edea's house and in the Balamb Garden computer system)                                                                                                 |
| Byte        | 393-399     | unused in fields                                                                                                                                                        |
| Long        | 400 and 404 | Related to monsters killed in Winhill, but I don't think it actually does anything. Will investigate.                                                                   |
| Byte        | 408         | unused in fields                                                                                                                                                        |
| Byte        | 409         | Balamb Garden computer system                                                                                                                                           |
| Byte        | 410-431     | unused in fields                                                                                                                                                        |
| Byte        | 432         | BG Main hall flags                                                                                                                                                      |
| Byte        | 433         | Flags. Switches are assigned all over BG. No idea what any of them control.                                                                                             |
| Byte        | 434         | Flags. Switches are assigned all over BG. No idea what any of them control.                                                                                             |
| Byte        | 435         | Flags. Switches are assigned all over BG. No idea what any of them control.                                                                                             |
| Byte        | 436         | Moomba friendship level in the prison? Some actions cause these flags to be set.                                                                                        |
| Byte        | 437         | In BG on Disc 2, keeps track of who's in your party. In the prison, it's the current floor you're on.                                                                   |
| Byte        | 438         | Cid vs Norg event flags                                                                                                                                                 |
| Byte        | 439         | Cid vs Norg event flags                                                                                                                                                 |
| Byte        | 440         | Event flags. (+1 Quad ambush, +2 quad item giver, +4/+8 Infirmary helped, +16 Nida, +64 Kadowaki Elixir, +128 Training center)                                          |
| Byte        | 441         | Cid vs Norg event flags                                                                                                                                                 |
| Byte        | 442         | Rinoa Garden tour flags                                                                                                                                                 |
| Word        | 443         | Zell Health in Prison (Hacktuar)                                                                                                                                        |
| Byte        | 445-447     | Propagator defeated flags                                                                                                                                               |
| Word        | 448         | Unknown                                                                                                                                                                 |
| Byte        | 450-451     | Various magazine/talk flags                                                                                                                                             |
| Byte        | 452         | Lunatic Pandora areas visited?                                                                                                                                          |
| Byte        | 453-455     | Moomba teleport variables                                                                                                                                               |
| Byte        | 456-457     | unused in fields                                                                                                                                                        |
| Byte        | 458-459     | Used with MUSICSKIP in some Balamb Garden areas                                                                                                                         |
| Byte        | 460         | Random flags (some used for Card Club)                                                                                                                                  |
| Byte        | 461-473     | unused in fields                                                                                                                                                        |
| Byte        | 474         | Random flags (some used for Card Club)                                                                                                                                  |
| Byte        | 475-478     | CC Group variables                                                                                                                                                      |
| Byte        | 479         | If set to 0, disables all random battles during area loading.                                                                                                           |
| Byte        | 480         | State of students in classroom (what they're doing).                                                                                                                    |
| Byte        | 481         | Controls a conversation in the cafeteria.                                                                                                                               |
| Signed Word | 482         | Error ratio of missiles                                                                                                                                                 |
| Byte        | 484         | Missile Base progression?                                                                                                                                               |
| Byte        | 485         | ToUK Progression (initially 0b111010101, +2 on finish quest. No other pops)                                                                                             |
| Byte        | 486         | ToUK room? (used to control map jumps in the maze)                                                                                                                      |
| Byte        | 487         | Missile base progression (also does something in BG2F classroom)                                                                                                        |
| Byte        | 488         | Alternate Party Flags. Irvine +1/+16, Quistis +2/+32, Rinoa +4/+64, Zell +8/+128.<sub>1</sub>                                                                           |
| Byte        | 489         | Random talk flags?                                                                                                                                                      |
| Byte        | 490         | Cafeteria cutscene                                                                                                                                                      |
| Byte        | 491         | ToUK stuff                                                                                                                                                              |
| Byte        | 492         | I think this is a door opener for the missile base if you choose a short time limit.                                                                                    |
| Byte        | 493         | Missile base timer related?                                                                                                                                             |
| Byte        | 494-527     | unused in fields                                                                                                                                                        |
| Signed Word | 528         | Sub-story progression (it's a progression variable for individual segments of the game)                                                                                 |
| Byte        | 530         | X-ATM related (defeated it in battle?)                                                                                                                                  |
| Byte        | 531         | Functionally unused. Read from at dollet, only manipulated in debug rooms.                                                                                              |
| Byte        | 532         | Controls footstep sounds at dollet (sand to concrete)                                                                                                                   |
| Byte        | 533         | not investigated                                                                                                                                                        |
| Byte        | 534         | not investigated                                                                                                                                                        |
| Byte        | 535         | not investigated                                                                                                                                                        |
| Byte        | 536         | not investigated                                                                                                                                                        |
| Byte        | 537         | not investigated                                                                                                                                                        |
| Byte        | 538         | not investigated                                                                                                                                                        |
| Byte        | 539         | not investigated                                                                                                                                                        |
| Byte        | 540-591     | unused in fields                                                                                                                                                        |
| Byte        | 592-593     | Seems to control angles and character facing.                                                                                                                           |
| Byte        | 594         | unused in fields                                                                                                                                                        |
| Byte        | 595         | not investigated                                                                                                                                                        |
| Byte        | 596         | not investigated                                                                                                                                                        |
| Byte        | 597         | not investigated                                                                                                                                                        |
| Byte        | 598         | not investigated                                                                                                                                                        |
| Byte        | 599         | not investigated                                                                                                                                                        |
| Byte        | 600         | not investigated                                                                                                                                                        |
| Byte        | 601         | not investigated                                                                                                                                                        |
| Byte        | 602         | not investigated                                                                                                                                                        |
| Byte        | 603         | not investigated                                                                                                                                                        |
| Byte        | 604         | not investigated                                                                                                                                                        |
| Byte        | 605         | not investigated                                                                                                                                                        |
| Byte        | 606         | not investigated                                                                                                                                                        |
| Byte        | 607         | not investigated                                                                                                                                                        |
| Byte        | 608         | not investigated                                                                                                                                                        |
| Byte        | 609         | not investigated                                                                                                                                                        |
| Byte        | 610         | not investigated                                                                                                                                                        |
| Byte        | 611         | not investigated                                                                                                                                                        |
| Byte        | 612         | not investigated                                                                                                                                                        |
| Byte        | 613         | not investigated                                                                                                                                                        |
| Byte        | 614         | not investigated                                                                                                                                                        |
| Byte        | 615         | not investigated                                                                                                                                                        |
| Byte        | 616         | not investigated                                                                                                                                                        |
| Byte        | 617         | not investigated                                                                                                                                                        |
| Byte        | 618         | not investigated                                                                                                                                                        |
| Byte        | 619         | not investigated                                                                                                                                                        |
| Byte        | 620         | not investigated                                                                                                                                                        |
| Byte        | 621         | not investigated                                                                                                                                                        |
| Byte        | 622         | not investigated                                                                                                                                                        |
| Byte        | 623         | not investigated                                                                                                                                                        |
| Byte        | 624         | not investigated                                                                                                                                                        |
| Byte        | 625         | Balamb visited flags (+8 Zell's room)                                                                                                                                   |
| Byte        | 626         | not investigated                                                                                                                                                        |
| Byte        | 627         | not investigated                                                                                                                                                        |
| Byte        | 628         | unused in fields                                                                                                                                                        |
| Byte        | 629         | not investigated                                                                                                                                                        |
| Byte        | 630         | not investigated                                                                                                                                                        |
| Byte        | 631         | not investigated                                                                                                                                                        |
| Byte        | 632         | not investigated                                                                                                                                                        |
| Byte        | 633         | not investigated                                                                                                                                                        |
| Word        | 634         | not investigated                                                                                                                                                        |
| Byte        | 636         | not investigated                                                                                                                                                        |
| Byte        | 637         | unused in fields                                                                                                                                                        |
| Byte        | 638         | not investigated                                                                                                                                                        |
| Byte        | 639         | unused in fields                                                                                                                                                        |
| Byte        | 640         | not investigated                                                                                                                                                        |
| Byte        | 641         | not investigated                                                                                                                                                        |
| Byte        | 642         | not investigated                                                                                                                                                        |
| Byte        | 643         | not investigated                                                                                                                                                        |
| Byte        | 644         | not investigated                                                                                                                                                        |
| Byte        | 645         | not investigated                                                                                                                                                        |
| Byte        | 646         | not investigated                                                                                                                                                        |
| Byte        | 647         | not investigated                                                                                                                                                        |
| Byte        | 648         | not investigated                                                                                                                                                        |
| Byte        | 649         | not investigated                                                                                                                                                        |
| Byte        | 650-655     | unused in fields                                                                                                                                                        |
| Word        | 656         | not investigated                                                                                                                                                        |
| Byte        | 658         | not investigated                                                                                                                                                        |
| Byte        | 659         | not investigated                                                                                                                                                        |
| Byte        | 660         | not investigated                                                                                                                                                        |
| Byte        | 661         | not investigated                                                                                                                                                        |
| Byte        | 662         | not investigated                                                                                                                                                        |
| Byte        | 663         | not investigated                                                                                                                                                        |
| Byte        | 664         | not investigated                                                                                                                                                        |
| Byte        | 665         | not investigated                                                                                                                                                        |
| Word        | 666         | not investigated                                                                                                                                                        |
| Byte        | 668         | not investigated                                                                                                                                                        |
| Byte        | 669-671     | unused in fields                                                                                                                                                        |
| Word        | 672         | not investigated                                                                                                                                                        |
| Byte        | 674         | unused in fields                                                                                                                                                        |
| Byte        | 675         | not investigated                                                                                                                                                        |
| Byte        | 676         | unused in fields                                                                                                                                                        |
| Byte        | 677         | not investigated                                                                                                                                                        |
| Byte        | 678         | not investigated                                                                                                                                                        |
| Byte        | 679         | unused in fields                                                                                                                                                        |
| Byte        | 680         | not investigated                                                                                                                                                        |
| Byte        | 681         | not investigated                                                                                                                                                        |
| Byte        | 682         | not investigated                                                                                                                                                        |
| Byte        | 683         | not investigated                                                                                                                                                        |
| Byte        | 684         | not investigated                                                                                                                                                        |
| Byte        | 685         | not investigated                                                                                                                                                        |
| Byte        | 686         | not investigated                                                                                                                                                        |
| Byte        | 687         | not investigated                                                                                                                                                        |
| Byte        | 688         | not investigated                                                                                                                                                        |
| Byte        | 689         | not investigated                                                                                                                                                        |
| Byte        | 690         | not investigated                                                                                                                                                        |
| Byte        | 691         | not investigated                                                                                                                                                        |
| Byte        | 692-719     | unused in fields                                                                                                                                                        |
| Byte        | 720         | Squall's costume (0=normal, 1=student, 2=SeeD, 3=Bandage on forehead)                                                                                                   |
| Byte        | 721         | Zell's Costume (0=normal, 1=student, 2=SeeD)                                                                                                                            |
| Byte        | 722         | Selphie's costume (0=normal, 1=student, 2=SeeD)                                                                                                                         |
| Byte        | 723         | Quistis' Costume (0=normal, 1=SeeD)                                                                                                                                     |
| Word        | 724         | Dollet mission time                                                                                                                                                     |
| Word        | 726         | not investigated                                                                                                                                                        |
| Byte        | 728         | Does lots of things.<sub>3</sub>                                                                                                                                        |
| Byte        | 729         | not investigated                                                                                                                                                        |
| Byte        | 730         | Flags (+1 Joined Garden Festival Committee, +4 Gave Selphie tour of BG, +16 Kadowaki asks for Cid, +32 and +64 Tomb of Unknown Kind hints?, +128 Beat all card people?) |
| Byte        | 731         | unused in fields                                                                                                                                                        |
| Word        | 732         | not investigated                                                                                                                                                        |
| Byte        | 734         | Split Party Flags (+1 Zell, +2 Irvine, +4 Rinoa, +8 Quistis, +16 Selphie).<sub>2</sub>                                                                                  |
| Byte        | 735         | not investigated                                                                                                                                                        |
| Byte        | 736-751     | unused in fields                                                                                                                                                        |
| Byte        | 752         | not investigated                                                                                                                                                        |
| Byte        | 753-1023    | unused in fields                                                                                                                                                        |
| Byte        | Above 1023  | Temporary variables used pretty much everywhere.                                                                                                                        |

# Notes

1.  When the party splits in disc 2, each party member in the inactive party except Selphie has one of the eight bits changed for this variable. One member has a flag in the 4 most significant bits, and the other has a flag in the 4 least significant bits. It's done this way so that when the characters appear, they animate towards different locations in the field, rather than stacking on top of each other.
2.  This byte contains flags for which characters are in Squall's party when the party splits in disc 2.
3.  List of everything that 728 holds throughout the game:
    1.  SeeD field exam "Conduct" score (lose points when you do something wrong at Dollet).
    2.  Train job attempts (Timber)
    3.  Tomb of the Unknown King student ID.
    4.  Who you took to space in disc 3.
4.  The field controlling restriction unlocking in Ultimecia's Castle uses this to figure out where to jump the party after they've broken a seal. It's unknown how SETPLACE actually sets this, it's not always related to the field ID or the SETPLACE parameter. This variable is also set at Balamb Garden's front gate manually.:5. List of everything that 341 holds throughout the game:
    1.  First flashback team
    2.  Selphie's current action when escaping from Deling's mansion (changes the dialogue)
    3.  FH Concert Crappiness
    4.  Something in B-Garden classroom during the paratrooper attack.
