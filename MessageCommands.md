Below is a list of universal commands you can use inside Actors. They're also usable in ActorFrames, although not every function that works on an Actor will work on an ActorFrame.

There are probably more than this, and many many more that are screen specific.

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

### Condition

While not exactly a command, it is something you can put inside your Actor. If it evaluates to false the Actor will not be shown.

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

# ActorScroller specific

### GainFocusCommand

Triggered when the ActorScroller is selected

### LoseFocusCommand

Triggered when the ActorScroller is deselected