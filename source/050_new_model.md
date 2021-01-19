
# A New Model

Potential ideas:

* An improved generative model for music
    * Training like BERT? <http://jalammar.github.io/illustrated-bert/>
    * Using mdtk for data augmentation in training (negative examples?), making them more robust
    * Alternative training objectives:
        * crossentropy slow and not musically informed
        * can we use something akin to word error rate (this has been done for text)
* Alternative ways to encode music: encoding chords and phrases in a low-rank continuous space
    * Have done some work on this with convnets and generating continuations
        * low rank was enforced by cross-product ing two vecs
    * Could investigate effect of different representations for music on performance

