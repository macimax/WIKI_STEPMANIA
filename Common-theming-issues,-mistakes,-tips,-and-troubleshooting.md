# Issues/Troubleshooting
## Code is not executing
- If this is a new file, make sure you hit F2 to reload and check for new resources.
- Is the file in the correct place and named correctly?
- Is error reporting enabled? (F3+F6, make sure "show errors" is not greyed out)
- Make sure this file is not a duplicate of an existing screen, such as a ScreenTitleMenu overlay folder and then a lua file named ScreenTitleMenu overlay.lua.

## "must return an actor" error when entering screen
You probably forgot to return the ActorFrame table in one of your files.

## "invalid class" or "unknown class" error when entering a screen
You might be returning a table instead of an Actor.

## SCREENMAN:SystemMessage() does not work
BGAnimations/ScreenSystemLayer overlay has been overwritten and is missing the messagecommand required to show messages.

## Actor not appearing in ActorFrame
If you've manually inserted it into the ActorFrame at a specific index, remember that lua is 1-indexed and actors at an index of 0 and below will not be compiled.

# Common beginner mistakes and solutions
List of things that beginners do. Don't do this!! Every beginning themer should read this before it's too late and you have to spend hours fixing your theme!
## Lack of ActorFrames / Not understanding the purpose of an ActorFrame
Example 1 of what not to do:
```lua
t[#t+1] = Def.ActorFrame{
  LoadActor("Sprite1")..{
    InitCommand=cmd(xy,200,300);
  };
  LoadActor("Sprite2")..{
    InitCommand=cmd(xy,200,350);
  };
  LoadActor("Sprite3")..{
    InitCommand=cmd(xy,200,400);
  };
  LoadActor("Sprite4")..{
    InitCommand=cmd(xy,200,450);
  };
};
```
In this example, only the y value is changing, and it's only changing by 50 steps every time. Plus if you want to change the position to say, x=200 and y=500, you'd have to adjust the position of all four items. This defeats the purpose of using an ActorFrame in the first place.

The correct solution is to do your positioning inside the ActorFrame, then adjust the offset of the item within the item.
```lua
t[#t+1] = Def.ActorFrame{
  --This positions the ActorFrame and all objects inside it at 200,300.
  --If you ever need to move the position of all the objects inside this
  --ActorFrame, you can change this command only.
  InitCommand=cmd(xy,200,300);
  LoadActor("Sprite1")..{
    --This sprite is not being adjusted, so there is no command needed.
    --InitCommand=cmd(y,0);
  };
  LoadActor("Sprite2")..{
    --[[
    This sprite is being adjusted by 50 pixels. It's position on the screen
    is the position of the ActorFrame plus any xy commands.
    The resulting position of this object is 350.
    ]]
    InitCommand=cmd(y,50);
  };
  LoadActor("Sprite3")..{
    InitCommand=cmd(y,100);
  };
  LoadActor("Sprite4")..{
    InitCommand=cmd(y,150);
  };
};
```

Example 2 of what not to do:
```lua
--There is no positioning code here, it's all done inside the "MyCoolActor.lua" file
t[#t+1] = LoadActor("MyCoolActor");
```
After reading the above, you can probably figure out why this is a bad idea.

