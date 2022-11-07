# Decoding Strategies for ASR/Acoustic Models


## Comparison of Decoding Strategies for CTC Acoustic Models
1) Abstract-Introduction:
   1) 3 options:
      1) fixed vocabulary, Weighted Finite State Transducers with n-gram LMs
      2) open vocabulary, character based LM, and beam search(Like Wav2Vec2)
      3) sequence-to-sequence models. input: sound, output: word string
   2) CTC requires that its output symbols are conditional independent of each other. 
      1) This property of CTC entails the use of language model to apply the connection of output symbols.
   3) We compare the following approaches:
      1) Greedy Search without linguistic information
      2) WFST search with word language model [7, 8]
      3) Beam search using character RNN language model [9,10]
      4) Sequence  to  Sequence  approach  using  neural  machine-translation
2) **I didn't continue the paper because it was what I was looking for.**
3) paper: https://isl.anthropomatik.kit.edu/downloads/comparison-decoding-strategies.pdf


## My Notes:
1) There are several approaches:
   1) CTC can return the output of words
      1) It has problem: OOV(out of vocabulary)
      2) There are some vocabs that may not appear in the dataset. At inference time, they may cause problems!
   2) CTC character based. There will be no problem of OOV(out of vocabulary), but it needs a language model to make the output prediction realistic
   3) byte-pair-encoding (BPE). they tokenize a corpus. They can create OOV words if they had large token size!
   4) Some believe that attention module can compensate the lack of language model in E2E models because it addresses the exact part of input features that are required. However, some are not in the favor of this idea
      1) https://www.isca-speech.org/archive/pdfs/interspeech_2021/egorova21_interspeech.pdf
         1) Conclusion: CTC alignments provide better temporal information about word positions than the pure attention-based E2E system and so are more suitable for extracting OOV occurrences
2) Examples:
   1) Wav2vec2 is character based mainly because it's trained over several languages!
   2) Most fast ASR models are based on byte-pair-encoding because they should be used for one language, and they are not open vocabulary.


