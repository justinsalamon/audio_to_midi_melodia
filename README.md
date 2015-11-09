# audio_to_midi_melodia
Extract the melody from an audio file and export to MIDI

# Usage
```bash
>python audio_to_midi_melodia.py <inputfile.wav> <outputfile.mid> <bpm>
```
For example:
```bash
>python audio_to_midi_melodia.py ~/song.wav ~/song.mid 60
```

# Dependencies
- Melodia melody extraction Vamp plugin: http://mtg.upf.edu/technologies/melodia
- Librosa: https://bmcfee.github.io/librosa/
- Vamp python module: https://pypi.python.org/pypi/vamp
