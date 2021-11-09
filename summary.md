# Linear

## What is it

### Definition:&#x20;

Linear regression assumes there is a linear relationship between features and response variable and use linear function to find a parameter that minimizes the loss. It has closed-form solution while most of other ML models don't.

### Cost function:

the most common technique to find an appropriate parameter is named OLS, ordinary least squares. The function is below

![](<.gitbook/assets/image (1).png>)

this is also called L2 loss; L1 Loss function stands for **Least Absolute Deviations**

### **Direct solution/closed-form solution:**

1. take the derivative of L2 loss formula and set it to zero (find its min)
2.

![](<.gitbook/assets/image (5).png>)

![](<.gitbook/assets/image (2).png>)

![](<.gitbook/assets/image (6).png>)

## When/where to use it

If the data meet the requirement of assumption of linear regression:

1. There is a **linear relationship **between the dependent variables and the regressors, meaning the model you are creating actually fits the data,&#x20;
2. &#x20;The errors or **residuals** of the data are **normally distributed** and **independent** from each other,&#x20;
3. There is **minimal multicollinearity **between explanatory variables, and&#x20;
4. **Homoscedasticity**. This means the variance around the regression line is the same for all values of the predictor variable.

## What it can do and what it can't do

### pro

Linear relationship with only if the assumption is meet&#x20;

### con

Too naive/simple, oversimplify the practical problem
