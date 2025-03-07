# <a name="top">Table of Contents </a>
* [Basic Lua Concepts](#lua)
    * [Actors](#actors)
* [How do I start a theme?](#how)
    * [metrics.ini](#metrics)
    * [ThemeInfo.ini](#themeinfo)
    * [BGAnimations](#bganim)
    * [Graphics](#graphics)
        * [Image Hints](#imghints)
    * [Languages](#lang)
    * [Fonts](#fonts)
    * [Scripts](#scripts)
    * [Sounds](#sounds)
    * [Other](#other)
* [Other Essential Topics](#topical)
    * [Debugging](#debug)
    * [Customization](#cust)
    * [Figuring new things out](#new)
    * [5.2 incompatibilities](#52_incompatibilities)
    * [Useful Resources](#res)

-----------------
One of the most frequent criticisms of StepMania 5 is its theme system. What was once merely an .ini file of metrics and a collection of graphics and .ini/XML files in the 3.0 and 3.9 days, has now become a scripting-capable environment with support for Lua.

On StepMania 5.x, the Lua API enables more dynamic and customizable experiences within the game. It’s a little trickier to figure out at first, but you can get used to it easily.

# <a name="lua">Basic Lua Concepts</a>  #

Before you begin theming, if you’re unfamiliar with Lua, you’ll likely need to learn how it works. [lua.org](https://www.lua.org/pil/1.html) has a pretty extensive and all-encompassing tutorial. If you’re already familiar with coding or just want a shorter tutorial [luatut.com’s Crash Course to Lua](http://luatut.com/crash_course.html) is pretty nice.
 
Now that you’re familiar with lua, you’ll need to learn how to use it in SM5.

## <a name="actors">Actors</a> ##  
#### [Back to top](#top)  

A basic concept when working with Lua scripts in StepMania themes and BGAnimations is the actor model. Everything rendered in StepMania is an actor, whether it’s a simple sprite or even an entire script of its own. For a more complete explanation, we’ll refer you to [quietly-turnings’s very helpful primer on the concept](https://quietly-turning.github.io/Lua-For-SM5/Introduction/Foreword).
 
The most basic form of script used to load a single actor is this;

```lua
local t = Def.ActorFrame{}

t[#t+1] = LoadActor("_file") .. {
	InitCommand=cmd(diffusealpha,0;x,SCREEN_CENTER_X;y,SCREEN_CENTER_Y),
	OnCommand=function(self)
		self:linear(0.4):addx(100):diffusealpha(1)
	end
}
 
return t
```
 
As mentioned, a single .lua file can only return one actor. But that actor can be an ActorFrame, which is a nested array of multiple actors. In this form, the actors appended with t[#t+1] are essentially building an “array” into the variable t (you can replace t with anything else) that is returned all at once at the end of the file.
 
Actors are given a duty through **commands**; the most common commands used on an actor are InitCommand (which occurs when the actor is initalized), the OnCommand (which is executed right after it is initialized, typically when a screen is entered), and the OffCommand (which is executed when a screen is exited). 
 
A command can consist of either a comma and semicolon-separated list of metric commands (as seen in the Init on the example), or as a Lua function performing actions on the actor. These can include metric commands (notice the different syntax) as well as embedded Lua scripts, allowing for more complex conditionals and dynamic content. Custom commands can also be defined and invoked using the `playcommand` and `queuecommand` commands, while StepMania can produce “messages” that actors may also react to (using `MESSAGEMAN:Broadcast(message)` and `messageMessageCommand`, replacing `message` with your message name).
 
If you need to see some examples of certain actors in action, check out [Docs/Themerdocs/Examples/Example_Actors](https://github.com/stepmania/stepmania/tree/master/Docs/Themerdocs/Examples/Example_Actors).

# <a name="how">How do I start a theme?</a> #  
#### [Back to top](#top)  
To create a theme, it is recommended that you have graphics programs (programs such as Adobe Illustrator, Affinity Designer, Inkscape, and Fireworks [RIP] are a great tool for design work, and bitmap editors such as GIMP, Paint.net, or Photoshop may also be useful) and a coding-focused text editor with syntax highlighting (i.e. on Windows, something that is _not_ Notepad.  Atom, Notepad++, Sublime Text, and Visual Studio Code are good options, but if you hate yourself feel free to use Notepad though.). On Windows, another useful program to have around is AstroGrep, since it is good for doing full-text searches of files.
 
The first step is **not to just copy and paste fallback or Default and modify it**. Feel free to poke around at it, but this tutorial isn’t about just making a graphical re-skin of the default like every first-time themer did in the 3.9 era. The Default theme is still useful; it is, by virtue, one of the most complete themes, so you can lift assets and code from it to work from (don't forget, StepMania is open source). But the key to theming is understanding how the code _works_.

Fallback is not meant to be a user-facing theme, but base metrics and scripts used by all themes; all StepMania 5.x themes are ultimately children of Fallback. This way, when changes are made to Fallback on later releases, they apply to all themes unless otherwise overridden.
 
The real first step is to create a blank folder. Then, you will create several other folders:
* [BGAnimations/](#bganim) - Scripts that control screen behavior.
* [Graphics/](#graphics) - Graphics assets and some scripts.
* [Languages/](#lang) - Files specifying translatable text.
* [Fonts/](#fonts) - Font files. Self explanatory.
* [Scripts/](#scripts) - Files containing Lua functions that can be invoked anywhere in the theme.
* [Sounds/](#sounds) - BGM and sound effect files. Self explanatory.
* [Other/](#other) - Miscellaneous files.
 
You will also need a [metrics.ini](#metrics). Some metrics you will need, such as for defining new screens, however some themers have resorted to moving things previously present in metrics to lua files, as working with metrics is more cumbersome and not very future-proof. An optional file is [ThemeInfo.ini](#themeinfo), which can be used to enter a display name and author information that is shown on startup, and in the StepMania settings menu.

## <a name="metrics">metrics.ini</a> ##  
#### [Back to top](#top)  
As in previous versions of StepMania, themes still look to `metrics.ini` as the primary source of information. The metrics define your custom screens and any metrics that you may wish to change. Lua is natively supported in the metrics. Every metric is defined in `_fallback`’s expansive metrics.ini, so feel free to Ctrl+F any time you’re looking for a metric that may fit your needs.
Metrics follow the following syntax:
    [ScreenScreenName]
    MetricA=do thing;
    MetricB=do other thing;
 
You can create custom screens within the metrics. Define the screen name, class, and fallback screen. The screen will inherit metrics and other properties from the screen class, and will fall back on the fallback screen. For example:

    [ScreenExampleScreen] # all screen names are preceded by “Screen”
    Class=”ScreenWithMenuElements”
    Fallback=”ScreenWithMenuElements” 

Then, in your BGAnimations folder,  you'll create a ScreenExampleScreen overlay file, along with any others you might want.


## <a name="themeinfo">ThemeInfo.ini</a> ##  
#### [Back to top](#top)  
An optional file with the theme's name and author. An example from the default theme:

	[ThemeInfo]
	DisplayName=Default
	Author=Midiman

## <a name="bganim">BGAnimations</a> ##  
#### [Back to top](#top)  
The BGAnimations folder is an essential part of your theme. Here you will define what goes on what screen in your theme. Syntax for filenames can be seen as `[Screen name] [layer].lua`. You can have a few different layers. Take ScreenTitleMenu for example:
* `ScreenTitleMenu background.lua`: Defines the background of ScreenTitleMenu. It is the lowest layer.
* `ScreenTitleMenu overlay.lua`: Defines the overlay, or top layer, on ScreenTitleMenu.
* `ScreenTitleMenu underlay.lua`: Defines the underlay on ScreenTitleMenu.
* `ScreenTitleMenu decorations.lua`: Defines the decorations on ScreenTitleMenu.

You can also define transitions to and from screens:
* `ScreenTitleMenu in.lua`: Defines the transition into ScreenTitleMenu.
* `ScreenTitleMenu out.lua`: Defines the transition out of the ScreenTitleMenu.
* `ScreenTitleMenu cancel.lua`: Defines what happens when you press the back button on ScreenTitleMenu (so different from out).
 
Note that your files are not restricted to being .lua files. For example, you can have your background file be `ScreenTitleMenu background.png`.
 
Another neat concept is using folders. For example, let’s say you want to pictures in your overlay and want an easy way to access them. You can create a folder, `ScreenTitleMenu overlay`, and place your pictures and lua file in there, which should be named `default.lua`. Note that folders are not restricted to being simply used for overlays and the like. You can place whatever your heart desires in your folders.

## <a name="graphics">Graphics</a> ##  
#### [Back to top](#top)  
Here you will place theme graphics and occasionally scripts. You do not have to place all of your graphics in the graphics folder, however some are required to be in Graphics, such as for customizing the music wheel (`MusicWheelItem Song NormalPart`, etc). These do not necessarily have to be images. Maybe you prefer to use a Quad or ActorMultiVertex. Note that all the possible graphic file names are located in `_fallback`, and many (if not all) of them are in action in default. 
Some scripts are located in graphics, including scrollers (that use metrics) and `Player judgment & combo`. You are not required to use any of these files or graphics. However, most of them will make your theming experience and life easier in the long run.

### <a name="imghints">Image Hints</a> ###   
Similar to how you can loop music by adding `(loop)` at the end of the filename, you can add various image hints to the end of image filenames.

* `(16bpp)` - Forces texture color depth to 16bpp.
* `(32bpp)` - Forces texture color depth to 32bpp.
* `(dither)` - Dithers the texture (if necessary, as opposed to banding).
* `(stretch)` - Stretches the texture internally (used for properly tiling/scrolling non-power of two images).
* `(mipmaps)` - Forces mipmap generation.
* `(nomipmaps)` - Disables mipmap generation.
* `(grayscale)` - Marks the image as grayscale.
* `(alphamap)` - Marks the image as an alpha map; all color is assumed to be white.
* `(res "x"x"y")` - Change the image's internal resolution. X and Y: horizontally and vertically pixels, respectively.
* `(doubleres)` - Marks the image as double resolution; texture dimensions must be evenly divisible by 4. Only compatible with SM 5 branch.

## <a name="lang">Languages</a> ##  
#### [Back to top](#top)  
Here you will create translations for your text, if you wish. See the language files in default and _fallback for examples of the syntax of these files.

Files use two-letter country codes ([ISO-639-1](http://www.loc.gov/standards/iso639-2/php/code_list.php); [Native Names](http://people.w3.org/rishida/names/languages.html)).

## <a name="fonts">Fonts</a> ##  
#### [Back to top](#top)  
This folder contains the theme's fonts, which consist of graphics files and `.ini` definitions.
Fonts are typically generated with Texture Font Generator (a Windows-only program).

## <a name="scripts">Scripts</a> ##  
#### [Back to top](#top)  
This folder is useful for defining functions that you wish to use throughout your entire theme. When making changes to files within this folder, you’ll have to press Ctrl+F2 to reload them and see your changes take place. Since you will be using these functions globally, be sure to not use local when defining your functions. Many scripts are defined within `_fallback`.

## <a name="sounds">Sounds</a> ##  
#### [Back to top](#top)  
This folder contains the sounds and music for the theme. To make a sound loop, add `(loop)` to the end of its filename (e.g. `ScreenSelectDifficulty music (loop)`).

## <a name="other">Other</a> ##  
#### [Back to top](#top)  
This folder contains miscellaneous files used in themes.

* `Profile Common.xsl`, `Profile Stats.xsl` - XSL stylesheets.
* `ScreenGameplaySyncMachine music.ssc` - Steps for the Sync Machine option.
* `ScreenHowToPlay steps.ssc` - Steps for `ScreenHowToPlay`.
* `SongManager PreferredCourses.txt` - Preferred Courses list.
* `SongManager PreferredSongs.txt` - Preferred Songs list.

# <a name="topical">Other Essential Topics</a> #  
  
## <a name="debug">Debugging</a> ##  
#### [Back to top](#top)
Often while developing your theme, you will run into a number of errors. These errors will pop up in game but tend to disappear fast. You can get them to stay by holding F3, bringing up the debug overlay, pressing F6 to bring up the theme section of the menu, and pressing 9, labeled as “Show Recent Errors” or something similar.
This menu also contains a number of other useful tools, including reloading the current screen (to put your changes to the current screen in effect) and reloading metrics and new textures/images. Use this menu often.

## <a name="cust">Customization</a> ##  
#### [Back to top](#top)  
You are not required to use any of the predefined screens and graphics and such. You could probably build a theme that's actually just Pac-Man, if you really wanted. If you're feeling creative, be creative. Let your creative juices run free.

## <a name="new">Figuring new things out</a> ##  
#### [Back to top](#top)  
While theming, you may run into the issue of wanting to do something, but having no idea how to do it! One great resource readily available is checking out the default theme for that thing, copying it, and making it your own. Similarly, you could copy from _fallback, but that may not be as useful. Or more useful. Who knows.
Another great resource is Lua.xml and LuaDocumentation.xml
But if what if it's not in default, or any theme you've seen? Feel free to head over to the stepmania devs IRC channel  (#stepmania-devs on freenode) and ask for help there.
 
## <a name="52_incompatibilities">5.2 incompatibilities</a> ##  
#### [Back to top](#top)  
On the StepMania master branch (5.2), there are several major changes that a theme must account for, including;

* The new **notefield** system (previously known as **newfield**). It is designed to be more flexible, and integrates with several other new components such as a new options menu system, and a new modifier framework. To learn how to utilize the new notefield, check out [Themes/_fallback/Scripts/02 NoteField.lua](https://github.com/stepmania/stepmania/blob/master/Themes/_fallback/Scripts/02%20NoteField.lua) (also in your install of StepMania), where a number of functions and explanations for how to use the notefield are defined. [NewField.md](https://github.com/stepmania/stepmania/blob/master/Docs/Themerdocs/5.1_incompatibilities/NewField.md) also goes over this in great detail.
* The new **menu framework** can be used to construct nested menu hierarchies with Lua code. It has a number of advantages, including being Lua-based, and having mouse support. [menu_system.md](https://github.com/stepmania/stepmania/blob/master/Docs/Themerdocs/5.1_incompatibilities/menu_system.md) provides details on its usage.
* **lua_config** is used in place of ThemePrefs. It is documented [here](https://github.com/stepmania/stepmania/blob/master/Docs/Themerdocs/lua_config_system.md)

## <a name="res">Useful Resources</a> ##  
#### [Back to top](#top)  
[Lua.xml](https://github.com/stepmania/stepmania/blob/master/Docs/Luadoc/Lua.xml) & [LuaDocumentation.xml](https://github.com/stepmania/stepmania/blob/master/Docs/Luadoc/LuaDocumentation.xml) (easier to read/search version [here](https://quietly-turning.github.io/Lua-For-SM5/LuaAPI))   
Everything in [Themerdocs](https://github.com/stepmania/stepmania/tree/master/Docs/Themerdocs)  
`_fallback` & `default` themes  
If you’re feeling bold: [source code](https://github.com/stepmania/stepmania/tree/master/src)