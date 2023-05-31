# FID (Fréchet Inception Distance)
FID is used to evaluate the quality of generated images.
It's a metric which is used to evaluate the quality of
generated images. It's based on the idea that the generated
images should be diverse and realistic.

## How does it work?
1. It uses a pretrained Inception model to extract features from the generated images and the real images.
2. It uses the extracted features to calculate the Fréchet distance between the two distributions.
3. The Fréchet distance is used to measure the quality of generated images.
4. The lower the Fréchet distance, the better the quality of the generated images.

## Fréchet distance

The Fréchet distance is a measure of similarity between two probability distributions over a metric space.</br>

### Formula
1. First, you need to compute the mean and covariance matrix of the feature representations extracted from real images and generated images.

2. Let μr and Σr be the mean vector and covariance matrix of the real image features, and μg and Σg be the mean vector and covariance matrix of the generated image features.

3. Compute the squared Euclidean distance between the mean vectors:

```||μr - μg||² = (μr - μg)ᵀ(μr - μg)```

4. Compute the matrix square root of the product of the covariance matrices:

```ΣrΣg = Σr^(1/2)(ΣrΣg)^(1/2)Σr^(1/2)```
where Σr^(1/2) is the matrix square root of Σr.

5. Compute the squared Frobenius norm of the matrix square root:

```||Σr^(1/2)ΣgΣr^(1/2)||_F² = trace(Σr + Σg - 2(ΣrΣg)^(1/2))```

6. Finally, the FID score is calculated as the sum of the squared Euclidean distance between the mean vectors and the squared Frobenius norm of the matrix square root:

```FID = ||μr - μg||² + ||Σr^(1/2)ΣgΣr^(1/2)||_F²```

## Conclusion
In a nutshell, this is another way to measure the quality and diversity of generated images. The lower the FID score, the better the quality and diversity of generated images.
We have also IS (Inception Score) which is another way to measure the quality and diversity of generated images. The higher the IS, the better the quality and diversity of generated images.
