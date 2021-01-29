# The very basics
These are the basic default keybindings to get you started.  They can be changed in the *Config Key/Joy Mappings* screen in the main options menu.

| key | action |
| --- | ------ |
| <kbd>Enter</kbd> | Go forward through a menu or screen |
| <kbd>Escape</kbd> | Return to a previous screen |
| <kbd>←</kbd>, <kbd>↓</kbd>, <kbd>↑</kbd>, <kbd>→</kbd> | Navigate the menus (and press arrows during gameplay) |

# Universal shortcuts

| Combination | Function |
| ----------- | -------- |
| <kbd>Alt</kbd> + <kbd>Enter</kbd> | Switches between windowed and fullscreen. |
| <kbd>Tab</kbd> | Speeds up UI to 2x while held, including animations and selections. |
| <kbd>~</kbd>| Slows down UI and animations to 0.25x(?) while held. |
| <kbd>Scroll Lock</kbd> | Jump immediately to the options menu. You can change this key binding in settings. |
| Screenshot key (<kbd>PrintScreen</kbd> or <kbd>F13</kbd> by default) | Save a lossy screenshot. You can change this key binding in settings. |
| <kbd>Shift</kbd> + *Screenshot key* | Save a lossless screenshot. |

# Universal debugger shortcuts

| Combination | Function |
| ----------- | -------- |
| <kbd>F1</kbd> | Insert coin |
| <kbd>F2</kbd> | Reload metrics and resources |
| <kbd>Shift</kbd> + <kbd>F2</kbd> | Reload metrics (also reloads language files) |
| <kbd>Ctrl</kbd> + <kbd>F2</kbd> | Reload scripts |
| Holding <kbd>F3</kbd> | Open the Debug Menu. |


# Debug Menu

The Debug Menu is accessed by holding <kbd>F3</kbd>.  From there, you can toggle between its three modes:

| Combination | Mode |
| ----------- | -------- |
| <kbd>F3</kbd> + <kbd>F5</kbd> | **Main** Debug Menu |
| <kbd>F3</kbd> + <kbd>F6</kbd> | **Theme** Debug Menu |
| <kbd>F3</kbd> + <kbd>F7</kbd> | **Profile** Debug Menu |

### Main Debug Menu

These keyboard shortcuts are available when the Debug Menu is in *Main Debug Menu* mode.

| Combination | Function |
| ----------- | -------- |
| <kbd>F3</kbd> + <kbd>1</kbd> | Toggle between Home mode, Freeplay, and Coin mode |
| <kbd>F3</kbd> + <kbd>2</kbd> | Toggle slow animations |
| <kbd>F3</kbd> + <kbd>3</kbd> | Halt rendering |
| <kbd>F3</kbd> + <kbd>4</kbd> | Toggle *Lights Debug*, used to test arcade cabinet lighting |
| <kbd>F3</kbd> + <kbd>5</kbd> | Toggle *Monkey Input*, used by themers for stress-testing input handling |
| <kbd>F3</kbd> + <kbd>6</kbd> | Toggle *Visual Rendering Stats* (FPS, average FPS, and vertices per frame counts) |
| <kbd>F3</kbd> + <kbd>7</kbd> | Toggle Vsync |
| <kbd>F3</kbd> + <kbd>8</kbd> | Toggle Multitexture (?) |
| <kbd>F3</kbd> + <kbd>0</kbd> | Write Preferences.ini to disk |
| <kbd>F3</kbd> + <kbd>E</kbd> | Pull back camera; useful for themers when designing screens |
| <kbd>F3</kbd> + <kbd>R</kbd> | Decrease StepMania volume by 10% |
| <kbd>F3</kbd> + <kbd>T</kbd> | Increase StepMania volume by 10% |
| <kbd>F3</kbd> + <kbd>A</kbd> | Mute all "Actions" (typically theme sound effects) |


# Music Select

| Combination | Function |
| ----------- | -------- |
| <kbd>Control</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd> | Reload the currently selected song and regenerate the cache for it |
| <kbd>Control</kbd> + <kbd>S</kbd> | Save current profile |
| <kbd>Control</kbd> + <kbd>Q</kbd> | Reload new song packs that have been placed in the songs folder since the game was started |
| <kbd>Control</kbd> + <kbd>Backspace</kbd> | Permanently delete the selected song (if `AllowSongDeletion` is enabled) |
| <kbd>F9</kbd> | Switch between transliterated and original song titles |

## Default gameplay combos & buttons
The following was taken from https://github.com/stepmania/stepmania/blob/master/Themes/_fallback/Scripts/03%20Gameplay.lua#L272

"+" means held at the same time. "," means one after the other.  If a setting has more than one combination it will be listed on another line.

### Music Select

| Default combination | metrics setting | What it does |
| ------------------- | --------------- | ------------ |
| Left | PreviousSongButton | Previous song |
| Right | NextSongButton | Next Song |
| Start | (hardcoded) | Begin Song |
| Left+Right+Select| (hardcoded) | Opens sort prompt |
| Left,Left,Right,Right| (hardcoded) | Exit |
| Start, Start<br>OR<br>Holding Start | (hardcoded) | Open Options Screen |
| Select | (hardcoded) | Open Options List |
| (Not used) | PreviousDifficultyButton | Switches to the previous difficulty. By default, CodeDetector is used instead. |
| (not used) | NextDifficultyButton | Switches to the next difficulty. By default, CodeDetector is used instead. |
| Ctrl+any letter | (hardcoded) | Switches the sorting to alphabetical and then jumps to the letter you've pressed. |

Start, Start or Holding Start opens the options screen if metric "OptionsMenuAvailable" is true.

Select opens options list if metric "UseOptionsList" is true. (Using the select button to open the options list is hardcoded and can't be changed, but you can add an additional combo to open the OptionsList using CodeDetector.)

| Default combination | CodeDetector setting | What it does |
| ------------------- | -------------------- | ------------ |
| Left+Right<br>OR<br>MenuLeft-MenuRight | NextSort1<br>NextSort2<br>NextSort3<br>NextSort4 | Cycle between sorting modes (in some themes)|
| MenuUp, MenuRight, MenuRight | NextGroup | Jump to next folder |
| (no default) | PrevGroup | Jump to previous folder |
| Up, Down, Up, Down<br>OR<br>MenuUp, MenuDown, MenuUp, MenuDown | ModeMenu1<br>ModeMenu2 | Open up the sorting selection menu (in some themes) |
| MenuUp-MenuDown | CloseCurrentFolder | Close the current folder |

Use _Up, Up_, _MenuUp, MenuUp_, _Down, Down_ or _MenuDown, MenuDown_ for change difficulty.

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