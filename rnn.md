# RNN

## What is it&#x20;

are a class of neural networks that allow previous outputs to be used as inputs while having hidden states, which is able to transform information in a temporal sequence

## RNN (Recurrent Neural Network)

[GIF LSTM\&RNN Procedure](https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21) [YouTube](https://www.youtube.com/watch?time\_continue=193\&v=8HyCNIVRbSU)

Short-term memory dependency, not capable for long-term memory

## The Vanishing Gradient Problem In RNN

Weights are assigned at the start of the neural network with the random values, which are close to zero, and from there the network trains them up. But, when you start with wrec close to zero and multiply xt, xt-1, xt-2, xt-3, … by this value, your gradient becomes less and less with each multiplication.

**RNN中容易出现Gradient Vanishing是因为在梯度在向后传递的时候，由于相同的矩阵相乘次数太多，梯度倾向于逐渐消失，导致后面的结点无法更新参数，整个学习过程无法正常进行.**

![](<.gitbook/assets/image (71).png>)

### **Why**

This arrow means that long-term information has to **sequentially** travel through all cells before getting to the present processing cell. This means it can be **easily corrupted by being multiplied many time by small numbers < 0.** This is the cause of vanishing gradients.

**!!!** For example: these two are the common-used activation functions in RNN

Sigmoid as activation function

![](<.gitbook/assets/image (72).png>)

Tanh as activation function

![](<.gitbook/assets/image (73).png>)

**When backpropagating, the partial derivative of tanh or sigmoid activation function will restrict itself between 0-1, 0-0.25, correspondingly, **_**if the Weight < 4 => dev\_sigmoid'\* W < 1**_**, so the multiplication/chain rule of these function values will go to 0 as more and more layers in the network. **

{% embed url="https://www.cnblogs.com/bonelee/p/10475453.html" %}

****

**More details:**

![](<.gitbook/assets/image (74).png>)

### **Problem**

**If a change in the parameter's value causes very small change in the network's output - the network just can't learn the parameter effectively, which is a problem.** (the gradients of the network's output with respect to the parameters in the early layers become extremely small)

### **Cause**

**Vanishing gradient problem depends on the choice of the activation function.** Many common activation functions (e.g sigmoid or tanh) 'squash' their input into a very small output range in a very non-linear fashion. For example, sigmoid maps the real number line onto a "small" range of \[0, 1], especially with the function being very flat on most of the number-line. **As a result, there are large regions of the input space which are mapped to an extremely small range.** In these regions of the input space, **even a large change in the input will produce a small change in the output**- hence the gradient is small.

This becomes much **worse when we stack multiple layers** of such non-linearities on top of each other. For instance, first layer will map a large input region to a smaller output region, which will be mapped to an even smaller region by the second layer, which will be mapped to an even smaller region by the third layer and so on. As a result, **even a large change in the parameters of the first layer doesn't change the output much.**

We can **avoid this problem by using activation functions which don't have this property of 'squashing' the input space into a small region.** A popular choice is Rectified Linear Unit which maps xx to max(0,x)max(0,x).

![](<.gitbook/assets/image (75).png>)

While **backproporgating**, the weights are getting smaller as shows above will cause the gradient small, training slow and even model will not be able to trained properly.

![](<.gitbook/assets/image (76).png>)



### **Solution**

1. Exploding Gradient
   * **Truncated Backpropagation** (step BP after a certain point; that's probably not optimal because then you're not updating all the weights; if you don't stop, then you're just going to have a completely irrelevant network.)
   * **Penalties** (penalize gradient)
   * **Gradient Clipping** (have a maximum limit for the gradient.)
2. Vanishing Gradient
   * **Weight Initialization** (initialize your weights to minimize the potential for vanishing gradient.)
   * **Echo State Networks**
   * **LSTM**

## Bi-directional RNN

### Why

LSTM in its core, preserves information from inputs that has already passed through it using the hidden state.

Unidirectional LSTM only preserves information of the **past** because the only inputs it has seen are from the past.

Using bidirectional will run your inputs in two ways, one from past to future and one from future to past and what differs this approach from unidirectional is that in the LSTM that runs backwards you preserve information from the **future** and using the two hidden states combined you are able in any point in time to preserve information from **both past and future**.

What they are suited for is a very complicated question but BiLSTMs show very good results as they can understand context better, I will try to explain through an example.

Lets say we try to predict the next word in a sentence, on a high level what a unidirectional LSTM will see is

> The boys went to ....

And will try to predict the next word only by this context, with bidirectional LSTM you will be able to see information further down the road for example

Forward LSTM:

> The boys went to ...

Backward LSTM:

> ... and then they got out of the pool

You can see that using the information from the future it could be easier for the network to understand what the next word is.

##

## When/where to use it&#x20;

## What it can do and what it can't do
