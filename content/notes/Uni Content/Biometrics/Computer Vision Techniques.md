---
title: "Computer Vision Techniques"
---

# Background Subtraction

What the fuck was he talking about in the background subtraction part

# Wavelets

Wavelets are used for:
- Scale-Space analysis
- Simultaneous decimation in space and frequency

## 2D Gabor Filter

$$g w 2 D(x, y)=\frac{1}{\sqrt{\pi \sigma^2}} e^{-\left(\frac{\left(x-x_0\right)^2+\left(y-y_0\right)^2}{2 \sigma^2}\right)} e^{-i 2 \pi \pi_0\left(\left(x-x_0\right) \cos \theta+\left(y-y_0\right) \sin \theta\right)}$$

$$\begin{array}{ll}-x_0, y_0 \text { - central position } & -\theta \text { -orientatio } \mathrm{n} \text { of the wavelet } \\-f_0  \text { - central frequency } & -\sigma \text { - width of the wavelet }\end{array}$$

#### Applications of Gabor Wavelets
1. Texture Modelling and Analysis
	1. Iris texture measurements for security systems
	2. Face feature extraction for automatic face recognition systems
2. Image coding
3. Image restoration

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224184042.png)

# Intensity and Spatial Processing Techniques

## Image Histogram
A histogram shows the number of pixels for each gray scale in an image

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224184222.png)

## Image Scaling
Sometimes the gray scales in an image are outside of the standard range  
\[0 – 255\]
In such cases, image scaling (or normalisation) is required to  
map the gray scales to the standard range
Methods for image scaling:
1. Linear scaling
2. Linear scaling with clipping
3. Absolute value scaling

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224184658.png)

## Histogram Stretching
Sometimes the histogram of the original image is too narrow leading to poor  
visibility
In order to enhance the image, a histogram stretching technique is used  
to simply stretch the domain of the histogram using linear scaling methods
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224185422.png)

# Edge Detection

**Edge** - Sharp change in intensity

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224215448.png)

Best way to find an edge is to take derivatives
1. Detect local maxima of first derivative
2. Detect the zero-crossing of the second derivative

$$\frac{\partial I}{\partial x} \approx I(x+1, y)-I(x, y) \rightarrow\begin{array}{|l|l|}\hline-1 & 1 \\\hline\end{array}$$

$$\frac{\partial I}{\partial y} \approx I(x, y+1)-I(x, y) \rightarrow\begin{array}{|c|}\hline-1 \\\hline 1 \\\hline\end{array}$$

By convolving these masks with the original image the partial derivatives can be calculated

## Prewitt Masks

$$\begin{array}{|c|c|c|}\hline-1 & -1 & -1 \\\hline 0 & 0 & 0 \\\hline 1 & 1 & 1 \\\hline\end{array}\hspace{1em}\begin{array}{|c|c|c|}\hline-1 & 0 & 1 \\\hline-1 & 0 & 1 \\\hline-1 & 0 & 1 \\\hline\end{array}$$

## Sobel Masks
Smooths the image before edge detection

$$\begin{array}{|c|c|c|}\hline-1 & -2 & -1 \\\hline 0 & 0 & 0 \\\hline 1 & 2 & 1 \\\hline\end{array}\hspace{1em}\begin{array}{|c|c|c|}\hline-1 & 0 & 1 \\\hline-2 & 0 & 2 \\\hline-1 & 0 & 1 \\\hline\end{array}$$

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230224221833.png)

## Laplacian of Gaussian (LoG)
In order to find edges of an image, LoG filter is convolved with the image and the zero-crossings of the filtered image is considered as edges
The Gaussian filter smoothes the edges before edge detection
A threshold can be used to determine how big the difference is between neighbouring pixels of a zero-crossing

# Feature Extraction or whatever

# Object Description

## Desirable Properties

- Complete - Different objects must have different descriptions  
- Congruent - Similar objects must have similar descriptors  
- Compact - Efficient. I.e., quantity of information  
- Invariant - Recognise independent of changes  
	- Illumination  
	- Geometry: Scale, Translation, Rotation

### Invariance
Recognise independent of orientation
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001205.png)

Can lead to ambiguities
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001229.png)

