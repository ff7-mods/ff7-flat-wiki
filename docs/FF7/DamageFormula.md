---
title: DamageFormula
---

## Accuracy Function considerations

Each of the upper nybble of the damage calculation determines what checks are done to accuracy of the action and whether or not it will connect, be critical or miss. Here are the functions in order processed based on the upper nybble:

| Upper Nybble | Functions |
|----|----|
| 0 | None (always hits) |
| 1 | [Physical Accuracy](DamageFormula#0:_Physical_Accuracy_Check), [Critical Check](DamageFormula#2:_Critical_Hit_Check) |
| 2 | [Magical Accuracy](DamageFormula#1:_Magical_Accuracy_Check) |
| 3 | Dummy \[3\] (always hits) |
| 4 | Dummy \[4\] (always hits) |
| 5 | Dummy \[5\] (always hits) |
| 6 | [Physical Accuracy](DamageFormula#0:_Physical_Accuracy_Check), [Critical Check](DamageFormula#2:_Critical_Hit_Check) |
| 7 | [Magical Accuracy](DamageFormula#1:_Magical_Accuracy_Check) |
| 8 | [Level-based Accuracy](DamageFormula#7:_Level-based_Accuracy) |
| 9 | [Manipulate](DamageFormula#6:_Manipulate_Accuracy_.28intended_solely_for_playable_characters.29) |
| A | [Physical Accuracy](FF7/DamageFormula#0:_Physical_Accuracy_Check "wikilink"), [Critical Check](DamageFormula#2:_Critical_Hit_Check) |
| B | [Physical Accuracy](FF7/DamageFormula#0:_Physical_Accuracy_Check "wikilink") |
| C | None (always hits) |
| D | None (always hits) |
| E | None (always hits) |
| F | None (always hits) |

# Damage Calculations

These are the damage functions according to an unmodded FF7-ENG 1.02 (1998)

## Standard Formulae

### X0:

*0x5DE5C0*

    Sets Target's 02h flag to 1. (Unknown effect)

### X1:

*0x5DE5DF*

    If Attack Property "Always Critical" is Set
        Set Critical Damage Flag
    End If

    x = ( Actor's Level * Actor's (M)Attack ) / 32
    y = ( Actor's Level + Actor's (M)Attack ) / 32
    z = Actor's (M)Attack + ( x * y )
    z = z * ( 512 - target's defense ) * Attack's Power
    Damage = z >> 13
    //This is a bit-shift left by 13 which is mathematically equivalent to dividing by 8192, but it's important to note that it doesn't actually divide as this is the source of the damage overflow glitch

    If Critical Damage Flag is set
        Damage = Damage * 2
    End If

    If Actor's Statuses include Berserk
        Damage = Damage * 3 / 2
    End If

    Long_Range = 0
    If Target is in Back Row
        Set Long_Range = 1
    End If

    If Attack is Short Range OR Command is Enemy Attack
        If Actor is in Back Row
            Long_Range = 1
        End If
    Else
        Long_Range = 0
    End If

    If Long_Range != 0
        Damage = Damage / 2
    End If

    If Target is Defending
        Damage = Damage / 2
    End If

    If Target's Back is exposed
        Damage = Damage * ( Target's Back Attack Modifier / 8 )
    End If

    If Actor's Statuses includes Frog
        Damage = Damage / 4
    End If

    Damage = Sadness( Damage )
    Damage = Split( Damage, 0 )
    Damage = Barrier( Damage )
      
    If Actor's Statuses include Mini
        Damage = 0
    End If
    Damage = Variance( Damage )

### X2:

*0x5DE9B8*

    multiNoSplit = ( ( ( Attack's Target Flags AND Ch ) - 4 ) == 0 ? 1 : 0 )
    Base = (Actor's Attack + Actor's Level) * 6
    Damage = (512 - Target's Defense) * Base * Attack's Power / 8192
    Damage = Sadness( Damage )
    Damage = SplitDamage( Damage, multiNoSplit )
    Damage = Barrier( Damage )
    Damage = Variance( Damage )

### X3:

*0x5DEA6D*

    If Attack Properties Damage MP is clear
        Damage = Target's HP
    Else
        Damage = Target's MP
    End If

    Damage = Damage * Attack's Power / 32

    If ActionData[AC] != 0 (?)
        Damage = Damage / 2
    End If

### X4:

*0x5DEAF7*

    If Attack Properties Damage MP is clear
        Damage = Target's MHP
    Else
        Damage = Target's MMP
    End If

    Damage = Damage * Attack's Power / 32

    If ActionData[AC] != 0 (?)
        Damage = Damage / 2
    End If

### X5:

*0x5DEB81*

    Damage = (Actor's (M)Attack + Actor's Level) * 6 + (Attack's Power * 22)
    Damage = SplitDamage( Damage )
    Damage = Barrier( Damage )
    Damage = Variance( Damage )

### X6:

*0x5DEBE5*

    Damage = Attack's Power * 20

### X7:

*0x5DEC0A*

    Damage = ( ( 512 - Target's Def ) * Attack's Power / 32 )
    Damage = Variance( Damage )

### X8:

*0x5DEC52*

    If ActionData[0x230] AND 40h
        ActionData[0x230] = 1
    Else
        ActionData[0x230] = 80h
    End If
    //presumably this checks if the target heals from restore element and will either recover or kill based on the result

### X9:

*0x5DEC8A*

    Actor's Attack = Actor's Strength * 2
    Use Damage X1 with adjusted stat

### XA:

*0x5DECAA*

    Damage = ( Attack's Power + Number of Targets - 1 ) / Number of Targets

## Additional Checks

### Sadness( Damage )

*0x5DE958*

    If Target's Status includes Sadness
        Damage = Damage - (Damage * 3 / 10)
    End If
    Return Damage

### SplitDamage( Damage, multiNoSplit )

*0x5DE8F4*

    If multiNoSplit == 0
        If No. of Attack's Targets >= 2
            Set Attack's split damage Target Flag
        Else
            Set multiNoSplit == 1
        End If
    End If

    If ActionData[0xAC] == 0
        Damage = Damage / 2
    Else
        If multiNoSplit == 0
            Damage = Damage * 3 / 2
        End If
    End If
    Return Damage

### Barrier( Damage )

*0x5DE82C*

    If Attack Property "Physical" is 0
        If Target's Statuses include MBarrier
            Set ActionData "MBarrier Active" flag
        End If
    Else
        If Target's Statuses include Barrier
            Set ActionData "Barrier Active" flag
        End If
    End If

    If ActionData "MBarrier Active" or "Barrier Active" flags are set
        Damage = Damage / 2
    End If

    If attack is Magic and EnabledMagic[7] == 0 (?)
        Damage = Damage + ( Damage * ( EnabledMagic[7] * (10 / 32) ) / 100 )
    End If
    Return Damage

### Variance( Damage ):

*0x5DE988*

    Damage = Damage ([0..255] + 3841) >> 12  //from RNGLUT in KERNEL.BIN
    //Again, we have another chance for overflow.

    If Damage == 0
        Damage == 1
    End If
    Return Damage

## Secondary Damage Formulae

### X0:

*0x5DECFB*

    Damage = Attacker's HP

### X1:

*5DED1E*

    Damage = Attacker's MHP - Attacker's HP

### X8:

*0x5DED73*

    Dice_Count = Attacker's Level / 10

    If Dice_Count < 2 then
        Dice_Count = 2
    Elseif Dice_Count > 6
        Dice_Count = 6
    End If

    total_dice_roll = 0
    For ( d_loop = 0; d_loop < Dice_Count; d_loop++ )
        die = [0..5]
        all_dice[d_loop] = die
        total_dice_roll += die + 1

        set die visualization based on roll
    Loop

    value_repeat = 0
    For ( d_value = 0; d_value < 6; d_value++ )

        repeat_count = 0
        For ( d_loop = 0; d_loop < Dice_Count; d_loop++ )

            If all_dice[d_loop] = d_value then
                repeat_count++
            End If
        Loop

        If repeat_count > value_repeat then
            value_repeat = repeat_count
        End If

    Loop

    Damage = value_repeat * 100 * total_dice_roll

### X9

*0x5DEEEF*

    Damage = Number of Successful Escapes

### XA

*0x5DEF1D*

    Damage = Target's HP - 1

### XB

*0x5DEF44*

    Damage = (Game Time Hours * 100) + (Game Time Minutes)

### XC

*0x5DEF88*

    Damage = Target's Kill Count * 10
    //This is intended to be used only on players
    //This will cause a memory leak if done on enemies

### XD

*0x5DEFDD*

    If target is playable character
        MateriaCount = 0;
        For ( MateriaLoop = 0; MateriaLoop < 8; MateriaLoop++ )
            If target has materia in weapon slot [MateriaLoop] then MateriaCount++
            If target has materia in armor slot [MateriaLoop] then MateriaCount++
        Loop
        Damage = MateriaCount * 1111
    End If

# Accuracy Functions

The point of these is to set the "attack will miss" flag in the current action memory structure.

### 0: Physical Accuracy Check

*0x5DDBB0*

    ;For the purposes of this code, "Dex" means the adjusted Dexterity of the actor/target if any in-battle dex bonuses have been granted.
    ;Same holds for the Physical Evade. Physical Hit rate has no in-game bonus opportunities.

    Check_For_Cover()

    HitChance = -1;

    If "Always connect" flag set then HitChance = 255;

    If target has one of the following statuses (Death, Sleep, Confu, Stop, Petrify, Manipulate, Paralysis) then
        Remove Sleep status
        Remove Confu status
        Remove Manipulate status
        HitChance = 255
    End If

    If action is flagged as "always hit" then HitChance = 255;

    Physical Chance = (Actor's Dex >> 2) + action physical hit rate
    If Actor is enemy then
        Actor's evade = Actor's Physical evade
    else
        Actor's evade = (Actor's Dex >> 2) + Actor's Physical evade
    End If
    If Target is enemy then
        Target's evade = Target's Physical evade
    Else
        Target's evade = (Target's Dex >> 2) + Target's Physical evade
    End If

    If HitChance = -1 Then
        HitChance = Physical Chance + Actor's evade - Target's evade
        HitChance = FuryAdjust(HitChance)
    End If

    If HitChance = 0 then HitChance = 1

    Luck Chance = [0..99]
    If (Actor's Luck / 4) > Luck Chance Then
        HitChance = 255 ;Lucky Hit
    Else
        If Actor is Player Character targetting an enemy Then
            If (Target's Luck / 4) > Luck Chance
                HitChance = 0 ;Lucky Dodge
            End If
        End If
    End If

    Miss Chance = (([0..65535] * 99) / 65535) + 1 ;essentially [1..100]
    if HitChance < Miss Chance then
        Set Miss flag
    End If

#### Check_For_Cover

`   This is where the game checks if the target is covered under a "cover"ing ally.`  
`   It only applies to Player Characters`  
`   It might be more complicated than I'm seeing, but that is definitely ONE of its functions`

#### FuryAdjust(HitChance)

       If HitChance < 255 then 
            If Actor is in Fury Status
                HitChance = HitChance - ((HitChance * 3) / 10)
            End If
        End If
        return HitChance 

### 1: Magical Accuracy Check

*0x5DDE5E*

    acc = Action's Accuracy
    tar_save = level / 2; //rounded down
    acc_bonus = actor's level - tar_save
    rand_0 = [0..99]
    rand_1 = [0..99]
    if acc < 255 then
       if target does not have instant-death, null, or heal properties to current attack then
          if attack is not (reflectable and target in reflect status) then
             if attack does not inflict statuses or inflicting status include: Death, Sleep, Confu, Stop, Petrify, or Paralysis then
                acc = Fury_Adj( acc );
                if target's M_Evade > rand_0 OR
                    acc + acc_bonus < rand_1 then
                   Set action miss flag
                end if
             end if
          end if
       end if
    end if

### 2: Critical Hit Check

*0x5DDF8E*

    If attack does not miss then
       if actor in lucky girl status then
          critical_chance = 255
       else
          critical_chance = ((actor's luck + actor's level) - target's level ) >> 2;
          if actor is playable character then
             critical_chance += weapon's critical bonus //?
          end if
          Critical_random = ( ( [0..65535] * 99 ) / 65535 ) + 1;
          if critical_chance > critical_random then
             attack set to critical
          end if
       end if
    end if

3, 4, and 5 don't exist. Since they don't set miss they will always hit.

### 6: Manipulate Accuracy (intended solely for playable characters)

*0x5DE0D0*

    int ally_loop;
    ManipSuccess = 0;
    for ( ally_loop = 0; ally_loop < 3; ally_loop++ )
    {
       if target is currently under manipulation by an actor then
          break;
       end if
    }
    if target is not currently being manipulated AND
        target is not a playable character AND
        target is an enemy AND
        actor is not currently manipulating an enemy AND
        target is not under manipulate status AND
        target's timer bar is running AND //like they're not stopped, petrified, etc
        target's attack resistance is "always-hit" then //?
       Manip_Chance = actor's level + 50 - target's level; //no less than 0
       if target count > 1 then
          Manip_Chance = ( Manip_Chance << 2 ) / 5;
       end if
       if actor's [0xAC] == 0 then
          Manip_Chance >> 1;
       end if
       if target's attack resistance is "always-hit" then
          Manip_Chance = 255;
       end if
       if actor's accessory property == 5 //"Increase manip rate" property on Hypnocrown
          if Manip_Chance < 100 then
             Manip_Chance = 100;
          end if
       end if
       If Manip_Chance > [0..99] then
          ManipSuccess = 1;
       end if
    end if
    If ManipSuccess == 1 then
       Set actor's manipulated enemy to target
       Display String 5Ah {"Manipulated <Enemy>"}
       Clear Actor's 0xE4 value //unknown
    else
       Set attack missed
    end if

This doesn't actually place the target in the manipulate status. That happens elsewhere.

### 7: Level-based Accuracy

*0x5DE08A*

    If Action's Accuracy > 0 then
       If the remainder of ( Target's level / Action accuracy ) is non-zero then
          Set attack missed
       end if
    end if

So if the accuracy IS 0, then it will always hit. This is to prevent a divide by zero error.
