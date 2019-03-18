There are multiple **note types** available in StepMania.

<table>
<thead><tr><th>Note Type</th><th>Key Symbol</th><th>Comments</th></tr></thead>
<tbody>
<tr><td>Tap</td><td>1</td><td>Standard note type</td></tr>
<tr><td>Hold Head</td><td>2</td><td>Tap the hold note (as charged note on beat, frezze arrows on dance, etc.) when it crosses the judgment row, then hold it down.</td></tr>
<tr><td>Hold/Roll End</td><td>3</td><td>You can let go of the hold when the end crosses the judgment row.</tr>
<tr><td>Roll Head</td><td>4</td><td>Tap the roll note when it crosses the judgment row, then hit repeatly it until the end.</td></tr>
<tr><td>Mine</td><td>M</td><td>Do not tap the negative notes (as mines, shock arrows, etc.) when it crosses or have your foot held down when it crosses. You will lose life!</td></tr>
<tr><td>Lift</td><td>L</td><td>Have your foot on the arrow before it crosses. Lift up when it does cross.</td></tr>
<tr><td>Fake</td><td>F</td><td>You can ignore this note: it does nothing for or against you.</td></tr>
</tbody><tr>
</table>

## StepF2 Notes
These note types are not implemented in StepMania and they likely never will be, but they are documented here in case you ever need to convert a SF2 chart to SM5.

StepF2 uses a different note syntax: `{player|note type|unknown|unknown}`, where player is X for P1, Y for P2, and Z for P3 and note type is a StepF2 or StepMania note type.
| Note Types | Key Symbol | Comments |
| ---------- | ---------- | -------- |
| Sudden | S | Acts like the sudden modifier, but per note. Will suddenly appear halfway up. |
| Vanish | v | Acts like the hidden modifier, but per note. Will disappear halfway up. |
| Hidden | H | This note cannot be seen. |