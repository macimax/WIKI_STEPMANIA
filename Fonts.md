Fonts can be generated using the Texture Font Generator included with StepMania. (If you're not on Windows, WINE works too)

**This help page can also be found in /Docs/Themerdocs/fontini.txt.**

# [common]
### CapitalsOnly
If set to 1, lowercase letters are drawn with uppercase letters instead.
### RightToLeft
Font should be rendered as right to left.
### DefaultStrokeColor
Sets default stroke color. (e.g. #00000000)

# [main]
### import
Imports a font page into the current font.

## (per-page)
### DrawExtraPixelsLeft
How many pixels to draw to the left of a character.
### DrawExtraPixelsRight
How many pixels to draw to the right of a character.
### AddToAllWidths
Adds x amount of pixels to all character widths, making them more spaced out.
### ScaleAllWidthsBy
Scales widths by the factor specified.
### LineSpacing
Modifies the space between lines of text when using wrapwidth or `\n`.
### Top
Specifies the top of the character. (in pixels)
### Baseline
Specifies the baseline of the character. (in pixels)
### DefaultWidth
Default width for a glyph.
### AdvanceExtraPixels
Rudimentary way to control letter spacing (TODO: What does this mean?)
### TextureHints
An alternative to throwing the [TextureHints](https://github.com/stepmania/stepmania/wiki/Theming#image-hints) in the filename.

## (general commands)
### MAP
Maps a keyword to a frame number. (e.g. `map up=0` maps the word 'up' to the first frame of the bitmap)
### RANGE
Defines a Unicode range to use.
### LINE
What characters are on which line of the bitmap image. For example, if the first row of your image has ABCDEFGH, you would put down `Line 0=ABCDEFGH`