# Auto-Encoder

## What

### Definition

it's self-supervised algorithm and basically encode itself, so it takes some sort of inputs, put some through a hidden layer, and then it gets outputs, but it aims for the outputs to be identical to the inputs. For Feature selection and Recommendation. The vanilla auto-encoder has the constraint that number of nodes in hidden layer must less than the input layer's, but we have serveral variations.

it compress the information taken from input and then reconstruct them into original dimension and check their dimension

{% embed url="https://www.youtube.com/watch?v=9zKuYvjFFS8" %}



![](.gitbook/assets/image%20%2862%29.png)

### Variation 

all have larger number of nodes in hidden layer than input layer

we cannot simple have larger number of nodes in hidden layer than input layer is that auto-encoder will try to cheat and just copy features or information from input layer to output layer without any feature compression or extraction.

#### Variational auto-encoder

Instead of having a bottleneck, we replace it by mean vector and standard deviation vector of the distribution. we have sampled vector operation, so back-propogation will be performed by adding the reparameterization trick.

![](.gitbook/assets/image%20%285%29.png)

#### Sparse auto-encoder

still compress things but with different sparse nodes

difference:

* number of nodes in hidden layer greater than input layer
* regularisation \(add constraints to hidden layer so that doesn't allow the autoencoder to use all of its hidden layer nodes every single time, so any time, only certain number of nodes will be used\)

#### Denoising auto-encoder

difference:

* randomly turn the input to zero \(add noisy\)
* calculate the error, instead of compare output with input layer, it compares with the original input before turning the input to zero
* get rid of noise \(watermark, etc\)

#### Contractive auto-encoder

difference:

* add penalty to the loss function to avoid auto-encoder simply copying the feature from input layer to output layer

#### Stacked auto-encoder

difference:

* add one more encoding hidden layer with less number of nodes, so there will be two encoding hidden layer and one decoding layer



## How 

Feature selection: take the six neurons in the input layer and transform them into three neurons in the hidden layer and then carry around these information and save some space and extract these features

![](.gitbook/assets/image%20%2898%29.png)

![](.gitbook/assets/image%20%2851%29.png)

## 

## Where

Feature selection

Recommendation

Fraud detection: 

1. train auto-encoder with only normal transaction
2. feed suspicious transactions into trained auto-encoder, the output of it will be significantly different than the other normal transaction.



