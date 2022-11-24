# audio_to_midi_melodia
Extract the melody notes from an audio file and export them to MIDI and (optionally) JAMS files.

The script extracts the melody from an audio file using the [Melodia](http://mtg.upf.edu/technologies/melodia) algorithm, and then segments the continuous pitch sequence into a series of quantized notes, and exports to MIDI using the provided BPM. If the `--jams` option is specified the script will also save the output as a JAMS file. Note that the JAMS file uses the original note onset/offset times estimated by the algorithm and ignores the provided BPM value.

Note: Melodia can work pretty well and is the result of [several years of research](http://www.justinsalamon.com/publications). The note segmentation/quantization code was written to be as simple as possible and will most likely not provide results that are as good as those provided by state-of-the-art note segmentation/quantization algorithms.

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
### Non-python dependencies
- Melodia melody extraction Vamp plugin: http://mtg.upf.edu/technologies/melodia
### Python dependencies
This program requires Python 2.7 (it has not been tested on Python 3 and will most likely crash).

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
