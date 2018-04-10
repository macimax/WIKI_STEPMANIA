Because this is seemingly documented nowhere?

"+" means held at the same time. "," means one after the other.
If a setting has more than one combination it will be listed on another line.

# Universal debugger shortcuts

| Combination | Function |
| ----------- | -------- |
| F1 | Insert coin |
| F2 | Reload metrics and resources |
| Shift+F2 | Reload metrics |
| Ctrl+F2 | Reload scripts |
| Holding F3 | Open the debug menu. I wont go in depth about it, since it states what buttons do what in the debug menu. |

# Universal shortcuts

| Combination | Function |
| ----------- | -------- |
| Alt+Enter | Switches between windowed and fullscreen... Except it's kind of buggy. |

# Music Select

## Debugger shortcuts
| Combination | Function |
| ----------- | -------- |
| Control+Shift+R | Reload the currently selected song and regenerate the cache for it |
| Control+S | Save current profile |
| Control+Q | Reload new song packs that have been placed in the songs folder since the game was started |
| Ctrl+Backspace | Permanently delete the selected song |
| F9 | Switch between transliterated and original song titles |

## Default gameplay combos & buttons
The following was taken from https://github.com/stepmania/stepmania/blob/master/Themes/_fallback/Scripts/03%20Gameplay.lua#L272

### Song select stuff

| Default combination | metrics setting | What it does |
| ------------------- | --------------- | ------------ |
| Left | PreviousSongButton | Previous song |
| Right | NextSongButton | Next Song |
| Start | (hardcoded) | Begin Song |
| Start,Start<br>Holding Start | (hardcoded) | Open Options Screen |
| Select | (hardcoded) | Open Options List |
| (Not used) | PreviousDifficultyButton | Switches to the previous difficulty. By default, CodeDetector is used instead. |
| (not used) | NextDifficultyButton | Switches to the next difficulty. By default, CodeDetector is used instead. |

Start,Start or Holding Start opens the options screen if metric "OptionsMenuAvailable" is true.

Select opens options list if metric "UseOptionsList" is true. (Using the select button to open the options list is hardcoded and can't be changed, but you can add an additional combo to open the OptionsList using CodeDetector.)

| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| Down,Down<br>MenuDown,MenuDown | PrevSteps1<br>PrevSteps2 | Make the difficulty harder |
| Up,Up<br>MenuUp,MenuUp | NextSteps1<br>NextSteps2 | Make the difficulty easier |
| Left+Right<br>MenuLeft-MenuRight | NextSort1<br>NextSort2<br>NextSort3<br>NextSort4 | Switch the sorting mode |
| MenuUp,MenuRight,MenuRight | NextGroup | Jump to next folder |
| (no default) | PrevGroup | Jump to previous folder |
| Up,Down,Up,Down<br>MenuUp,MenuDown,MenuUp,MenuDown | ModeMenu1<br>ModeMenu2 | Open up the sorting selection menu |
| MenuUp-MenuDown | CloseCurrentFolder | Close the current folder |
### Modifier codes

Some of these are for [Pump](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes#pump) mode, which is where the UpLeft, UpRight, DownLeft, DownRight buttons come from. They don't affect [Dance](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes#dance) mode, so you can ignore them if you don't play Pump mode.

| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| Left,Right,Left,Right,Left,Right,Left,Right | CancelAll | Remove all modifiers |
| DownRight, DownLeft, UpRight, UpLeft, DownRight, DownLeft, UpRight, UpLeft, Center | CodeDetector setting | Enables/Disables the [Mirror](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#turn) modifier. |
| (no default combo) | Left | Enables/Disables the [Left](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#turn) modifer. |
| (no default combo) | Right | Enables/Disables the [Right](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#turn) modifier. |
| UpLeft, UpRight, UpLeft, UpRight, DownLeft, DownRight, DownLeft, DownRight, Center | Shuffle | Enables/Disables the [Shuffle](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#turn) modifier. |
| UpLeft, UpRight, DownLeft, DownRight, UpLeft, UpRight, DownLeft, DownRight, Center | SuperShuffle | Enables/Disables the [SuperShuffle](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers) modifier. |
| (no default combo) | NextTransform | Cycles between transform modifiers |
| UpLeft, UpRight, UpLeft, UpRight, Center | NextScrollSpeed | Jumps to the next scroll speed (ex: 1x -> 2x, 2x -> 3x) |
| UpRight, UpLeft, UpRight, UpLeft, Center | PreviousScrollSpeed | Jumps to the previous scroll speed |
| (no default combo) | NextAccel | Cycles between [Accel](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#acceleration) modifiers | 
| (no default combo) | NextEffect | Cycles between [Effect](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#effects) modifiers |
| (no default combo) | NextAppearance | Cycles between [Appearnace](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#appearance) modifiers |
| (no default combo) | NextTurn | Cycles between [Turn](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#turn) modifiers |
| UpLeft, DownLeft, UpRight, DownRight, UpLeft, DownLeft, UpRight, DownRight, DownRight | Reverse | Enables/Disables the [Reverse](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers#scroll) modifier |
| (no default combo) | HoldNotes | You know what this does. |
| (no default combo) | Mines | You know what this does. |
| (no default combo) | Dark | You know what this does. |
| (no default combo) | Hidden | You know what this does. |
| (no default combo) | RandomVanish | You know what this does. |

# Evaluation Screen

## Default combinations
| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| MenuLeft-MenuRight<br>Select | SaveScreenshot1<br>SaveScreenshot2 | Save a screenshot. |