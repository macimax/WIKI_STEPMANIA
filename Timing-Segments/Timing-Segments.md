A **timing segment** is an element of a simfile that can affect gameplay. There are multiple types:

## BPM

## Stop
Stops scrolling for x beats/seconds.
## Delay
Seems to do the same thing as Stop.
## Time Signature

## Warp
Anything during this segment will be skipped.
## Combo

## Tickcount
Affects the amount of combo ticks you get during a hold note in pump mode(?)

## Label

## Speed
* **Percent**: A percent of 2 will make the song scroll twice as fast, multiplying the player's current speed.
* **Length**: The time in beats it takes to change speed. a value of 1 will make it linearly scale from the current scroll speed to the new one in 1 beat. 0 will make it change instantly.
* **Mode**: Beats or seconds. 0 = beats, 1 = seconds.
## Scroll
Seems to do the same thing as speed, but with only the percent parameter.
## Fake
Notes during this segment won't be counted for or against you.