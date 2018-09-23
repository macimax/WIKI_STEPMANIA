A **timing segment** is an element of a simfile that can affect gameplay. There are multiple types:

## BPM
Change the speed for x beats, replacing the old BPM per a new one.

## Stop
Stops scrolling for x beats/seconds. Notes placed on the same segment must be pressed before the pause.
## Delay
Same thing as Stop, but notes on the same segment must be pressed after the pause.
## Time Signature

## Warp
Anything during this segment will be skipped.
## Combo

## Tickcount
Affects the amount of combo ticks you get during a hold note in pump mode(?)

## Label
Label segments allow charts to have segments that are labeled with a name, like in many Harmonix rhythm games and the Guitar Hero series. These do not affect the chart visually at all, and though themes could display them or take other actions based on them, there are very few, if any, themes that actually do. As such, they aren't very popular among chart creators either, though some of the StepMania 5 bundled songs do use them.

## Speed
* **Percent**: A percent of 2 will make the song scroll twice as fast, multiplying the player's current speed.
* **Length**: The time in beats it takes to change speed. a value of 1 will make it linearly scale from the current scroll speed to the new one in 1 beat. 0 will make it change instantly.
* **Mode**: Beats or seconds. 0 = beats, 1 = seconds.
## Scroll
This affects the display of the notes instead of changing the scroll speed.
Four different notes in a segment with a scroll speed of 0 will appear to be one single line of notes. This is different from setting Speed to 0, because Speed takes effect when the player enters the segment. Setting Speed to 0 would also show every single note in the song, not just the notes in the segment.
## Fake
Notes during this segment won't be counted for or against you.