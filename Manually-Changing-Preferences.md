Most preferences can (and should) be set with StepMania's UI, but there are times when you may want to manually edit *Preferences.ini* where your settings are stored.

Before attempting to edit your *Preferences.ini* file, it is important to understand

+ StepMania expects specific values for each preference
+ many of these are not documented anywhere yet (we're working on it!)
+ providing an invalid value may cause StepMania to not work as expected (or at all)

With that established, if you wish to proceed, you'll need to quit StepMania first if it is actively running.  This will ensure that any changes you make manually will stick when you start StepMania next time.

# Finding *Preferences.ini*
The location of your *Preferences.ini* file depends on your operating system.

## Windows

SM5.0.x Path: `%appdata%\StepMania 5\Save\Preferences.ini`

SM5.1-beta Path: `%appdata%\StepMania 5.1\Save\Preferences.ini`


## macOS

SM5.0.x Path: `~/Library/Preferences/StepMania 5/Preferences.ini`

SM5.1-beta Path: `~/Library/Preferences/StepMania 5.1/Preferences.ini`

For better or worse, Apple hides the *Library* directory by default but there are a few ways to get there.

Finder's *Go* menu has a *Go To Folder...* item which brings up a dialog box.  Copy and paste the path provided above and click *Go*.

![Go To Folder... + Preferences.ini path](http://i.imgur.com/xrUN4gHh.png)

Alternatively, it is possible to [un-hide the Library directory from Finder](http://osxdaily.com/2014/12/16/show-user-library-folder-os-x-yosemite/) which would allow you to navigate it like any other folder.

## Linux

SM5.0.x Path: `~/.stepmania-5.0/Save/Preferences.ini`

SM5.1-beta Path: `~/.stepmania-5.1/Save/Preferences.ini`