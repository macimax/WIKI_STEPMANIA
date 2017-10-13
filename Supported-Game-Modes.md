StepMania supports multiple game modes:

*All StepsTypes are prefixed with `StepsType_`, this is omitted here for readability.

## Dance
Your regular DDR simulation game mode.

This mode uses SM, SSC, SMA, or DWI chart files.

There is Single (4key), Solo (6key), Double (8key), or Versus (2 players, 4key each) styles.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Dance_Single | Your normal 4 panel dance mode. |
| Double | Dance_Double | Both P1 & P2 pads are used for one player. |
| Solo | Dance_Solo | Only one player can play at a time(?), and there are two diagonal arrows at the top left and right. |
| Couple | Dance_Couple |  One chart, but P1 & P2 have different steps. Like old IIDX doubles. |
| Threepanel | Dance_Threepanel | Like Single, but the down arrow isn't used. |
| Routine | Dance_Routine | It's like Couple in that it's for two players, but the notefield is adjusted to a doubles width and charts can feature crossovers between pads. |

## Pump
Your regular 5key game mode, used for simulating Pump It Up.
Four arrows are pointed diagonally, with an additional 5th step in the center.

This mode uses the same chart files as dance.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Pump_Single | It's Single. But for Pump It Up. |
| HalfDouble | Pump_halfdouble | The player stands in the center of the P1 and P2 pad. Only six panels are used. |
| Double | Pump_Double | Same as Dance. |
| Couple | Pump_Couple | Same as Dance, although this style isn't used much. |
| Routine | Pump_Routine | Same as Dance. Note that in PIU, this is usually called Double Performance or Co-op x2. |

Additionally, you should know that StepF2 uses the #DESCRIPTION tag to mark a chart as Double Performance or Single Performance. It will have DP or SP in the tag.

## kb7
7keys mode.

| Style | StepsType | Description |
| ----- | --------- | ----------- |
| Single | Kb7_Single | ?????? |

## kickbox
4key, 6key, or 8key.

## lights
Used for testing the lights of a StepMania cabinet, or how you want your simfile to control the lights. It's not playable.

## para
para para paradise game mode, 5key.

## beat
Simulates Beatmania or Beatmania IIDX, with 5+1key, 7+1key, or doubles for each. Most songs are keysounded.

This mode uses BMS chart files for songs.

There is single5, single7, double5, double7, and whatever the versus styles are called. Contrary to their names the styles each have an additional turntable 'key', except for doubles having two.

## popn
5key or 9key game mode. Some songs are keysounded.

This mode uses PMS chart files for songs.

## techno
TechnoMotion. 4key, 5key, 8key, 8(double), 10(double), and 16(double) is supported.

## ds3ddx
Dance Station 3DDX, 4key + 4hand...

## karaoke
nonfunctional karaoke gamemode.

## Maniax
DanceManiax, 4 and 8key