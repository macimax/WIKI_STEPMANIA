Below is a list of commands you can use inside Actors. They're also usable in ActorFrames, although not every function that works on an Actor will work on an ActorFrame.

Note: This list is incomplete.

# Universal Commands

### InitCommand

Executed before the screen displays it's 'on' state. Useful for positioning your graphic.

### OnCommand

Executed as the screen is displayed. Useful for animations as the player enters a screen. Note that if StepMania has to process something during this screen the render thread will not update, so if you're planning on doing a heavy operation you should create a static screen using InitCommands instead.

### OffCommand

Executed as the screen is being exited (Ex: Player picked a choice in a menu)

### AnimationFinishedCommand

Executed when your animation is finished (If you have one)

### CodeMessageCommand

Executed when any button is pressed. You must have CodeNames set in the respective screen in metrics.ini for this to function correctly.

| Parameters | Description |
| ---------- | ----------- |
| Name | the name of the code you specified. So if you have `Codeleft="Left"` in metrics.ini and you press left, params.Name would be "left" |
| PlayerNumber | PLAYER_1 or PLAYER_2 |

### StorageDevicesChangedMessageCommand

Executed when the state of a memory card changes. (Refer to the MemoryCardState Enum for more info)

### Condition

While not exactly a command, it is something you can put inside your Actor. If it evaluates to false the Actor will not be shown.

Many more global commands can be found by looking at MessageManager.cpp in the source.

# Screen Specific

## ScreenSelectMusic

Note: You can probably find more in ScreenSelectMusic.cpp by checking what is broadcasted to MESSAGEMAN.

### SetMessageCommand
This command also works in Course mode.

Broadcast when a MusicWheelItem is being set with new information, such as when scrolling up and down. Can access parameters using SetMessageCommand=function(self, params)

| Parameters | Description |
| ---------- | ----------- |
| Song | An instance of the Song that was just set to the MusicWheelItem. |
| Course | If in course mode, an instance of the Course that was just set to the MusicWheelItem. |
| Index | The index of the MusicWheelItem that was just set. |
| HasFocus | If the MusicWheelItem is focused or not. |
| Text | The name of the song group this MusicWheelItem is from? |


### CurrentStepsPXChangedMessageCommand

Replace 'X' with either 1 or 2 (for the player number). Triggered when the currently selected steps change, whether it be by changing the difficulty or selecting another song.

### CurrentSongChangedMessageCommand

Self explanatory.

### PreviousSongMessageCommand or NextSongMessageCommand

Triggered when the player selects a different song in the songwheel by tapping left or right.

### ChangeStepsMessageCommand

Also probably works in ScreenSelectCourse. Triggered when steps are changed. Need to check player & direction using ChangeStepsMessageCommand=function(self, params) then params.Player and params.Direction.

params.Player is always PLAYER_1 or PLAYER_2 and params.Direction is always 1 or -1.

## ScreenSelectCourse

### CurrentCourseChangedMessageCommand

Self explanatory.

### CurrentTrailPXChangedMessageCommand

Replace 'X' with either 1 or 2 (for the player number). Triggered when the Trail is changed. Might work in other screens?
## OptionsList
### OptionsListOpened / OptionsListClosed
Triggered when a player opens/closes the OptionsList.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |

### OptionsListQuickChange
Triggered when a player changes their selection on the OptionsList by pressing a button. Only broadcast when the list type is SELECT_ONE.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Direction | Either 1 or -1. |
| Selection | The index of the currently selected item? |
### OptionsListLeft / OptionsListRight
Triggered when a player presses left/right?

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Selection | The index of the currently selected item? |
### OptionsMenuChanged
Triggered when the player enters or exits a menu in the OptionsList.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Menu | The name of the the new menu in the OptionsList, as defined in metrics under ScreenOptionsMaster. |
### OptionsListPop
Unknown, possibly when the player exits from an OptionsList submenu.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
### OptionsListPush
Same as above except when entering a submenu.
### OptionsListStart
Unknown.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
### OptionsListReset
Triggered when they press the reset button in the OptionsList, resetting their modifiers to ModsLevel_Preferred.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |

## ScreenGameplay

### LifeChangedMessageCommand

Activated whenever a player's life changes.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| LifeMeter | Amount of life in a decimal from 0 to 1 |

If the lifebar is type is battery it will also have LivesLeft and LostLife.
### HealthStateChangedMessageCommand

Activated whenever a player's health state changes...

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| HealthState | A HealthState Enum, which is either `HealthState_Hot`, `HealthState_Alive`, `HealthState_Danger`, or `HealthState_Dead`. |
| OldHealthState | self explanatory. |

### PlayerFailedMessageCommand
This one's obvious.

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |

### ScoreChangedMessageCommand

Activated whenever a player's score changes. Params include PlayerNumber and MultiPlayer, but can also include ToastyCombo in certain cases.

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| MultiPlayer | ??? |
### JudgmentMessageCommand
Triggered when a judgment happens, either because a player stepped on a note or they completely missed it.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| MultiPlayer | If they're multiplayer, probably |
| TapNoteSccre | The TapNoteScore |
| Early | True if early, false if late |
| TapNoteOffset | Offset of the judgement |
| HoldNoteScore | The HoldNoteScore |

### ComboChangedMessageCommand

Activated whenever a combo changes.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| OldCombo | ??? |
| OldMissCombo | ??? |
| PlayerState | An instance of PlayerState. This may not always be present. |
| PlayerStageStats | An instance of PlayerStageStats. This may not always be present. |

### ToastyAchievedMessageCommand

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| ToastyCombo | ??? |
| Level | ??? |

### ToastyDroppedMessageCommand

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
### DoneLoadingNextSongMessageCommand

Unknown, might be triggered during course mode


## ScreenNameEntryTraditional

### MenuTimerExpiredMessageCommand

Triggered when the timer reaches 0. (Why this even exists is unknown)

# ActorScroller specific

### GainFocusCommand

Triggered when the ActorScroller is selected

### LoseFocusCommand

Triggered when the ActorScroller is deselected