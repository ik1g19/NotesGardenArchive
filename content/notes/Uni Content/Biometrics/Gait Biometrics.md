---
title: "Gait Biometrics"
---

**Advantages**
- Perceivable at a distance
- Hard ot disguise

**Potential Applications**
- Security
- Surveillance
- Immigration
- Forensics
- Medicine

# Databases

## Early UCSD Data

- 6 Subjects
- 7 Sequences
- Sony Hi8 Video camera

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173228.png)

## HiD (NIST) Database

- Acquired by NIST/ USF on DARPA  
- Human ID at a Distance (HiD) program  
- 122 subjects  
- Canon progressive scan 30 fps  
- Included change in surface, shoe and luggage (covariates)  
- Included evaluation protocol

![|250](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173332.png)

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173352.png)

![|400](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173416.png)

## Southampton Data

- 100 subjects  
- Sony TRV900E digital camcorders  
- Filmed indoors and outdoors  
- Included covariate data for 12 subjects  
- Also from HiD

![|200](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173500.png)

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173537.png)

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173557.png)

## CASIA (B) Database

- 24 subjects  
- 11 Viewpoints  
- Different clothing and carrying conditions

![|250](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173702.png)

![|500](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173718.png)

![|600](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325173737.png)

## Other Datasets

- Old Southampton data  
- CMU  
- Wuhan  
- Maryland  
- MIT  
- GATech  
- Southampton Multibiometrics (face in video, gait, ear, semantics)

# Techniques for Gait Extraction and Description

#### Silhouette Descriptions (Common)
- Established statistical analysis  
- (Temporal) symmetry  
- (Velocity) moments  
- (Unwrapped) silhouette

![|250](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325174117.png)

#### Modelling Movement (Few)
- Pendular thigh motion model  
- Coupled and forced oscillator  
- Anatomically-guided skeleton

![|250](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325174137.png)

## Velocity Moments

- Extension of spatial moments  
- Applied to silhouettes  
- Selected by ANOVA

$$
A_{m n \mu \gamma}=\frac{m+1}{\pi} \sum_{i=2}^{\text {images }} \sum_{x, y} U(i, \mu, \gamma) S(m, n) P_{i_{x, y}}
$$

$$
\begin{aligned}
& A_{m n \mu \gamma}=\text { Velocity Moment } \\
& \mathrm{U}(i, \mu, \gamma) \propto v_x^\mu v_y^\gamma \propto \text { velocity } \\
& \mathrm{S}(m, n)=\text { centralised moment } \\
& \quad P_{i x, y}=\text { Pixel grey scale at }(x, y)
\end{aligned}
$$

![|300](notes/Uni%20Content/Biometrics/Images/gait%20moments.gif)

Trying to walk differently:
![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325175410.png)

![|300](notes/Uni%20Content/Biometrics/Images/gait%20moments%202.gif)

## Average Silhouette

- Popular technique for gait representation
- Also called gait energy/entropy image

![|300](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325175608.png)

1. Background is taken from each frame and pixels thresholded resulting in a binary image
![|150](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325175723.png)
2. Normalize silhouettes by height to account for distance
![|150](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325175802.png)
3. Add all silhouettes together and divide by the number of frames
4. Resulting image is the signature
![|150](notes/Uni%20Content/Biometrics/Images/Pasted%20image%2020230325175840.png)

### HiD Baseline Analysis
- Form silhouette (background subtraction +)
- Detect gait periods
- Frame Similarity between centered Silhouettes
Frame Similarity $=\frac{\text { Number of pixels in intersections }}{\text { Number of pixels in Unions }}$
- Estimate correlation of frame similarity between probe and gallery sequences
- Similarity is median of max. correlation between gallery and probe sequences