## Region Description

### Area
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001342.png)
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001355.png)

### Perimeter
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001412.png)
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001422.png)

### Compactness
Measures the efficiency with which a boundary encloses an area
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001455.png)
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001505.png)

#### Examples
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001536.png)

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001554.png)

### Dispersion
Measures the occupancy as the ratio between the area of the circle enclosing the region and the area of the region

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001629.png)

Can alternatively be measured as the ratio between the circle enclosing and contained inside the region

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001702.png)

### Moments
Consider the region as a distribution
$$
m_{p, q}=\sum_x \sum_y x^p y^q I(x, y) \Delta A
$$
Zero-order: Total Mass
$$
m_{0,0}=\sum_x \sum_y I(x, y) \Delta A
$$
First-order/Centre of mass
$$
m_{1,0}=\sum_x \sum_y x I(x, y) \Delta A \quad m_{0,1}=\sum_x \sum_y y I(x, y) \Delta A
$$
Location of centre of mass
$$
\begin{aligned}
&\bar{x}=\frac{m_{1,0}}{m_{0,0}}\\
&\bar{y}=\frac{m_{0,1}}{m_{0,0}}
\end{aligned}
$$
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001931.png)

#### Invariance
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319001957.png)

#### Centralised Moments (Translation Invariant)
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324205737.png)
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324205752.png)

#### First-Order Centralised Moments
$$
\begin{gathered}
\mu_{1,0}=\sum_x \sum_y(x-\bar{x}) I(x, y) \Delta A \\
\mu_{1,0}=\sum_x \sum_y x I(x, y) \Delta A-\sum_x \sum_y^{-} \bar{x} I(x, y) \Delta A \\
\mu_{1,0}=\sum_x \sum_y x I(x, y) \Delta A-\bar{x} \sum_x \sum_y I(x, y) \Delta A \\
\mu_{1,0}=m_{0,1}-\frac{m_{0,1}}{m_{0,0}} m_{0,0} \\
\mu_{1,0}=0
\end{gathered}
$$

#### Second-Order Centralised Moments
$$
\begin{gathered}
\mu_{2,0}=\sum_x \sum_y(x-\bar{x})^2 I(x, y) \Delta A \\
\mu_{2,0}=\sum_x \sum_y\left(x^2-2 x \bar{x}+\bar{x}^2\right) I(x, y) \Delta A \quad \bar{x}=\frac{m_{1,0}}{m_{0,0}} \\
\mu_{2,0}=m_{2,0}-2 m_{1,0} \frac{m_{1,0}}{m_{0,0}}+\left(\frac{m_{1,0}}{m_{0,0}}\right)^2 m_{0,0} \\
\mu_{2,0}=m_{2,0}-\frac{m^2{ }_{1,0}}{m_{0,0}}
\end{gathered}
$$

#### Example of Centralised Moments
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324210427.png)

#### Normalised Central Moments (Scale Invariant)
The normalised central moment of order (p+q) is obtained by dividing the central moment of the same order by a normalisation factor
$$
\begin{gathered}
x^{\prime}=k x \quad y^{\prime}=k y \\
\eta_{p q}=\frac{\mu_{p q}}{\mu_{00}^\gamma} \\
\gamma=\frac{p+q}{2}+1 \quad \forall p+q \geq 2
\end{gathered}
$$

#### Second-Order Normalised Centralised Moments
$$
\begin{aligned}
& \eta_{2,0}=\frac{\mu_{20}}{\mu_{00}^\gamma} \quad \gamma=\frac{2+0}{2}+1=2 \\
& \mu_{2,0}=m_{2,0}-\frac{m_{1,0}^2}{m_{0,0}} \quad \quad \mu_{0,0}=m_{0,0} \\
& \eta_{2,0}=\frac{m_{2,0}}{m_{0,0}^2}-\frac{m^2{ }_{1,0}}{m^3{ }_{0,0}} \\
&
\end{aligned}
$$

