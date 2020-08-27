# Transformer

Transformer is an algorithm that uses attention mechanism to boost the training speed by parallelization. It is widely used in Natual Language Processing, Time-series data analysis. It has the architecture of encoder and decoder.   



{% embed url="https://www.michaelphi.com/illustrated-guide-to-transformers/" %}

Paper: Attention is all you need

## Architecture:

![](.gitbook/assets/image%20%2887%29.png)

Multi-headed attention is a module in the transformer network that computes the attention weights for the input, and produces an output vector with encoded information on how each word should attend to all other words in the sequence.

## Multi-Headed Attention

### **Self-attention:** Query, key and value

“The query key and value concept come from retrieval systems. For example, when you type a query to search for some video on Youtube, the search engine will map your **query** against a set of **keys** \(video title, description etc.\) associated with candidate videos in the database, then present you the best matched videos \(**values**\).

![](.gitbook/assets/image%20%2817%29.png)

So **basically, the dot product of Query and Key is computing their cosine similarity to see how these two related to each other, also, because we always want to find the best match item, the cosine similiary is supposed to be higher is better, so it is also the indicator of higher score get more focus.** Then scale the product by square root of dimension and get their softmax value to enhance the larger value so that we will get clue on where to get more attention \(By doing a softmax the higher scores get heighten, and lower scores are depressed. This allows the model to be more confident about which words to attend too.\). **Then the calculated attention matrix will have a dot product with the Value, which the higher softmax scores will keep the value of words/embedding the model learns is more important.**

### Multi-attention head

Set number of multi-attention head N, then split Query, Key and Value to N times of splitting.

**To make this a multi-headed attention computation, you need to split the query, key, and value into N vectors before applying self-attention.** The split vectors then go through the self-attention process individually. Each self-attention process is called a head. Each head produces an output vector that gets concatenated into a single vector before going through the final linear layer. In theory, **each head would learn something different therefore giving the encoder model more representation power.**

![](.gitbook/assets/image%20%2872%29.png)

### The Residual Connections, Layer Normalization, and Feed Forward Network

![](.gitbook/assets/image%20%2813%29.png)

#### Understanding

![](.gitbook/assets/image%20%2869%29.png)

Orignial positional embedding was added to multi-headed attention output vector, which retaining the position related information which we are adding to the input representation/embedding across the network. This part uses the idea of Resnet, which is able to train a very deep neuron network without gradient vanishing by skipping some layers

![](.gitbook/assets/image%20%2860%29.png)







\*\*\*\*

\*\*\*\*

\*\*\*\*



