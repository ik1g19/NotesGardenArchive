The examples the system uses to learn are called the training set

Each training example is called a training instance

Applying ML techniques to large amounts of data can help discover patterns that were note immediately apparent. This is called **[[Data Mining]]**

Machine Learning is great for:
- Problems for which existing solutions require a lot of hand-tuning or long lists of rules: one Machine
- Learning algorithm can often simplify code and perform better.
- Complex problems for which there is no good solution at all using a traditional approach: the best
- Machine Learning techniques can find a solution.
- Fluctuating environments: a Machine Learning system can adapt to new data.
- Getting insights about complex problems and large amounts of data

# Types of Machine Learning System

- Whether or not they are trained with human supervision ([[Supervised Learning|supervised]], [[Unsupervised Learning|unsupervised]], [[Semi Supervised Learning|semi supervised]], and [[Reinforcement Learning]])
- Whether or not they can learn incrementally on the fly (online versus batch learning)
- Whether they work by simply comparing new data points to known data points, or instead detect patterns in the training data and build a predictive model, much like scientists do (instance-based versus model-based learning)

## Supervised Learning

In [[Supervised Learning]], the training data you feed to the algorithm includes the desired solutions (labels)

![[Pasted image 20230909193646.png]]

A typical supervised learning task is classification

Another typical task is to predict a target numeric value, given a set of features called **predictors**
- This sort of task is called [[content/keywords/Regression|Regression]]

Some regression algorithms can be used for classification and vice versa

The most important supervised learning algorithms:
- [[K-Nearest Neighbors]]
- [[Linear Regression]]
- [[Logistic Regression]]
- [[Support Vector Machine]]s (SVMs)
- Decision Trees and [[Random Forest]]s
- Neural networks


## Unsupervised Learning

The training data is unlabeled

Some of the most important unsupervised learning algorithms:
- Clustering
	- [[k-Means]]
	- [[Hierarchical Cluster Analysis]] (HCA)
	- Expectation Maximization
- Visualization and [[Dimensionality Reduction]]
- [[Principal Component Analysis]] (PCA)
	- Kernel PCA
	- Locally-Linear Embedding (LLE)
	- t-distributed Stochastic Neighbor Embedding (t-SNE)
- Association rule learning
	- Apriori
	- Eclat

These algorithms try to preserve as much structure as they can (e.g., trying to keep separate clusters in the input space from overlapping in the visualization), so you can understand how the data is organized and perhaps identify unsuspected patterns

A related task is [[Dimensionality Reduction]]
- In which the goal is to simplify the data without losing too much information

One way to do this is to merge several correlated features into one

For example, a car’s mileage may be very correlated with its age, so the dimensionality reduction algorithm will merge them into one feature that represents the car’s wear and tear
- This is called feature extraction

>[!Tip]
>It is often a good idea to try to reduce the dimension of your training data using a dimensionality reduction algorithm before you feed it to another Machine Learning algorithm (such as a supervised learning algorithm). It will run much faster, the data will take up less disk and memory space, and in some cases it may also perform better

[[Anomaly Detection]] is another unsupervised task
- The system is trained with normal instances, and when it sees a new instance it can tell whether it looks like a normal one or whether it is likely an anomaly

![[Pasted image 20230909194954.png]]

Another unsupervised task is [[Association Rule Learning]]

In which the goal is to dig into large amounts of data and discover interesting relations between attributes
- For example, suppose you own a supermarket. Running an association rule on your sales logs may reveal that people who purchase barbecue sauce and potato chips also tend to buy steak. Thus, you may want to place these items close to each other

## Semisupervised Learning

Some algorithms can deal with partially labelled training data

Usually a lot of unlabeled data and a little bit of labelled data

![[Pasted image 20230909195420.png]]

## Reinforcement Learning

The learning system, called an agent in this context, can observe the environment, select and perform actions, and get rewards in return (or penalties in the form of negative rewards)

It must then learn by itself what is the best strategy, called a [[Policy]], to get the most reward over time

A policy defines what action the agent should choose when it is in a given situation

## Batch and Online Learning

### Batch Learning

In [[Batch Learning]], the system is incapable of learning incrementally. It must be trained using all the available data