#### Invariant Moments (Rotation Invariant)
$$
\begin{aligned}
M 1= & \eta_{20}+\eta_{02} \\
M 2= & \left(\eta_{20}-\eta_{02}\right)^2+4 \eta_{11}^2 \\
M 3= & \left(\eta_{30}-3 \eta_{12}\right)^2+\left(3 \eta_{21}-\eta_{03}\right)^2 \\
M 4= & \left(\eta_{30}+\eta_{12}\right)^2+\left(\eta_{21}+\eta_{03}\right)^2 \\
M 5= & \left(\eta_{30}-3 \eta_{12}\right)\left(\eta_{30}+\eta_{12}\right)+\left(\left(\eta_{30}+\eta_{12}\right)^2-3\left(\eta_{21}-\eta_{03}\right)^2\right)+ \\
& \left(3 \eta_{21}-\eta_{03}\right)\left(\eta_{21}+\eta_{03}\right)\left(3\left(\eta_{30}+\eta_{12}\right)^2-\left(\eta_{21}+\eta_{03}\right)^2\right) \\
M 6= & \left(\eta_{20}-\eta_{02}\right)\left(\left(\eta_{30}+\eta_{12}\right)^2-\left(\eta_{21}+\eta_{03}\right)^2\right)+4 \eta_{11}\left(\eta_{30}+\eta_{12}\right)\left(\eta_{21}+\eta_{03}\right) \\
M 7= & \left(3 \eta_{21}-\eta_{03}\right)\left(\eta_{30}+\eta_{12}\right)\left(\left(\eta_{30}+\eta_{12}\right)^2-3\left(\eta_{21}+\eta_{03}\right)^2\right)+ \\
& \left(3 \eta_{12}-\eta_{30}\right)\left(\eta_{21}+\eta_{03}\right)\left(3\left(\eta_{12}+\eta_{30}\right)^2-\left(\eta_{21}+\eta_{03}\right)^2\right)
\end{aligned}
$$
#### Invariant Moments
$$
\begin{gathered}
M=\eta_{20}+\eta_{02} \\
\eta_{2,0}=\frac{\mu_{20}}{\mu_{00}^2} \quad \eta_{0,2}=\frac{\mu_{02}}{\mu_{00}^2} \\
M=\frac{\mu_{20}+\mu_{20}}{\mu_{00}^2}
\end{gathered}
$$

#### Example Invariant Moments
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324212206.png)

#### Advantages of Moments
- Work on grey scale as well as binary objects
- Can utilise pixel brightness
- Access to detail

#### Disadvantages of Moments
- Assumes only one object present
- Computationally expensive
- High order moments
- Large numbers
- Sensitive to noise

## Shape Description

**Drawbacks**
- Difficult to extract curves from images
- Ambiguous (many objects can have similar shapes)
- Analytic complexity in many areas

Boundary/ Shape description
- Discrete
	- Chain Codes
	- Run-Length Codes
	- Extreme points
- Curves
	- Polynomials
	- Splines
	- Wavelets
	- Fourier
- Properties (Discrete/Curve)
	- Length
	- Curvature
	- Bending energy
	- Convexity

### Fourier Descriptors
1. Have image and template image
2. Take boundaries of both
3. Find Fourier Expansion of boundaries
4. Convert to Fourier Descriptors of boundaries

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325164834.png)

#### Common Fourier Descriptors
**Polar** Fourier Descriptors (angular)  
- Cumulative Angular Function  
- Fourier Series (trigonometric form) 

**Elliptic** Fourier Descriptors  
- Complex Curve  
- Fourier Series (complex/trigonometric form)

#### Elliptic Fourier Descriptors
Basic approach
1. To obtain a complex function from the 2D curve  
2. To perform a Fourier expansion  
3. To define descriptors from Fourier coefficients

##### Complex curve
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325170327.png)

##### Alternative Definitions
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325170433.png)

##### Trigonometric Expansion
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325170930.png)

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325171013.png)

##### Trigonometric Form
$$
\begin{array}{ll}
a_{x k}=\frac{2}{T} \int_0^T x(t) \cos (k \omega t) d t & a_{y k}=\frac{2}{T} \int_0^T y(t) \cos (k \omega t) d t \\
b_{x k}=\frac{2}{T} \int_0^T x(t) \sin (k \omega t) d t & b_{y k}=\frac{2}{T} \int_0^T y(t) \sin (k \omega t) d t
\end{array}
$$

