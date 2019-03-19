StepMania supports a number of play modes, normally selectable after you pick your profile and style.

The name before the slash is what it's referred to in fallback, the name after the slash is the common name.

### Normal / Regular
Your regular play mode, normally with 3 stages, plus an [[Extra Stage]] if the player gets any method used depending on theme (AA on FINAL STAGE in the default theme) (and Extra Stage is enabled), plus a Special Stage (More commonly known as Encore Extra Stage or One More Extra Stage) if the player passes the Extra Stage.

When Event Mode is enabled there are infinite stages, no TOTAL RESULTS and no Extra Stage.

Some themes uses this default mode and don't be changed, and some themes use different scoring systems (as ITG, EXTREME, Supernova2, Etc.).

Note for players: the Dance Points (or DP) is showned on some themes as EX-SCORE.

Note for themers: some themes show ScreenEvaluationStage (Results on actual stage) regards if any player passes or fails the song, and if the player passes FINAL STAGE, EXTRA STAGE or ENCORE EXTRA, the last result is showned and changes to ScreenEvaluationSummary (TOTAL RESULTS).

#### Evaluation
* NO PLAY: Song/course not played
* FAILED: Fail the song/course
* ASSIST CLEAR: Clear the song/course using NO HOLDS/REMOVE options
* CLEAR: Clear the song/course without using NO HOLDS/REMOVE options
* HARD CLEAR: Clear the song/course using PRESSURE/SUDDENDEATH/BATTERY/4 LIVES/RISKY options
* FULL COMBO: Clear the song/course with FULL COMBO
* ALL W1: Clear the song/course with _W1-only_ judges (marked as _Fantastic_ on default themes of the 5.x branch) and displays the maximum score.

### Rave
Battle against another player or a CPU. A gauge at the top determines who is winning or losing, and a gauge at the bottom fills up as you hit notes. When the gauge is full an attack modifier is temporarily applied to the opposite player. A draw can be happenned.
The gauge fills up to level 3 and then restarts at 0. Attacks can be defined per "character" which different character have different attack, defined in `Characters\[Character Name Here]\character.ini`.

### Nonstop / Course
Course mode. Pick a course to play a series of songs in order. It reads from .crs files in the Courses folder, but also has auto generated randomized ones from your song groups.

Note for themers: During this mode, you stay in ScreenGameplay until the course ends (or fails) and then you're taken to ScreenEvaluationNormal.

### Oni / Challenge
The same as Course mode, but the lifebar type is set to 4 LIVES.

### Endless
Play songs until you fail.