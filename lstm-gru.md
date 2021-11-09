# LSTM-GRU

LSTM and GRU designed for solving the problem of gradient vanishing in vanilla RNN. It contains 3 gates, forget gate, input gate, output gate, which control the information flow inside the network transition. It also is able to transmit information on a long-term basis, so even the information that is useful for the current state mentioned in the temporal sequence long time ago, the model is still able to capture it.&#x20;

## The Vanishing Gradient Problem In RNN

**When backpropagating, the partial derivative of tanh or sigmoid activation function will restrict itself between 0-1, 0-0.25, correspondingly, **_**if the Weight < 4 => dev\_sigmoid'\* W < 1**_**, so the multiplication/chain rule of these function values will go to 0 as more and more layers in the network. **

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

## What is it&#x20;

LSTM and GRU designed for solving the problem of gradient vanishing in vanilla RNN. It contains 3 gates, forget gate, input gate, output gate, which control the information flow inside the network transition. It also is able to transmit information on a long-term basis, so even the information that is useful for the current state mentioned in the temporal sequence long time ago, the model is still able to capture it.&#x20;

## LSTM (Long Short-Term Memory)

[GIF LSTM Procedure](https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21) [YouTube](https://www.youtube.com/watch?time\_continue=193\&v=8HyCNIVRbSU)

[Understanding LSTM](https://colah.github.io/posts/2015-08-Understanding-LSTMs/)

![](<.gitbook/assets/image (105).png>)&#x20;

### Gates

#### Forget gate

This gate decides what information should be thrown away or kept, The closer to 0 means to forget, and the closer to 1 means to keep.

#### Input Gate

To update the cell state (memory pipeline); decides what information is relevant to add from the current step

#### Output Gate

The output gate decides what the next hidden state should be

### Avoid gradient vanishing HOW?

{% embed url="https://weberna.github.io/blog/2017/11/15/LSTM-Vanishing-Gradients.html" %}

1. **By turning the multiplication to additive**

Weight matrix are no longer multiplication, instead, cell state is adding the previous information and current processed information and pass through.

![](<.gitbook/assets/image (77).png>)

**2. Gates functions**

If we start to converge to zero (gradient vanishing/above function), we can always set the values of _f\_t_ (and other gate values) to be higher in order to bring the value of&#x20;

![](<.gitbook/assets/image (78).png>)

closer to 1, thus preventing the gradients from vanishing (or at the very least, preventing them from vanishing _too_ quickly). One important thing to note is that the values _f\_t_, _sigma\_t_, _i\_t_, and _˜C\_t_ are things that the network _**learns**_** **to set (conditioned on the current input and hidden state). Thus, in this way the network learns to decide _**when**_** to let the gradient vanish, and **_**when**_** to preserve it, by setting the gate values accordingly!**

Summary: Two main things to answer why and how:

* **The additive update function for the cell state gives a derivative that's much more ‘well behaved’**
* **The gating functions allow the network to decide how much the gradient vanishes, and can take on different values at each time step. The values that they take on are learned functions of the current input and hidden state.**





HOW: 　　**Question: How do GRU fix vanishing gradient problem?(GRU如何解决梯度消失的问题？)** 　　1. 在标准的RNN中，梯度是严格的按照所有的中间节点流动的，而LSTM在网络中创造了适应性的短连接（create adaptive shortcut connection）。**在LSTM中，可以选择性的遗忘和记忆此前的信息，在梯度的流动中做了短连接，避免梯度计算中的大量累积.** (add new info / remove older info with its weights) 　　2. 通过公式也可以看出，在LSTM中，Ct=f\_t∗C\_t−1+i\_t∗C\_t˜C\_t=f\_t∗C\_t−1+i\_t∗C\_t\~，其中C\_t−1 C\_t−1是此前的信息，Ct˜Ct\~是当前时刻的新信息，CtCt是最终的信息。**可以看到CtCt和Ct−1Ct−1此时是线性关系，不再是RNN中的乘积关系，因此梯度在计算的时候不再是连乘关系，梯度以线性在中间节点流动，因此就会保证很长时间的记忆**

W\_rec = 1&#x20;

![](<.gitbook/assets/image (79).png>)



### Procedure

[GIF LSTM Procedure](https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21) [YouTube](https://www.youtube.com/watch?time\_continue=193\&v=8HyCNIVRbSU)

1. Decide what information we're going to **throw away** from the cell state (forget gate, value range from 0-1 by sigmoid)
2. Decide what new information we’re going to **store/add in the cell state** ;
   * a sigmoid layer called the “input gate layer” decides which values we’ll update.
   * a tanh layer creates a vector of new candidate values, C\~t, that could be added to the state
3. Decide what we're going to output
   * First, we run a **sigmoid layer** which decides what parts of the cell state we’re going to output. Then, we put the cell state through **tanh (to push the values to be between −1 and 1)** and **multiply** it by the output of the sigmoid gate, so that we only output the parts we decided to.

### **Why use Tanh and Sigmoid**

* _**The sigmoid (0 - 1) layer tells us which (or what proportion of) values to update and the tanh (-1 - 1) layer tells us how to update the state (increase or decrease)**_
* _**The output from tanh can be positive or negative, determining whether increases and decreases in the state.**_
* After the addition operator the absolute value of c(t) is potentially larger than 1. Passing it through a tanh operator ensures the values are **scaled between -1 and 1 again**, thus **increasing stability** during back-propagation over many timesteps.

Tanh and sigmoid have

* Well defined gradient at all points
* They are both easily converted into probabilities. The sigmoid is directly approximated to be a probability. (As its 0-1); Tanh can be converted to probability by (tanh+1)/2 will be between 0-1
* Well defined thresholds for classes. -> tanh-> 0 and sigmoid -> 0.5
* They can both be used in calculating the binary crossentropy for classification

### LSTM Variations

[LSTM Variations](https://colah.github.io/posts/2015-08-Understanding-LSTMs#variants-on-long-short-term-memory)&#x20;

![](<.gitbook/assets/image (80).png>)

1. &#x20; \* This means that we let the gate layers look at the cell state. The above diagram adds peepholes to all the gates, but many papers will give some peepholes and not others.
2. &#x20; \* We only forget when we’re going to input something in its place. We only input new values to the state when we forget something older.
3. &#x20; \* Cheaper computational cost \* 3 gates vs 2 gates in gru \* no ouput gate, no second non linearity and they don't have memory ct it is same as hidden state in gru. \* \*\*update gate\*\* in gru does the work of \*\*input and forget gate in lstm.\*\*

![](<.gitbook/assets/image (81).png>)

![](<.gitbook/assets/image (82).png>)

![](<.gitbook/assets/image (83).png>)

**Why "1-" in output gate**

Instead of doing selective writes and selective forgets, we define forget as 1 minus write gate. So whatever is not written is forgotten.

#### Standardisation vs Normalisation

### Timestep

60 timesteps of the past information from which our RNN is gonna try to learn and understand some correlations, or some trends, and based on its understanding, it's going to try to predict the next output.

Too small number will cause overfitting

### Improve RNN

1. **Getting more training data**: we trained our model on the past 5 years of the Google Stock Price but it would be even better to train it on the past 10 years.
2. **Increasing the number of timesteps**: the model remembered the stock prices from the 60 previous financial days to predict the stock price of the next day. That’s because we chose a number of 60 timesteps (3 months). You could try to increase the number of timesteps, by choosing for example 120 timesteps (6 months).
3. **Adding some other indicators**: if you have the financial instinct that the stock price of some other companies might be correlated to the one of Google, you could add this other stock price as a new indicator in the training data.
4. **Adding more LSTM layers**: we built a RNN with four LSTM layers but you could try with even more.
5. **Adding more neurones in the LSTM layers**: we highlighted the fact that we needed a high number of neurones in the LSTM layers to respond better to the complexity of the problem and we chose to include 50 neurones in each of our 4 LSTM layers. You could try an architecture with even more neurones in each of the 4 (or more) LSTM layers.

## GRU

![](<.gitbook/assets/image (84).png>)



## When/where to use it&#x20;

1. time series data

## What it can do and what it can't do

