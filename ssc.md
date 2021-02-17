# About

(This wiki page is in progress... Feel free to alter it as needed...)

Stepmania's [.sm](https://github.com/stepmania/stepmania/wiki/sm) format was updated to include more tags and more organization. Thus, .ssc was born.

SSC also supports advanced timing data including per-chart timing data, delays, warps, scroll speed, fake sections, and more.

# Header Tags

Each TAG will have values that you can set/change. The format is as follows: TAG:VALUE; The value can be either a single line or span multiple lines. Just make sure it starts with : and ends with ;.

## \#VERSION

This is the version of the .ssc File Format.

## \#TITLE

Sets the Song's Title.

## \#SUBTITLE

Sets the Song's Subtitle. (Optional)

## \#ARTIST

Sets the Song's Artist.

## \#TITLETRANSLIT

Sets the Song's Title Translation.

## \#SUBTITLETRANSLIT

Sets the Song's Subtitle Translation.

## \#ARTISTTRANSLIT

Sets the Song's Artist Translation.

## \#GENRE

Sets the Song's Genre.

## \#ORIGIN

Where the song came from if it's a crossover from an existing game.

No theme is known to use this, so it's essentially useless.

## \#CREDIT

Sets the .ssc Creator/Credits. Usually the \#CREDIT tag in the note data is used instead.

## \#BANNER

Sets the path to the Banner. (Based on the current Song's directory.)

## \#BACKGROUND

Sets the path to the Background. (Based on the current Song's directory.)

## \#PREVIEWVID

Sets the path to the Preview Video. This is usually used in 'pump' based themes where there is a spot in the music select that plays the video. (Based on the current Song's directory.)

## \#JACKET

Sets the path to the Jacket. (Based on the current Song's directory.)

## \#CDIMAGE

Sets the path to the CD Image. (Based on the current Song's directory.)

## \#DISCIMAGE

Sets the path to the Disc Image. (Based on the current Song's directory.)

## \#LYRICSPATH

Sets the path to the [LRC](https://github.com/stepmania/stepmania/wiki/lrc) file containing the song's lyrics. (Based on the current Song's directory.)

## \#CDTITLE

Sets the Song's CD Title.

## \#MUSIC

Sets the path to the Song. (Based on the current Song's directory.)

## \#PREVIEW

Sets the path to a Preview file. If a valid preview file is set it will be played in the music wheel instead of the samplestart/samplelength defined for the song. (Based on the current Song's directory.)

## \#OFFSET

Sets the Song's Offset. (Effects the timing of the start of the NOTES.)

## \#SAMPLESTART

Sets when to play the song's sample when hovering over it in the music wheel.

## \#SAMPLELENGTH

Sets the Song's Sample Length.

## \#SELECTABLE

Allows or disallows the song from appearing in the music wheel. This is usually for a theme's tutorial song or other song not normally encountered during gameplay. (Values are `YES` or `NO`)

## \#BPMS

Sets the Song's Beats Per Minute's at certain times. (Can have multiple changes.)

## \#DISPLAYBPM
This can be used to override the BPM shown on ScreenSelectMusic. This tag supports three types of values:
 
* A number by itself (e.g. `#DISPLAYBPM:180;`) will show a static BPM.
* Two numbers in a range (e.g. `#DISPLAYBPM:90:270;`) will show a BPM that changes between two values.
* An asterisk (`#DISPLAYBPM:*;`) will show a BPM that randomly changes.

## \#STOPS

Sets the Song's Stops at certain times. (Can have multiple changes.)

## \#DELAYS

Sets the Song's Delays at certain times. (Can have multiple changes.)

## \#WARPS

Sets the Song's Warps at certain times. (Can have multiple changes.)

## \#TIMESIGNATURES

Sets the Song's Timing Signatures at certain times. (Can have multiple changes.)

## \#TICKCOUNTS

Sets the Song's checkpoint-hold tick count rate. (Can have multiple changes.)

## \#COMBOS

Sets the Song's Combo at certain times. (Can have multiple changes.)

## \#SPEEDS

Sets the Song's Rate(?) at certain times. (Can have multiple changes.)

## \#SCROLLS

(someone edit this section.)

## \#FAKES

Contains the Song's [Fake segments](https://github.com/stepmania/stepmania/wiki/Timing-Segments#fake). (Can have multiple Fake segments.)

## \#LABELS

Contains the Song's [Label segments](https://github.com/stepmania/stepmania/wiki/Label-segments). (Can have multiple Label segments.)

## \#LASTSECONDHINT

A float value. Tells StepMania when to end the song if your longest chart is shorter than this value. Normally song length is determined by the longest chart.
Required if your chart has only EDIT difficulties, as EDITs are not factored into song length calculation.

## \#BGCHANGES

Sets the Song's Background Changes.

An example of a background change:
```
#BGCHANGES:1.813=Impostor Advisory.mp4=1.000=1=0=1===CrossFade==,
99999=-nosongbg-=1.000=0=0=0 // don't automatically add -songbackground-
;
```

TODO: Add more documentation here.

## \#KEYSOUNDS

Play a sound at a certain time, tied to a successful tap of a note or hold of a hold note.

Alternatively if you add a keysound in an empty row it will be converted to an AutoKeysound and will play automatically.

You can add keysounds using the editor.

The \#KEYSOUNDS tag is formatted like `#KEYSOUNDS:\bgm.wav,01.wav,02.wav,` (yes, the `\` is intentional, the tag is actually written like that.)

## \#ATTACKS

Sets the Song's Attacks. The syntax is identical to [how modifiers are applied in a course](https://github.com/stepmania/stepmania/wiki/Courses#mods).

# NOTE DATA

After these tags have been set, you can now start setting up the notedata. (Charts/Steps as StepMania would call it.)

All timing related tags can also be used in the notedata section. Combo, Tickcount, Attacks, keysounds, also works. #MUSIC also works in the notedata section allowing you to have different songs for each steps, although in multiplayer it will pick the master player's song.

\#DISPLAYBPM also seems to be supported in this section, but no theme displays per-chart BPMs.

## \#NOTEDATA

This tag has no value (#NOTEDATA:;) and represents the beginning of a note data section in the file.

## \#CHARTNAME

Sets this Chart's Name. ("Style - Difficulty" is the default/standard.)

## \#STEPSTYPE

Sets this Chart's Step Type. ("GameType-Style" is the default/standard.)

## \#DESCRIPTION

Describes this Chart's Type/Style/Difficulty.

## \#CHARTSTYLE

Sets this Chart's Style Custom Name.

## \#DIFFICULTY

Sets this Chart's Difficulty. Possible values are: `Beginner`/`Easy`/`Medium`/`Hard`/`Challenge`/`Edit`

## \#METER

Sets this Chart's Foot Meter, more commonly known as the difficulty level in other rhythm games.

The foot meter can be any number.

## \#RADARVALUES

Sets this Chart's Radar Values. Usually these are automatically generated by the editor. (someone edit this section more.)

## \#CREDIT

Sets this Chart's Creators/Credits.

## \#NOTES

Sets this Chart's Notes.

## \#NOTES2

This tag is written instead of \#NOTES if you have keysounds in your ssc. Despite this, the ssc loader still loads it the same regardless of the tag.