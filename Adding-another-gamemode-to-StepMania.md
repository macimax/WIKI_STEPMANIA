**This is a work in progress. Don't expect to actually be able to add them and compile it right away. Also, the instructions are not really in order, but it should still work in the end.**

This is not an easy task! If you don't know C++, you may want to look into using a simpler game engine that may suit your needs better.

# Step 1. GameManager.cpp
Head to the g_StepsTypeInfos array and append your stepstype for your style at the bottom.
An example StepsType is:
```cpp
{ "dance-single",	4,	true,	StepsTypeCategory_Single }
```
the first argument is the name of your style, the second one is the amount of note columns it has (aka how many buttons you use), nobody knows what the third one does so keep it true, and the fourth is the type.

**Note: These are prefixed with StepsTypeCategory in the source code. This is omitted for readability on this page.**

| StepsTypeCategories | Meaning |
| ------------------- | ------- |
| Single | Single player, 1 panel |
| Double | Single player, 2 panels |
| Couple | Two players, one chart, notefields kept separate |
| Routine | Two players, one chart, notefields put together like doubles |

Next you must fill out a `static const Style` array for every style you've added above.
It's easier to copy and paste an existing style than for me to describe how it works, so just do that. Make sure you edit the amount of columns for player and that you match the name to the name you defined above, and that you matched the stepsType to the stepsType you defined above.
After adding your styles, add a `static const Style` with an array of your styles. In the below example the styles `g_Style_Popn_Five` and `g_Style_Popn_Nine` have been defined.
```cpp
static const Style *g_apGame_Popn_Styles[] =
{
	&g_Style_Popn_Five,
	&g_Style_Popn_Nine,
	nullptr
};
```

Then add Automappings... I don't know how these work.

Then finally add your gamemode with `static const Game`, prefixing it with `g_Game_`. It's easier to look at an existing gamemode than for me to explain it, so copy and paste an existing one.
Make sure you change the name, point the styles to the array of styles you've defined above, point it to the AutoKeyMappings, etc.

It seems that the second array will never NOT be filled with `GameButtonType_Step`, but make sure you have exactly as many entries as buttons in the array.

Finally, edit the `static const Game *g_Games[]` array to point to the new gamemode you've defined above. If everything worked out, the style should now be registered with GAMEMAN (although there is still much more to be done)

# Step 2. Adding note types for your game mode
???

# Step 3. Adding the noteskin
???

# Step 4. Registering a new NotesLoader to load charts for your new gamemode
Copy and paste an existing one and... Good luck. I don't know enough C++ to tell you how it works.