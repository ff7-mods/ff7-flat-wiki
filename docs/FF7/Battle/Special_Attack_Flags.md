---
title: Special_Attack_Flags
---

Attacks and Items can have additional Special Properties that Damage Calculation takes into account when applying damage. The storage of these bits is reversed from the standard way by having "0" if the effect is active and "1" if it is not.

| Bit  | Effect                                                  |
|:----:|---------------------------------------------------------|
| 0001 | Damage MP instead of HP                                 |
| 0002 | Unknown. Appears in several attacks (see below)         |
| 0004 | Attack affected by Darkness (unused but works)          |
| 0008 | Unused                                                  |
| 0010 | Caster Drains some of the damage done                   |
| 0020 | Caster Drains HP and MP based on damage done            |
| 0040 | Unknown. Only appears in Limit Break: Blade Beam        |
| 0080 | Ignore Status Effect Defense when attempting to Inflict |
| 0100 | Causes "Miss" if target is not dead                     |
| 0200 | Can be reflected                                        |
| 0400 | Ignores Defense Calculation                             |
| 0800 | Does not re-target if target is inflicted with "Death"  |
| 1000 | Unused                                                  |
| 2000 | Always a Critical Hit                                   |
| 4000 | Unused                                                  |
| 8000 | Unused                                                  |

  
The 0004 bit here causes darkness to halve the accuracy byte when the ability data is loaded. The fact that this bit is unset for all enemy attacks is the true cause of the infamous "darkness bug", likely the design intent was to make this interaction configurable on a per-action basis, but then enemy actions were just never flagged. The other Unused ones don't seem to have any immediately obvious effect on damage calculation and they aren't used in any attack available to player or enemy. They are probably place-holders for temporary variables set during damage calculation.

## Attacks with Property 0002h

After testing this significantly, it cannot be determined what this effect is based on a visual inspection. Here is a complete list of attacks that have this property. No enemy exclusive attacks have it.

- Life
- Life2
- Confu
- Haste
- Slow
- Death
- Escape
- Remove
- Fire3
- Ice3
- Bolt3
- Quake2
- Quake3
- Bio3
- Demi3
- FullCure
- Ultima
- Choco/Mog
- Shiva
- Ifrit
- Ramuh
- Titan
- Odin
- Leviathan
- Bahamut
- Kjata
- Alexander
- Phoenix
- Neo Bahamut
- Hades
- Typoon
- Bahamut ZERO
- Knights of Round
- White Wind
- Big Guard
- Bad Breath
- Beta
- Aqualung
- Trine
- Magic Breath
- Pandora's Box
- Fat-Chocobo
- Gunge Lance

  
Things it doesn't do:  
-Alter Camera Movement (this info seems to be in the animation)  
-Affect Animations between single/multiple targets (although it looks like it should)  
-Change damage infliction timing (individually or all at once)  
-Alter Battle Timer for any character (this info seems to be in the animation)  
NOTE: After going through and decompiling the executable for FFVIIPC, it does not look like this property is checked for. Neither does it check for the Blade Beam property. At one time this may have been the "use multi-target animation on multiple targets" flag, but the animation handles that now. Likewise, removing the Blade Beam property does nothing to the Blade Beam attack itself. It was likely replaced by [Additional Effect](../Attack_Special_Effects) 1Ah.
