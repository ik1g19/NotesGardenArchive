---
title: Machine Learning for Pattern Recognition
---

# Feature Spaces
Many computer vision applications involving machine learning take the following form
![|400](https://remnote-user-data.s3.amazonaws.com/TPDSN8DLRM72geLmCJQL2cxPQwM3-oGKro6cHjmKi7P4nk2rx30F9gx0pDUEJXDknWKCKHe56fnlEGn2iodX0btCv5kaPRnpPl0tXsYkwbYzo3axmOwdGTnPFTzWwWtI.png) 
Feature Extractor - Where cool image processing happens
- Make featurevectors from image
Machine Learning - Uses feature vectors to make intelligent decisions

# Key Terminology
Featurevector - A mathematical vector
- A list of, usually real, numbers
- The dimensionality of featurespace is the dimensionality of every vector in it
	- Vectors of different dimensionality can't exist in the same featurespace
- The number of elements is the dimensionality of the vector
- Represents a point in a featurespace
	- Or equally, a direction in the featurespace
- Has a fixed number of elements in it
 
# Distances in Featurespace
Feature extractors are often designed so they produce vectors that are close together for similar inputs
- The closeness of two vectors can be computed in the featurespace by measuring a distance between the vectors
![|400](https://remnote-user-data.s3.amazonaws.com/Z-iT6VB5XdFVm45YI7vAORsCWwGS6xtUFEAWFejPBaSMH6q05h8cokRpRHDZzQosrd3w5t0_uc9D5D96K0XVgrJ8YQ1FRq7Mivyo0A5cx1UjAqaYOpQUm4aA4SHL1f0a.png) 

# Euclidean Distance (L2 Distance)
- Computed via an extension of Pythagoras theorem to n dimensions
- The straight line distance between two points
	- (Most intuitive distance)
$$D_2(p,q)=\sqrt{\sum\limits_{i=1}^{n}(p_i-q_i)^2}=||p-q||=\sqrt{(p-q)\cdot (p-q)}$$
![|400](https://remnote-user-data.s3.amazonaws.com/O63dQPeKpN0kXAh-r6cOROvhNl4bLAe6ywpyijVoRUVf4pEyLP1ppouxG_MgRTW0bGnQ4CWRwD03o8sPe5E8fbFAC312NGFaED8Ilh1REkVJRvmzcQASwdFgXqOt1KGe.png) 

# Taxicab/Manhattan Distance (L1 Distance)
![|400](https://remnote-user-data.s3.amazonaws.com/E8MEKysPbPd8b3PAiE1BzkVE3XB25ghnYymSfgEnOziGKV4vmgkgtQ3WTxwpkW4WnHbjUYJW_vDqtOfewRXWwbIUXVHDebvqLcaSLmyqtfK3oZz5We5c2lqxYUiLaKdc.png)
$$D_1(p,q)=\sum\limits_{i=1}^{n}|p_i-q_i|=||p-q||_1$$
L1 distance is computed along paths parallel to the axes of the space
 
# Cosine Similarity
![|400](https://remnote-user-data.s3.amazonaws.com/AuRYGludWUnZGSo2yLHCuUiTQsfNWDjgcprMnMpB-FXtUgwillIDbYYE690VHeW-1gRfWyb2xpQWe89TeBI3AQd7UwXwd2HTsCoK03iEIq5Kte8EQ2K5gcnepNeH0He1.png)  
- Useful if you don't care about the relative length of the vectors
$$\cos(\theta)=\frac{p\cdot q}{||p||\text{ }||q||}=\frac{\sum\limits_{i=1}^{n}p_iq_i}{\sqrt{\sum\limits_{i=1}^{n}p_i^2}\sqrt{\sum\limits_{i=1}^{n}q_i^2}}$$
- Measures the cosine of the angle between the two vectors
	- It is not a distance

# Choosing Good Featurevector Representations for Machine Learning
Choose features which allow to distinguish objects or classes of interest
- Similar within classes
- Different between classes
Keep number of features small
- Machine-learning can get more difficult as dimensionality of featurespace gets large
 
# Supervised Machine Learning: Classification
- Classification - The process of assigning a class label to an object (typically represented by a vector in a featurespace
- Supervised machine learning algorithms use a set of pre-labelled training data to learn how to assign class labels to vectors (and the corresponding objects)
	- Multiclass Classifier - Has many classes
	- Binary Classifier - Only has two classes

# Linear Classifiers
![|400](https://remnote-user-data.s3.amazonaws.com/iF4tz5_0L_4zrf6-qamsyCcLfsQG6TayjtR3ARH9NwTmQQeALsvaGXM4uf8vUqGs4U-FsbkCXvP0LtumWbNveELPVAjnG6j7O0aOm8wanaMtWc4Kbesmwi-7_RievIby.png) 
- Try to learn a hyperplane that separates two features in featurespace with minimum error
- To classify a new image, you need to check what side of the hyperplane its on
![|400](https://remnote-user-data.s3.amazonaws.com/JHbHZ-wcuwzYOBIFrvZ5oVBJcu_LABnglOgFKfSzlZ-yK7io2W5a8-KJZ2eWsEI5XOeLeMVGHzrBXW1Xj8RCT7ouJKA6aNMUsGloU3CugTHGBKeqpxEt1rFdNDNtFWM1.png) 
- A Type of binary classifier
- Many hyperplanes could be chosen
	- Different linear classification algorithms apply different constraints when learning the classifier

# Non-linear Binary Classifiers
Linear classifiers work best when the data is linearly separable
![|400](https://remnote-user-data.s3.amazonaws.com/biJBVAnfaPZK_AJyk-9uAz3jbAS8BFBCfKGLtGV5NKOfPPaU769mhlxPuQRQQCn8229ZreTqsijl4yhD9R_Hi7Uf5SRrq6I7Tp0TpRmzjLrPzsXthJzrXVbA_XpxXnoR.png) 

Non-linear binary classifiers (such as Kernel Support Vector Machines) learn non-linear decision boundaries
![|400](https://remnote-user-data.s3.amazonaws.com/ZaheNa3XbTYyvOgKR8de3-ZxO1yBGkxhK-o54Si3LNdpVtwbgc0f9tzJ1S2tyVHXmJGLE09Rdv5p4Zl-KHKPx7cc0y1PrDJ9S1CMsadQUEo8IDhXn1JFVoJT54LpETnE.png) 

This can help reduce error, as seen in this example
![|400](https://remnote-user-data.s3.amazonaws.com/IXW2SKBjzZq21VviDd20DRY2Fl75azNgN0l3oj0eZ8Fkl7Hma1pk0Q8H6DgryAweSzzjnuIQmOOCnEN5_6M3agaGgNjYvXmEgL2KTMnW2rw9Aajs2eT0y-aISjk6Fyka.png) 
However, by overfitting you can lose generality

# Multiclass Classifiers: K Nearest Neighbours
Assign an unknown point a class based on the classes of the k-nearest neighbours
![|400](https://remnote-user-data.s3.amazonaws.com/7GDekSCXYifZYCudy7xPwXD97oBXxy9fbF8Ada6RMkGuijFS0nWGnzPohiXMu55k3w7DvKnTnxVpyA_FFML1hXhRvEHtzrnmvz8sAoA3IWNdYLXrbAPzZ-Nlqv3zVveF.png) 
## K-Nearest Neighbour Problems
Computationally expensive if there are
- Many dimensions
- Lots of training examples
 
# Multiclass Linear Classifiers
## One versus All (OvA) / One versus Rest (OvR)
One classifier per class
## One Versus One (OvO)
$k\frac{k-1}{2}$ classifiers
- Effectively pairing all the classifiers together
 
# Unsupervised Machine Learning: Clustering
- Aims to group data without any prior knowledge of what the groups should look like or contain
- Items with similar vectors should be grouped together by a clustering operation
- Some clustering operations create overlapping groups

# K-Means Clustering
A featurespace clustering algorithm for grouping data into k groups with each group represented by a centroid
1. The value of K is chosen
2. K initial cluster centres are chosen
3. The following process is performed iteratively until the centroids don't move between iterations

Each point is assigned to its closest centroid
The centroid is recomputed by the mean of all the points assigned to it.
- If the centroid has no points assigned, it is randomly re-initialised to a new point

4. The final clusters are created by assigning all points to their nearest centroid