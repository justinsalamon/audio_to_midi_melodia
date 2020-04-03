# audio_to_midi_melodia
Extract the melody notes from an audio file and export them to MIDI and (optionally) JAMS files.

The script extracts the melody from an audio file using the [Melodia](http://mtg.upf.edu/technologies/melodia) algorithm, and then segments the continuous pitch sequence into a series of quantized notes, and exports to MIDI using the provided BPM. If the `--jams` option is specified the script will also save the output as a JAMS file. Note that the JAMS file uses the original note onset/offset times estimated by the algorithm and ignores the provided BPM value.

Note: extracting a MIDI melody from a polyphonic audio file involves two main steps: 
1. melody extraction 
2. note segmentation. 

**Melody extraction** is the task of estimating the continuous fundamental frequency (f0) of the melody from a polyphonic audio recording. This is achieved using the Melodia melody extraction algorithm, which is the result of [several years of research](http://www.justinsalamon.com/phd-thesis.html). 

**Note segmentation** is the task of converting the continuous f0 curve estimated by Melodia (which can contain e.g. glissando and vibrato) into a sequence of quantized notes each with a start time, end time, and fixed pitch value. **Unlike Melodia, the note segmentation code used here was written during a single-day hackathon** and designed to be as simple as possible. Peformance will vary depending on musical content, and it will most likely not provide results that are as good as those provided by state-of-the-art note segmentation/quantization algorithms.

# Usage
```bash
>python audio_to_midi_melodia.py infile outfile bpm [--smooth SMOOTH] [--minduration MINDURATION] [--jams]
```
For example:
```bash
>python audio_to_midi_melodia.py ~/song.wav ~/song.mid 60 --smooth 0.25 --minduration 0.1 --jams
```
Details:
```
usage: audio_to_midi_melodia.py [-h] [--smooth SMOOTH]
                                [--minduration MINDURATION] [--jams]
                                infile outfile bpm

positional arguments:
  infile                Path to input audio file.
  outfile               Path for saving output MIDI file.
  bpm                   Tempo of the track in BPM.

optional arguments:
  -h, --help            show this help message and exit
  --smooth SMOOTH       Smooth the pitch sequence with a median filter of the
                        provided duration (in seconds).
  --minduration MINDURATION
                        Minimum allowed duration for note (in seconds).
                        Shorter notes will be removed.
  --jams                Also save output in JAMS format.
```

# Installation
**Windows users:** if you run into any installation issues please [read and try the solutions on this thread](https://github.com/justinsalamon/audio_to_midi_melodia/issues/4) before posting an issue, thanks!

### Non-python dependencies
- Melodia melody extraction Vamp plugin: http://mtg.upf.edu/technologies/melodia
- Please read and follow the installation instructions in Melodia's README file.
### Python dependencies
This program requires Python 2.7 (it has not been tested on Python 3 and might crash).

**Windows users must use a 32-bit installation of Python 2.7**, even if their OS is 64 bit, and **place the Melodia vamp plugin files in the correct path** (`C:\Program Files (x86)\Vamp Plugins`). Otherwise you might get the following error: `TypeError: Failed to load plugin: mtg-melodia:melodia`.

All python dependencies (listed below) can be installed by calling `pip install -r requirements.txt`.
- soundfile: https://pypi.org/project/SoundFile/
- resampy: https://pypi.org/project/resampy/
- vamp: https://pypi.python.org/pypi/vamp
- midiutil: https://pypi.org/project/MIDIUtil/
- jams: https://pypi.org/project/jams/
- numpy: https://pypi.org/project/numpy/
- scipy: https://pypi.org/project/scipy/

Known to work with the following module versions on python 2.7:
- SoundFile==0.10.2
- resampy==0.2.1
- vamp==1.1.0
- MIDIUtil==1.2.1
- jams==0.3.3
- numpy==1.16.2
- scipy==1.2.1

# How to contribute
If you would like to contribute a feature and/or bugfix to this repository, please follow the following steps:
1. Create an issue describing the bug/feature
2. I will reply on the issue thread to determine whether the feature can/should be added
3. Discuss design/implementation details in the issue thread and reach consensus
4. Once consensus is reached re: design/implementation, start a pull request
5. Request code review once the pull requets is ready for review
6. Fix requested changes to the pull request (if any)
7. Pull request will then be merged

IMPORTANT: please be sure to always discuss a proposed feature/fix in an issue *before* creating a pull request.
