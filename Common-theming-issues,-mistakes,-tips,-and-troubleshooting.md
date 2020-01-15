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
List of things that beginners do. Don't do this!!
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