#Music

A library to aid the use of musical concepts in lua projects.


##Installation
This music.lua can be dropped into a project, and required as thus:
`music = require "music"`

##Examples

###Transposing a frequency up a fifth.
```lua
    local freq = 634
    print(freq * music.pitchRatio(music.interval("P5")))
    -- 949.92668673982
```

###Testing if two notes are enharmonic
```lua
    local CSharp = "C#"
    local BSharps = "B##"
    local FNatural = "F"

    print(music.noteAsInt(CSharp) == music.noteAsInt(BSharps))
    print(music.noteAsInt(CSharp) == music.noteAsInt(FNatural))
    print(music.noteAsInt(BSharps) == music.noteAsInt(FNatural))
    -- true
    -- false
    -- false
```

###Printing out the pitches for a G# harmonic minor scale:
```lua
    local GSMinor = music.scale("G#",music.scales.harmonic)
    local outtable = {}
    for _,n in ipairs(GSMinor) do
        table.insert(outtable,music.intAsNote(n))
    end
    print(table.concat(outtable,","))
    -- G#,A#,B,C#,D#,E,F#
```

##Function Reference

###music.pitchRatio(semitones)
Returns a ratio that will modify a sound by `semitones`.

###music.midiToFrequency(midinote [, afreq])
Returns the frequency value of a midi note. If `afreq` is given it is used as
A4's pitch instead of the standard 440Hz.

###music.noteToInt(notename)
Given a valid `note` (as a string), returns an integer value describing the notes
pitch in relation to a C. Returns an integer between 0 and 11.

A valid note pitch is one where the first character is the base note, and every
character after it is either a # or b, that will raise or lower the pitch. For
instance, `C` is the same as `Dbb` or even `Ebbbb`.

###music.intToNote(noteint)
Does the reverse of music.noteAsInt. Returns a notestring.

###music.normalizeNoteName(notename)
Given a note string, returns a sane version of the notestring.
```lua
    local crazynote = "Cbb#b#bbb##"
    print(music.normalizeNoteName(crazynote))
    -- A#
```

###music.interval(interval)
Gives the number of semi tones needed to aquire the specified `interval`. A
valid interval will always have a quality, and then a number specifying the
interval. Valid qualities are `P` for perfect, `M` for major, `m` for minor, `d`
for diminished, and `A for augmented.

###music.chord(root,chord)
Gets a chord `chord` built off of `root`. Chord is a table with intervals inside.
Example:
`d_minor_chord = music.chord("D",music.chords.minor) -- Result: {2, 5, 9}`


###music.scale(key,scale)
Given a key and scale, returns a table of the pitches in a scale. Example:
`local DMaj = music.scale("D",music.scales.major)`


##Variable Reference

###Scales
####Major
`music.scales.major`  

####Minor
`music.scales.minor`  
`music.scales.harmonicminor`  
`music.scales.melodicminor`  

####Other modes
`music.scales.dorian`  
`music.scales.phrygian`  
`music.scales.lydian`  
`music.scales.mixolydian`  
`music.scales.aeolian`  
`music.scales.locrian`  

###Chords
`music.chords.major`  
`music.chords.minor`  
`music.chords.dim`  
`music.chords.MM7`  
`music.chords.Mm7`  
`music.chords.mm7`  
`music.chords.dim7`  
`music.chords.hdim7`  

##TODO
* Fix intervals so you can have a dim 7. Perhaps just use a simple table look up?
  No fancy trickery?
* Add in testing.