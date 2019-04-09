Under construction

# Step 1.
Copy and paste the [UnlockManager] section from _fallback into the metrics.ini of your theme somewhere, such as below `[Common]`.

# Step 2
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
