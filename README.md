# Gemini FM MIDI Converter
The Gemini FM MIDI Converter converts MIDI files into ASCII data that can be compiled and played on the MSX with the [Gemini FM music replayer](https://github.com/TheNetNomad/Gemini-FM). Generated ASCII must be compiled with GFMASM.COM to play with GEMINIFM.COM. 

This is in developement. Try it yourself online [here](https://netnomad.neocities.org/gemconv/)

This code derived from and heavily based on g200kg's [midi-dump](https://github.com/g200kg/midi-dump) and jannone's [webMSX integration template](https://github.com/jannone/webmsx-integration-template).

# Usage
Upload a MIDI file in the below format using the "Select File:" button on the top left off the screen. If the MIDI file is capable of being dumped, a portion of the dump will appear beneath the webMSX display as well as a "Convert MIDI File" button. Pressing this button will convert the file and play it within webMSX.

To alter the tempo or the transposition of each channel, use the input fields above the text area on the right hand side. Press the "Reconvert" button to reconvert and reload the MIDI file with these new parameters. You may also edit the GFMASM listing in the below text area, and then press the "Reassemble" button to load your changes into webMSX. Please note that the "Reconvert" button will undo any manual changes done in the text area.

To save your result, you may click the first floppy disk icon on the lower webMSX menu and select "Save Disk Image" to save an MSX-DOS disk. Alternatively, you may copy the GFMASM listing from the text area.

# MIDI Format

Unfortunately you cannot just load any 'ol MIDI file into the GFM MIDI converter and have it work. This program needs the following to be true to create valid playback data:

- Only note on, note off, and program change events will be parsed.			
- All melodic data must reside between MIDI channels 1 and 6, which will be mapped to FM channels 0 through 5 appropriately.
- Each of these channels must be monophonic.
- Any key on event must be followed by a key off event before another key on can be issued, including percussion.
- All program changes/instrument settings must be between 1 - 32, which will be mapped to the [appropriate instrument](https://github.com/TheNetNomad/Gemini-FM#Instrument-Table).
- All drum data must reside on MIDI channels 9 or 10 and must be one of five notes corresponding to the five OPLL drum tones (see below).

## MIDI Drum Map
| Drum Tone | MIDI Note Name | MIDI Note Number |
| --- | --- | --- |
Bass Drum | C3 | 36
Snare | D3 | 38
Tom | G3 | 43
Crash | C#4 | 49 
Hi Hat | F#3 |  42
