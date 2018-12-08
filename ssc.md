# About

(This wiki page is in progress... Feel free to alter it as needed...)

Stepmania's .sm format was updated to include more tags and more organization. Thus, .ssc was born. You can refer to the [.sm](https://github.com/stepmania/stepmania/wiki/sm) wiki to see the differences.

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

Sets the .ssc Creator/Credits.

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

Sets the Song's Selectivity. (YES OR NO)

## \#BPMS

Sets the Song's Beats Per Minute's at certain times. (Can have multiple changes.)

### \#DISPLAYBPM
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

(someone edit this section.)

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

Sets the Song's Last Second Hint.

## \#BGCHANGES

Sets the Song's Background Change. (Can have multiple changes.)

## \#KEYSOUNDS

Play a sound at a certain time. Keysounds aren't tied to notes.

Note: Missing documentation on how this works, check [NotesLoader.cpp](https://github.com/stepmania/stepmania/blob/master/src/NotesLoaderSSC.cpp#L239) for the source code

## \#ATTACKS

Sets the Song's Attacks. (Can have multiple changes.)

# \#NOTE DATA

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

Sets this Chart's Foot Meter. (Any Number.)

## \#RADARVALUES

Sets this Chart's Radar Values. (someone edit this section more.)

## \#CREDIT

Sets this Chart's Creators/Credits.

## \#NOTES

Sets this Chart's Notes.