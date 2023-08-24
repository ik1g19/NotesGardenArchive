# Input Data

Training Data:
$$
\begin{gathered}
\left(x^1, \hat{y}^1\right) \\
\left(x^2, \hat{y}^2\right) \\
\vdots \\
\vdots \\
\left(x^{10}, \hat{y}^{10}\right)
\end{gathered}
$$
$$y=b+wx$$
![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625145221.png|400]]

Compute $b$ and $w$ to find which best fit the data

# Function to Learn

Can be converted to an optimization problem minimizing a loss function

$$
\mathrm{L}(w, b)=\sum_{n=1}^{10}\left(\hat{y}^n-\left(b+w \cdot x^n\right)\right)^2
$$

$$
w^*, b^*=\arg \min _{w, b} L(w, b)=\arg \min _{w, b} \sum_{n=1}^{10}\left(\hat{y}^n-\left(b+w \cdot x^n\right)\right)^2
$$

# Linear Regression: Gradient Descent

Follow the direction of the gradient to compute the minima

$\eta$ is the learning rate, controls how far you jump

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625182213.png|450]]

## Momentum

Controls the smoothness of descent

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625182538.png|450]]

## Regularization

You want to control the parameters that are $w$ to a certain region

$\lambda$ is the parameter that controls the amount of regularization that you are doing

$L_2$ regularization is where you want the parameters of your model to be as small as possible

$L_1$ regularization is used as feature selection - you want some of your features to be 0

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625184228.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625184318.png|450]]

### Regularization to control Under/Overfitting

#### Ridge Regression

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230625184429.png|450]]

#### LASSO (Least Absolute Shrinkage and Selection Operator Regression)

$$
J(\theta)=\operatorname{MSE}(\theta)+\alpha \sum_{i=1}^n\left|\theta_i\right|
$$

#### Elastic Net

$$
J(\theta)=\operatorname{MSE}(\theta)+r \alpha \sum_{i=1}^n\left|\theta_i\right|+\frac{1-r}{2} \alpha \sum_{i=1}^n \theta_i^2
$$

# Probabilistic Generative Model

**Generative Model** - Attempt to model how the data is generated, they try to understand the true data distribution of the input data and the output labels

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626093441.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626093516.png|450]]

## Gaussian Distribution

The shape of the function is determined by the mean $\mu$ and the covariance matrix $\Sigma$

## Maximum Likelihood

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626095509.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626095631.png|450]]

## Doing the Classification

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626095840.png|500]]

## Three Steps

1. Function Set (Model)

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626100235.png|450]]

2. Goodness of a funciton
	- The mean $\mu$ and covariance $\Sigma$ that maximize the likelihood (the probability of generating data)

3. Find the best function
	- Can be solved

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626101040.png|450]]


# Discriminative Model

If $y$ value is binary, then this is a classification problem

## Probabilistic Interpretation

We assume the training data is generated based on a Probabilistic Distribution Function (PDF)

We aim to estimate this PDF by $f(x)$ which is characterized by parameters $w$ and $b$, so we write it as $f_{w,b}(x)$

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626102516.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626102735.png|450]]

## Data Generation Probability

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626113418.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626113433.png|450]]

## Error Function

Cross entropy finds how far one distribution is from another

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230626114035.png|450]]



