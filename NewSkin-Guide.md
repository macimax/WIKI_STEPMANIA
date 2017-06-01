# <a name="top">Table of Contents</a>
* [noteskin.lua](#noteskin)
* [notes.lua](#notes)
    * [Parameters](#params)
    * [Taps](#taps)
        * [State & Texture Maps](#maps)
        * [Actors](#actor)
    * [Holds](#holds)
        * [State Maps](#map2)
        * [Textures](#tex)
        * [Texture Flip](#flip)
        * [Filtering](#filter)
        * [Hold Data](#data)
    * [Optional Taps](#optaps)
* [Layers - receptors.lua & explosions.lua](#layers)
    * [Commands](#cmd)
        * [PlayerStateSetCommand](#pssc)
        * [WidthSetCommand](#wsc)
        * [ReverseChangedCommand](#rcc)
        * [BeatUpdateCommand](#buc)
        * [ColumnJudgmentCommand](#cjc)
        * [HoldCommand](#hc)
* [Useful Resources](#res)
---------------------------
The NewSkin system is an extension of the NewField, revamping how noteskins work and making them much more flexible.  Instead of a bunch of metrics and specifically named files, the NewSkin system is based entirely around Lua and allows you to use whichever files you want, and even allows you to create parameters for your skin, allowing individual player customization.

With the removal of the all of the metrics and specially named files and such, the file directory is much smaller. Also, due to the great flexibility of the system, few files are actually required. The files you'll 100% need are:
`noteskin.lua` - The base of the noteskin. Probably the most important file of the noteskin, it also contains all of the other lua files you will be using in your noteskin.
`notes.lua` - Contains code for the notes in the columns. Taps, holds, etc.

All other files are completely optional, however it is common to make a `receptors.lua` and `explosions.lua` to handle -- you guessed it -- receptors and explosions. Note that your filenames (aside from `noteskin.lua`) can be whatever your heart desires, as long as you point to them in `noteskin.lua`.

_Side note: the default noteskin has a good enough guide, but I figured we could use a wiki page too._

# <a name="noteskin">noteskin.lua</a>  
#### [Back to top](#top)
The format for an average `noteskin.lua` file is as follows:
```lua
return {
	notes = "notes.lua",
	layers = {"receptors.lua", "explosions.lua"},
	supports_all_buttons = false,
	buttons = {"Left", "Down", "Up", "Right", "UpLeft", "UpRight", "DownLeft", "DownRight"},
	fallback = "",
	skin_parameters = {},
	skin_parameter_info = {},
}
```
Now let's go over what all of that means:  
* `notes = "notes.lua"` - The path to the notes file of your noteskin. The `notes.lua` will be explained later.  
* `layers = {"receptors.lua", "explosions.lua"}` - The extra layers of your noteskin. You can have as many or as little layer files as you like. Layer files are explained later.  
* `supports_all_buttons = false` - Self-explanatory.  
* `buttons = {"Left", "Down", "Up", "Right", "UpLeft", "UpRight", "DownLeft", "DownRight"}` - Also self explanatory. Here is a [list of buttons, along with their matching stepstype](https://gist.github.com/YungDaVinci/07eea35922bf2248d931458de2b7817b).  Note that you don't have to repeat buttons in your buttons table.
* `fallback = ""` - Chooses the noteskin to fallback on. If something in your noteskin errors out, the game will use this noteskin instead.  
* `skin_parameters = {}` - Allows you to make parameters for your noteskin, such as making particles, quantizing holds, or anything else you wanna do. Parameters can be anything you want them to be. For example, the default noteskin's parameters are:
```lua
skin_parameters= {
	quantize_holds= false,
	explosions= {
		particles= true,
		particle_dist= 128,
		particle_life= 1,
		particle_size= 32,
		num_particles= 16,
		particle_blend= "BlendMode_WeightedMultiply",
	},
	receptors= {
		warning_time= 2,
	},
},
```
Notice how in the skin_parameters table you simply set the value of each parameter. If a parameter is a table like `explosions` in our example, then it creates a submenu in the theme's nesty menu.  

* `skin_parameter_info = {}` - Defines the description of your parameters and options, if necessary. For options that are booleans, like `quantize_holds` in our example, you do not need to provide the options, simply the translations. 
Format for providing translations is as follows:
```lua
skin_parameter_info={
	[parameter_name]= {
		translation= {
			[lang]= {title= "[title]", explanation= "explanation"},
		},
	}
}
```

Each element (`[lang]`) in the translation table is a different translation. The same two-letter language codes used by normal  language files are used here. So you'd use `en` for the english version, `ja` for the japanese version, `es` for the spanish version, etc..

So, for `quantize_holds`, the  table looks:
```lua
quantize_holds= {
	translation= {
		en= {title= "Quantize holds", explanation= "When on, holds will be quantized."},
	},
},
```
For our `explosions` table, we can put a translation on the `explosions` option, and on each individual element of the table.  

If your option is a number (like `particle_life`, `particle_size`, and `num_particles`), your table should have a `type` element, which should be either `"int"` or `"float"`. If it's `"int"`, then it's whole numbers; if it's `"float"`, it's decimals. Optional to add in the table are `min` and `max` values, limiting the range of the number. If they aren't specified, then the theme sets any `min` and `max` values.  

Tables for `particle_life` and `particle_size`:
```lua
particle_life= {
	type= "float", min= .1, max= 10, translation= {
		en= {title= "Particle Life", explanation= "Number of seconds particles live for."},
	},
},
particle_size= {
	type= "int", min= 0, max= 2000, translation= {
		en= {title= "Particle Size", explanation= "A higher number makes the particles larger."},
	},
},
```
For string fields, a list of choices must be provided.  The engine will ensure that the value the theme sets is in the list of choices. Note that the choices also have entries in the translation table.
```lua
particle_blend= {
	choices= {
		"BlendMode_Normal", "BlendMode_Add", "BlendMode_Subtract",
		"BlendMode_Modulate", "BlendMode_CopySrc", "BlendMode_AlphaMask",
		"BlendMode_AlphaKnockOut", "BlendMode_AlphaMultiply",
		"BlendMode_WeightedMultiply", "BlendMode_InvertDest",
		"BlendMode_NoEffect"},
	translation= {
		en= {
			title= "Particle Blend Mode", explanation= "Changes how the particles are blended.",
			choices= {
				"Normal", "Add", "Subtract",
				"Modulate", "Copy Source", "Alpha Mask",
				"Alpha Knock Out", "Alpha Multiply",
				"Weighted Multiply", "Invert Dest",
				"No Effect"},
		},
	},
}
```

# <a name="notes">notes.lua</a>  
#### [Back to top](#top)
##### [(default's notes.lua, also with documentation)](https://github.com/stepmania/stepmania/blob/master/NoteSkins/default/notes.lua)
In your `notes.lua` (or whatever else you decide to name it) you will define what the different types of notes look like. Those notes are:
* Taps
* Mines
* Lifts
* Holds & Reverse Holds
* Rolls & Reverse Rolls 

Optionally, you can also define:  
* Hold Heads & Tails
* Roll Heads & Tails
* All of the above, but reverse

How to go about doing this will be explained.

The system calls a function from all of the noteskin's actors, with the arguments of a list of buttons to be used, the current stepstype, and the skin parameters. Your files should return a function with those arguments, like so:
```lua
return function(button_list, stepstype, skin_parameters)

	return {columns = [columns], vivid_operation = false}
end
```
The function must also return a table, with elements of `columns` and `vivid_operation`. `vivid_operation` is useful for when you wish to have a vivid noteskin, where animations start at different times. You'll likely want this to be false.

What exactly goes into the table of columns? Let's see:
```lua
for i, button in ipairs(button_list) do
	columns[i]= { -- i is a number
		width = 64,
		padding = 0,
		custom_x = 0,
		hold_gray_percent = .25
		use_hold_heads_for_taps_on_row= false,
		anim_time = 1,
		quantum_time = 1,
		anim_uses_beats = true,
		taps={
			NoteSkinTapPart_Tap={
				state_map= tap_state_map,
				actor= Def.Sprite{ Texture="tap_note", 
					InitCommand=function(self) self:rotationz(rots[button]) end }},
			NoteSkinTapPart_Mine={
				state_map= mine_state_map,
				actor= Def.Sprite{Texture="mine"}},
			NoteSkinTapPart_Lift= {
				state_map= lift_state_map,
				actor= Def.Sprite{Texture= "lift",
					InitCommand= function(self) self:rotationz(rots[button]) end}},
			},
		holds={
			TapNoteSubType_Hold={
				{ -- This table is for the inactive state of holds.
					state_map= hold_inactive_map,
					textures= {hold_tex},
					flip=" TexCoordFlipMode_None",
					disable_filtering = false,
					length_data = hold_length,
				},
				{ -- This is for active holds
					state_map= hold_active_map,
					textures= {hold_tex},
					length_data= hold_length,
				},
			},
			TapNoteSubType_Roll= {
				{
					state_map= hold_inactive_map,
					textures= {roll_tex},
					length_data= hold_length,
				},
				{
					state_map= hold_active_map,
					textures= {roll_tex},
					length_data= hold_length,
				},
			},
		},
		optional_taps= {
			NoteSkinTapOptionalPart_HoldHead={
				state_map= tap_state_map,
				inactive_state_map= tap_state-map,
				actor= Def.Sprite{Texture="hold head"}},
			NoteSkinTapOptionalPart_HoldTail={
				state_map= tap_state_map,
				inactive_state_map= tap_state-map,
				actor= Def.Sprite{Texture="hold tail"}},
			NoteSkinTapOptionalPart_RollHead={
				state_map= tap_state_map,
				inactive_state_map= tap_state-map,
				actor= Def.Sprite{Texture="roll head"}},
			NoteSkinTapOptionalPart_RollHead={
				state_map= tap_state_map,
				inactive_state_map= tap_state-map,
				actor= Def.Sprite{Texture="roll head"}},
		}
	}
	columns[i].reverse_holds = columns[i].holds
end
```
Whew! A lot of code right? Let's break it down.

## <a name="params">Parameters</a>
#### [Back to top](#top)
```lua
width = 64,
padding = 0,
hold_gray_percent = .25
use_hold_heads_for_taps_on_row= false,
anim_time = 1,
quantum_time = 1,
anim_uses_beats = true,
```
These are like parameters for your notes. 
* `width` - Widths of your columns. Columns can be different widths. Defaults to 64.
* `padding` - Padding, or distance between this column and the next one. A value of 2 means 1 pixel on each side. Defaults to 0.
* `custom_x` - If set, the column will be placed at this position instead of automatically positioned. Defaults to 0.
* `hold_gray_percent` - How black a released hold turns. If it's at 0, the hold turns completely black when released.
* `use_hold_heads_for_taps_on_row` - If a hold starts on the same row as a tap, the tap will be a hold head. Self explanatory.
* `anim_time` - Defines how long the animations for taps lasts. Optional, defaults to 1.
* `quantum_time` - How many beats quantizations cover. For example, if your `quantum_time` is 2, 4th notes occur 4 times every 8 beats, 8th notes occur 8 times every 8 beats (essentially becoming 4ths), etc etc.
* `anim_uses_beats` - Specifies if anim_time is beats or seconds. `anim_time` of 1 and `anim_uses_beats` set to true means that taps, holds, and receptors will take 1 beat to go through their animations.

## <a name="taps">Taps</a>
Taps are handled by a quantized_tap structure.  A quantized_tap contains an actor for the tap, a state map to use to quantize it, and a vivid memory of its world that was destroyed. If the vivid flag is not set, it will be treated as false. If you are making a vivid noteskin, you probably want to use the global vivid_operation flag. Each element in taps is the set of quantized_taps to use for that column. There is one quantized_tap for each noteskin part.

The `taps` table has three elements - `NoteSkinTapPart_Tap`, `NoteSkinTapPart_Mine` and `NoteSkinTapPart_Lift`, which define, you guessed it, taps, mines, and lifts respectively. Let's go over the elements of these tables.

### <a name="maps">`state_map = tap_state_map`</a>  
#### [Back to top](#top)
This is the state map for the tap notes. It tells the game what frames to use for the quantization of a note and the current beat. [default's notes.lua](https://github.com/stepmania/stepmania/blob/master/NoteSkins/default/notes.lua) has a more elaborate explanation of how this works. Note that you are allowed to define this anywhere in your file before you use it (preferably before the `for` loop, if you are using the same state map for all your columns, which you probably are). Syntax for state maps is as follows:
```lua
local tap_state_map = {
	parts_per_beat =parts_per_beat, quanta= {
		{per_beat= 1, states = states}
		--(etc, etc)
	}
}
```
`per_beat` - Stepmania uses this field to pick the quantization that fits how far the note is from directly on the beat. The simplest way to think about it would be to multiply this number by 4 to know which quantization this will be active on. So a per_beat of 1 will be for 4th notes, 2 for 8ths, 3 for 12ths, etc etc.

`states` - Gets the states that this quantization will use.  
_Note: When you make your sprite sheets, be sure to put the dimensions in the name of the sheet. For example, if it was named 'taps' and had 4 row and 4 columns, you'd name it `taps 4x4.png`._  
What if you have a 3D noteskin? Then instead of a `state_map`, you will use a `texture_map`. Instead of states, texture maps have trans_x and trans_y fields for translating the texture.
```lua
local tap_texture_map = {
	parts_per_beat =parts_per_beat, quanta= {
		{per_beat= 1, trans_x= 0, trans_y= 0}
		--(etc, etc)
	}
}
```

`parts_per_beat` - Must be the lowest common multiple of your `per_beat`s in your `quanta` table. If a `per_beat` is not the lowest common multiple, it is ignored.

default's state_map:
```lua
local parts_per_beat= 48
local tap_state_map= {
	parts_per_beat= parts_per_beat, quanta= {
		{per_beat= 1, states= {1}}, -- 4th
		{per_beat= 2, states= {3}}, -- 8th
		{per_beat= 3, states= {5}}, -- 12th
		{per_beat= 4, states= {7}}, -- 16th
		{per_beat= 6, states= {9}}, -- 24th
		{per_beat= 8, states= {11}}, -- 32nd
		{per_beat= 12, states= {13}}, -- 48th
		{per_beat= 16, states= {15}}, -- 64th
	},
}
```

There are a few functions for convienience for state maps, defined in _fallback:
* `NoteSkin.generic_state_map(anim_frames, per_beats)` - Useful for when your animations for all of your quantizations are the same. `anim_frames` is the number of frames of your animations, `per_beats` is a table of the quantizations you want.
* `NoteSkin.single_quanta_state_map(anim_frames)` - Useful for things that are unquantized, like hold bodies or mines. `anim_frames` is a table of the frames of the animation of the thing.

### <a name="actor">`actor` </a>
#### [Back to top](#top)
As you can probably guess, this is the actor for the tap, lift, or mine, whichever one you're working with. If you aren't working with a bar noteskin or something similiar, you will likely want to include a `rots` table, with each button that your noteskin support and what to rotate it to. For example:
```lua
return function(button_list, stepstype, skin_parameters)
	local rots = {Left=90, Down=0, Up=180, Right=270}
	
	
	-- blah blah blah...
	
	for i, button in ipairs(button_list) do
		columns[i] = {
			-- stuff
		
			NoteSkinTapPart_Tap={
				state_map = tap_state_map,
				actor = Def.Sprite{
					Texture="taps",
					InitCommand=function(self) self:rotationz(rots[button])
				}
			},
		
			-- you get the idea
		}
	end
end
```

## <a name="holds">Holds</a>
#### [Back to top](#top)
Holds are not actors at all.  Instead, they are handled through a series of tubes, like a big truck. A quantized_hold has a state map (same as a tap's state map), a set of textures for its layers, and its own vivid love for the world it protects. A hold texture must have the top cap, body, and bottom cap in each frame.  The top cap must be 1/6 of the frame height, the body must be 2/3 of the frame height, and the bottom cap must be the remaining 1/6 of the frame.  The second half of the body must be identical to the first. This is so that during rendering, the first half of the body section can be repeated to cover the length of the hold.  Putting the top cap and bottom cap in the same frame as the body avoids gap and seam problems.

There are two elements in the `holds` table - `TapNoteSubType_Hold` and `TapNoteSubType_Roll`. These tables have both inactive and active tables, for controlling when they're active and inactive. The inactive table comes before the active table. These tables also have a few important elements.

### <a name="map2">`state_map = hold_inactive_map`/`hold_active_map`</a>
This is identical to the [state maps for taps](#maps). If your holds don't have special quantizations, you'll likely want to use `NoteSkin.single_quanta_state_map` to make your life easier.

### <a name="tex">`textures = {hold_tex}`</a>
Textures is a table so that the holds can be rendered as multiple layers. Textures must be the same sizes and dimensions .This replaces the HoldActiveIsAddLayer flag that was in the old noteskin format.

### <a name="flip"> `flip="TexCoordFlipMode_None"` </a>
This allows you to flip the textures. Possible choices are `"TexCoordFlipMode_X"`,`"TexCoordFlipMode_Y"`, `"TexCoordFlipMode_XY"`, or `"TexCoordFlipMode_None"`. If you don't include it, it defaults to `"TexCoordFlipMode_None"`.

### <a name="filter"> `disable_filtering = true` </a>
If disable_filtering is set to true, then texture filtering will be turned off when rendering the hold.

### <a name="data"> `length_data= hold_length` </a>
The length_data table tells the system how long each part of the hold is. If the table is not present or one of the values is not a number, the default values are used. The default values are as follows:
```lua
local hold_length= {
	start_note_offset= -.5,
	end_note_offset= .5,
	head_pixs= 32,
	body_pixs= 32,
	tail_pixs= 32,
}
```

* `start_note_offset` - Where to start drawing the hold body, relative to the note the head occurs at.
* `end_note_offset` - Where to stop drawing the hold body, relative to the note the hold ends at.
* `head_pixs` - How many pixels tall the head section of the texture is.
* `body_pixs` - How many pixels tall one body section is. Remember that the body occurs twice, so this is only half the distance from the end of the head to the beginning of the tail. The body occurs twice so that part of the texture can be repeated when rendering a long hold.
* `tail_pixs` - How many pixels tall the tail section of the texture is.
If the hold texture is marked as doubleres, then head_pixs, body_pixs, and tail_pixs need to be half the pixel height each part has in the texture.

## <a name="optaps"> Optional Taps </a>
#### [Back to top](#top)
If you want, you are also able to define hold and roll heads and tails. If you do not define heads, they will fall back on normal taps. If you don't define tails, there just won't be extra tails.  
From default:
```lua
optional_taps= {
	-- This will be used if NoteSkinTapOptionalPart_RollHead or
	-- NoteSkinTapOptionalPart_CheckpointHead does not exist.
	NoteSkinTapOptionalPart_HoldHead= {
		state_map= tap_state_map,
		-- Taps can have an inactive_state_map if they need to look
		-- different when the hold they're on is not active.
		inactive_state_map= tap_state_map,
		actor= Def.Sprite{Texture= "hold_head 2x8.png"}},
	-- This will be used if NoteSkinTapOptionalPart_RollTail or
	-- NoteSkinTapOptionalPart_CheckpointTail does not exist.
	NoteSkinTapOptionalPart_HoldTail= {
		state_map= tap_state_map,
		actor= Def.Sprite{Texture= "hold_tail 2x8.png"}},
	NoteSkinTapOptionalPart_RollHead= {
		state_map= tap_state_map,
		actor= Def.Sprite{Texture= "roll_head 2x8.png"}},
	NoteSkinTapOptionalPart_RollTail= {
		state_map= tap_state_map,
		actor= Def.Sprite{Texture= "roll_tail 2x8.png"}},
	NoteSkinTapOptionalPart_CheckpointHead= {
		state_map= tap_state_map,
		actor= Def.Sprite{Texture= "checkpoint_head 2x8.png"}},
	NoteSkinTapOptionalPart_CheckpointTail= {
		state_map= tap_state_map,
		actor= Def.Sprite{Texture= "checkpoint_tail 2x8.png"}},
},
```

# <a name="layers">Layers (receptors.lua & explosions.lua)</a>
#### [Back to top](#top)
##### default's [receptors.lua](https://github.com/stepmania/stepmania/blob/master/NoteSkins/default/receptors.lua) and [explosions.lua](https://github.com/stepmania/stepmania/blob/master/NoteSkins/default/explosions.lua)
Similar to notes.lua, layer files must return a function that takes a button list, and optionally the steps type and skin parameters. The function must return a table containing actors for each column. These are full actors and their update functions will be called every frame.  
Example format:
```lua
return function(button_list, stepstype, skin_paramters)
    local cols = {}
    for i, button in ipairs(button_list) do
        cols[i] = Def.ActorFrame{
            -- do stuff
        }
    end
    return cols
end
```

## <a name="cmd">Commands</a>
#### [Back to top](#top)
Layer files are all passed a few commands, allowing you to have pretty much full control over what happens.

### <a name="pssc">PlayerStateSetCommand</a>
The param table has one element, param.PlayerNumber.  This is the number of
the player the field is for.

### <a name="wsc">WidthSetCommand</a>
WidthSet is sent immediately after the OnCommand is executed.  The elements
in the param table are:
* ```column``` The NoteFieldColumn the layer is in.
* ```column_id``` The id of the column.
* ```width``` The width of the column set by the noteskin.
* ```padding``` The padding set by the noteskin.

### <a name="rcc">ReverseChangedCommand</a>
ReverseChanged is sent when the reverse scale goes from negative to positive,
or from positive to negative.  It is not sent every frame.
Param table elements:
* ```sign``` -1 if the column is in reverse mode, 1 if it's not.

### <a name="buc">BeatUpdateCommand</a>
BeatUpdate occurs every frame.  Param table elements:
* ```beat``` The current beat.
* ```beat_distance``` Distance in beats to the next note in this column.
* ```second_distance``` Distance in seconds to the next note in this column.
* ```pressed``` True when the column goes from not pressed to pressed.
* ```lifted``` True when the column goes from pressed to not pressed.

### <a name="cjc">ColumnJudgmentCommand</a>
ColumnJudgment occurs when something is judged in the column.
Param table elements:
* ```bright``` True if the player's combo is greater than the
BrightGhostComboThreshold metric.
* ```tap_note_score``` If the judgment is for a tap note, this is the
judgment.  This is nil for holds.
* ```hold_note_score``` If the judgment is for a hold note, this is the
judgment.  This is nil for taps.

### <a name="hc">HoldCommand</a>
Hold occurs every frame when there is an active hold passing over the
receptors.  Param table elements:
* ```type``` The TapNoteSubType of the hold.
* ```life``` The current life value for the hold.  0 is a dropped hold, 1 is
a hold that is currently being held, in between is a hold that is going from
held to dropped.
* ```start``` True if this is the first frame the hold is active.
* ```finished``` True if this is the frame after the hold ended.

# <a name="res">Useful Resources</a>
#### [Back to top](#top)
* [Lua.xml](https://github.com/stepmania/stepmania/blob/master/Docs/Luadoc/Lua.xml) & [LuaDocumentation.xml](https://github.com/stepmania/stepmania/blob/master/Docs/Luadoc/LuaDocumentation.xml) (easier to read version hosted [here](https://yungdavinci.github.io/SM5-Lua-API/Lua.xml))   
* [The default noteskin](https://github.com/stepmania/stepmania/tree/master/NoteSkins/default)
* If you’re feeling bold: [source code](https://github.com/stepmania/stepmania/tree/master/src)  

