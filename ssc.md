# About

(This wiki page is in progress... Feel free to alter it as needed...)

Stepmania's .sm format was updated to include more tags and more organization. Thus, .ssc was born. You can refer to the [.sm](https://github.com/stepmania/stepmania/wiki/sm) wiki to see the differences. Only .ssc files supportes BPM splitted across difficulties.

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

Sets the path to the Preview Video. (Based on the current Song's directory.)

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

Sets the path to a Preview file. (Based on the current Song's directory.)

## \#OFFSET

Sets the Song's Offset. (Effects the timing of the start of the NOTES.)

## \#SAMPLESTART

Sets the Song's Sample Start Timing.

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

A float value. Tells StepMania when to end the song if your longest chart is shorter than this value.
Required if your chart has only EDIT difficulties.

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

Play a sound at a certain time. Keysounds aren't tied to notes.

Note: Missing documentation on how this works, check [NotesLoader.cpp](https://github.com/stepmania/stepmania/blob/master/src/NotesLoaderSSC.cpp#L239) for the source code

## \#ATTACKS

Sets the Song's Attacks. The syntax is identical to [how modifiers are applied in a course](https://github.com/stepmania/stepmania/wiki/Courses#mods).

# NOTE DATA

After these tags have been set, you can now start setting up the notedata. (Charts/Steps as StepMania would call it.)

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

Whatever this tag is, it doesn't seem to actually be used...