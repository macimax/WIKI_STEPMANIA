You can extend StepMania with various forms of add-ons to customize your gameplay experience.

Add-ons are usually distributed in ZIP files. Your [user data folder](https://github.com/stepmania/stepmania/wiki/User-Data-Locations) contains a number of subfolders where custom content should be placed.

# Types

## Themes
Themes are used to customize StepMania's interface.  You can download themes from the [StepMania forum](https://www.stepmania.com/forums/themes/), as well as other websites; themes compatible with 5.0.12 are also compatible with 5.1. Themes from older versions (SM3.9 and variants, 4 alpha, 4 beta) are not supported in SM5 branch.

Themes are installed in the `Themes` subfolder of your user data folder. Note that the theme folder placed in the `Themes` directory _must_ be the one that contains folders such as `BGAnimations`, `Graphics`, etc. 

---

⚠️ Sometimes unzipping a theme will cause it to be nested too deeply within subfolders, preventing StepMania from properly loading it.   If you've used StepMania's in-game UI to switch to a new theme, and you end up seeing plain white text on a black background, this is likely what happened.  

![folders nested too deeply](https://i.imgur.com/BP3TjLOl.png)

Quit StepMania, and check to see if you accidentally have something like `./Themes/Some Cool Theme/Some Cool Theme/`.  If so, move the innermost folder up a level so that you have a structure like `./Themes/Some Cool Theme/`

---

#### Making Your Own Theme

In SM5 themes are primarily constructed using Lua scripts and [an associated API](https://quietly-turning.github.io/Lua-For-SM5/LuaAPI), graphic files, and metrics.  If you're interested in building your own themes, see the [Theming page](https://github.com/stepmania/stepmania/wiki/Theming) on the wiki for more information on basic concepts.

## NoteSkins
NoteSkins change the appearance of the notes, from standard arrows, to spheres or even bars. 

NoteSkins are installed in the `NoteSkins` subfolder of your user data directory. On StepMania 5.1 and older, NoteSkins only support one [game mode](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes) at a time, and are placed in subfolders of the `NoteSkins` directory that correspond to the game they are designed for (i.e. `./NoteSkins/dance/` or `./NoteSkins/pump/` or `./NoteSkins/para/`).

NoteSkins compatible with 5.0.12 are also compatible with 5.1.  NoteSkins from older versions (SM3.9, 4 alpha, 4 beta) are not supported in SM5.

#### Making Your Own NoteSkin

In SM5, NoteSkins are constructed using a combination of graphic files, metrics, and Lua scripts.  You can learn more at the [NoteSkins wiki page](NoteSkins).

## Announcers
Announcers are used to provide voice clips triggered by specific screens, in-game events, etc. Announcers are compatible with any version of StepMania, for example an announcer created for StepMania 3.9 will still work in StepMania 5.