##### Discrete Computation
$$
\begin{array}{lll}
a_{x k}=\frac{2}{m} \sum_{i=1}^m x_i \cos (k \omega i \tau) & \text { and } & b_{x k}=\frac{2}{m} \sum_{i=1}^m x_i \sin (k \omega i \tau) \\
a_{y k}=\frac{2}{m} \sum_{i=1}^m y_i \cos (k \omega i \tau) & \text { and } & b_{y k}=\frac{2}{m} \sum_{i=1}^m y_i \sin (k \omega i \tau)
\end{array}
$$

##### Basic Approach
1. To obtain a complex function from the 2D curve
$$
c(t)=x(t)+j y(t)
$$
2. To perform a Fourier expansion
$$
\left[\begin{array}{l}
x(t) \\
y(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0} \\
a_{y 0}
\end{array}\right]+\sum_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]
$$
3. To define descriptors from Fourier Coefficients

##### Invariant Descriptors
$$
\left[\begin{array}{l}
x(t) \\
y(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0} \\
a_{y 0}
\end{array}\right]+\sum_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]
$$
###### Translation
$$
\begin{gathered}
{\left[\begin{array}{l}
x^{\prime}(t) \\
y^{\prime}(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0} \\
a_{y 0}
\end{array}\right]+\sum_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]+\left[\begin{array}{l}
t_x \\
t_y
\end{array}\right]} \\
{\left[\begin{array}{l}
x^{\prime}(t) \\
y^{\prime}(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0}-t_x \\
a_{y 0}-t_y
\end{array}\right]+\sum_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]}
\end{gathered}
$$
###### Translation Invariant
$$
a_{x k}^{\prime}=a_{x k} \quad b_{x k}^{\prime}=b_{x k} \quad a_{y k}^{\prime}=a_{y k} \quad b_{y k}^{\prime}=b_{y k} \quad \text { for } k \neq 0
$$

###### Scale
$$
\left[\begin{array}{l}
x^{\prime}(t) \\
y^{\prime}(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0} \\
a_{y 0}
\end{array}\right]+s \sum_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]
$$
###### Scale Invariant
$$
\frac{a_{x k}^{\prime}}{a_{x 1}^{\prime}}=\frac{a_{x k}}{a_{x 1}} \quad \frac{b_{x k}^{\prime}}{b_{x 1}^{\prime}}=\frac{b_{x k}}{b_{x 1}} \quad \frac{a_{y k}^{\prime}}{a_{y 1}^{\prime}}=\frac{a_{y k}}{a_{y 1}} \quad \frac{b_{y k}^{\prime}}{b_{y 1}^{\prime}}=\frac{b_{y k}}{b_{y 1}} \quad \text { for } k \neq 0
$$

###### Rotation
$$
\begin{aligned}
& {\left[\begin{array}{l}
x^{\prime}(t) \\
y^{\prime}(t)
\end{array}\right]=\frac{1}{2}\left[\begin{array}{l}
a_{x 0} \\
a_{y 0}
\end{array}\right]+\left[\begin{array}{cc}
\cos (\rho) & \sin (\rho) \\
-\sin (\rho) & \cos (\rho)
\end{array}\right]_{k=1}^{\infty}\left[\begin{array}{ll}
a_{x k} & b_{x k} \\
a_{y k} & b_{y k}
\end{array}\right]\left[\begin{array}{c}
\cos (k \omega t) \\
\sin (k \omega t)
\end{array}\right]} \\
\\
& a_{x k}^{\prime}=a_{x k} \cos (\rho)+a_{y k} \sin (\rho) \quad b_{x k}^{\prime}=b_{x k} \cos (\rho)+b_{y k} \sin (\rho) \\
& a_{y k}^{\prime}=-a_{x k} \sin (\rho)+a_{y k} \cos (\rho) \quad b_{y k}^{\prime}=-b_{x k} \sin (\rho)+b_{y k} \cos (\rho) \\
& a_{x 0}^{\prime}=a_{x 0} \quad a_{y 0}^{\prime}=a_{y 0}
\end{aligned}
$$

##### Example
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325172343.png)

![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325172406.png)

##### Multiscale
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325172642.png)

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325172707.png)

