---
title: F8_PMVIE
---

- Opcode: **0xF8**
- Short name: **PMVIE**
- Long name: Set Movie

#### Memory layout

| 0xF8 | *M* |
|------|-----|

#### Arguments

- **const UByte** *M*: Movie ID to set.

#### Description

Sets the movie file that will be played at a future point in the script by [MOVIE](F9_MOVIE).

#### FF7 Movie ID List

| ID  | Movie File   | Brief Description                                         |
|-----|--------------|-----------------------------------------------------------|
| 0   | fship2.avi   | Clouds rolling                                            |
| 1   |              |                                                           |
| 2   | d_ropego.avi | Ropeway Up to Gold Saucer                                 |
| 3   | d_ropein.avi | Ropeway Down to Gold Saucer                               |
| 4   | u_ropein.avi | Arriving at Gold Saucer                                   |
| 5   | u_ropego.avi | Leaving Gold Saucer                                       |
| 6   | gold2.avi    | Gold Saucer ride; ends with moon                          |
| 7   | gold3.avi    | Chocobo Races go past; view from carriage                 |
| 8   | gold4.avi    | Gold Saucer flythrough; ends with gold statue             |
| 9   | gold6.avi    | Balloons released past the carriage                       |
| A   | gold5.avi    | Haunted house from the carriage                           |
| B   | boogup.avi   | Up to Bugenhagen's machine                                |
| C   | boogdown.avi | Down from Bugenhagen's machine                            |
| D   | junair_u.avi | Up on Junon Airstrip mechanism                            |
| E   | junair_d.avi | Down on Junon Airstrip mechanism                          |
| F   | junelein.avi | Junon elevator up (top level)                             |
| 10  | junelego.avi | Junon elevator down (top level)                           |
| 11  | junin_in.avi | Junon elevator down (bottom level)                        |
| 12  | junin_go.avi | Junon elevator up (bottom level)                          |
| 13  | moriya.avi   | Unknown                                                   |
| 14  | mkup.avi     | Cloud looks up to the first Mako reactor                  |
| 15  | northmk.avi  | North Mako reactor explodes                               |
| 16  | mk8.avi      | Jessie's bomb explodes to escape                          |
| 17  | ontrain.avi  | Cloud jumps on train                                      |
| 18  | mainplr.avi  | Train circles the pillar                                  |
| 19  | smk.avi      | South Reactor platform explodes after boss defeat         |
| 1A  | southmk.avi  | Cloud falls from platform                                 |
| 1B  | plrexp.avi   | Sector 7 pillar bomb explodes                             |
| 1C  | fallpl.avi   | Party escapes as pillar crumbles                          |
| 1D  | monitor.avi  | Snoozing guard at Shinra HQ; elevator door opens          |
| 1E  | bike.avi     | Cloud's bike and party escape on truck                    |
| 1F  | mtnvl.avi    | Nibelheim mountain, reactor, and rope bridge pan          |
| 20  | mtnvl2.avi   | Pan to Nibelheim reactor                                  |
| 21  | brgnvl.avi   | Nibelheim ropebridge snaps                                |
| 22  | nvlmk.avi    | Pod in Nibelheim reactor explodes, releasing monster      |
| 23  | nivlsfs.avi  | Nibelheim fire; Sephiroth looks up & moves through flames |
| 24  | jenova_e.avi | Sephiroth talks to Jenova and pulls off the statue        |
| 25  | junon.avi    | Junon to Mako Cannon pan                                  |
| 26  | hiwind0.avi  | Cloud climbs up to Junon airfield; Highwind               |
| 27  | mtcrl.avi    | Falling down scaffolding (Corel route)                    |
| 28  | gold1.avi    | Skyway to Gold Saucer (first visit)                       |
| 29  | biskdead.avi | Dyne & Barret in the past; Barret loses grip              |
| 2A  | boogdemo.avi | Bugenhagen's demo; shooting star & black hole             |
| 2B  | boogstar.avi | Bugenhagen's demo; Earth & the Lifestream                 |
| 2C  | setogake.avi | Stone Seto and the moon                                   |
| 2D  | rcktfail.avi | Rocket takes off, then stalls and tilts                   |
| 2E  | jairofly.avi | Tiny Bronco take-off and shooting                         |
| 2F  | jairofal.avi | Tiny Bronco crashes                                       |
| 2F  | gold7.avi    |                                                           |
| 2F  | gold7_2.avi  |                                                           |
| 2F  | earithdd.avi | Aeris death                                               |
| 2F  | funeral.avi  | Aeris funeral                                             |
| 2F  | car_1209.avi |                                                           |
| 2F  | opening.avi  | Opening                                                   |
