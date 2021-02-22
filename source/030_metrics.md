
# New metrics for Evaluating Musical Generations

## Features of symbolic music

- [ ] Discuss different features which can be extracted

## The MIDI degradation toolkit

In [@mcleod_midi_2020] we present the MIDI degradation toolkit (MDTK). It was originally
developed for an Automatic Music Transcription (AMT) setting, specifically, to generate
large datasets for training discriminative models which correct transcription errors.
MDTK is a python [@van_rossum_python_1995] package which contains, amongst other things,
functions which alter the symbolic music data input. 

We see in @fig:mdtk_degradation_example.

*@fig:data_formats shows.

![An example degradation performed by MDTK](source/figures/example.png "Example MDTK degradation"){#fig:mdtk_degradation_example width=100%}

![Data formats.](source/figures/dataformats.pdf "Different data formats handled"){#fig:data_formats width=100%}

### Data augmentation

## Evaluation via downstream task performance

- [ ] Describe tasks as proposed in [@mcleod_midi_2020] which could be used to evaluate
  models which compose

## A phrase-level metric for short-term structure

## A piece-level metric for long-term structure