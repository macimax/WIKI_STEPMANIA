# Additional files
Note: If you're on Windows, you must replace every backslash with a forward slash.

For example:
`AdditionalSongFolders=H:/StepMania5/Songs`

## AdditionalCourseFolders

Adds additional courses.

## AdditionalSongFolders

Adds additional songs. The engine will treat the path as a folder named `/AdditionalSongs/`, like for example `/AdditionalSongs/SomeGroupFolder/SomeSongHere/`

## AdditionalFolders

Adds additional folders.

# Memory Cards

If you want to set up memory cards, you'll find better help on [this page](https://github.com/stepmania/stepmania/wiki/Creating-Static-Mount-Points-For-USB-Profiles-(Linux)). The options are listed here for completion.

## MemoryCards

`1` to enable, `0` to disable.

## MemoryCardOsMountPointP1 & MemoryCardOsMountPointP2

The mount points of your memory card for each player. If you are one windows, you must replace the backslash with a forward slash.

Example: `MemoryCardOsMountPointP1=G:/`

## MemoryCardProfileSubdir

The name of the folder that stores the data on the memory card.

For example, `MemoryCardProfileSubdir=StepMania 5` will make a folder named `StepMania 5` and save all data in that folder after the player plays a round with a card inserted.

## MemoryCardProfileImportSubdirs

Imports old profile subdirectories into new ones. For example, `MemoryCardProfileImportSubdirs=StepMania 5 Old` will import a profile from the directory named `StepMania 5  Old` on your memory card into the new directory you specified in the above setting.

## MemoryCardProfiles

Boolean setting. Unknown function. Enables profiles on the memory cards?

## MemoryCardUsbBusP1 & MemoryCardUsbBusP2

`-1` to disable. Might be used for importing a drive by USB bus instead of by letter.

## MemoryCardUsbLevelP1 & MemoryCardUsbLevelP2

`-1` to disable. Unknown.

## MemoryCardUsbPortP1 & MemoryCardUsbPortP2

`-1` to disable. Might be used for mounting a device by USB port instead of by letter.

# Graphical settings

## VideoRenderers

Allows you to set the video renderer. Usually this setting is just `d3d, opengl`.

## TrilinearFiltering

???

## VisualDelaySeconds

Sets the visual delay in seconds & decimals. Default is `0.000000`.

## Vsync

Vertical sync. `0` is off, `1` is on.

## Windowed

...I think this one is obvious. `0` is off, `1` is on.

## PAL

???

## MovieColorDepth

Color depth of movies. Either `16` or `32`.

## DisplayColorDepth

Color depth of StepMania. Either `16` or `32`.

## MovieDrivers

???

## HighResolutionTextures

Enables high res textures.

## DisplayAspectRatio

The aspect ratio of the resolution. This probably shouldn't be touched unless the options menu doesn't have your obscure aspect ratio.

## DisplayHeight & DisplayWidth

Height and width of the StepMania window.

## Interlaced

`1` for on, `0` for off.

## RefreshRate

The refresh rate of StepMania. Usually `60`.

## DisableScreenSaver

`1` disables the screen saver. (My screensaver still activates with this on, so I don't think it works...)