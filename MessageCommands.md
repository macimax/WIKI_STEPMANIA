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

params:
* Name, which is the name of the code you specified. So if you have `Codeleft="Left"` in metrics.ini and you press left, params.Name would be "left".
* PlayerNumber: Self explanatory.

### StorageDevicesChangedMessageCommand

Executed when the state of a memory card changes. (Refer to the MemoryCardState Enum for more info)

### Condition

While not exactly a command, it is something you can put inside your Actor. If it evaluates to false the Actor will not be shown.

Many more global commands can be found by looking at MessageManager.cpp in the source.

# Screen Specific

## ScreenSelectMusic

Note: You can probably find more in ScreenSelectMusic.cpp by checking what is broadcasted to MESSAGEMAN.

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

## ScreenGameplay

### LifeChangedMessageCommand

Activated whenever a player's life changes. Params include Player and LifeMeter.

If the lifebar is type is battery it will also have LivesLeft and LostLife.

### ScoreChangedMessageCommand

Activated whenever a player's score changes. Params include PlayerNumber and MultiPlayer.

### ComboChangedMessageCommand

Activated whenever a combo changes. Params include Player, OldCombo, and OldMissCombo, and also PlayerState and PlayerStageStats if they're currently present.

## ScreenNameEntryTraditional

### MenuTimerExpiredMessageCommand

Triggered when the timer reaches 0.

# ActorScroller specific

### GainFocusCommand

Triggered when the ActorScroller is selected

### LoseFocusCommand

Triggered when the ActorScroller is deselected