# Estimator

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230628175645.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230628175801.png|450]]

The more complex the model, the more likely you run into the issue of overfitting to that particular training data set - and becoming variant from the others

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630124923.png|450]]

# Decision Tree

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630133323.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630133353.png|450]]

## Gini Index/Score


Suppose that we split the tree by feature $x$

We get 2 nodes: left and right (nodes 1 and 2)

Let $p_{i,k}$ denote the ratio of class k instances among the training instances in node $i$ ($i = 1$ or 2)

Gini score of node $i$:
$$
G_i=1-\sum_{k=1}^n p_{i, k}^2
$$

A node's Gini attribute measures its impurity

A node is 'pure' (ginin=0) if all training instances it applies to belong to the same class

### Algorithm
- Choose the feature that provide the lowest of the (weighted) sum of the Gini score of the children nodes
- Repeat until reaching leaf node (e.g., Gini score is “very small”)

## Entropy

Entropy is the number of questions you need to ask on average to get to the data

Level of information, surprise, or uncertainty

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630134248.png|600]]

$$
H_i=-\sum_{\substack{k=1 \\ p_{i, k} \neq 0}}^n p_{i, k} \log _2\left(p_{i, k}\right)
$$
## Creating a Decision Tree using Gini Index

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140019.png|450]]

### Split on Outlook

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140129.png|450]]

### Split on Temperature

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140148.png|450]]

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140156.png|450]]

### Split on Humidity

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140212.png|450]]

### Split on Wind

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140225.png|450]]

### Feature Selection

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140244.png|450]]

### Depth 1

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140259.png|450]]

### Depth 2

![[notes/Uni Content/Machine Learning Technologies/Images/Pasted image 20230630140309.png|450]]

## Advantages

- If each training example has its own leaf, easy to achieve 0% error rate on training data
- Less effort for data preparation (no normalization, scaling)
- Model Interpretability (WhiteBox Model)

If a black box model, such as a neural network says that a particular person appears on a picture, it is hard to know what actually contributed to this prediction

## Disadvantages

- High Training Time, more expensive
- High Variance => Overfitting
- Instability: sensitivity to variation in dataset (e.g., rotation, change in data, etc.)

