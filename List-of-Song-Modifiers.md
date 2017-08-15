# General

## Speed Modifiers
XMod (default): Change the speed of arrows by a decimal value (0.5x, 1.5x, 2.0x, 2.75, etc)

CMod: Short for "Constant Mod", this allows you to set a constant speed for arrows. The song bpm and stops are ignored.

MMod: Set a minimum speed for arrows. If a song has a variable BPM it will match the minimum BPM. Meaning if your MMod is m600 and the song goes from 150 to 300 bpm, your note speed will be from 600 to 750.

## Perspective

Incoming: The notefield is tiled towards the player. Notes will appear from farther away and zoom towards the note receptors.

Overhead (default): Notes will scroll on a flat surface from bottom to top.

Space: The notefield is tilted away from the player.

Hallway: The notefield is tilted towards the player at a lesser angle.

Distant: The notefield is tilted away from the player, but on a lesser angle.

## Acceleration

Boost: Notes start slow and accelerate towards the receptors.

Brake: Notes start fast and decelerate towards the receptors.

Wave: Notes speed up and slow down as they go towards the receptors.

Expand: Notes get closer and farther like a spring.

Boomerang: Notes fly in from the top (or bottom if reverse), decelerate towards the bottom, then reverse and accelerate back towards the note field.

## Effects

## Appearance

Hidden: Notes become invisible 3/4ths of the way before reaching the receptors.

Sudden: Notes are invisible, then become visible 1/4th of the way towards the receptors.

Stealth: Notes are completely invisible.

Blink: Notes flash between visible and invisible.

## Turn

(This changes the notes themselves instead of how they appear)

Mirror: The chart is mirrored.

Backwards: The chart is mirrored?

Left: Left becomes down, down becomes right, right becomes up, up becomes left.

Right:

Shuffle: The chart is randomized, but tries to prevent jacks(?).

Cement Mixer/SuperShuffle: The chart is randomized completely.

Soft Shuffle: Left and right are flipped.

## Insert

## Remove

Removes notes to make the song easier.

Little:

No Jumps: Removes notes requiring you to hit two arrows at the same time.

No Hands: Removes notes requiring you to hit three arrows at the same time.

No Quads: Removes notes requiring you to you hit four arrows at the same time.

No Stretch:

No Rolls: Removes roll notes.

No Lifts: Removes lift notes.

No Fakes: Removes fake notes.

## Scroll

Reverse: Notes come from top to bottom.

Split:

Alternate:

Cross:

Centered:

## Holds

No Holds: Removes hold notes, obviously.

Planted: Adds more holds. A lot of them.

Twister: Adds more holds, but allows for the possibility of more than two holds at a time.

Holds To Rolls: All holds are now rolls.

## Mines

## Attacks

On: If the simfile has an #ATTACKS section, it will play scripted modifiers during gameplay.

Random Attacks: Randomly add and remove different modifiers during gameplay.

# Extra

# Life Type

Bar: Normal lifebar type.

Battery: Miss a note and lose a life. If you run out of lives, you fail the song.

# Bar Drain

Normal: Self explanatory

No Recover: Don't recover life upon scoring well.

Sudden Death: Same as Battery + 1 life. If you miss a note you fail.

# Battery Lives

Self explanatory.

# Fail type

Immediate: Fail when the lifebar or battery is empty.

Delayed:

Fail at end: Fail at the end of the song if your lifebar or battery is empty.

Off: You can't fail.