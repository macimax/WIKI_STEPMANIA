#Data Locations

Modern operating systems have user profiles; by default, StepMania 5.0 and later store user data (such as score data and settings) within a folder in your operating system's home directory. The exact location varies by platform;

* **Windows**: `%APPDATA%\StepMania 5\`
* **Linux**: `~/.stepmania-5.0/`
* **macOS**: `~/Library/Application Support/StepMania 5/`

Songs and other add-ons can be loaded from StepMania's user data directory, using the subfolders provided within.

For songs, the folder hierarchy ''must'' be `Songs/Group name/Song folder`. Similarly, themes must be `Themes/Theme name/[theme folders and metrics.ini]`. If these folders are any deeper in hierarchy, SM will not load them properly.

#### macOS notes
The *~/Library* directory is hidden from Finder by default, which makes adding content on OS X somewhat cumbersome.  You can follow the instructions from the Wiki page on [Manually Changing Preferences](Manually-Changing-Preferences) but use the path provided above to access your StepMania profile directory.

## Portable Mode

In some cases, such as if you are running StepMania from a portable drive, or otherwise do not wish to store profile data in your home directory, StepMania can be configured to store user data within its installation directory instead&emdash;which was the default behaviour on older versions such as 3.9. 

To activate Portable Mode, create a blank text file named ``Portable.ini`` in the folder where StepMania was installed. User profile data is stored within a ``Save`` folder within the installation directory.

## Storing content in other locations

The [Preferences file](https://github.com/stepmania/stepmania/wiki/Preferences.ini) contains settings that can be used to load content, such as songs, courses, and add-ons, from locations different from the user data directory or where StepMania is installed. This is useful if you are running multiple builds of StepMania and wish to keep your song library synchronized between them, or if you want to store your content on a different hard drive or partition to conserve disk space.

You can add multiple paths on each Additional* preference by separating them with a comma.

For example:
`AdditionalSongFolders=C:/SomeFolder/Songs,E:/Coolpath/Songs`

Note: If you're on Windows, you must replace every backslash with a forward slash.

For example:
`AdditionalSongFolders=H:/StepMania5/Songs`

### AdditionalFolders

Adds additional content. The engine will treat the path similarly to the user data folder, so multiple subfolders of content and add-ons (i.e. "Songs", "NoteSkins", "Themes", etc.) can be placed inside it.

### AdditionalSongFolders

Adds additional songs. The engine will treat the path as a folder named `/AdditionalSongs/`, like for example `/AdditionalSongs/SomeGroupFolder/SomeSongHere/`

### AdditionalCourseFolders

Adds additional courses.
