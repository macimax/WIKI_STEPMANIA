You can extend StepMania with various forms of add-ons to customize your gameplay experience.

Add-ons are usually distributed in ZIP files. Your [user data directory](https://github.com/stepmania/stepmania/wiki/User-Data-Locations) contains a number of subfolders where they are placed.

# Types
## Themes
Themes are used to customize StepMania's interface. On version 5.0 and newer, themes are constructed using Lua scripts and an associated API. You can download themes from the [StepMania forum](https://www.stepmania.com/forums/themes/), as well as other websites; themes compatible with 5.0.12 are also compatible with 5.1, but neither 5.0.12 or 5.1 support themes from older versions (such as 3.9 and 4.0). If you're interested in building your own themes, see the [Theming page](https://github.com/stepmania/stepmania/wiki/Theming) on the wiki for more information on basic concepts.

Themes are installed in the `Themes` subfolder of your user data directory. Note that the theme folder placed in the `Themes` directory _must_ be the one that contains folders such as `BGAnimations`, `Graphics`, etc. If these folders are placed at a deeper directory level within the folder placed in the directory (i.e. the folder structure looks like `Themes/greattheme-ver1.0/Great Theme/` rather than `Themes/Great Theme/`), it will not load, and attempting to use it will load Fallback (a plain, base theme used as base code for all other themes) instead.

## Noteskins
Noteskins change the appearance of the notes, from standard arrows, to spheres or even bars. 

Noteskins are installed in the `NoteSkins` subfolder of your user data directory. On StepMania 5.1 and older, noteskins only support one [game mode](https://github.com/stepmania/stepmania/wiki/Supported-Game-Modes) at a time, and are placed in subfolders of the `NoteSkins` directory that correspond to the game they are designed for (i.e. ``dance`` or ``pump`` for instance).

StepMania 5.2 uses a different noteskin system, where a single noteskin can support multiple games by containing graphics for their respective notes. Hence, noteskins for 5.2 are not stored in game-specific subfolders.

## Announcers
Announcers are used to provide voice clips triggered by specific screens, in-game events, etc.