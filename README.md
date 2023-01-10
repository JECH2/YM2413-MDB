# YM2413-MDB
YM2413-MDB is an 80s FM video game music dataset with multi-label emotion annotations. It includes 669 audio and MIDI files of music from Sega and MSX PC games in the 80s using YM2413, a programmable sound generator based on FM. The collected game music is arranged with a subset of 15 monophonic instruments and one drum instrument.

## Update Log
- [Version 1.0.2](https://zenodo.org/record/7520537) is available: [Wrong emotion tag issue in the verification annotation file was fixed](https://github.com/jech2/YM2413-MDB/issues/2).

- [Version 1.0.1](https://zenodo.org/record/7479134): Fix ticks per beat value adjust to tempo where tempo values are not 150. Also, madmom downbeat files are updated from DBNBeatTracker(ISMIR, 2015) to TCNBeatTracker(Newer one EUSIPCO, 2019).

## Dataset
- includes:
    - uploaded vgm, midi, wav files ( 669 files excluding no note event files )
    - metadata of the emotion tags
    - other useful files such as downbeat estimated files by madmom, vgm event sequence txt files (F-number, Note On, Rhythm, Volume, Instrument)
- [Dataset demo page](https://jech2.github.io/YM2413-MDB/)
- [Dataset download link in Zenodo](https://zenodo.org/record/6566363)
- wav files were generated by using VGMPlay's vgm2wav

## YM2413 Converter
YM2413 Converter is a converter .vgm file to .mid file specifically for game music played by YM2413 sound chip, the sound chip in Sega Master System Japanese version.

Emulated sound chip source code was originally from the [VGMPlay](https://github.com/vgmrips/vgmplay), which was written in C.

FM sound chip data from two sites were tested.  
- https://www.smspower.org/Tags/FM
- https://vgmrips.net/packs/chip/ym2413

### Dependencies
python=3.8, miditoolkit, pandas, tqdm, scipy, matplotlib

### How to use the converter
First, you need to download the dataset and place it right directory: Default is ../YM2413-MDB-v1.0.0.
```
$ cd converter
$ python get_ydr.py
$ python run_converter.py
$ python postprocessing.py [--adjust_tempo --remove_delayed_inst]

```
### QnA about midi conversion
Since the pitch range that the FM synthesisized-VGM file can express(integer that is equivalent to Hz) is different from the MIDI(semitone-quantized pitch value), 
we cannot give a perfect 1:1 correspondence(or conversion). However, updates are being made to use the dataset as easy to use as possible.

- Why some of the notes / pitch values in midi files are not accurate?

It is due to the pitch bend. The pitch value (in Hz) is not always constant within one note. For these cases, pitch bend events are generated.

- Why some of the music downbeats in midi files are not accurate?

Since there are some music files that doesn't have any drum instrument. For those files, madmom algorithm is not accurate.

## Audio Rendering
Generated midi file are rendered using [VST2413](http://www.keijiro.tokyo/vst2413/). Although we manually rendered each midi files using [Ableton live 11](https://www.ableton.com/), we are planning to update this process in script level(python).



## TODO
- Upload music generation code
- Upload dataset usage


## Acknowledgement
[ValleyBell](https://github.com/ValleyBell) from VGMRips Community for discussing about vgm2midi conversion


## Citation
```
@inproceedings{{YM2413-MDB},
         author = {Eunjin Choi, Yoonjin Chung, Seolhee Lee, JongIk Jeon, Taegyun Kwon, Juhan Nam},
         title = {{YM2413-MDB}: A Multi-Instrumental {FM} Video Game Music Dataset with Emotion Annotations},
         booktitle = {Proc. Int. Society for Music Information Retrieval Conf.},
         year = {2022}
}
```
