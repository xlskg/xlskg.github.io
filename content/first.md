Title: First Article
Date: 2019-03-18 16:00

# Content
## How to analysis neural network abilities 
From Two dimensions: 
1. Representation Abilities. NN == RN
2. Optimization. RN has stronger 

- Residual network has same representation ablitiy with tranditional neual netork. But RN is easiesr to optimize.  
- Proposed residual network in [Identity_Mappings_in_Deep_Residual_Networks_95817.pdf](../media/Identity_Mappings_in_Deep_Residual_Networks_95817.pdf) has less representional ability than gating and 1x1 convolutional shortcuts.

## Problem on traditional NN
1. Deeper neural networks are more difficult(Accuracy/Efficiency) to train.
2. With the network depth increasing, accuracy gets saturated and then degrades rapidly.

## Model Architecture
|Original in [Deep_residual_learning_for_image_recognition_c2a0b.pdf](../media/Deep_residual_learning_for_image_recognition_c2a0b.pdf)|Proposed in [Identity_Mappings_in_Deep_Residual_Networks_95817.pdf](../media/Identity_Mappings_in_Deep_Residual_Networks_95817.pdf)|
|---------------------------------------------------------|---------------------------------------|
|![image]({static}/media/original_image.png)| ![image]({static}/media/full_pre.png)|

### Formula
$$y_{1} = h(x_{l}) + \mathcal F(x_{l}, \mathcal W_{l}), $$
$$x_{l+1} = f(y_{1})$$