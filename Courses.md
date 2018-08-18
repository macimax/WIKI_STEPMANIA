Most of this was taken from Docs/CourseFormat.txt, which may or may not be outdated.

To set up a course, create a text file in a folder in Courses with a .crs extension, then fill it with the tags available below.

A complete example of a course (this one comes with StepMania, you can see it for yourself at `Courses/Default/Jupiter.crs`):
```#COURSE:Jupiter;
#SCRIPTER:Midiman;
#METER:Medium:5;

#GAINSECONDS:120;
#SONG:StepMania 5\Springtime:Medium;nodifficult;

#GAINSECONDS:25;
#SONG:StepMania 5\MechaTribe Assault:Easy;nodifficult;
```

Another example:
```#COURSE:My Awesome Course - The Revenge;
#METER:Medium:8;

#MODS:
	TIME:1.00:END:50.00:MODS:C150;
#SONG:In The Groove/Dawn:Overhead;
#SONG:In The Groove/Mouth:;
#SONG:In The Groove 2/Funk Factory:;
#SONG:In The Groove 3/Disconnected Zeo:;
```
# Header content
Header Content is any course-defining data, such as the title, banner, and other parameters.
## #COURSE
The title of the course. Ex. `#COURSE:My Course!;`

## #COURSETRANSLIT
The title of the course, transliterated into english. Ex. `#COURSETRANSLIT:My Course, Translated!;`

## #SCRIPTER
The author of the course.

## #REPEAT
If this is present, the course does not end.
Useful for endless & workout courses.
Ex. `#REPEAT:YES;`

## #LIVES
The maximum(?) number of lives attainable in the course. Enabling this will automatically force your course into an Oni course. Ex. `#LIVES:4;`

## #DESCRIPTION
A description for your course, if any theme uses it. Ex. `#DESCRIPTION:Hello world!`

## #BANNER
A banner for your course. Ex. `#BANNER:My Banner.png;`

## #BACKGROUND
A background for your course. Currently only available in SM5 and sm-ssc. Ex. `#BACKGROUND:My Background.png;`

## #STYLE
Denote which styles may be played on this course. This is useful for cloning courses for doubles and single styles.
Ex. `#STYLE:SINGLE,VERSUS;`

## #METER
A custom-set meter for that course difficulty. You may set the difficulty
for Beginner, Easy, Medium, Hard, Challenge and Edit difficulties.
Ex. `#METER:Beginner:3;`

# Song Content
Song Content makes up the entries in the course, and also allows for timed modifiers.

## #GAINSECONDS
The number of seconds gained before starting a song. This and #LIVES are
mutually exclusive: you can either have one, the other, or none: both
is not possible. This is meant to be used for Survival courses. Ex. `#GAINSECONDS:60.5;`

## #SONG
#SONG can take quite a variety of parameters, of which may be useful to you
for testing or other purposes.
`*` is a wildcard item, meaning that StepMania will always pick a random song
for this part of the course.
You can also replace with `BEST*`, `WORST*`, `GRADEBEST*`, or `GRADEWORST*`, where `*` 
is a number to retrieve the first of each category above.

Ex. `#SONG:*:Medium:2x;` or `#SONG:BEST1:Medium:2x;`

As well as that, you may also do Group Random, like such:
`#SONG:Dance Dance Revolution 8th Mix/*:Medium:2x;`

If the above is not applicable, StepMania will search for the song title as best it can, depending on what you give it:

`#SONG:Xepher:Medium:2x;` Will simply search the title of the song.

`#SONG:DDR Supernova/Xepher:Medium:2x;` Will search for the exact directory.

#SONG can also apply different effects on each entry in the course by adding special modifiers to the modifiers segment:

For example, `#SONG:*:Medium:showcourse;` forces the course to never be hidden, noshowcourse being the reverse of such.

`nodifficult` also exists to disable a player from changing difficulties, 
barring the player from making it easier or harder ( Gauntlets & Survivals
do not allow you to change difficulties ).

Finally, `award*`, where `*` is a number, allows you to control how many lives the player gains from successfully completing a course in Oni mode.

## #MODS
To add [Modifiers](https://github.com/stepmania/stepmania/wiki/List-of-Song-Modifiers), place a #MODS tag below the #SONG tag with your modifiers. If instead you would like the mods to apply to all songs, put the #MODS tag above the first #SONG tag (not 100% sure on this one).

Modifiers can be assigned in a variety of formats, the most effective three being the following:

1. Repeated Modifier Block w/ Length:
```#MODS:TIME:0.500:LEN:0.500:MODS:2x;
#MODS:TIME:1.500:LEN:0.500:MODS:0.5x;
```
2. Nested Modifier Block w/ Length:
```
#MODS:
	TIME:0.500:LEN:0.500:MODS:2x;
	TIME:1.500:LEN:0.500:MODS:0.5x;
```
3. Nested Modifier Block w/ Ends:
```
#MODS:
	TIME:0.500:END:1.000:MODS:2x;
	TIME:1.500:END:1.500:MODS:0.5x;
```

# Some information for themers

If a song in a course uses a wildcard to pick a song like `#SONG:*:Medium:2x;`, doing `course:GetCourseEntry(i):GetSong();` (where course is the instance of your course and i is the index of the song) will return `nil`. Make sure you account for that and indicate that the song is random in the course screen.