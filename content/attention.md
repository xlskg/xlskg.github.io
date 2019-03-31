Title: Attention
Date: 2019-03-30

# Background
## Attention
Attention is proposed in [1]. 

It fixes the issue: RNN encoder-decorder network need to compress all necessary information of a source sentence into **a fixed-length vector**.

It is a new method to calculate distinct context value for each target tag.

## Encoder-Decorder framework
### Encoder
**Encoder** read the input sentence: A sequence of vectors $\mathbf{x} = (x_{1},...,x_{T_{x}})$, ouput a vector $\mathbf{c}$
$$
    h_{t} = f(x_{t},h_{t-1})\tag{1}
$$
$$
    \mathbf{c} = q({h_{1},...,h_{T_{x}}})\tag{2}
$$

Note:

1. In (1), $h_{t}$ is only dependend on $h_{t-1}$ and $x_{t}$, just same as language model. $f$ is some nonlinear function(eg. LSTM)
2. In (2), $\mathbf{c}$ is a vector generated from the sequence of the hidden state. $q$ is some nonliner function. In RNN encoder-decoder model, $q$ = last element of hidden sequence. 

### Decoder
**Decoder** predict the next word $y_{t^\prime}$ given:

1. the context vector $\mathbf{c}$ 
2. all the previously predicted words ${y_1,...,y_{t^\prime-1}}$

In a concise mathematical language: the decoder defines a **probability** over the translation $\mathbf{y}$ by **decomposing** the joint probability into the ordered conditionals:

$$
    p(\mathbf{y}) = \prod_{t=1}^{T}p(y_t|{y_1,...,y_{t-1}},\mathbf{c})\tag{3}
$$

In particluar, with an RNN:

$$
    p(y_t|{y_1,...,y_{t-1},\mathbf{c}}) = g(y_{t-1},s_t,\mathbf{c})\tag{4}
$$

Some questiones: 

1. Is there any new $q$ function to calculate **context**. Can we get a new $q$ that is conditioned on a distinct context vector $c_i$ for each target $y_i$? [1]
2. Do we have an attention model that is independent with RNN? [2]


# Detail
## Distinct Context $c_i$ for each target $y_i$
$$
    p(y_i|y_1,...,y_{i-1},\mathbf{x}) = g(y_{i-1},s_i,c_i)\tag{5}
$$
Where
$$
    s_i = f(s_{i-1},y_{i-1},c_i)\tag{6}
$$
$$
    c_i = \sum_{j=1}^{T_x}a_{ij}h_j\tag{7}
$$
$$
    a_{ij} = \frac{\exp(e_{ij})}{\sum_{k=1}^{T_x}\exp(e_{ik})}
$$
$$
    e_{ij} = \alpha(s_{i-1},h_j)
$$

- $\alpha$ is a feedforward neural network
- $a_{ij}$ is a probability that the target word $y_i$ is aligned to a source word $x_j$. (soft alignment)
- i-th context vector $c_i$ is the expected annotation over all the annotation with probabilities $a_{ij}$

## Context independent with RNN
### Self-Attention Vector
![image]({static}/media/transformer_self_attention_vectors.png)

- Query Vector: a vector to **query** another vecotor
- Key Vector: a vector to **be queried**
- Value Vector: a vector of current word.

$$
    q_1 = X_1 \times W^Q\\
    k_1 = X_1 \times W^K\\
    v_1 = X_1 \times W^V
$$

### Self-Attention Representation
![image]({static}/media/self-attention-output.png)

A self-attention context-aware representation of word.

### Multi-Head Self-Attention Representation
![image]({static}/media/transformer_multi-headed_self-attention-recap.png)



# Reference
1. [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473)
2. [Attention is All you need](https://arxiv.org/abs/1706.03762) 
3. [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)



