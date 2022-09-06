# Deep Learning Metrics


## mAP@.5:.95:
   1. This the average scores the model gets for `[mAP@.50, mAP@.55, mAP@.60, ..., mAP@.95]`
   2. The `0.50` and others are IoU thresholds at which the sample is chosen to be correctly detected.
   3. Ex: `mAP@.95` means that a detected sample should have an IoU(detected box and ground truth box) score higher than 0.95 to be considered as a correct sample.