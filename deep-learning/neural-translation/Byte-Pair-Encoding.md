# Byte Pair Encoding:

## Neural Machine Translation of Rare Words with Subword Units
1) Abstract & Introduction
   1) NMT is open vocabulary!
   2) Rare and unknown words are encoded as a sequence of sub-word units.
   3) human names are the primary source of rare words because they don't usually appear in dictionaries!
2) All in all, this paper says using subword units can alleviate the problems in translating rare words.
   1) Because it's capable of modeling various words using sub-words :)
3) Byte Pair Encoding:
   1) Instead of bytes, characters or sequence of characters are used for word segmentation!
   2) The number of vocabularies is equal to number of initial vocabs and the total of merged operations
      1) For example, if `A` and `B` occur together a lot, they are merged to `AB`.
   3) If a word in not seen in the training set, the encoder converts it to the largest known units!
