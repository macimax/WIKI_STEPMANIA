There are multiple **note types** available in StepMania.

| Note Type | Key Symbol | Comments |
| --- | --- | --- |
| Tap | 1 | Standard note type |
| Hold Head | 2 | Tap the hold note (as charged note on beat, frezze arrows on dance, etc.) when it crosses the judgment row, then hold it down. Note: Releasing the key during hold note in some themes breaks your combo. |
| Hold/Roll End | 3 | You can let go of the hold when the end crosses the judgment row. |
| Roll Head | 4 | Tap the roll note when it crosses the judgment row, then hit repeatly it until the end. |
| Mine | M | Do not tap the negative notes (as mines, shock arrows, etc.) when it crosses or have your foot held down when it crosses. You will lose life and in some themes breaks your combo! |
| Lift | L | Have your foot on the arrow before it crosses. Lift up when it does cross. |
| Fake | F | You can ignore this note: it does nothing for or against you. |
| AutoKeysound | K | This 'note' is not really a note, it marks a keysound that will play automatically at this row. No note will appear here, and this is only used for empty rows. |

## StepF2 Notes
These note types are not implemented in StepMania and they likely never will be, but they are documented here in case you ever need to convert a SF2 chart to SM5.

StepF2 uses a different note syntax: `{note type|attribute|fake flag|reserved flag}`.

Some older songs also have `{1e0}` but what it is is a mystery... For now, anyway.

| Note Types | Key Symbol | Comments |
| ---------- | ---------- | -------- |
| P1 Tap Note | X | |
| P1 Hold Head | x | |
| P2 Tap Note | Y | |
| P2 Hold Head | y | |
| P3 Tap Note| Z | |
| P3 Hold Head | z | |
| P4 Tap Note | 1 | Turns into P4 ONLY when P1, P2, and P3 is present, otherwise it's a regular note. |
| P4 Hold Head | 2 | Same as P4 tap note |
| Heart | F | This note does nothing. Uses heart icon ONLY when P1,P2, and P3 is present otherwise it's a fake note. |
| Sudden | S | Acts like the sudden modifier, but per note. Will suddenly appear halfway up. |
| Vanish | V | Acts like the hidden modifier, but per note. Will disappear halfway up. |
| Hidden | H | This note cannot be seen. |

| Note Attributes | Key symbol | Comments |
| --------------- | ---------- | -------- |
| Normal | n | This note does not have an attribute. |
| Vanish | v | see above |
| Sudden | s | see above |
| Hidden | h | see above |

fake: if 1, this note is a fake note. If 0, this note is judged normally.

reserved flag: Not used for anything.

