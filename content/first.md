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

- xl and xl+1 are input and output of the l-th unit, 
- F is a residualfunction. 
- h(xl) = xl is an identity mapping 
- f is a ReLU function

## Compare with tranditional NN
| \ | Residual Network | Tranditional NN |
|------|-------------|-------|
| Unraveled View | ![image]({static}/media/residual network.png) | ![image]({static}/media/tranditional NN.png) |
| Formula | \begin{aligned} y_{3} &= y_{2} + f_{3}(y_{2})\\ &=[y_{1} + f_{2}(y_{1})] + f_{3}(y_{1} + f_{2}(y_{1}))\\ &=[y_{0} + f_{1}(y_{0}) + f_{2}(y_{0}+ f_{1}(y_{0}))] + f_{3}(y_{0} + f_{1}(y_{0}) + f_{2}(y_{0}+f_{1}(y_{0}))) \end{aligned} | $y_{3}^{FF} = f_{3}^{FF}(f_{2}^{FF}(f_{1}^{FF}(y_{0})))$ |
| Feature | have **O(2n)** implicit paths connecting input and output | **ONE** path |

## More important: Gradient 
From $x_{l+1} = x_{l} + \mathcal F(x_{l}, \mathcal W_{l})$

To $x_{L} = x_{l} + \sum_{i=l}^{L-1} \mathcal F(x_{i}, \mathcal W_{i})$

- The model is in a **residual** fashion between any units L and l. (where the name residual come from)
- The formula is summation instead of matrix-vector products

**Gradient**: $$\frac {\partial \varepsilon}{\partial x_{l}} = \frac {\partial \varepsilon}{\partial x_{L}}\frac{\partial x_{L}}{\partial x_{l}} = \frac{\partial \varepsilon}{\partial x_{L}}(1+\frac{\partial}{\partial x_{l}} \sum_{i=l}^{L-1} \mathcal F(x_{i}, \mathcal W_{i}))$$

- Information is directly propagated back to any shallower unit l$\frac {\partial \varepsilon}{\partial x_{L}$
- General the $\frac{\partial}{\partial x_{l}} \sum_{i=l}^{L-1} \mathcal F$ cannot be always -1

So, the gradient of a layer **does not** vanish even when the weights are arbitrarily small.

## Various types of shortcut connections
![image]({static}/media/shortcut connections.png)

### A simple modification
$$ x_{l+1} = \lambda_{l}x_{l} + \mathcal F(x_{l}, \mathcal W_{l})$$
$$ x_{L} = (\prod_{i=l}^{L-1}\lambda_{i})x_{l} + \sum_{i=l}^{L-1}\hat{\mathcal F}(x_{i}, \mathcal W_{i})$$
$$ \frac {\partial \varepsilon}{\partial x_{l}} = \frac {\partial \varepsilon}{\partial x_{L}}((\prod_{i=l}^{L-1}\lambda_{i})+\frac{\partial}{\partial x_{l}}\sum_{i=L}^{L-1} \hat{\mathcal F}(x_{i}, \mathcal W_{i}))$$

## Various types of activation function
![image]({static}/media/activation function.png)

- Short out completely
- BN for ease overfit

# Reference
- [Deep_residual_learning_for_image_recognition_c2a0b.pdf]({static}/media/Deep_residual_learning_for_image_recognition_c2a0b.pdf)
- [Identity_Mappings_in_Deep_Residual_Networks_95817.pdf]({static}/media/Identity_Mappings_in_Deep_Residual_Networks_95817.pdf)
- [Residual_Networks_Behave_Like_Ensembles_of_Relatively_Shallow_Networks_13899.pdf]({static}/media/Residual_Networks_Behave_Like_Ensembles_of_Relatively_Shallow_Networks_13899.pdf)
