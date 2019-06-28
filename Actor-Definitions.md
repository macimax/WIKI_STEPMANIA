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

# ActorFrameTexture

# ActorMultiTexture

# ActorMultiVertex
# ActorProxy
# ActorScroller
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

## File
Sets the font file. Example:
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
# ModIconRow
# PaneDisplay
# PercentageDisplay
# Quad
# RollingNumbers
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