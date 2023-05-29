# Inception Score:
Inception score is used to evaluate the quality of generated images. It's a metric which is used to evaluate the quality of generated images. 
It's based on the idea that the generated images should be diverse and realistic.

## How it works?
1. It uses a pretrained Inception model to classify the generated images.
2. It uses the softmax output of the Inception model to calculate two metrics: marginal entropy and conditional entropy.
3. conditional entropy is used to measure the quality of generated images.
4. marginal entropy is used to measure the diversity of generated images.
**5. conditional entropy is used to calculate the Inception score. The marginal entropy is not used in the Inception score.** 

## Marginal entropy
1. The marginal entropy is the average of the softmax output of the Inception model.
2. It shows how diverse the generated images are. If the generated images are diverse, the marginal entropy will be high.
The equation for marginal entropy is as follows:</br>
3. H(y) = -∑[p(y) * log(p(y))] </br>
4. where p(y) is the softmax output of the Inception model for a sample.</br>
5. The marginal entropy is calculated for all the generated images and then the average of them is calculated. It's **not**
calculated for each class.


## Conditional entropy
The conditional entropy is the average of the softmax output of the Inception model for each class.
It shows how realistic the generated images are. If the generated images are realistic, the conditional entropy will be low.
The equation for conditional entropy is as follows:</br>
H(y|x) = -∑[p(y|x) * log(p(y|x))] </br>
where p(y|x) is the softmax output of the Inception model for each class.</br>
The conditional entropy is calculated for each class and then the average of them is calculated. 


## Inception score
1. Generate a set of images using the generative model.
2. Pass the generated images through a pre-trained Inception model to obtain the softmax probabilities for each image.
3. Calculate the conditional entropy for each generated image based on its softmax probabilities. 
   4. The conditional entropy is computed as:
   4. H(y|x) = -∑[p(y|x) * log(p(y|x))] 
   5. Here, p(y|x) represents the probability distribution of class labels given a generated image x, and the summation is taken over all possible class labels.
4. Average the conditional entropies over all generated images to obtain the mean conditional entropy.
5. Calculate the exponential of the mean conditional entropy to obtain the Inception Score.
6. The Inception Score is calculated as:
   7. mean_conditional_entropy = 1/N * ∑[H(y|x)]
   **7. IS = exp(mean_conditional_entropy)**
   8. Here, mean_conditional_entropy is the mean conditional entropy calculated in the previous step.
