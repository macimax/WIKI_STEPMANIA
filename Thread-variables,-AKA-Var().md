list of variables you can pull from Var()

## GameCommand
Used to get the name of ActorScroller items in metrics.

For example if you're using an ActorScroller for ScreenSelectPlayMode and one of your choices looks like this:
`ChoiceStandard="applydefaultoptions;name,Standard;text,Normal;playmode,regular;difficulty,easy;screen,ScreenSelectMusic;setenv,sMode,Normal"`

Then if you want to show unique icons per choice with ScreenSelectPlayMode Icon, you can obtain the name field of the choice and the text field of the choice by getting the GameCommand variable and doing GetText() and GetName().

Example of it in action:
```lua
local gc = Var("GameCommand"); --Grab GameCommand variable
local text = gc:GetText() --The name field from a choice defined in metrics
local name = gc:GetName() --The text field from a choice defined in metrics

return Def.ActorFrame{
    LoadActor(name)..{};
    LoadFont("Common Normal")..{
        Text=text;
    };
}
```

## LoadingScreen
Returns the name of the current screen.