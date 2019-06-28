A list of classes and what constructors they take. All classes are prefixed with `Def.` when used in a lua file.

# Universal
These constructors can be used in ANY class.
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
Sets the font file using a font from the Fonts folder of your theme. Example:
```lua
Def.BitmapText{
    Font="Common Normal";
    Text="Marisa Kirisame";
    OnCommand=cmd(decelerate,.6;addx,-120;diffusealpha,1);
};
```
## File
The same as Font except you have to provide a full path. (This has been depreciated for years, but it still hasn't been removed. At this point it's unlikely to ever get removed so you're probably fine to continue using it.)

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
# Sprite
Sprite class for displaying static or animated sprites.
## Texture
Sets the texture of the sprite.
# StepsDisplay
# StepsDisplayList
# TextBanner
# WorkoutGraph