"+" means held at the same time. "," means one after the other.
If a setting has more than one combination it will be listed on another line.

# The very basics
The default keybindings can be changed by going into the key configuration settings in the options menu. Here are the very basics to get you started:

| key | action |
| --- | ------ |
| Enter | Go forward through a menu or screen |
| Escape | Return to a previous screen |
| Arrow keys | Navigate the menus (and press arrows during gameplay) |

# Universal debugger shortcuts

| Combination | Function |
| ----------- | -------- |
| F1 | Insert coin |
| F2 | Reload metrics and resources |
| Shift+F2 | Reload metrics (also reloads language files) |
| Ctrl+F2 | Reload scripts |
| Holding F3 | Open the debug menu. While displaying the debug menu you can press the listed keys to switch menus and toggle debug functions. |

# Universal shortcuts

| Combination | Function |
| ----------- | -------- |
| Alt+Enter | Switches between windowed and fullscreen... Except it's kind of buggy. |
| Tab | Speeds up UI to 2x while held, including animations and selections. |
| ~ | Slows down UI and animations to 0.25x(?) while held. |
| Scroll Lock | Jump immediately to the options menu. You can change this key binding in settings. |
| Screenshot key (PrintScreen or F13 by default) | Save a lossy screenshot. You can change this key binding in settings. |
| Shift + Screenshot key | Save a lossless screenshot. |


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

### Music Select

| Default combination | metrics setting | What it does |
| ------------------- | --------------- | ------------ |
| Left | PreviousSongButton | Previous song |
| Right | NextSongButton | Next Song |
| Start | (hardcoded) | Begin Song |
| Start, Start<br>OR<br>Holding Start | (hardcoded) | Open Options Screen |
| Select | (hardcoded) | Open Options List |
| (Not used) | PreviousDifficultyButton | Switches to the previous difficulty. By default, CodeDetector is used instead. |
| (not used) | NextDifficultyButton | Switches to the next difficulty. By default, CodeDetector is used instead. |
| Ctrl+any letter | (hardcoded) | Switches the sorting to alphabetical and then jumps to the letter you've pressed. |

Start, Start or Holding Start opens the options screen if metric "OptionsMenuAvailable" is true.

Select opens options list if metric "UseOptionsList" is true. (Using the select button to open the options list is hardcoded and can't be changed, but you can add an additional combo to open the OptionsList using CodeDetector.)

| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| Down, Down<br>OR<br>MenuDown, MenuDown | PrevSteps1<br>PrevSteps2 | Make the difficulty harder |
| Up, Up<br>OR<br>MenuUp, MenuUp | NextSteps1<br>NextSteps2 | Make the difficulty easier |
| Left+Right<br>OR<br>MenuLeft-MenuRight | NextSort1<br>NextSort2<br>NextSort3<br>NextSort4 | Cycle between sorting modes |
| MenuUp, MenuRight, MenuRight | NextGroup | Jump to next folder |
| (no default) | PrevGroup | Jump to previous folder |
| Up, Down, Up, Down<br>OR<br>MenuUp, MenuDown, MenuUp, MenuDown | ModeMenu1<br>ModeMenu2 | Open up the sorting selection menu |
| MenuUp-MenuDown | CloseCurrentFolder | Close the current folder |

Some themes use Left+Right for Sort menu instead of Cycle between sorting modes, leaving this function disabled.

### Modifier codes

Some of these are for [Pump](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes#pump) mode, which is where the UpLeft, UpRight, DownLeft, DownRight buttons come from. They don't affect [Dance](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes#dance) mode, so you can ignore them if you don't play Pump mode.

| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| Left, Right, Left, Right, Left, Right, Left, Right | CancelAll | Remove all modifiers |
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
| (no default combo) | NextTheme **(DEPRECIATED)** | Cycles to the next theme. |
| (no default combo) | NextTheme2 **(DEPRECIATED)** | Cycles to the next theme. |
| (no default combo) | NextAnnouncer **(DEPRECIATED)** | Cycles to the next announcer. |
| (no default combo) | NextAnnouncer2 **(DEPRECIATED)** | Cycles to the next announcer. |
| (no default combo) | BackInEventMode | ??? |
| (no default combo) | PrevOptionsList | Goes to the previous options list menu, if UseOptionsList is enabled on the music select screen metrics. |
| (no default combo) | NextOptionsList | Goes to the next options list menu, if UseOptionsList is enabled on the music select screen metrics. |

# Evaluation Screen

## Default combinations
| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| MenuLeft-MenuRight<br>OR<br>Select | SaveScreenshot1<br>SaveScreenshot2 | Save a screenshot. |