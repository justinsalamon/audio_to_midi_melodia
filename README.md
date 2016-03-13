# audio_to_midi_melodia
Extract the melody from an audio file and convert it to MIDI.

The script extracts the melody from an audio file using the [Melodia](http://mtg.upf.edu/technologies/melodia) algorithm, and then segments the continuous pitch sequence into a series of quantized notes, and exports to MIDI using the provided BPM. If the `--jams` option is specified the script will also save the output as a JAMS file. Note that the JAMS file uses the original note onset/offset times estimated by the algorithm and ignores the provided BPM value.

Note: Melodia can work pretty well and is the result of several years of research. The note segmentation/quantization code was hacked in about 30 minutes. Proceed at your own risk... :)

# Usage
```bash
>python audio_to_midi_melodia.py infile outfile bpm [--smooth SMOOTH] [--minduration MINDURATION] [--jams]
```
For example:
```bash
>python audio_to_midi_melodia.py ~/song.wav ~/song.mid 60 --smooth 0.25 --minduration 0.1 --jams
```
For further help use:
```bash
>python audio_to_midi_melodia.py --help
```

# Dependencies
- Melodia melody extraction Vamp plugin: http://mtg.upf.edu/technologies/melodia
- Librosa: https://bmcfee.github.io/librosa/
- Vamp python module: https://pypi.python.org/pypi/vamp
- midiutil: https://code.google.com/p/midiutil/
- NumPy & SciPy: http://www.scipy.org/
- JAMS: https://github.com/marl/jams