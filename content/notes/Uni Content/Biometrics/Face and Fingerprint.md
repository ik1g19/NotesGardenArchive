---
title: "Face and Fingerprint"
---

# Processes

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225191833.png)

# Fingerprints

## Fingerprint Sensors

### Optical Fingerprint Sensors

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225191908.png)

### Capacitive Fingerprint Sensors

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225191932.png)

## Fingerprint Pattern 1

Fingerprint is a set of ridges

**Macro-singularities**:
- Arch
- Loop
- Whorl

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225192444.png)

## Fingerprint Pattern 2

**Minutiae**/**Galton's Characteristics**:
- Terminations - End points
- Bifurcations - Splitting points

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225192756.png)

## Fingerprint Pattern 3

### Dependent on Resolution

#### High
##### Sweat Pores
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225193404.png)

#### Medium
##### Incipient Ridges
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225193518.png)

#### Low
##### Minutiae (And Creases)
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225193553.png)

## Basic Enhancement

### Histogram Equalisation
Used to whiten whites and blacken blacks
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225193846.png)

## Basic Filtering

### Median Filtering
Used to average out noise
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225193919.png)

## Basic Feature Extraction

### Thresholding
Sharpens contrast
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230225194031.png)

## Enhancements

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235333.png)

Image normalization to have a specific mean and variance  
Orientation estimation by using the angle of gradient of the image  
Local frequency of the image is estimated  
Is the local feature recoverable or not? Compose a mask for regions which are recoverable
A bank of Gabor filters tuned to local ridge orientation and ridge frequency is applied

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235450.png)

## Recognition Approaches

### Minutiae
Choose maximum alignment of minutiae pairings
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235544.png)

#### Minutiae Detection

##### Termination Minutia
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235842.png)

##### Bifurcation Minutia
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235906.png)

##### False Minutia
![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235927.png)

#### Matching Minutiae
Create feature vector
![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319000028.png)

### Correlation
Maximise match between fingerprint images
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230318235619.png)

Holistic fingerprint recognition using Gabor filters
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319000231.png)

### Ridges
Maximise match of selected ridge features
- Local orientation
- Frequency
- Shape
- Texture

#### Texture Based Matching
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319000315.png)

## Challenges

- Pressure/ skin deformation - nonlinear change in appearance  
- Image quality and forensic use  
- Skin condition – effect of drugs  
- Legal issues – is a fingerprint unique and permanent?

### Pressure Correction 1
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319000434.png)

### Pressure Correction 2
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230319000451.png)

# Face Recognition

## Approaches

- Holistic - Image as a whole
- Model Based - Recognition by parts

## Eigenface Overview

1. Calculate a set of weights based on the input image and the $M$ eigenfaces by projecting the input image onto each of the eigenfaces.
2. Determine if the image is a face at all (whether known or unknown) by checking to see if the image is sufficiently close to "face space."
3. If it is a face, classify the weight pattern as either a known person or as unknown.
4. (Optional) Update the eigenfaces and/or weight patterns.
5. (Optional) If the same unknown face is seen several times, calculate its characteristic weight pattern and incorporate into the known faces.

### Principal Component Analysis (PCA)
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324190404.png)

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324190426.png)

### Eigenface Approach
1. Collect image dataset (multiple samples with variation in expression and lighting. (Say four images of ten people, so $M=40$.)
2. Calculate the $(40 \times 40)$ matrix $L$, find its eigenvectors and eigenvalues, and choose the $M^{\prime}$ eigenvectors with the highest associated eigenvalues. (Let $M^{\prime}=$ 10 in this example.)
3. Combine the normalized training set of images to produce the $\left(M^{\prime}=10\right)$ eigenfaces
4. For each known individual, calculate the class vector by averaging the eigenface pattern vectors per subject. Choose thresholds for face class, and face space.
5. For new face image calculate pattern vector and distances to classes, to face space. If the minimum distances < threshold, face class identified
6. If the new image is known, this image may be added to the original set of familiar face images, and the eigenfaces may be recalculated

## Haar Wavelets

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324190615.png)

## Face Databases

- FERET
- Notre Dame HumanID
- University of Texas Video Database

## Face Recognition in Changing Illumination

### Intensity and Spatial Processing Techniques
#### Histogram Equalisation
The integration of a probability distribution function is known as cumulative distribution function (cdf), i.e:
$$
C(X)=\int_0^X p(x) d x
$$
Let us consider a histogram as a pdf. The objective of histogram equalisation is to process the original image so that the cdf of the processed image becomes a linear function(or the pdf becomes uniform).
Therefore we need to find a transformation function $s=T(r)$ so that the histogram of the processed image is uniform ($r$ and $s$ are the grey scales of the original and processed images respectively).
According to the probability laws, the following equation should hold for the histograms of the original $p_r(r)$ and processed $p_s(s)$ images
$$
\int_0^s p_s(S) d S=\int_0^r p_r(T) d T
$$
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324191515.png)

#### Method
![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324191833.png)

#### Varying Gamma
$V_{\text {out }}=V_{i n}^\gamma$
Given the half left of the face image as a reference, we can locally set gammas to change the image in the darker areas to become as bright as the left part
Masking is optional and may be used to leave out facial hairs
Histogram equalisation followed by:
$$(a=0.1, \tau=10)$$
$$I(x, y)=\frac{I(x, y)}{\left(\operatorname{mean}(\min (\tau, I(x, y)))^a\right)^{\frac{1}{a}}}$$

![|150](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324192126.png)

#### Local Binary Patterns
$1$ if greater than or equal to the middle value
$0$ if less than the middle value

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324192601.png)

Left table is without preprocessing
Right table is with preprocessing
Variability of the differently lit faces is reduced
![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324192836.png)

## Multiple Features

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324193022.png)

## Challenges in Face Recognition

- Lighting/ illumination  
- Viewpoint  
- Occlusion  
- Resolution  
- Facial expression  
- Ageing  
- Make-up/ cosmetics

## Gabor Wavelet Facial Expression Analysis

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324201416.png)

## Component Facial Expression Analysis

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324202207.png)

## Active Shape Models

- Label face points in training data
- Compress data using PCA
- Evaluate eigenvectors
- Acquire face image
- Iterate model to find face features
- Determine feature vector
- Active appearance models include texture

![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324203826.png)

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324204147.png)

## Face De-ageing

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324204820.png)

## Age Estimation

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230324205413.png)

