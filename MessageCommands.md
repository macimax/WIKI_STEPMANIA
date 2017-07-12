Below is a list of universal commands you can use inside Actors. They're also usable in ActorFrames, although not every function that works on an Actor will work on an ActorFrame.

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