StepMania supports various game modes; they are divided into _games_ (an overarching definition of a specific number of columns and the directions or actions they represent, i.e. 4 inputs in cardinal directions for `dance`, vs. 5 inputs in the corners and center of the pad for `pump`), and _styles_ (variations of a _game_ that determine how many inputs are used; i.e. single vs. double):

**All StepsTypes are prefixed with `StepsType_`, this is omitted here for readability.**

## Dance
The standard 4-column dance game, as popularized by franchises such as _Dance Dance Revolution_ and _In the Groove_, with columns corresponding to the four cardinal directions.

This mode uses SM, SSC (on SSC and 5.x branch), SMA (on AMX and 5.x branch), or DWI chart files.

There is Single (4key), Double (8key), or Versus (2 players, 4key each) styles, Solo (6key) and Couple optional.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Dance_Single | Your normal 4 panel dance mode. |
| Double | Dance_Double | Both P1 & P2 pads are used for one player. |
| Solo | Dance_Solo | 4-panel, except with additional top-left and top-right columns. Due to its origins from a _DDR_ spin-off with 1-player cabinets, and other limitations, this mode can only be played by a single player. |
| Couple | Dance_Couple |  One chart, but P1 & P2 have different steps. The playing fields are kept separate. (You can think of this like old IIDX doubles or 'duel' custom charts in other rhythm games) |
| Threepanel | Dance_Threepanel | Like Single, but the down arrow isn't used. |
| Routine | Dance_Routine | It's like Couple in that it's for two players, but the notefield is adjusted to a doubles width and charts can feature crossovers between pads. |

## Pump
A 5-column mode, designed for simulating Pump It Up (or in the case of _Pump it Up Pro_ and _Pump it Up Infinity_, using it as part of an official title that uses StepMania as its engine). Four arrows are pointed diagonally, with an additional 5th step in the center.

This mode uses the same chart files as dance.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Pump_Single | Single, 5-panel pad. |
| HalfDouble | Pump_halfdouble | Uses only six panels in the middle of the pad (the 1p Center and right corners, and 2p left corners and center) |
| Double | Pump_Double | Same as Dance. |
| Couple | Pump_Couple | Same as Dance, although this style isn't used much. |
| Routine | Pump_Routine | Same as Dance. Note that in PIU, this is usually called Double Performance or Co-op x2. |

Additionally, you should know that StepF2 uses the #DESCRIPTION tag to mark a chart as Double Performance or Single Performance. It will have DP or SP in the tag.

## kb7
A 7-column mode influenced by PC-based rhythm games (such as DJMax and o2Jam; this style is also emulated by Osu!Mania 7K mode) that typically divide the notes into two banks of three columns each (usually mapped to the SDF and JKL keys respectively), which flank a central column (usually mapped to the spacebar).

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Kb7_Single | Standard kb7 layout  |

## kickbox

The StepsType is missing from the lua documentation. (Maybe this mode was removed or not fully implemented?)

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Human | kickbox_human | 4key |
| Quadarm | kickbox_quadarm | 4key 
| Insect | kickbox_insect | 6key |
| Arachnid | kickbox_arachnid | 8key |

## lights
This game type is used for testing lighting cues (primarily on arcade cabinets), and defining custom lighting cues within a simfile. It is not playable.

| Style | StepsType |
| ----- | --------- |
| ??? | Lights_Cabinet |

## para
Simulates _Para Para Paradise_; it is a 5-key mode, except using left, upleft, up, upright, and right directions (originally designed to be used with a hand sensor array).

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Para_Single | 5key. |

## beat
Simulates Beatmania or Beatmania IIDX, with 5+1key, 7+1key, or doubles for each. Most songs are keysounded.

This mode uses BMS chart files for songs.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| single5 | Bm_Single5 | 5+1key game mode |
| versus5 | Bm_Versus5 | Unknown, might be the beat equivalent to Couple? |
| double5 | Bm_Double5 | Both sides are used. |
| single7 | Bm_Single7 | 7+1key game mode |
| double7 | Bm_Double7 | Both sides are used. |
| versus7 | Bm_Versus7 | Unknown (see versus5) |

Contrary to their names the styles each have an additional turntable 'key', except for doubles having two. A turntable key is splitted on turn left and turn right.

## Ez2

Simulates _EZ2Dancer_ (upleft, down, and upright steps, and two columns for hand sensors).

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Ez2_Single | 1 pad |
| Double | Ez2_Double | 2 pad |
| Real | Ez2_Real | Divides the hand sensors into upper and lower halves. |# 

## popn
Simulates _Pop'n music_. Note: _Battle_ and _PSP_ charts are unimplemented.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| five | Pnm_Five | 5key game mode. |
| nine | Pnm_Nine | 9key game mode. |

Some songs are keysounded. This mode uses PMS chart files for songs.

## techno
Simulates TechnoMotion.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single4 | Techno_Single4 | Identical to dance_single |
| Single5 | Techno_Single5 | Identical to pump_single |
| Single8 | Techno_Single8 | eight panels are used: ⬅⬇⬆➡↙↘↗↖ |
| Double4 | Techno_Double4 | Identical to dance_double |
| Double5 | Techno_Double5 | Identical to pump_double |
| Double8 | Techno_Double8 | 16 panels (doubles) |

## ds3ddx
Dance Station 3DDX.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Ds3ddx_Single | 4key + 4hand... |

## karaoke
nonfunctional karaoke gamemode.

## Maniax
DanceManiax mode.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Maniax_Single | 4key |
| Double | Maniax_Double | 8key |