AutoStepper is a Java console program designed to automatically create StepMania SM files with these features:

* Generate all difficulty levels
* Generate holds & jumps
* Obtain banner & background art
* Run locally without interaction
* Process multiple music files at once
* Multiple beat detection methods
* Cross-platform support

So, here it is -- AutoStepper by Phr00t's Software (www.phr00t.com):

https://github.com/phr00t/AutoStepper

It works on a common line with arguments, which are all optional. If you just run the Java program, it will scan & process all mp3s (and wavs) in the current directory, and spit out folders for each song in the same directory (90 seconds worth of steps).

The arguments are:

input=[file/dir] output=[songs dir] duration=[seconds to process] synctime=[offset start time in seconds] tap=[true/false] hard=[true/false]

If you set tap=true, AutoStepper won't try and automatically calculate the BPM or offset, and will instead prompt you to hit ENTER along with 30 consecutive beats. AutoStepper will then do the rest.

It is best to let AutoStepper run through a whole bunch of music, and ones that it might not get exactly right -- to then pull out & use tap=true on them.

You can also use the output as a base to further edit & perfect songs, with AutoStepper doing most of the dirty work.

I will add it is optimized for pad use, not keyboard use (e.g. difficulty isn't high enough). Enjoy, it is free!

- Phr00t