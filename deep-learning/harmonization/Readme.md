# Harmonization

## A deeplearning-based multisite neuroimage harmonization framework established with a traveling-subject dataset
### Abstract:
1. image harmonization is done to remove the artifacts created on neurimages due to different capturing devices.
   1. Some images from different sites might have different site effects which must be removed!


## DeepHarmony: A deep learning approach to contrast harmonization across scanner changes
1) Abstract: 
   2) Using Unet they want to mitigate the scanner result over a cohort of MS patients
3) Harmonization(U-Net Implementation)
   4) ![img.png](images/deep-harmoni-arch-image.png)
   4) Unet has a new concatenation at the end: they concat the inputs channel to the layer prior to final layer
      5) The first green arrow
      6)  This allows the network to include the input contrasts in the final 1x1 convolutional layer, directing the final feature maps to only augment the input contrasts, instead of recreating the target contrasts entirely.
   6) The second innovation is the use of strided convolutions instead of pooling layers
      5) They believe that using 4*4 kernels eliminates the artifacts created by strided conv and upsampling layers reported previously.
6) Network Training:
   7) Mean Absolute Error was used as the training loss function
      8) So small differences could contribute as well
   9) Adam
   10) No Dropout or regulation
   11) SSIM was used and MAE were used as validation metrics
   12) 