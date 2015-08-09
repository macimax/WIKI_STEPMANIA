Hey, listen!
-------
The docs need a TON of work! Please ask on the forums and suggest anything you think should be in here. We devs know way too much detailed technical stuff and it's hard to pick up what people actually want to know - so any requests for documentation are really welcomed.

On this page, you will find various StepMania documentation.

Data Locations
--------------
Modern operating systems have user profiles, which means certain files are in different locations from previous versions of StepMania.

A list of user data locations:

* __Windows__: `%APPDATA%/StepMania 5.0/`
* __Linux__: `~/.stepmania-5.0/`

### Mac OS
On Mac OS 10.7 (Lion) and newer, the Library directory in `/Users/<username>` is no longer readily accessible as it was in previous versions of Mac OS.

You can get there using the *Go to Folder...* command. It can be found in the *Go* menu at the top of your screen while on your Desktop.

You should install your user content via this path: `~/Library/Application Support/StepMania 5/`

and you can access your preferences via: `~/Library/Preferences/StepMania 5/`

Portable Mode
-------------
If you wish to make your copy of StepMania portable, create a blank file called `Portable.ini` in the StepMania install folder. This will create the various save folders in the directory itself. (As a side effect, this makes it similar to an install of [StepMania 3.9](versions/stepmania-3-9).)

Command Line
------------
StepMania accepts a number of command line arguments.

* `--theme="themename"` - Sets the theme to use.
* `--language=lang` - Sets the language to use.
* `--ExportLuaInformation` - Exports Lua documentation to `Lua.xml`.
