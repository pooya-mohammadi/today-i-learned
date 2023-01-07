# Cancer Diagnosis
## Colorectal Cancer Diagnosis from Histology Images: A Comparative Study
1. Abstract:
   1. cancer detection from low-resolution and scarce histology images using transfer-learning
   2. they have proposed an adaptive approach for cancer detection
2. Introduction: 
   1. InceptionV3 is used!
3. Al-Ahli Benchmark Dataset
   1. They took the images, applied data augmentation and lowered the resolution to mimic the low-resolution acquisition.
4. Methods:
   1. Basic Machin Vision algorithms like LBP
   2. Transfer Learning:
      1. three types of transfer learning applied to InceptionV3
   3. Adaptive Cnn
      1. They have proposed a new compact CNN model which is implemented in C++!
5. Results:
   1. cancer detection(binary classification): adaptive wins
   2. cancer identification(multi-class classification): transfer learning wins
6. References: https://arxiv.org/abs/1903.11210
