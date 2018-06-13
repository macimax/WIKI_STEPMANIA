Various gimmicks that commonly appear in pump charts.

## notes that are actually hold notes

Right on your hold note, set speed to 1000 and length to whatever you want (above 0), then set scrolling factor to 0.001.

## Make all notes disappear before they reach the receptors
If you just want to make the notes invisible, add an attack segment with the Hidden modifier.
If you want to make the notes disappear and not count for your score, add a fake segment and an attack segment that has Hidden & StealthPastReceptors (SM 5.1+ required).

## Make individual notes disappear before they reach the receptors
Add a warp somewhere and copy and paste the same notes, minus the one you want to disappear. When the player crosses the warp and jumps to the new set of notes, it will make it look like the notes disappeared.

## Make stopped notes appear and disappear in the playfield
Make a warp that lands on a segment with a scrolling factor of 0. then 0.25 after, set the scrolling factor back to 1 with a warp that jumps past the note you want to make disappear.

## Stutter gimmick
Add a delay for the length of time until the next note.