First the system is trained, and then it is launched into production and runs without learning anymore - this is called [[Offline Learning]]

If you want a batch learning system to know about new data, you need to train a new version of the system from scratch on the full dataset, then stop the system and replace it with the new one

### Online Learning

In [[Online Learning]], you train the system incrementally by feeding it data instances sequentially, either individually or by small groups called mini-batches

Each learning step is fast and cheap, so the system can learn about new data on the fly as it arrives

Online learning is great for systems that receive data as a continuous flow and need to adapt to change rapidly or autonomously

Once an online learning system has learned about new data instances, it does not need them anymore, so you can discard them, which can save a huge amount of space

Online learning algorithms can also be used to train systems on huge datasets that cannot fit in one machine's main memory (out-of-core learning)
- This algorithm loads part of the data, runs a training step on that data, and repeats the process until it has run on all of the data

![[Pasted image 20230909200421.png]]

The learning rate - how fast an online learning system should adapt to changing data

If you set a high learning rate, then your system will rapidly adapt to new data, but it will also tend to quickly forget the old data (you don’t want a spam filter to flag only the latest kinds of spam it was shown). Conversely, if you set a low learning rate, the system will have more inertia; that is, it will learn more slowly, but it will also be less sensitive to noise in the new data or to sequences of non-representative data points

A challenge of online learning is that if bad data is fed to the system, the system's performance will gradually decline

## Instance-Based versus Model-Based Learning
### [[Instance-Based Learning]]

The system learns examples by heart, and then generalizes to new cases using a similarity measure

![[Pasted image 20230909201021.png]]

### Model-based Learning

Another way to generalise from a set of examples is to build a model of these examples, then use that model to make predictions

This is called [[Model-Based Learning]]

![[Pasted image 20230909201136.png]]


![[Pasted image 20230909201309.png]]

There does seem to be a trend here! Although the data is noisy (i.e., partly random), it looks like life satisfaction goes up more or less linearly as the country’s GDP per capita increases. So you decide to model life satisfaction as a linear function of GDP per capita. This step is called model selection: you selected a linear model of life satisfaction with just one attribute, GDP per capita

$$\text{life\_satisfaction} = \theta_0 + \theta_1 \times \text{GDP\_per\_capita}$$

This model has two model parameters, $\theta_0$ and $\theta_1$

By tweaking these parameters, you can make your model represent any linear function

![[Pasted image 20230909201841.png]]

Before you can use your model, you need to define the parameter values $\theta_0$ and $\theta_1$

In order to find the values that the model will perform best with, you need to specify a performance measure
- You can either define a utility function (or fitness function) that measures how good your model is
- Or you can define a cost function that measures how bad it is

For [[Linear Regression]] problems, people typically use a cost function that measures the distance between the linear model's predctions and the training examples - the objective is to minimize this distance

Where linear regression comes in - you feed it your training examples and it find the parameters that make the linear model fit best to your data

This is called **training** the model

![[Pasted image 20230909202250.png]]

```python
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import sklearn

# Load the data
oecd_bli = pd.read_csv("oecd_bli_2015.csv", thousands=',')
gdp_per_capita = pd.read_csv("gdp_per_capita.csv",thousands=',',delimiter='\t', encoding='latin1', na_values="n/a")

# Prepare the data
country_stats = prepare_country_stats(oecd_bli, gdp_per_capita)
X = np.c_[country_stats["GDP per capita"]]
y = np.c_[country_stats["Life satisfaction"]]

# Visualize the data
country_stats.plot(kind='scatter', x="GDP per capita", y='Life satisfaction')
plt.show()

# Select a linear model
lin_reg_model = sklearn.linear_model.LinearRegression()

# Train the model
lin_reg_model.fit(X, y)

# Make a prediction for Cyprus
X_new = [[22587]] # Cyprus' GDP per capita
print(lin_reg_model.predict(X_new)) # outputs [[ 5.96242338]]
```

What a typical machine learning project looks like:
- You studied the data.
- You selected a model.
- You trained it on the training data (i.e., the learning algorithm searched for the model parameter values that minimize a cost function).
- Finally, you applied the model to make predictions on new cases (this is called inference), hoping that this model will generalize well.