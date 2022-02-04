# Gemini FM MIDI Converter
The Gemini FM MIDI Converter converts MIDI files into ASCII data that can be compiled and played on the MSX with the [Gemini FM music replayer](https://github.com/TheNetNomad/Gemini-FM). Generated ASCII must be compiled with GFMASM.COM to play with GEMINIFM.COM. 

This is in early developement. Try it yourself online [here](https://netnomad.neocities.org/gemconv/)

This code derived from and heavily based on g200kg's [midi-dump](https://github.com/g200kg/midi-dump).

# MIDI Format

Unfortunately you cannot just load any 'ol MIDI file into the GFM MIDI converter and have it work. This program needs the following to be true to create valid playback data:

- Only note on, note off, and program change events will be parsed.			
- All melodic data must reside between MIDI channels 1 and 6, which will be mapped to FM channels 0 through 5 appropriately.
- Each of these channels must be monophonic.
- Any key on event must be followed by a key off event before another key on can be issued, including percussion.
- All program changes/instrument settings must be between 1 - 32, which will be mapped to the [appropriate instrument](https://github.com/TheNetNomad/Gemini-FM#Instrument-Table).
- All drum data must reside on MIDI channels 9 or 10 and must be one of five notes corresponding to the five OPLL drum tones (see below).
- The input file must not be too big ("too big" is to be determined).

Please note that GFMASM.COM does not do any error checking and at this point, neither does the MIDI converter. Not meeting this criteria (or potentially other criteria I have not identified yet- early developement, please bare with me!) can lead to a MIDI file that is converted fine into ASCII data that is assembled fine into a binary file that does not play properly.

## MIDI Drum Map
| Drum Tone | MIDI Note Name | MIDI Note Number |
| --- | --- | --- |
Bass Drum | C3 | 36
Snare | D3 | 38
Tom | G3 | 43
Crash | C#4 | 49 
Hi Hat | F#3 |  42

# To Do
- Auto load result into WebMSX and automatically compile and play (unsure if this is feasible)
- Data validation/error checking
- Some method of embedding comments into GFMASM listing from the MIDI file (sysex?)
- Many many many bugfixes


