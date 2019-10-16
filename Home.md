# Welcome!

StepMania is a free and open source, cross-platform rhythm game. It supports common key-based rhythm game formats (including 4-panel and 5-panel dance games among others), as well as keyboard and dance pad controllers. It is customizable with user-made add-ons such as themes, and provides an integrated editor for creating your own simfiles. 

StepMania can also be used with dance game cabinets, and has been used as the basis for several major commercial products including _Pump it Up Infinity_ and _StepManiaX_.

Hey, listen!
------------
The docs need a TON of work! Please ask on the forums and suggest anything you think should be in here. We devs know way too much detailed technical stuff and it's hard to pick up what people actually want to know - so any requests for documentation are really welcomed.


Configuration & Setup
------------
* [The Beginner's Guide](https://raw.githubusercontent.com/stepmania/stepmania/5_1-new/Docs/Userdocs/sm5_beginner.txt) - a general guide for new players
* [System requirements](Minimum-Requirements)
* [Installing StepMania](Install-Guide) - install guide for Windows, macOS, and Linux
* [Customizing StepMania](Customization) - information about custom themes, noteskins, and announcers
* [Manually Changing Preferences](Manually-Changing-Preferences)


Basic Engine Info
------------
* [Versions](https://github.com/stepmania/stepmania/wiki/Versions)
* [User data locations](https://github.com/stepmania/stepmania/wiki/User-Data-Locations)
* [Supported file formats](https://github.com/stepmania/stepmania/wiki/File-Formats)
* [Supported games](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes)
* [Play modes](https://github.com/stepmania/stepmania/wiki/Play-Modes)
* [Courses](https://github.com/stepmania/stepmania/wiki/Courses)
* [Key Bindings](Key-Bindings-and-combinations)

Charting Help
------------
* [Note types](https://github.com/stepmania/stepmania/wiki/Note-Types)
* [Timing segments](https://github.com/stepmania/stepmania/wiki/Timing-Segments)
* [Label segments](https://github.com/stepmania/stepmania/wiki/Label-segments)
* [Note And Timing Gimmicks](https://github.com/stepmania/stepmania/wiki/Note-and-timing-gimmicks)
* [(advanced) NewField Mod System](https://github.com/stepmania/stepmania/wiki/NewField-mod-system)

Theming Help
------------
* [Theming](https://github.com/stepmania/stepmania/wiki/Theming)
* [Fonts](https://github.com/stepmania/stepmania/wiki/Fonts)
* [Noteskins](https://github.com/stepmania/stepmania/wiki/Noteskins)
* [MessageCommands](https://github.com/stepmania/stepmania/wiki/MessageCommands)
* [Commands & Constructors](https://github.com/stepmania/stepmania/wiki/Actor-Definitions)
* [Unlock System](Unlock-System)
* [Preferred Sort](Preferred-Sort)

Programming Help
------------
* [Compiling StepMania](https://github.com/stepmania/stepmania/wiki/Compiling-StepMania)
* [Adding new lua functions](https://github.com/stepmania/stepmania/wiki/Adding-new-lua-functions-to-the-source)


USB Profiles
------------
You may want to create static mount points for USB-based profiles. Doing so will allow you associate a USB port on your PC with a specific player's memorycard slot, as is common on arcade cabinets.

* [Static mount points for USB profiles (Linux)](Creating-Static-Mount-Points-For-USB-Profiles-%28Linux%29)
* [Static mount points for USB profiles (Windows)](Static-Mount-Points-for-USB-Profiles-(Windows))


Command Line Arguments
------------
StepMania accepts a number of command line arguments.

* `--theme="themename"` - Sets the theme to use.
* `--language=lang` - Sets the language to use.
* `--ExportLuaInformation` - Exports Lua documentation to `Lua.xml`.