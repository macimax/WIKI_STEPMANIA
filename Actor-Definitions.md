This is a list of Actor classes available to SM5's Lua API along with the constructors and commands each takes.

If you are looking for functions specific to each Actor class (i.e., not `InitCommand`, `OnCommand`, etc.), then open the Docs/Luadoc/Lua.xml file included with your StepMania installation or view the [online API docs](http://dguzek.github.io/Lua-For-SM5/LuaAPI).

---

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

## StartTransitioningCommand

This is supposed to play when a screen activates its transition to go to the next screen, but there are irregularities as to when it plays.

The behaviour of this command is different between 5.1 and 5.3. In 5.1 it will play at the same time as an OnCommand.

Supposedly StartTransitioningCommand will be fired when the screen begins to transition to the next screen, so it being played when the screen reaches its "On" state in 5.1 should be regarded as a glitch, not intended behaviour?

In Transition.cpp:
```cpp
void Transition::StartTransitioning( ScreenMessage send_when_done )
{
    if( m_State != waiting )
        return;	// ignore
	
    // If transition isn't loaded don't set state to transitioning.
    // We assume elsewhere that m_sprTransition is loaded.
    if( !m_sprTransition.IsLoaded() )
        return;
	
    m_sprTransition->PlayCommand( "StartTransitioning" );

    m_MessageToSendWhenDone = send_when_done;
    m_State = transitioning;
}
```

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
Special actor with multiple vertices. Refer to [Docs/Themerdocs/ScreenAMVTest overlay.lua](https://github.com/stepmania/stepmania/blob/5_1-new/Docs/Themerdocs/ScreenAMVTest%20overlay.lua) for more information. 
# ActorProxy
A special actor that renders exactly like the actor you're cloning.

DOES NOT support diffusing, it is rendered as is. You can zoom it or move it, though.

Example:
```lua
Def.ActorFrame{
    Def.Sprite {
        Name="Background";
        Texture=THEME:GetPathG("Videos","Background");
    };
    Def.ActorProxy {
        Name="Banner2";
        OnCommand=function(self)
            self:SetTarget(self:GetParent():GetChild("Background"));
        end;
    };
}
```
# ActorScroller
Actor with children that allows you to scroll between them.
Refer to [Docs/Themerdocs/Examples/Example_Actors/ActorScroller.lua](https://github.com/stepmania/stepmania/blob/5_1-new/Docs/Themerdocs/Examples/Example_Actors/ActorScroller.lua) for more information.

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
## ScrollerSubdivisions
Normally the scroller will only calculate the next point for the actor to scroll towards in the TransformFunction. Setting this to a value above 1 will add a point for it to tween towards before stopping at the end point.
(In English: you can make circular strollers with it.)

## ~~GainFocusCommand & LoseFocusCommand~~

These two commands are not part of an ActorScroller. In fact, they're from ScreenSelectMaster. However since the two classes are nearly identical people expect GainFocus & LoseFocus to be in ActorScroller too... Unfortunately you'll have to write a workaround.

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
The same as Font except you have to provide a full path. (This has been deprecated for years, but it still hasn't been removed. At this point it's unlikely to ever get removed so you're probably fine to continue using it.)  Providing a full path to the font's ini file like this is currently the only way to load a custom Font into a BitmapText actor within the context of a Lua-scripted simfile.

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
An ActorScroller that can add and delete children on the fly.

It has no lua bindings, so it's useless to the end user.
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

You can set texture hints in the filename of a sprite. They do various things. For example: `testimage (stretch) (doubleres).png` sets the stretch and doubleres hint.

| hint | what it does |
| ---- | ------------ |
| doubleres | Indicates that the image is high resolution and should be displayed at half the size your theme would normally display actors (The size of actors is determined by the ScreenHeight metric). This is useful when you want to make a 1080p theme without having to meticulously position your actors, so you use ScreenHeight=540 and give all the sprites the doubleres hint. |
| res 123x456 | Override the resolution of your graphic. 123 would be the width and 456 the height in this example. |
| dither | ??? |
| stretch | Allows usage of customtexturerect and texcoordvelocity commands without graphical corruption. |
| mipmaps | ??? |
| nomipmaps | ??? |
| grayscale | If the image is marked grayscale, then use all bits not used for alpha for the intensity.  This way, if an image has no alpha, you get an 8-bit grayscale; if it only has boolean transparency, you get a 7-bit grayscale. |
| alphamap | This indicates that the only component in the texture is alpha; assume all color is white. |
| 32bpp | Sets the color depth of the sprite to 32 bits. (I'm not sure why you'd ever need this) |
| 16bpp | Same thing as 32bpp except 16 bits. |

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

## FrameXXXX, DelayXXXX
The old way of setting frames and delays. Replace XXXX with a number. This may be beneficial in some situations because you can actually reuse an existing frame in the sprite. Example:
```lua
Def.Sprite{
    Texture="yukari 10x1.png";
    Frame0000=7; --Uses frame 7 in the sprite
    Delay0000=0;
    Frame0001=1; --Uses frame 1 in the sprite
    Delay0001=7.884;
};
```

## AnimationFinishedCommand

Executed when your animation is finished (If this is an animated sprite)

# StepsDisplay
# StepsDisplayList
# TextBanner
# WorkoutGraph