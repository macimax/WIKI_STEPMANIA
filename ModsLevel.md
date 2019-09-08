# Preferred
user-chosen player options.  Does not include any forced mods. Modifiers will persist throughout the entire round.

Use this if you are building a custom replacement for ScreenPlayerOptions.  Changes to ModsLevel_Preferred are applied to Stage, Song, and Current when ScreenGameplay starts.  Approach speeds in ModsLevel_Preferred are ignored.
# Stage
Preferred + forced stage mods

ModsLevel_Stage is a holding area the engine uses when building the active attacks a course or song forces on a player.  It should not be used by a theme.
# Song
Stage + forced attack mods. Modifiers will only persist during the song.

Changes to ModsLevel_Song while on ScreenGameplay take effect over time, governed by an approach speed.  ModsLevel_Song should only be modified by the theme on ScreenGameplay, because it is reset to the contents of Preferred when ScreenGameplay starts.

If you are setting an attack during a song through lua, use this one.
# Current
Changes to ModsLevel_Current on ScreenGameplay take effect immediately, but are quickly nullified as Current tweens toward Song.  The approach speeds in Current are ignored.  Changing Current when not on ScreenGameplay will have no effect.