## Making a file/actor then copypasting it for player 2
**NOOOOOO!!!!!! DO NOT DO THIS!!!!!!!!** You are only making it harder for you and everyone else to debug your theme if you do this. You are making it take twice as long to implement your features if you do this. Seriously, **do not do this**.
```lua
t[#t+1] = LoadActor("MyCoolSprite_P1")..{
    InitCommand=cmd(xy,300,SCREEN_CENTER_Y;player,PLAYER_1);
  };
t[#t+1] = LoadActor("MyCoolSprite_P2")..{
    InitCommand=cmd(xy,SCREEN_WIDTH-300,SCREEN_CENTER_Y;player,PLAYER_2);
  };
```
Instead:
```lua
--This will load it only if the player is joined, so it doesn't load an unnecessary sprite and then make it invisible.
--If you want to load it anyway (in case LateJoin is enabled), use "for player in ivalues(PlayerNumber)"
for player in ivalues(GAMESTATE:GetEnabledPlayers()) do
  --This loads "MyCoolSprite_P1" or "MyCoolSprite_P2"
t[#t+1] = LoadActor("MyCoolSprite_"..pname(player))..{
    InitCommand=function(self)
      --For player 1 it will be on the left, for player 2 it will be on the right
      if player == PLAYER_1 then
        self:x(300)
      else
        self:x(SCREEN_WIDTH-300)
      end
      self:y(SCREEN_CENTER_Y);
    end;
  };
end
```
You might be asking "Okay, but my code is another lua file! How do I pass in the player?". Well, that's what the second argument of LoadActor is for.
Let's say you have a file named "label.lua"
```lua
t[#t+1] = LoadActor("Label");
```
You can supply the player (or anything, actually) as the second argument to LoadActor, where it will be passed in as a variable named `...`.
```lua
t[#t+1] = LoadActor("Label", PLAYER_1);
```
Then in the first line of Label.lua:
```lua
local player = ...
```
## Variable allocation then usage than discarding
This is fairly obvious. Don't allocate memory if you don't need to, only do it when you need to use a variable more than once.
```lua
CurrentSongChangedMessageCommand=function(self)
  local song = GAMESTATE:GetCurrentSong();
  if song then --Song is only being used once
    local meter = GAMESTATE:GetCurrentSteps(PLAYER_1):GetMeter(); --meter is only being used once
    self:settext(meter);
  end;
end;
```
This function could be changed to this:
```lua
CurrentSongChangedMessageCommand=function(self)
  if GAMESTATE:GetCurrentSong() then
    self:settext(GAMESTATE:GetCurrentSteps(PLAYER_1):GetMeter());
  end;
end;
```
(Of course, you are free to ignore this one if you don't care about wasting memory)

## Using cmd
cmd() has a performance penalty because it has to be translated.
```lua
Def.Quad{
    OnCommand=cmd(addx,-300;linear,0.15;addx,300);
}
```
Use function(self) instead.
```lua
Def.Quad{
    OnCommand=function(self) self:addx(-300):linear(0.15):addx(300) end;
}
```
(Of course, you are free to ignore this one if you don't care about causing lag)

## Putting both P1 and P2 messagecommands when not needed
Let's say you have a function that returns an Actor and one of the parameters for that function is the player. But CurrentStepsChanged is an old style of MessageCommand, so you think it's impossible and put both in. Don't do this.
```lua
CurrentSongChangedMessageCommand=cmd(playcommand,"Set");
CurrentStepsP1ChangedMessageCommand=cmd(playcommand,"Set");
CurrentStepsP2ChangedMessageCommand=cmd(playcommand,"Set");
CurrentTrailP1ChangedMessageCommand=cmd(playcommand,"Set");
CurrentTrailP2ChangedMessageCommand=cmd(playcommand,"Set");
```
The solution (assume player is a variable that is either PLAYER_1 or PLAYER_2):
```lua
["CurrentSteps"..pname(player).."ChangedMessageCommand"]=cmd(playcommand,"Set");
["CurrentTrail"..pname(player).."ChangedMessageCommand"]=cmd(playcommand,"Set");
```
This will ensure your actor only listens to the commands it needs.

## Making a function to map an enum to an int
Far too many people do this because they don't realize the Reverse() function exists.
```lua
local function GetDiffAsInt(diff)
  if diff == "Difficulty_Beginner" then
    return 0
  elseif diff == "Difficulty_Easy" then
    return 1
  elseif diff == "Difficulty_Medium" then
    --(you get the idea)--
  end
end;
```
This entire function could be replaced with
```lua
local function GetDiffAsInt(d)
    return Difficulty:Reverse()[d];
end;
```

## Creating an array for an existing enum
```lua
local difficulties = {"Difficulty_Beginner", "Difficulty_Easy", "Difficulty_Medium", "Difficulty_Hard", "Difficulty_Challenge", "Difficulty_Edit"}
```
enums are iterable. this is the same as `local difficulties = Difficulty`. In fact you don't need to declare a variable at all, because you can access a value from the enum using Enum[i] where i is the position to access. Ex. `Difficulty[1]` returns `"Difficulty_Beginner"`.

## copypasted actors that use enums
Enums are iterable with for loops. You don't need to copy and paste the actor you're trying to generate every time.
```lua
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Beginner')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Easy')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Medium')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Hard')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Challenge')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
t[#t+1]=DrawDifList(PLAYER_2,'Difficulty_Edit')..{
  OffCommand=cmd(linear,0.25;addx,500);
};
```
The entire thing could be shortened to
```lua
for diff in ivalues(Difficulty) do
  t[#t+1]=DrawDifList(PLAYER_2,diff)..{
    OffCommand=cmd(linear,0.25;addx,500);
  };
end;
```