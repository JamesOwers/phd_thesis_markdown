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
"by rote". This approach has had much success for NLP, in particular see these recent
approaches: BART [@lewis_bart_2020] and, subsequently, Speller100 [@lu_speller100_2021].

In this chapter we present a toolkit for adding noise to symbolic music: the MIDI
degradation toolkit (MDTK). This is previously work published work, jointly authoured by
the author of this thesis and a collaborator, presented at the 21st
International Society for Music Information Retrieval Conference.

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

### The degradations available in MDTK

*@fig:mdtk_degradations

<!-- Poster here: https://my.visme.co/editor/ZC9rcldZYVVxWHI4dnlkenl3WSsvQT09OjqIz8AkTj_aD5FHgykZ9SSL -->
![Illustrations for all the degradations currently available in MDTK](source/figures/mdtk_degradations.png "The degradations available in MDTK"){#fig:mdtk_degradations width=100%}


We see in @fig:mdtk_degradation_example.

*@fig:data_formats shows.

![An example degradation performed by MDTK](source/figures/example.png "Example MDTK degradation"){#fig:mdtk_degradation_example width=100%}

![Data formats.](source/figures/dataformats.pdf "Different data formats handled"){#fig:data_formats width=100%}

## An experiment illustrating performance gains with MDTK
