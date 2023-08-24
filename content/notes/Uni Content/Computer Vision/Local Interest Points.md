---
title: Local Interest Points
---
# What makes a good Interest Point in an Image?
- Invariance to brightness change
	- Local changes as well as global ones
- Sufficient texture variation in the local neighbourhood
- Invariance to position between the angle/position of the scene to the camera
# Finding Interest Points
## Different types of interest points to choose from
### Blob Detection - Difference-of-Gaussian Extrema
![|200](https://remnote-user-data.s3.amazonaws.com/aMdPOOwczOgzvqXqJ4I1I63efazF5aRvMBXds4R27kRVlHarabPZzDCWDfFBj2cm37KGhiacPl139iCPu5JIXEfHSwcwt6aopI6xEq6dEDu_SVmDdOP-yIuoO6rGZr14.png) 
### Corner Detection - Harris and Stephens
![|200](https://remnote-user-data.s3.amazonaws.com/beEThfWceMkMF6riundQ4w71N5-meJN4o157TdEUV5ogaQA0mtGVBCFhh5VdvSbHCo5qaSn3b7m_iE1jimGzPgzCz2-Hp4Vpfb7-yfGGx7gzvFIl8oUXLaKI_n0_JkSK.png) 
# Harris and Stephens Corner Detector
## Basic Idea
- Shifting that window by a small amount in any direction should give a large change in intensity
- Search for corners by looking through a small window
## "Flat" Region
No change in all directions
![|200](https://remnote-user-data.s3.amazonaws.com/bmDg-eaIoCTTnbVI8w4POY5E7Jmuc1HXQkpGCAE0dW__19MYQ-Y_3kr1uncBUb3bkiEeq4bk3pPPDidnZDiwvN_SJkluNkncjzYFnD_oFo4dWGre97L8Y8B-Y_MvnfOd.png) 

## "Edge" Region
No change along the edge direction
![|200](https://remnote-user-data.s3.amazonaws.com/XwRLRFhiUB_69yKDyYpBupG0jurIO1tRLLV4tEvzbC6J3TmAC2-TxX7lfrRYj0w7tcD4qs6ZWbkr0oNfbTCPeLrs4ezVucUuSCd2Wg-eZVmNsKnrx6yn117zu05c1kvr.png) 
## "Corner" Region
Significant change in all directions
![|200](https://remnote-user-data.s3.amazonaws.com/iAwkm99HKJHOYAlBcMFSoldgDOfPwF_99OfQmqpcoIQHqR9BNnnBgmbUu3S3tUfIRJM3bvaOWYSwdjH8LRcoMnOgYpZ1PTLbynNCtrGki62bkkEma4nrMjxkxWUgfeaW.png) 
## Mathematics
Weighted average change in intensity between a window and a shifted version by $(\Delta x,\Delta y)$ of that window
### The Structure Tensor
![|200](https://remnote-user-data.s3.amazonaws.com/Je6Z478m9wLorS8b1OY40dESQjYfAdoqFGTA1vj-AV3e3jL-g_ng4HJdWl_65kC0_4G9N7ouOg4cPr_ZiMBd5SvYcRfpLNmYBwqfjpSVdc3z0qErPpVuqXrAdutUTxpt.png) 
The square symmetric matrix $\textbf{M}$ is called the Structure Tensor or the Second Moment Matrix 
$$\textbf{M}=\begin{bmatrix}
\sum_W(I_x(x_i,y_i))^2 & \sum_WI_x(x_i,y_i)I_y(x_i,y_i))\\
\sum_WI_x(x_i,y_i)I_y(x_i,y_i) & 
\sum_W(I_y(x_i,y_i))^2
\end{bmatrix}$$
- The eigenvalues and vectors tell us the rates of change and their respective directions
- It concisely encodes how the local shape intensity function of the window changes with small shifts
- As with the 2d covariance matrix, the structure tensor describes an ellipse
![|400](https://remnote-user-data.s3.amazonaws.com/Dt9rM1y7UIgDaWDRXOZvFw0-vTpcPyePBL6YpxeNluy8isGJHUtUN0SRhrX5NPqJXJcd-jPuWhXtaIjMhLL-C7caWTzbMUOZNExKrSer32r19eNXHN19VEy3WcPRzSRi.gif) 
The Taylor expansion allows us to approximate the shifted intensity
We can substitute and simplify the previous equation to
$$\begin{bmatrix}
\Delta x & \Delta y\\
\end{bmatrix}
\textbf{M}
\begin{bmatrix}
\Delta x\\
\Delta y\\
\end{bmatrix} 
- \begin{bmatrix}
\Delta x & \Delta y\\
\end{bmatrix}
\begin{bmatrix}
\sum_W(I_x(x_i,y_i))^2 & \sum_WI_x(x_i,y_i)I_y(x_i,y_i))\\
\sum_WI_x(x_i,y_i)I_y(x_i,y_i) & 
\sum_W(I_y(x_i,y_i))^2
\end{bmatrix}
\begin{bmatrix}
\Delta x\\
\Delta y\\
\end{bmatrix} $$
$$E(x,y)=\sum\limits_Wf(x_i,y_i)[I(x_i,y_i)-I(x_i+\Delta x,y_i+\Delta y)]^2$$
Where
- $I(x_i,y_i)$ - Intensity in window
- $f(x_i,y_i)$ - Weighting function
- $I(x_i+\Delta x,y_i + \Delta y)$ - Intensity in shifted window
# Harris and Stephens Response Function
Rather than compute the eigenvalues directly, Harris and Stephens defined a corner response function in terms of the determinant and trace of $\textbf{M}$
![|400](https://remnote-user-data.s3.amazonaws.com/EeUxo5u5UcFr0kmT9qXROSL63tTyAPGV-S0TvFu9km65cyjzX5475WBTOmXYAGL1unx3ORhFQHVJ0lmyC2Lh-SFdyUQYk4Z9xHJ7QGj7Tk2Iv1E-hJknr6Lb0s4tbh8v.png) 
Where
- k - A small empirically set constant (usually 0.04 - 0.06)
![|400](https://remnote-user-data.s3.amazonaws.com/mLQjESv_ysA_GTuTJ51rdS-z39hRn1-mqwBHKJr-XVn4a3hc8dQWw-XmxVsRhDPYgRjd1Lq-LLeWouF_kiYw2VDliWCqQT-_zxp85Tz6jzyJW_KjU89E6la1bF6SX_50.png)
# Harris and Stephens Detector
- Take all points with the response value above a threshold
1. Keep only the points that are local maxima
	- i.e. Where the current response is bigger than the 8 neighbouring pixels
# Scale in Computer Vision
## The Problem of Scale
- If you use a technique that uses a fixed size processing window (e.g. Harris corners) then this causes problems
- As an object gets closer to the camera it gets larger with more detail, as it moves further away it gets smaller and loses detail
## Scale Space Theory
### A formal framework for handling the scale problem
- Key notion - Image structures smaller than sqrt(t) have been smoothed away at a scale t
- Represent the image by a series of increasingly blurred/smoothed images parameterised by a scale parameter t
	- Where t represents the amount of smoothing
# Gaussian Scale Space
Many types of scale space are possible
Only the gaussian function has the desired properties for image representation
- These provable properties are called the "scale space axioms"

Gaussian scale space is defined as
![|400](https://remnote-user-data.s3.amazonaws.com/GHenUWytFRU2JFwkYgkxaF_CemFSDlRj9nVGWfXFy359y6Bruf4mNb4IGJglWhBJs3uwaIv2fw3txINTudvcIxJ0QlSApvJ1of5_UvUZ-4F0j8mTU5pr1Axwwqrgq7MU.png)
$$L(\cdot,\cdot,;t)=g(\cdot,\cdot;t)*f(\cdot,\cdot)$$
Where
- $g(\cdot,\cdot;t)*f(\cdot,\cdot)$ - A convolution of the gaussian with parameter t over the image $f(\cdot,\cdot)$
- $L(\cdot,\cdot,;t)$ - A set of images
	- $\cdot,\cdot$ - Spatial coordinates of the image
	- t - Scale parameter $(t\geq0)$
		- $t=\sigma^2=\text{variance of the gaussian}$
# Nyquist-Shannon Sampling Theorem
If a function x(t) contains no frequencies higher than B hertz, it is completely determined by giving its ordinates at a series of points spaced $\frac{1}{2B}$ seconds apart
So, if you filter the signal with a low-pass filter that halves the frequency content, you can also half the sampling rate without loss of information
## Gaussian Pyramid
Every time you double t in scale space, you can half the image size without loss of information
![|400](https://remnote-user-data.s3.amazonaws.com/ODRxuLwXv4lScvGNPzZ_Hj0CdgJV3e7aR1uoHdL3OxWOG-nd_q0BTxHLYCaimi6PNFzC3KgKzwAuG2ShT_UarYhUvmujmsOjMStOnDyiln9LXXHqFPgNsSYhusgoJgYV.png) 
Leads to a much more efficient representation
- Less memory
- Faster processing
# Multi-Scale Harris and Stephens
We define a gaussian scale space with a fixed set of scales and computer the corner response function at every pixel of each scale and keep only those with a response above a certain threshold
# Blob Detection
Laplacian of Gaussian  LoG  is the second derivative of a gaussian
By finding the local minima or maxima after convolving a  LoG, you get a blob detector 
## Scale Space  LoG  
By finding extrema of this function in scale space, you can find blobs at their respective scale (~sqrt(2t))
- Just need to look at the neighbouring pixels

Useful property
- If a blob is detected at $(x_0,y_0;t_0)$ in an image, then under a scaling of that image by a factor s, the same blob would be detected at $(sx_0,sy_0;s^2t_0)$ in the scaled image

Normalised scale space  LoG  is defined as
![|400](https://remnote-user-data.s3.amazonaws.com/v3_U8z6HjKA6SOQqD4Ojmg1j0WKGCs68SIYjtXxgQqTbSUNDaUgVqstw1vq8YXvcygidEXLdVQYIdpLzplusdVV86tS6alXCLxXPmeY3crZEcDOTbd5dyR9jgppV_sXD.png) 
## Scale Space DoG
In practice its computationally expensive to build a  LoG scale space
But you can make the approximation
![|400](https://remnote-user-data.s3.amazonaws.com/EoOil7XsYINvpDlyB1m94xLhtTmM2-m4ANAtfnVa3NR0i-gRzn-jJ4vuDHkUkeKkxdBnMs2kYrDuqpLNTvkFkOnKs4fk_lZoNFHRcZZptkaVoZReGx0K_NzShpesJfT9.png) 

This is called a Difference-of-Gaussians (DoG)
- Implies that the  LoG scale space can be built from subtracting adjacent scales of a Gaussian scale space
## DoG Pyramid
For efficiency you can build a DoG pyramid
- Images between a doubling of scale are an octave
![|400](https://remnote-user-data.s3.amazonaws.com/V3paxVIVgQRuMsYQX2cE-V1xpBwDcEwUwuA7j8CsPGL5Ws9uxIMz5QOUhOxixPwS3RPDzAO5QP3mv5JIkcTx8sxgw2MQPKG3o6m4pVGc0ALnRzDXjspnopyo4ORDj1E9.png) 
An oversampled pyramid as there are multiple images between a doubling of scale