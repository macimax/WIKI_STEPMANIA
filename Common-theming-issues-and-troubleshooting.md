# Code is not executing
- If this is a new file, make sure you hit F2 to reload and check for new resources.
- Is the file in the correct place and named correctly?
- Is error reporting enabled? (F3+F6, make sure "show errors" is not greyed out)
- Make sure this file is not a duplicate of an existing screen, such as a ScreenTitleMenu overlay folder and then a lua file named ScreenTitleMenu overlay.lua.

# "must return an actor" error when entering screen
You probably forgot to return the ActorFrame table in one of your files.

# "invalid class" or "unknown class" error when entering a screen
You might be returning a table instead of an Actor.

# SCREENMAN:SystemMessage() does not work
BGAnimations/ScreenSystemLayer overlay has been overwritten and is missing the messagecommand required to show messages.