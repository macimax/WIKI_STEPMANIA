
Under construction

# Updated "Custom" Unlock System

## Step 1.  Locking
In your metrics.ini file you need to tell the theme what songs are unlocks. Under **[UnlockManager]** add the following:

```ini
[UnlockManager]
AutoLockChallengeSteps=false
UnlockNames="1,2"
Unlock1Command=song,"DDR 4thMIX/.59";require,"UnlockRequirement_StagesCleared",0
Unlock2Command=song,"DDR 2ndMIX/MAKE IT BETTER (So-REAL Mix)";require,"UnlockRequirement_StagesCleared",0
```

### Explanation
Now, with the example above, it's locking **.59** from **4thMIX** and **MAKE IT BETTER (So-REAL Mix)** from **2ndMIX**.

The way these lines work is you need to identify them with the **UnlockNames** line. Whatever goes between the words **Unlock** and **Command** is what you put where the example has **"1,2"**. Using numbers helps so when you're setting what songs to unlock later, you can know which one you're unlocking without needing a long text line.

Then the next lines lock the specific songs. To select a song to lock you need to give the folder name then / then the songs folder name. Like this: **song,"GROUP FOLDER/SONG FOLDER";**

It doesn't matter what the requirement is because SM5 doesn't automatically unlock songs based on the "require" part of these lines from testing that's been conducted. But you still do need it there to lock the song so for this example, it's using: **require,"UnlockRequirement_StagesCleared",0**

So now if you close SM5 and reopen it, you'll notice that the songs you've listed are now hidden/locked on your music select screen.

**IMPORTANT NOTE:** If you edit the **[UnlockManager]** lines in your **Metrics.ini** you'll need to restart SM rather than just pressing F2 for the metrics to reload. The songs get locked while the songs are being cached before the game fully boots up. So they won't lock if you don't restart the game (if it's already open that is).

## Step 2.  Unlocking
In your themes folder under **BGAnimations\ScreenSelectMusic in** (you could do this elsewhere but this is where we're doing it for this example). Add the following in the default.lua:

```lua
if (PROFILEMAN:GetProfile(PLAYER_1):GetNumTotalSongsPlayed() >= 10)
or (PROFILEMAN:GetProfile(PLAYER_2):GetNumTotalSongsPlayed() >= 10) 
then
	UNLOCKMAN:UnlockEntryID('1')
else
	UNLOCKMAN:LockEntryID('1')
end
```

```lua
if (PROFILEMAN:GetProfile(PLAYER_1):GetNumTotalSongsPlayed() >= 20) 
or (PROFILEMAN:GetProfile(PLAYER_2):GetNumTotalSongsPlayed() >= 20) 
then
	UNLOCKMAN:UnlockEntryID('2')
else
	UNLOCKMAN:LockEntryID('2')
end
```

### Explanation
In this example these lines of code now unlock the songs based off number of songs played on the currently loaded profiles and locks the songs if they number of songs haven't been met. This is a long way to code it so you could make it more concise.

The breakdown for the code is as follows:

```lua
if (PROFILEMAN:GetProfile(PLAYER_1):GetNumTotalSongsPlayed() >= ##) 
or (PROFILEMAN:GetProfile(PLAYER_2):GetNumTotalSongsPlayed() >= ##) 
then
```

This condition checks if Player 1's profile _OR_ Player 2's profile have played greater than or equal to the number of songs you want to set as the songs unlock requirement.

In terms of the way these unlock, you're free check for whatever here - you could check for number of calories burnt, number of songs played, total jumps made by the player etc. Pretty much anything you can pull from the **PROFILE MANAGER (PROFILEMAN)** or elsewhere. This opens up a world of possibilities for an unlocking system and doesn't hold us back with just the few unlock options currently provided by the StepMania engine through UNLOCKMAN.

For example, if you placed this code on the Evaluation screen, you could even show what song was unlocked by the player. So the options and features you could tie to this are plentiful.

------------

```lua
UNLOCKMAN:UnlockEntryID('#')
```

This line unlocks the unlock ID that we set back in your Metrics.ini. This makes the song available if Player 1 or Player 2 have hit the milestone.

------------

```lua
UNLOCKMAN:LockEntryID('#')
```

This line locks the song if the requirements are not met.  If the song was already locked, it will stay locked.  This is an important line because once you set the song as "unlocked", it will remain unlocked until you lock it again.  So, if Player 1 unlocks it and you don't have the "lock" command here, it will remain unlocked for all players, even if they haven't passed the milestone.  This code is one strategy for keeping a song locked for each individual player until they meet the requirement themselves.

------------



# Built In Unlock System (Original)

## Step 1.
Copy and paste the [UnlockManager] section from _fallback into the Metrics.ini of your theme somewhere, such as below `[Common]`.

## Step 2
You can already see some examples of its usage in the section, but to start off, add a name to the `UnlockNames` field. Then use that name to make an unlock command for the song or course you want to lock.

For example:

```ini
UnlockNames="Unlock1"
Unlock1Command=song,"Pledge";require,"UnlockRequirement_ArcadePoints",500
```

Here is a list of the unlock requirements you can set:

| name | description | argument |
| ---- | ----------- | -------- |
| UnlockRequirement_ArcadePoints | Get a certain number of arcade points. | Num points to unlock |
| UnlockRequirement_DancePoints | Get a certain number of dance points (or EX-SCORE). | Num points to unlock |
| UnlockRequirement_SongPoints | Get a certain number of song points. | Num points to unlock |
| UnlockRequirement_ExtraCleared | Pass the extra stage. | None |
| UnlockRequirement_ExtraFailed | Fail the extra stage. | None |
| UnlockRequirement_Toasties | Get a number of toasties. | Num toasties to unlock |
| UnlockRequirement_StagesCleared | Clear a number of stages. | Num stages to unlock |
| UnlockRequirement_NumUnlocked | Have a number of locked items already unlocked. | Num items needed to unlock |
