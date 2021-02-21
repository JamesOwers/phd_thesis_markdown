
# Literature Review

...TODO... 

- [ ] Add content and TODOs from Quip:
    - [ ] https://quip.com/vVjVADMamfDm/2-Literature-Review
    - [ ] https://quip.com/v0MOAQGvMH3O/Literature-Review-Org-Notes
    - [ ] move data and notes tables in ./tables (use YAML, [allows large text blocks
      for notes](https://stackoverflow.com/a/3790497/2550114) easy to convert to table
      with python)
- [ ] outline the different problems people currently try to / can solve, and how these
  problems relate to 'being able to compose'
- [ ] Review available metrics
    - [ ] Motivate the need for automated evaluation metrics
    - [ ] Why has there been more work on audio than symbolic?
    - [ ] Motivate the need for better evaluation for both short and long term by
      highlighting shortcomings for each method reviewed
- [ ] Describe state-of-the-art generative models for music composition
- [ ] Identify a gap with respect to modelling long term dependencies by outlining
  claims and proof of them thus far - this is a specific thing we are going show is
  poorly evaluated
- [ ] Inform the reader about the multitude of different ways we can represent music and
  their relative strengths and weaknesses
- [ ] Address ethical shortcomings with respect to learning to compose
- [ ] Update bibtex references to non-arxiv reference if available


## Challenges addressed in the literature and how they are evaluated


## A summary of evaluation methods for creative models
...TODO... how to evaluate generative models with a focus on music - how do people
evaluate their success

### The need for automated metrics
- [ ] Humans are expensive - show some efforts
- [ ] Humans do not agree - show some research proving this
- [ ] Humans are susceptible to change their opinion depending on context - show some
  research proving this
- [ ] Consistency is key when tracking performance over the long term
- [ ] Attempts to unify metrics and human opinion - give WMT as an example
  [@haddow_wmt_2020]

### Differences between evaluating audio and symbolic outputs

[@dhariwal_jukebox_2020]

### The impossible task of satisfying all evaluation requirements with a single metric
- [ ] Should tie a metric with performance for an intended task [@theis_note_2016]

### Evaluation metrics and representations used for extracting musical structures


## Models for composing music
...TODO... State caveats about our distinctions:

1. Learning is essentially copying
2. By specifying the method of learning, we are incorporating expert knowledge
3. All models must work with a human composer to some extent - the programmer must
   choose a representation for the music and is therefore a composer in some senses

- [ ] Make and curate comparison table of models:
    - [ ] keep as csv
    - [ ] at min, we can use pandas to read and auto convert for insertion here
    - [ ] is there a way to `@reference` the file here and have pandoc insert? <- **do
      not spend time on this, cursory google!** 
- [ ] Music Transformer [@huang_music_2019]
- [ ] MuseNet [@payne_musenet_2019]
- [ ] Extend table from Chapter 7 and information from Chapter 6 in review paper
  [@briot_deep_2019] 
- [ ] Go through https://paperswithcode.com/task/music-generation


### Models which learn from scratch
...TODO... These are the models which our research pertains to

### Models which do not learn from scratch
...TODO... These models are stated to highlight why they are different, have an unfair
advantage in certain contexts, or explain why they are out of scope with respect to the
investigation of this thesis.

#### Heuristic models which primarily copy and edit music from a database

#### Models which incorporate expert knowledge into their design
...TODO... e.g. with respect to structural hierarchy

#### Models which only work in conjunction with a human composer

#### Proprietary models

Models for which adequate details of their design are not publicly available


## Methods for representing music on a computer
...TODO... how to represent music data - (in relation to 'from scratch', what is the
minimal information supplied to the models, and is there evidence of what difference it
makes (either by experiment or just by reasoning?)

- [ ] Note our desires with respect to our modelling challenges: we want the input to be
  *minimal and flexible* - the model should learn as much as possible as if it were a
  human listener
    - [ ] Ideally we would work directly on sound, but this involves an additional layer
      of representation.

### Information that must be captured about a musical performance

### The different representations of symbolic musical information

#### Summary of differences
- [ ] Highlight where *information* captured by each representation is both
  **different** and **more/less amenable to being learned**

### Availability of data for each representation
- [ ] Quantity,
- [ ] Quality,
- [ ] Legal issues

### Availability of software for different representations
- [ ] Describe MusPy [@dong_muspy_2020] for conversion between data formats
- [ ] Describe Music21 [@cuthbert_music21_2010] for conversion between data formats

### Evidence from the literature regarding modelling performance differences
- [ ] Find any reviews (or lack thereof) of model performance differences with respect
  to:
    - [ ] evaluation metrics
    - [ ] speed

## Ethical considerations when designing automated methods for composing music
