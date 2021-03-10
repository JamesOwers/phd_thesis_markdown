# Data augmentation

<!-- https://www.wikizero.com/en/Wikipedia:Emerson -->
> ...I have always been of opinion that consistency is the last refuge of the
unimaginative: but have we not all seen, and most of us admired, a picture from
[Whistler's] hand of exquisite English girls strolling by an opal sea in the fantastic
dresses of Japan?

-- Oscar Wilde, "The Relation of Dress to Art: A Note in Black and
White on Mr. Whistler's Lecture", Pall Mall Gazette, February 28, 1885.

A model's generalisability is its most important quality with respect to predicting its
future performance in a new data context; we can expect a model which generalises well
to perform _according to its evaluation_ within a context nominally similar to the data
from which its parameters were learned -- the training dataset. A model which does not
generalise well could still report very high evaluation metrics on the training dataset
but perform poorly when released into the real world; its parameters having been
overfitted to the training dataset.

Many strategies are employed to encourage models to generalise. For instance, one
strategy, regularisation, controls the complexity of the model which can be learned. The
idea is that simple models can generalise better; if a model is too powerful or complex
it could simply learn the training dataset "by rote" and, since it has learned no
abstract patterns, do nothing but regurgitate parts of the training dataset. A model can
be regularised by adding a term to its loss function to penalise extreme settings of
parameters i.e. changing the likelihood of learning a given set of parameters.

Data augmentation encompasses methods which aim to improve generalisability by
effectively expanding the size of, and/or adding noise to, the training dataset seen by
the model. By seeing a larger quantity of more variant data than the training dataset
the model will better generalise -- if there is randomised noise, the model cannot learn
"by rote". This approach has had much success within the field of NLP, in particular see
these recent approaches: BART [@lewis_bart_2020] and, subsequently, Speller100
[@lu_speller100_2021]. Within the field of computer vision, [@cubuk_autoaugment_2019]
advocate the automated application of data augmentation for the ImageNet task
[@deng_imagenet_2009], a classification task for image data. They find that by
automatically tuning the type of data augmentation they apply for each task, they can
attain a significant improvement over the state-of-the-art. In [@antoniou_data_2018],
the authors explicitly investigate the effects of generating augmented data in low-data
regimes, advocating the use of learned generators---essentially what MDTK's `Degrader`
objects are, described below---using GANs. Finally, in [@salamon_deep_2017], the authors
solve their low-data regime issue for environmental sound classification by using data
augmentation, finding that performing augmentations such as pitch shifting and time
stretching leads to a 6 percentage point boost in classification accuracy. MDTK enables
similar such data augmentation techniques to be performed on symbolic music.

In this chapter we present a toolkit for adding noise to symbolic music: the MIDI
degradation toolkit (MDTK). This is previously published work, jointly authoured by the
author of this thesis and a collaborator, presented at the 21st International Society
for Music Information Retrieval Conference.

## The MIDI degradation toolkit

In [@mcleod_midi_2020] we presented MDTK. It was originally developed for an Automatic
Music Transcription (AMT) setting, specifically, to generate large datasets for training
discriminative models which correct transcription errors. MDTK is a python
[@van_rossum_python_1995] package which contains, amongst other things, functions which
alter the symbolic music data input.

The paper, poster, and a short introductory video
are available online here:
[https://program.ismir2020.net/poster_6-10.html](https://program.ismir2020.net/poster_6-10.html)

The toolkit code is open source, and available on GitHub here:
[https://github.com/JamesOwers/midi_degradation_toolkit](https://github.com/JamesOwers/midi_degradation_toolkit)

### The degradations made available by MDTK

*@fig:mdtk_degradations provides a visualisation of the 8 different types of
degradations available for application with the package. Each function which performs a
degradation considers the input to be a sequence of notes and either edits, removes, or
adds a note to the sequence.

<!-- Poster here: https://my.visme.co/editor/ZC9rcldZYVVxWHI4dnlkenl3WSsvQT09OjqIz8AkTj_aD5FHgykZ9SSL -->
![Illustrations for all the degradations currently available in MDTK](source/figures/mdtk_degradations.png "The degradations available in MDTK"){#fig:mdtk_degradations width=100%}

We now briefly describe each of these degradations:

* Changes to pitch:
  1. `pitch_shift`: changes the pitch of a random note. By default, the new pitch is
     chosen uniformly at random from all possible pitches (a minimum and maximum pitch
     can be given, and the valid range defaults to 21--108 inclusive). It can also be
     drawn from a weighted distribution of intervals around the original pitch, for
     example to emphasize octave errors from overtones. We also include a flag to force
     the new pitch to align with the pitch of some other note in the input, to reduce
     out-of-key shifts, if desired.
* Changes to timing:
  * For all of these degradations, care is taken to ensure that the shifted note does
    not lie outside the input's initial time range. A minimum and maximum resulting
    duration can be specified, as well as a minimum and maximum shift amount. We also
    include flags to align some combination of the shifted note's onset or duration with
    those of other notes from the input, ensuring the note lies on some metrical grid,
    if desired.
  2. `onset_shift`: changes the note's onset time (the time at which the note begins
     sounding), leaving its offset time (the time at which the note ends sounding)
     unchanged
  3. `offset_shift`: changes the note's offset time, leaving its onset time unchanged
  4. `time_shift`: changes the note's onset and offset times by the same amount, leaving
     its duration unchanged
* Adding new notes or removing existing notes:
  5. `add_note`: introduces a new note, flags to align an added note's pitch, onset, or
     duration to those of existing notes are included.
  6. `remove_note`: removes a random note from an input
* Splitting/combining existing notes:
  7. `split_note`: cuts a random note into some number of consecutive notes of shorter
     duration (the first of which begins at the original note's onset time and the last
     of which ends at the original note's offset time). By default the note is split
     into two shorter notes, but this---as well as a minimum allowable duration for the
     resulting notes---can be set with a parameter.
  8. `join_notes`: takes two or more consecutive notes at the same pitch (with a maximum
     allowable gap---set with a parameter---allowed between them), and joins them into a
     single note with onset time equal to that of the first note and offset time equal
     to that of the last.

### Additional tools provided by MDTK

MDTK also includes the `Degrader` class, which can be used to degrade inputs
dynamically. When instantiating a `Degrader` object, the proportion of inputs that
should remain undegraded is set with a parameter (which can be 0). The probability of
each degradation being performed on the input (if it is to be degraded) can also be set
at this time. Then, each time `Degrader.degrade(input)` is called, a randomly degraded
version of the input is generated according to the proportions set during object
creation. The `Degrader` class can be easily inserted into any model training procedure
in order to dynamically create new degraded inputs during each epoch, enabling the model
to be trained on a dataset which is essentially unlimited in size.

Additional utility functions are provided to convert between MIDI format and Pandas
DataFrames [@mckinney_data_2010] & [@pandas_software_2021] holding the sequence of notes
-- pandas DataFrames are a useful data structure in Python to hold columnar data. The
toolkit can also handle data in the midi-like command format. An illustration of data
types is given in *@fig:data_formats.

![Data formats -- On the left, a piano roll, on the right, the same data expressed as a
sequence of commands. The piano roll has two parts - the first (shown above) indicates
where notes are sounding, the second (shown below) shows where note onsets are
happening.](source/figures/dataformats.pdf "Different data formats handled by
MDTK"){#fig:data_formats width=100%}

## An experiment illustrating performance gains with MDTK



![TODO: it's not clear that we need this...leaving here for now. An example degradation performed by MDTK](source/figures/example.png "Example MDTK degradation"){#fig:mdtk_degradation_example width=100%}
