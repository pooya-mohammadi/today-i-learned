# Wav2Letter: an End-to-End ConvNet-based SpeechRecognition System
1) Inputs: MFCC, power-spectrum, and raw-wave 
   1) MFCC dimensionality compression - 13 coefficients
2) Output: letter scores (one score per letter, given a dictionary L)
3) CNN model
   1) 1D convolutional neural networks
   2) pointwise activation func
      1) HardTanh & ReLU led to same results
   3) strid & no pooling
   4) raw-wave has a huge first conv-layer at the beginning of the arch with a large stride to compensate for the enormous input size(16KHz)
   5) MFCC & power spectrum do not have the first layer of the main arch
4) No CTC -> something like it
   1) ASG: Audio Segmentation Criterion which does not have blank letters and other features where used
   2) caterpillar is turned to caterpil2ar to solve the repetition problem.
5) beam search decoder
   1) Relies heavily on KenLM 
6) GitHub:
   1) https://github.com/silversparro/wav2letter.pytorch
   2) https://github.com/LearnedVector/Wav2Letter
      1) greedy decoder 
      2) ctc
7) Paper:
   1) https://arxiv.org/pdf/1609.03193.pdf