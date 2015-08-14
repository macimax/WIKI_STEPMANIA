**This page is an in-progress info dump right now, it'll be sliced up into a bunch of other pages later!**

Theming
-------
Themes have changed a lot since the [StepMania 3.0](wiki/versions/stepmania-3-0) and [3.9](wiki/versions/stepmania-3-9) days. What was once merely an .ini file of metrics and a collection of graphics and BGAnimations has now become a scripting-capable environment.

With recent changes allowing StepMania to take advantage of operating system user profiles, Themes are now meant to be installed in the user data directory.

### Theming System ###
Unlike StepMania 3.9 and earlier, where every theme fell back on the default (SMMAX) theme, [StepMania 5](wiki/versions/stepmania-5-0) uses a system with a `_fallback` theme, allowing themers to not be confined by the choices made in the default theme. 

(In order to fully appreciate this, try making an evaluation screen in StepMania 3.9; you'd have to duplicate the metrics of each evaluation mode screen entirely in order to make your changes.)

That being said, if you are looking for where something is done and you don't see it in the default theme, it might be time to check the fallback.

### Folder Layout ###
A theme consists of various files and folders:

* `BGAnimations/` - Scripts that control screen backgrounds and behavior.
* `Fonts/` - Font graphics and `.ini` files.
* `Graphics/` - Theme graphics (and sometimes scripts to handle logic).
* `Languages/` - Theme strings, one language per `.ini` file.
* `Other/` - Assorted theme-related files.
* `Scripts/` - Theme-wide Lua scripts.
* `Sounds/` - The sounds and music used in the theme.
* `metrics.ini` - The main file controlling the theme.
* `ThemeInfo.ini` - An informational file with the theme's name and author.

### metrics.ini ###
As in previous versions of StepMania, themes still look to `metrics.ini` as the primary source of information. The metrics set up various system and screen elements. Unlike previous versions of StepMania, Lua is natively supported in the metrics.

### ThemeInfo.ini ###
An optional file with the theme's name and author. An example from the default theme:

	[ThemeInfo]
	DisplayName=Default
	Author=Midiman

### Other/ ###
This folder contains miscellaneous files used in themes.

* `Profile Common.xsl`, `Profile Stats.xsl` - XSL stylesheets.
* `ScreenGameplaySyncMachine music.ssc` - Steps for the Sync Machine option.
* `ScreenHowToPlay steps.ssc` - Steps for `ScreenHowToPlay`.
* `SongManager PreferredCourses.txt` - Preferred Courses list.
* `SongManager PreferredSongs.txt` - Preferred Songs list.

### Languages/ ###
This folder contains the strings for each language as `.ini` files. Files use two-letter country codes ([ISO-639-1](http://www.loc.gov/standards/iso639-2/php/code_list.php); [Native Names](http://people.w3.org/rishida/names/languages.html)).

### Sounds/ ###
This folder contains the sounds and music for the theme. To make a sound loop, add `(loop)` to the end of its filename (e.g. `ScreenSelectDifficulty music (loop)`).

(The usage of Lua to load sounds dynamically will be explained later.)

### Fonts/ ###
This folder contains the theme's fonts, which consist of graphics files and `.ini` definitions. StepMania 3.9 had a separate `Numbers` directory; it is now merged into here.

Fonts are typically generated with Texture Font Generator (a Windows-only program).

### Scripts/ ###
The Scripts folder contains Lua scripts that are used throughout the theme. Example uses include setting up branches, theme colors, and the MusicWheelItem TextBanner.

### Graphics/ ###
The Graphics folder contains the theme graphics. For the most part, these are images, but there are some Lua scripts included as well.

An uncommon practice in the StepMania 3.9 days was to use `.actor` files or `BGAnimation.ini` for certain theme elements in the Graphics folder. This practice continues today, though `.lua` files are used instead.

### BGAnimations/ ###
While the metrics handle the control of the theme, BGAnimations are considered the "heart" of the theme. Each theme will handle BGAnimations differently, though there are some common rules to be observed.

A list of possible BGAnimation layers for each screen:

* `in` - Transition in.
* `out` - Transition out.
* `cancel` - Transition when hitting "Back".
* `background` - Screen background.
* `underlay` - Screen underlay.
* `decorations` - Screen "decorations", a system that allows easier development of elements.
* `overlay` - Screen overlay, appears over everything.

### Image Hints ###
Similar to how you can loop music by adding `(loop)` at the end of the filename, you can add various image hints to the end of image filenames.

* `(16bpp)` - Forces texture color depth to 16bpp.
* `(32bpp)` - Forces texture color depth to 32bpp.
* `(dither)` - Dithers the texture (if necessary, as opposed to banding).
* `(stretch)` - Stretches the texture internally (used for properly tiling/scrolling non-power of two images).
* `(mipmaps)` - Forces mipmap generation.
* `(nomipmaps)` - Disables mipmap generation.
* `(grayscale)` - Marks the image as grayscale.
* `(alphamap)` - Marks the image as an alpha map; all color is assumed to be white.
* `(doubleres)` - Marks the image as double resolution; texture dimensions must be evenly divisible by 4.

### Screens ###
Various screens make up the StepMania experience. All screens derive from a base `Screen` class, while most menu screens are derived from `ScreenWithMenuElements`.

### Decorations ###
The Decorations system is a relatively new feature of StepMania theming. Decorations are intended to bridge the gap between Lua-based elements and `metrics.ini`.

#### Decoration Functions ####
* `LoadFallbackB()` - Loads the decorations from any screen this one falls back on. This is typically used at the start of a decorations file.