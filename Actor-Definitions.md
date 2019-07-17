A list of classes and what constructors and commands they take.

**If you are looking for functions and not InitCommand, OnCommand, etc then open the Docs/Luadoc/Lua.xht file included with your StepMania installation or view it online [here](https://dguzek.github.io/Lua-For-SM5/API/Lua.xml)**

There are three ways of loading classes:
1. `LoadActor()`, which chooses the correct class and loads the file for you. In this example "Graphics/Reimu.png" is being loaded and LoadActor is choosing to load it as a Sprite class. (The .png on the end is not necessary, SM will pick the closest file name.)
```lua
LoadActor(THEME:GetPathG("","Reimu.png"))..{
    InitCommand=cmd(zoom,0.3;addy,2;animate,false);
};
```
2. Prefixing the class name with with `Def.` when used in a lua file, then using one of the constructors listed below.
```lua
Def.Sprite{
    Texture=THEME:GetPathG("","Reimu");
    InitCommand=cmd(zoom,0.3;addy,2;animate,false);
};
```
3. Using the `Class` constructor.

Example:
```lua
{
    Class=Sprite,
    Texture=THEME:GetPathG("","Reimu"),
    InitCommand=cmd(Center)
}
```

# Universal
These constructors & commands can be used in ANY class.

## InitCommand

Executed before the screen displays it's 'on' state. Useful for positioning your graphic.

## OnCommand

Executed as the screen is displayed. Useful for animations as the player enters a screen. Note that if StepMania has to process something during this screen the render thread will not update, so if you're planning on doing a heavy operation you should create a static screen using InitCommands instead.

## OffCommand

Executed as the screen is being exited (Ex: Player picked a choice in a menu)

## Condition
If this evaluates to false, the actor will not be created.
Example:
```lua
LoadActor("image")..{
    Condition=GAMESTATE:IsSideJoined(PLAYER_1);
};
```

## Name
Sets the name of the actor, allowing you to use `self:GetChild("Name")` in an ActorFrame and run commands on the child actor.
Example:
```lua
Def.ActorFrame{
    OnCommand=function(self)
        --This will get a handle on the below actor named 'ImageActor'.
        self:GetChild("ImageActor"):addx(100);
    end;
    LoadActor("image")..{
        Name="ImageActor";
    };
};
```
# Actor
Basic class that every other actor takes from.

# ActorFrame
Basic class that holds other actors.

## UpdateRate
Amount to multiply the delta time by when updating.

## FOV
The angular width of the field of view used to render children.

## VanishX & VanishY
The position of the vanishing point used for the FOV rendering.
example:
```
VanishX= _screen.cx,
VanishY= _screen.cy,
```

## Lighting
Whether to apply lighting. Incomplete implementation, do not use.

## AmbientColor, DiffuseColor, SpecularColor
Different color values used when lighting is applied.
```
AmbientColor= ".75,.75,.75",
DiffuseColor= "0,0,.25",
SpecularColor= ".25,0,0",
```
# ActorFrameTexture
Refer to Docs/Themerdocs/Examples/Example_Actors/ActorFrameTexture.lua for more information.

# ActorMultiTexture

# ActorMultiVertex
Special actor with multiple vertices.
# ActorProxy
# ActorScroller
Actor with children that allows you to scroll between them.

## NumItemsToDraw
Number of items to draw. Default is 7 if this parameter is omitted.
## SecondsPerItem
Time it takes to scroll to an item. Default is 1 if this parameter is omitted. Setting it to 0 will break scrolling.
## TransformFunction
Your basic transform function... Example:
```lua
TransformFunction=function(self,offset,itemIndex,numItems)
    self:y(32*offset)
end,
```
## GainFocusCommand

Triggered when the ActorScroller is selected. Can be used in any child item of the ActorScroller.

## LoseFocusCommand

Triggered when the ActorScroller is deselected. Can be used in any child item of the ActorScroller.

# ActorSound
# Banner
# BGAnimation
# BitmapText
LoadFont() is an alias for Def.BitmapText{}.

## Text
Sets the text of the BitmapText actor, obviously.
Example:
```lua
LoadFont("Common Normal")..{
    Text="Marisa Kirisame";
    OnCommand=cmd(decelerate,.6;addx,-120;diffusealpha,1);
};
```
## Font
Sets the font file using a font from the Fonts folder of your theme. Example which is functionally identical to the above LoadFont():
```lua
Def.BitmapText{
    Font="Common Normal";
    Text="Marisa Kirisame";
    OnCommand=cmd(decelerate,.6;addx,-120;diffusealpha,1);
};
```
## File
The same as Font except you have to provide a full path. (This has been depreciated for years, but it still hasn't been removed. At this point it's unlikely to ever get removed so you're probably fine to continue using it.)

LoadFont() uses this internally.

Example:
```lua
Def.BitmapText{
    File=THEME:GetPathF("Common","Normal");
    Text="Marisa Kirisame";
    OnCommand=cmd(decelerate,.6;addx,-120;diffusealpha,1);
};
```

# BPMDisplay
# ComboGraph
# ControllerStateDisplay
# CourseContentsList
# DeviceList
# DifficultyIcon
# DynamicActorScroller
# FadingBanner
# GradeDisplay
# GraphDisplay
# GrooveRadar
# HelpDisplay
# HoldJudgment
# InputList
# LogDisplay
# MemoryCardDisplay
# MeterDisplay
# Model
Class that loads models.
## Materials, Meshes,Bones
The Materials, Meshes, and Bones for the model of course. The full path must be supplied.

# ModIconRow
# PaneDisplay
# PercentageDisplay
# Quad
# RollingNumbers
Class that has numbers that 'roll' up or down to the next set number instead of jumping to the number.

They are a child of a BitmapText, however their 'constructors' are set through metrics.

A basic example of a RollingNumbers defined in metrics:
```ini
[RollingNumbersExample]
Fallback="RollingNumbers"

TextFormat="%04.0f"
ApproachSeconds=10
Commify=true
LeadingZeroMultiplyColor=Color.Orange
```
Which is then loaded in lua:
```lua
Def.RollingNumbers{
    -- RollingNumbers derives from BitmapText, so you're gonna need a font.
    Font="Common Normal",

    -- The Text field is ignored.

    -- Let's load the metrics and set our target number
    -- If you don't call Load, your RollingNumbers actor will not be rendered
    -- and you won't be able to set the target number.
    OnCommand= function(self)
        self:Load("RollingNumbersExample"):targetnumber(1000)
            :xy(_screen.cx, _screen.cy - 100)
    end
};
```

## TextFormat
How many trailing zeroes you want, using the format "xx.0f", where xx is the number.
## ApproachSeconds
How many seconds it takes to reach the target number (explained later)
## Commify
Whether or not to use commas every 3 digits, i.e. 1,000 vs 1000. Commify can only be true or false.
## LeadingZeroMultiplyColor
The color of the closest zero to the number. For example, if you were to make LeadingZeroMultiplyColor red, and your RollingNumber was at 100 with a TextFormat of "%04.0f", then then the zero before the 1 (0100) would be red.


# ScoreDisplayAliveTime
# ScoreDisplayCalories
# SongBPMDisplay
# SongMeterDisplay
# Sound
## File
The file for this sound to load.
## SupportPan
set to `true` or `false`, defaults to false if omitted. When set to `true` the command `playforplayer()` is usable.
## SupportRateChanging
set to `true` or `false`, defaults to false if omitted. When set to true the RageSound can be adjusted.
## IsAction
set to `true` or `false`, defaults to false if omitted. When set to true it will be muted if MuteActions is on.
# Sprite
Sprite class for displaying static or animated sprites. Will also play video files.
## Texture
Sets the texture of the sprite.
## Frames
A table containing the frame rate of your animated sprite. For example:
```lua
Def.Sprite{
	Name= "title",
	Texture= "Idle 11x1",
	Frames= {
		{Frame= 0, Delay= 0.025},
		{Frame= 1, Delay= 0.03},
		{Frame= 2, Delay= 0.025},
		{Frame= 3, Delay= 0.03},
		{Frame= 4, Delay= 0.025},
		{Frame= 5, Delay= 0.03},
	}
},
```
Alternative example with the third and fourth arguments supplied:
```lua
{
{Frame= 0, Delay= .016, {0, 0}, {.25, .25}},
{Frame= 1, Delay= .016, {0, 0}, {.25, .25}},
{Frame= 2, Delay= .016, {0, 0}, {.25, .25}},
{Frame= 3, Delay= .016, {0, 0}, {.25, .25}},
}
```
Frame is optional, defaulting to 0.

Delay is optional, defaulting to 0.

The two tables are optional upper left and lower right corners of the fraction of the frame to use.  The example makes the sprite only use the upper left corner of each frame.

Normally one would use the command 'SetAllStateDelays' if their sprite has the same delay for each frame of animation instead of using the Frames constructor.

## AnimationFinishedCommand

Executed when your animation is finished (If this is an animated sprite)

# StepsDisplay
# StepsDisplayList
# TextBanner
# WorkoutGraph