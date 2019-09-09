Preferred Sort is a way to create custom song groups in the Music Wheel without rearranging the physical location of the songs on your hard drive. There are plenty of reasons to do this, for example a folder of routine songs, combining folders, a folder of your favorite songs, etc.

# Step 1. How to create the file
Create a text file in the Other folder of your theme.
* If you would like to use more than one Preferred Sort at a time or change the sort with lua, choose a name and prefix it with `SongManager `. (Examples: `SongManager Special.txt`, `SongManager Basic.txt`, `SongManager MyAwesomeCustomSort.txt`)
* If you only want to use one preferred sort and you want it set by default, name it `SongManager PreferredSongs.txt`.

# Step 2. Valid preferred sort entries
Song folders in the preferred sort are optional, but you can use them if you'd like. To add a song group, put `---` and then the name of your group, then put the songs you want on the next lines.

For a song you can do `SongGroup/SongFolder` or just `SongFolder`, where `SongGroup` is the name of the song group and `SongFolder` is the folder the song is in.

To add every single song in a group, do `SongGroup/*`

A group named "Unlocks" will be pushed to the bottom of the groups list. Groups with 0 valid songs will not be added.

### Example File
```
---Special Songs
01 Special/*
02 Mixtapes/*
---StepMania
StepMania 5/Springtime
```
In this example every song from the folders `01 Special` and `02 Mixtapes` is being added to a group named `Special Songs` and the song `Springtime` in the `StepMania 5` folder is being added to a group named `StepMania`.

# Step 3. Setting the wheel to preferred sort

### Manual way
In ScreenSelectMusic, run this lua somewhere. (NameOfMySort is what you named your preferred sort, of course. In this example it would be loading `Other/SongManager NameOfMySort.txt`)
```lua
SCREENMAN:GetTopScreen():GetMusicWheel():ChangeSort("SortOrder_Preferred");
SONGMAN:SetPreferredSongs("NameOfMySort.txt");
```

### Metrics way
Make sure your text file in the Other folder of your theme is named `SongManager PreferredSongs.txt`.

In the `[ScreenSelectMusic]` section of your metrics.ini, add `DefaultSort="Preferred"`.

# Bonus: Using lua to write custom preferred sorts
There are more novel ways to use preferred sorts than just making a preferred sort by hand and then setting it. For example: A favorites manager which creates a preferred sort that adds a group with your favorite songs after you select your profile, a preferred sort that contains only easy songs, etc.

(TODO)