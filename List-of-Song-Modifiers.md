# General

**Note**: Some themes may not show all options. Refer to the PlayerOptions section in the luadoc for more information.

Unless otherwise specified, all functions are assumed to take (float) value, (float) approach_speed as arguments.

## General/etc
| Name | Function name | Function Arguments | Description |
| ----------- | ------------- | ------------------ | ----------- |
| NoteSkin | NoteSkin | (string) the name of the noteskin | Changes the noteskin. (Probably can't be applied during a song.) |

## SPEED

| Name | Function name | Description |
| ----------- | ------------- | ----------- |
| XMod | XMod | (default) Change the speed of arrows by a decimal value. Possible maximum SPEED is 10x on some themes and 8x on most themes. (Default: 1x, Usually have x1, x0.5, x0.25 or x0.1 increments, this last on some themes) |
| CMod | CMod | Short for "Constant Mod", this allows you to set a constant speed for arrows. The song bpm, speed changes and stops are ignored. |
| MMod | MMod | Set a minimum speed for arrows. If a song has a variable BPM it will match the minimum BPM. Meaning if your MMod is m600 and the song goes from 150 to 300 bpm, your note speed will be from 600 to 750. |
| Random Speed | RandomSpeed | Unknown.

## Perspective
| Name | Function name | Description |
| ----------- | ------------- | ----------- |
| Incoming | Incoming |  The notefield is tiled towards the player. Notes will appear from farther away and zoom towards the note receptors.
| Overhead | Overhead | (default) Notes will scroll on a flat surface from bottom to top. |
| Space | Space | The notefield is tilted away from the player.
| Hallway | Hallway | The notefield is tilted towards the player at a lesser angle. |
| Distant | Distant | The notefield is tilted away from the player, but on a lesser angle. |
| (not selectable by player) | Skew | Skew is one of the mods for controlling the perspective.<br>Skew moves the vanishing point for the note field away from the center of the screen.<br>Skew has no effect in single mode if Center1Player is true.<br>Skew has no effect in double mode. |

## Acceleration

Normal: Notes moves at the same speed.

Boost: Notes start slow and accelerate towards the receptors.

Brake: Notes start fast and decelerate towards the receptors.

Wave: Notes speed up and slow down as they go towards the receptors.

Expand: Notes get closer and farther like a spring.

Boomerang: Notes fly in from the top (or bottom if reverse), decelerate towards the bottom, then reverse and accelerate back towards the note field.

## Effects

Most effects can be amplified if you use them in the #ATTACKS field in a simfile. They can also be stacked.

Dizzy: The notes spin in their lanes

Twirl: The notes spin in 3D

Confusion: The notes and note receptors spin.

Drunk: The notes and note receptors sway to the left and right

Beat: The note and note receptors bounce left and right to the beat of the song

Tornado: notes fly in to the left, then to the right as they line up with the receptors

Mini: Makes the notefield small

Big: Makes the notefield big

XMode: The notes come in from a certain angle (You probably want to use this with #ATTACK so you can amplify it)

Bumpy: The notefield is "bumpy" in that the notes ripple towards and back in your direction.

Invert: The receptors are inverted. (Down, Left, Right, Up)

Flip: the receptors are flipped. (Right, Up, Down, Left)

## APPAREANCE

Visible: Notes are completely visible.

Hidden: Notes become invisible 3/4ths of the way before reaching the receptors. ATTACKS: Visibility range can be adjusted with an argument.

Sudden: Notes are invisible, then become visible 1/4th of the way towards the receptors. ATTACKS: Visibility range can be adjusted with an argument.

Stealth: Notes are completely invisible.

Blink: Notes flash between visible and invisible.

RandomVanish: Unknown function.

These two aren't part of StepMania's default, but some custom themes implement them:

Sudden+: Cover the bottom half of the notefield with a window or image that can be adjusted with EffectUp or EffectDown.

Hidden+: Cover the top half of the notefield (where the receptors are) with a window that can be adjusted with EffectUp or EffectDown.

StealthPastReceptors: Exactly what it says on the tin (5.1 only)

## TURN

(This changes the notes themselves instead of how they appear)

Mirror: The chart is mirrored.

Backwards: The chart is mirrored?

Left: The chart is turn left.

Right: The chart is turn right.

Shuffle: The chart is randomized, but tries to prevent jacks(?).

Cement Mixer/SuperShuffle: The chart is randomized completely.

Soft Shuffle: Left and right are flipped.

## Insert

Wide: Extra jumps on 1/4 beats.

Big: Adds notes on 1/8th beats.

Could someone add descriptions for the rest of the moddifiers in this section please? Thanks.

## SCROLL

Normal: Notes come from bottom to top.

Reverse: Notes come from top to bottom.

Split:

Alternate: The orientation of the receptor switches every time, so the first one is upright, the second one is downscroll, the third is up, the fourth is down.

Cross: The outer receptors are upright, and the inner receptors are at the bottom.

Centered: The receptors are vertically centered.

## Attacks

On: If the simfile has an #ATTACKS section, it will play scripted modifiers during gameplay.

Random Attacks: Randomly add and remove different modifiers during gameplay. Known as "RandAttack" internally.

## Hide

These can be stacked.

Dark: The STEP ZONE (or note receptors) is disabled.

Blind: Your combo and judgements are invisible.

Cover: The BGA is darkened.

# ASSIST options

## Remove

Removes notes to make the song easier and some themes enable assist clear.

Little: Removes notes requiring you to hit out of 1/4 beat. Known as CUT on _DDR_ series.

No Jumps: Removes notes requiring you to hit two arrows at the same time.

No Hands: Removes notes requiring you to hit three arrows at the same time.

No Quads: Removes notes requiring you to you hit four arrows at the same time.

No Stretch:

No Rolls: Removes roll notes.

No Lifts: Removes lift notes.

No Fakes: Removes fake notes.

## Holds

(Known as "Frezze Arrows" on _DDR_ series)

No Holds: Disables hold notes to make the song easier (Some themes enable assist clear).

Planted: Adds more holds. A lot of them.

Twister: Adds more holds, but allows for the possibility of more than two holds at a time.

Holds To Rolls: All holds are changed by rolls.

## Mines

Off: Removes negative notes.

On (Default): Negative notes (as mines or SHOCK ARROWS) are present. Hitting negative note drains the LIFE GAUGE or removes a life in battery modes.

Additive: Some tap notes are turned to negative notes, some negative notes are added at the end of holds.

Attack Mines: Hitting negative notes adds a random modifier during gameplay that decays instead of draining the LIFE GAUGE or removing a life in battery modes.

# Extra

## LIFE GAUGE
| Name | Function name | Description |
| ----------- | ------------- | ----------- |
| NORMAL | Bar | Normal lifebar type. Known as "Normal" on _DDR_ series. |
| Battery | Battery | Miss a note and lose a life. If you run out of lives, you fail the song. |
| 4 LIVES (Only on some themes) | Battery + 4 lives | You have 4 lives by default. If you run out of lives, you fail the song. |
| RISKY (Only on some themes) | Battery + 1 life | Miss a note and fail the song. |

**Note**: Some themes have this option in Player Options instead of Song Options, and some themes enable hard clear. Also, may change the options depending on theme.

## Gauge Drain

| Name | Function name | Description |
| ----------- | ------------- | ----------- |
| NORMAL | Normal-Drain | Self explanatory. |
| PRESSURE | NoRecover | Don't recover life upon scoring well. |
| Sudden Death | SuddenDeath | Same as Battery + 1 life (RISKY on _DDR_ series). If you miss a note you fail. |

**Note**: Some versions/variants implement custom LIFE GAUGE changes that alterate PRESSURE and SUDDENDEATH in the _Preferences.ini_ or _stepmania.ini_ on earlier versions, that may be changed by the user.

## Battery Lives

Self explanatory. 

**Note**: "1 life" = RISKY on _DDR_ series.

## Fail type

Immediate: Fail when the lifebar or battery is empty. Known as "FailImmediateContinue" internally.

Delayed:

Fail at end: Fail at the end of the song if your lifebar or battery is empty. Known as "FailAtEnd" internally.

Off: You can't fail. Known as "FailOff" internally.

IIDX: This fail type is custom and is in some themes. If your lifebar is <=80% at the end of the song, you will fail. Known as "FailIIDX" internally.

Due to a bug, playing SM 3.9 and variants using "Battery", 4 LIVES or RISKY options will change the fail type to Immediate. 