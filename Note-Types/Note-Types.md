There are multiple **note types** available in StepMania.

| Note Type | Key Symbol | Comments |
| --- | --- | --- |
| Tap | 1 | Standard note type |
| Hold Head | 2 | Tap the hold note (as charged note on beat, frezze arrows on dance, etc.) when it crosses the judgment row, then hold it down. |
| Hold/Roll End | 3 | You can let go of the hold when the end crosses the judgment row. |
| Roll Head | 4 | Tap the roll note when it crosses the judgment row, then hit repeatly it until the end. |
| Mine | M | Do not tap the negative notes (as mines, shock arrows, etc.) when it crosses or have your foot held down when it crosses. You will lose life! |
| Lift | L | Have your foot on the arrow before it crosses. Lift up when it does cross. |
| Fake | F | You can ignore this note: it does nothing for or against you. |

## StepF2 Notes
These note types are not implemented in StepMania and they likely never will be, but they are documented here in case you ever need to convert a SF2 chart to SM5.

StepF2 uses a different note syntax: `{note type|attribute|fake flag|unknown flag}`.

Note type: read below

Attribute: v,s,h for vanish, sudden, and hidden

fake: if 1, this note is a fake note. If 0, this note is judged normally.

unknown flag: unknown

| Note Types | Key Symbol | Comments |
| ---------- | ---------- | -------- |
| P1 Tap Note | X | |
| P1 Hold Head | x | |
| P2 Tap Note | Y | |
| P2 Hold Head | y | |
| P3 Tap Note| Z | |
| P3 Hold Head | z | |
| Heart | F | This note does nothing? |
| Sudden | S | Acts like the sudden modifier, but per note. Will suddenly appear halfway up. |
| Vanish | V | Acts like the hidden modifier, but per note. Will disappear halfway up. |
| Hidden | H | This note cannot be seen. |