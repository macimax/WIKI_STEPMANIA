# Custom Content

Songs, Themes, NoteSkins, Characters, and other custom content should be loaded from StepMania's *user data folder*, using the subfolders within.

This is different than older versions of StepMania (e.g. SM3.9) where all content was added directly the primary StepMania install folder.  Separating the application from your content makes it easier to install or upgrade to new versions of SM5 without accidentally deleting your content.

## Where to Install

The location of your *user data folder* varies by OS:

If you're using **SM5.0.12**:

<table>
<tbody>
  <tr>
    <td>Windows 10, 8, 7</td>
    <td>C:\Users\<code>USERNAME</code>\AppData\Roaming\StepMania 5\</td>
  </tr>
  <tr>
    <td>macOS</td>
    <td>/Users/<code>USERNAME</code>/Library/Application Support/StepMania 5/</td>
  </tr>
  <tr>
    <td>Linux</td>
    <td>/home/<code>USERNAME</code>/.stepmania-5.0/</td>
  </tr>
</tbody>
</table>

If you're using **SM5.1-beta**:

<table>
<tbody>
  <tr>
    <td>Windows 10, 8, 7</td>
    <td>C:\Users\<code>USERNAME</code>\AppData\Roaming\StepMania 5.1\</td>
  </tr>
  <tr>
    <td>macOS</td>
    <td>/Users/<code>USERNAME</code>/Library/Application Support/StepMania 5.1/</td>
  </tr>
  <tr>
    <td>Linux</td>
    <td>/home/<code>USERNAME</code>/.stepmania-5.1/</td>
  </tr>
</tbody>
</table>

In each of these paths, <code>USERNAME</code> will be your OS username.

🔷 Tip: If you find yourself adding content frequently, you may wish to create a shortcut there. The user content folder can be tedious to manually navigate to.

#### Windows notes

In Windows 10, you can find your AppData folder by typing `%appdata%` into the Windows search bar in your taskbar.

In older versions of Windows, you can type `%appdata%` into a *Run* dialog (<kbd>Windows key</kbd> + <kbd>R</kbd>).

#### macOS notes

The `~/Library/` folder is hidden from Finder by default, which makes adding content on macOS cumbersome.  You can [unhide the Library folder](https://apple.stackexchange.com/a/378378) or copy/paste the appropriate path from above into Finder's [*Go To Folder...* dialog](https://osxdaily.com/2011/08/31/go-to-folder-useful-mac-os-x-keyboard-shortcut/)

#### Linux notes

Many file managers (Nautilus for Ubuntu, Thunar for Mint's Xfce, etc.) will hide folders that begin with `.` by default, but allow you to toggle this on/off with <kbd>Control</kbd> + <kbd>H</kbd>.

## Portable Mode

In some cases, such as if you are running StepMania from a removable disk or otherwise do not wish to store custom content in your home directory, StepMania can be configured to read from its installation folder instead.  Longtime players may recognize this configuration as where custom content was installed for SM3.9.

To activate Portable Mode, create a blank text file named `Portable.ini` in the folder where StepMania was installed.  User data will now be stored within and loaded from a `Save` folder within the installation folder (for example, `./StepMania/Save/Songs/` and `./StepMania/Save/NoteSkins/`).

## Storing content in other locations

The [Preferences file](https://github.com/stepmania/stepmania/wiki/Preferences.ini) contains settings that can be used to load content, such as songs, courses, and add-ons, from locations different from the user data folder or where StepMania is installed. This is useful if you are running multiple builds of StepMania and wish to keep your song library synchronized between them, or if you want to store your content on a different hard drive or partition to conserve disk space.

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
