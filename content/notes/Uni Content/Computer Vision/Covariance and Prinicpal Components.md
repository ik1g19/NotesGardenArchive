---
title: Covariance and Prinicpal Components
---
# Random Variables and Expected Values
Variance and covariance are expressed in terms of random variables and expected values
Random Variable - A variable that takes on different values due to chance
- The set of sample values from a single dimension of a featurespace can be considered to be a random variable
The expected value $E[X]$ is the most likely value a random variable will take
We will assume the values an element of a feature can take are equally likely
So the expected value is just the mean value
# Variance
Variance $\sigma^2$ is the mean squared difference from the mean
Effectively a measure of how spread-out the data is
$$\sigma^2(x)=\frac{1}{n}\sum\limits_{i=1}^{n}(x_i-\mu)^2$$
# Covariance
Covariance $\sigma(x,y)$ measures how two variables change together
It is technically $E[(x-E[x])(y-E[y])]$
$$\sigma(x,y)=\frac{1}{n}\sum\limits_{i=1}^{n}(x-\mu_x)(y-\mu_y)$$
The variance is the covariance when the two variables are the same (\sigma(x,x)=\sigma^2(x)) 
A covariance of 0 means the variables are uncorrelated

# Covariance Matrix
Encodes how all possible pairs of dimensions in an n-dimensional data set vary together
$$\Sigma=\begin{bmatrix}
\sigma(X_1,X_1) & \sigma(X_1,X_2) & ... & \sigma(X_1,X_n)\\
\sigma(X_2,X_1) & \sigma (X_2,X_2) & ... & \sigma(X_2,X_n)\\
... & ... & ... & ...\\
\sigma(X_n,X_1) & \sigma(X_n,X_2) & ... & \sigma(X_n,X_n)
\end{bmatrix}$$
The covariance matrix is a square symmetric matrix
![|400](https://remnote-user-data.s3.amazonaws.com/Xpv_rK9URuvkjTvmpGlFKJi3i1z66oQ0zgbZm8O2mAkYZL8V-juD4R0jwgJvfbicBP-Q7FSuQVoMZaduhkm6MmdzlCCAow0NwAc99ZJW_8kgiUKUNdPmxhKaSOn5nzkd.png) 
# Mean Centring
The process of computing the mean (across each dimension independently) of a set of vectors, and then subtracting the mean vector from every vector in the set
All the vectors will be translated so their average position is the origin
![|400](https://remnote-user-data.s3.amazonaws.com/0WtNAd-YtLPMBpuSI9ogei6eEVHvKyN1QbCYu9FsZm6tHM5pcvc2s3b9de9G7I4LhzIZyq6jHZ64HZ_pMTt5uMONEm9-Upc2geFKwsznX4hT0TNF5ZXedMMUe16sXIzY.png)

# Covariance Matrix Properties
Consider a matrix of mean centred featurevectors
$$\Sigma \propto Z^TZ$$
The covariance matrix $\Sigma$ is directly proportional to the transposed matrix $Z^T$ multiplied by the original matrix $Z$ 

# Principle Axes of Variation
## Basis
A set of n linearly independent vectors in an n dimensional space
- Vectors are orthogonal
- They form a "coordinate system"
- There are an infinite number of possible basis
## The First Principal Axis
For a given set of n dimensional data, the first principle axis (or principal axis) is the vector that describes the direction of greatest variance
![|400](https://remnote-user-data.s3.amazonaws.com/uhMsBAdcESitpERI71YUhHnYOpm6QnhoHs-MF_1qFmw9CMTJPmsBduKPx1_DW858jzBPu-HoSC2lFK-M7npiPC645QHOuree3ecdgVZc9Std3DgKEr1SPuabjIS22gwI.png) 
## The Second Principal Axis
The second principal axis is a vector in the direction of greatest variance orthogonal (perpendicular) to the first major axis
![|400](https://remnote-user-data.s3.amazonaws.com/RnGLZ2BrSw3A2sY-vCuU8mfQPsJoDUz45fJ-OKbwJ8S6n5rvMlQegDD0TB_t1SG4cvQVeNwpFQ7TqkfDYbo4HWkLHSwjJhFAsCuALb0CwFRgvCVzCW3OfGHfOXYE6zkr.png) 
## The Third Principal Axis
In spaces with 3 or more dimensions, the third principle axis is the direction of greatest variance orthogonal to both the first and second principal axes
The set of n principal axes of an n dimensional space are a basis

# Eigenvectors and Eigenvalues
$$\colorbox{aqua}A \colorbox{pink}v = \colorbox{lightgreen}{λ} \colorbox{pink}v$$
Where
- $\colorbox{pink}{v}$ - An n dimensional vector, known as an eigenvector
- $\colorbox{lightgreen}λ$ - A scalar value, known as an eigenvalue
- $\colorbox{aqua}A$ - An n\times n square matrix

There are at most $n$ eigenvector-eigenvalue pairs
If A is symmetric, then the set of eigenvectors is orthogonal
- The eigenvector corresponding to the largest eigenvalue is the first principle component
- Therefore, if A is a covariance matrix, then the eigenvectors are the principal axes
- The eigenvalues are proportional to the variance of the data along each eigenvector

# Finding Eigenvectors and Eigenvalues
For small matrices (n\leq 4) there are algebraic solutions to finding all the eigenvector-eigenvalue pairs
For larger matrices, numerical solutions to the Eigendecomposition must be sought

# Eigendecomposition
Breaks a matrix down into a matrix Q, a diagonal eigenvalue matrix \Lambda (only has values along the diagonal) and the inverse of the first matrix $Q^{-1}$
$$A=Q\Lambda Q^{-1}$$
If A is real symmetric (i.e. a covariance matrix), then Q^{-1}=Q^T (i.e. eigenvectors are orthogonal), therefore
$$A=Q\Lambda Q^T$$
So the eigendecomposition of a covariance matrix $A$ ($A=Q\Lambda Q^T$) gives you the principal axes and their relative magnitudes
## Ordering
Some solvers are optimised to only find the top k eigenvalues and corresponding eigenvectors, rather than all of them
Standard eigendecomposition solver implementations will order the eigenvectors (columns of Q) such that the eigenvalues (in the diagonal of \Lambda) are sorted in order of decreasing value

# Principal Component Analysis
## Linear Transform
The effects of a linear transform can be reversed if W is invertible
$$Z=TW^{-1}$$
This is a lossy process if the dimensionality of the spaces is different
A linear transform W projects data from one space into another
$$T=ZW$$
T can have fewer dimensions than Z
Where original data is stored in the rows of Z

![|400](https://remnote-user-data.s3.amazonaws.com/oFScSOCtwOE-e_tKPq7rmZjxSk-yRxPsv5ePsgDyhn5FPYQn_e_lt4KECL0JLzKMj9SRW0sn25o3zjfw-KzX_G1jWeZAmwroCs--nqyXwvjNLZPo2smc6Z040ubnQU7B.png)

![|400](https://remnote-user-data.s3.amazonaws.com/fYsdP0JJlZ03kGEGvFamo2GcGx3wMWAPFzROFDCIapsAhfOFIS70xf4wyrrzxqYIonYdlq7vfxrZprmAThjldz_MXOp2L_0chhTZj32JnEmMZJFL5a5grI6UC8n8J74u.png)
## PCA
PCA is an Orthogonal Linear Transform that maps data from its original space to a space defined by the principal axes of the data
Dimensionality reduction can be achieved by removing the eigenvectors with low eigenvalues from Q
i.e. Keeping the first L columns of Q, assuming the eigenvectors are sorted by decreasing eigenvalue 
The transform matrix W is just the eigenvector matrix Q from the eigendecomposition of the covariance matrix of the data
Maps data from one dimension into another
### PCA Algorithm
1. Project the original vectors into a lower dimensional space $T_L$ 
$$T_L=ZQ_L$$
2. Sort the columns of Q and the corresponding diagonal values of \Lambda so that the eigenvalues are decreasing
3. Select the L largest eigenvectors of Q (the first L columns) to create the transform matrix $Q_L$
4. Form the vectors into a matrix Z, such that each row corresponds to a vector
5. Perform the eigendecomposition of the matrix $Z^TZ$, to recover the eigenvector matrix Q and diagonal eigenvalue matrix $\Lambda$
$$Z^TZ=Q\Lambda Q^T$$
6. Mean-centre the data vectors

# Eigenfaces (Eigenimages)
Flatten a grey level image into a vector
- Take each row and add it to the vector
![|400](https://remnote-user-data.s3.amazonaws.com/RhCsaBmFGEPl3qN5wLBAW_UBjASkWSKB18VSZ3nDx_ml0cVcXTE5t3_iBZ8XNcwTTcKOVq_B4-nggF3DVlDIjmBqJzYpVSSxI8U5quvKSfCZq0hpHKfBofZitv_ZQMRG.png) 
This causes some problems
- Highly susceptible to image noise
- It is not invariant to
	- Change in position/orientation/scale of the object in the image
	- Changes in lighting
	- Size of the image
## Making it invariant
Align (rotate, scale and translate) the images so that a common feature is in the same place
- i.e. The eyes in a set of face images
Require almost the same object pose across images
- i.e. Faces facing the front
Make all the aligned images the same size
Optionally - Normalise (or histogram equalise) the images so they are invariant to global intensity changes
## Another problem is the size of the featurevectors
A potential solution is to apply PCA
- Fewer dimensions makes applying machine learning much more tractable
- PCA can be used to reduce the dimensionality
- A smaller number of dimensions allows greater robustness to noise and mis-alignment
	- There are fewer degrees of freedom, so noise/mis-alignment has much less effect
	- And dominant features are captured
If the images are 100x200 pixels, the vector has 20000 dimensions
This is impractical and the vectors are highly susceptible to image noise and variations due to slight mis-alignments
