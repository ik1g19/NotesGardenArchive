---
title: Image Sampling
---
# Concepts

- [[Fourier Transform]]
- [[Aliasing]]

---

# Sampling Signals  

![|400](https://remnote-user-data.s3.amazonaws.com/bOlCevRBG3Va1ErzkhOPz4r-OklHb2kBfWWhmEEOVxtCLFJ56QbviNgqR-ibFM8KM92QfBlRLYua4dx8ex9YDJ7pj6q8nxo0hC8gq4YnVxGp4uBA271vC1yrQSUMK8aZ.png)

![|400](https://remnote-user-data.s3.amazonaws.com/M8g_BEZSH9CZJQKwHR542oUMhXoziLRxzb1B3imcwrNIuF3UGrxcLhe3jb1nBg2_gFY82BDl_ZbgUpSM7gYmISiihN33oaqJ3fWfU4d5tNa5Ua1Pq-hYpV4o4ea0QYOK.png)

![|400](https://remnote-user-data.s3.amazonaws.com/mXOLSg5UPhMhgl-K_lifu0aMIoL2NqlwEzef98E38BhxW0Lt3nwhJ79vCTcQ3XbuL_dcBuUW1u9U0JzfEFODjlGJHDpubJfSd1c6-HA7cL9GBopaR7Jy6_96aC4g-8ZU.png) 

Bad sampling - where you sample too little, you get the wrong signal
- This is called Aliasing

Good sampling - where you sample often, you get a more accurate signal

Aliasing - The wrong signal is obtained due to poor sampling

# Aliasing in Sampled Imagery

![|400](https://remnote-user-data.s3.amazonaws.com/sTvSLx2sc5Us4PrxTV4VP5WUiEQC0kj28qtrbdHHqfLsRZyYceoXsHBMzYlA8DPiEWINu2a7THb45cQLyNlR9ZNLnDb4DRMe0axTSK-yEItfS5j25Lt9T8GdRmp3uP1T.png)

The blinds have a high frequency structure, there is an extra pattern in the low resolution image
 
# Correct and Incorrect Apparent Wheel Motion

In films wheels can appear to rotate the wrong way, this is because the sample rate is too low, so the wheel appears to move the opposite direction

![|400](https://remnote-user-data.s3.amazonaws.com/93RNOo8Dw4nMWe0LjmSXU784AjhrgBSNcwBZ5d5-K6EZ32i-0U1Ar52VmfRMQi9sJPysN-eWr0NZxa2Eedzs3LrAe6cup5uBXjcDYX6N1N1-BpWn_hnAgmxPOlfBMjZS.png) 
 
# In the Frequency Domain

![|400](https://remnote-user-data.s3.amazonaws.com/1pjs0LXcX7K5IL8YxGfJvzAy75-e0kxwHHmuf0sgFjtuKn5zeEs7sRBYyo7kw3O7AeuHiREMdg_izhExnGdTnZ8zHwrN69PagE7gfhtZan7tZJPj013b-q48WOLTN114.png)  

- So the minimum sampling frequency is 2\*max 
- When sampled at a correct frequency - when the spectra repeat they just touch
- The sampling process is to make the range of signals (spectrum) repeat
- When sampled at a low frequency - the spectra overlap. The high frequency areas (grey areas) have been corrupted
- When sampled at a high frequency - the spectra are quite far apart

# Sampling Theory  

Guideline - Two pixels for every pixel of interest

Nyquist's sampling theorem - In order to be able to reconstruct a signal from its samples we must sample at minim at twice the maximum frequency in the original signal
 
# 1D Discrete Fourier Transform

$Fp_u=\frac{1}{N} \sum\limits_{i=0}^{N-1} p_i e^{-j\frac{2\pi}{N}iu}$ 
- Purpose of Discrete Fourier - Discrete Fourier calculates frequency from data points
- In the continuous domain you could integrate, since the domain is now discrete we have to use a summation
- $p_i$ is a vector of sampled points
- $Fp_u$ is a vector of sampled frequencies
- N is the number of data points 
- $e^{-j\theta}=cos\theta-jsin\theta$

# Transform Pair for Sampled Pulse

![|400](https://remnote-user-data.s3.amazonaws.com/0wCgDuLbgl8iByCehou1z7nQfds9uEYpad7L0A2YTQeMagG-d_yzLh-sbDNW74m6mRN628CUIZb8gIy503U720xxVjGJbplAvCVOgf-HFXFmOQQBqIhsrDSNZHHN3ImI.png)  

The Fourier transform takes us from the time domain to - the frequency domain

The sampling theorem says that if you don't sample well enough - then you can't get back again
## Signal Reconstruction from its Transform Components

![|400](https://remnote-user-data.s3.amazonaws.com/CBHMczyidmRIdjXkwWLtdRbw8610OSHBe5g-zEoZSfsuuUQPWYCrO0MbjaL0h7hv9rwFWte2jVUkWxcKEhuLEi1B5eB-El2N53E-shbM6JFn5xHawVblu3nfNnf0PEnA.png) 
 
# 2D Fourier Transform
## Forward Transform
-  __x__  and  __y__  - Two dimensions of space
-  __u__  and  __v__  - Two dimensions of frequency
- $\textbf{F}\textbf{P}_{u,v}=\frac{1}{N^2}\sum\limits_{x=0}^{N-1}\sum\limits_{y=0}^{N-1}\textbf{P}_{x,y}e^{-j(\frac{2\pi}{N})(ux+vy)}$
-  N  x  N  image with pixels $\textbf{P}_{x,y}$
## Inverse Transform
$$\textbf{P}_{x,y}=\sum\limits_{u=0}^{N-1}\sum\limits_{v=0}^{N-1}\textbf{F}\textbf{P}_{u,v}e^{j(\frac{2\pi}{N})(ux+vy)}$$

# Implementation via Fast Fourier Transformation

This is a 1-D Fourier Transformation

![|400](https://remnote-user-data.s3.amazonaws.com/mkiAk6nlpkQSlgb8Hfhedz8WiFBXtP7sTrBj1CbWW6ybWW0G54K6kSpuTGDDITi7ozFz9QAWFaevReOslpbXiI8F0Vpthq_dJ8ljQbM4RHseXGIjtI8v5TR8YwlwiVyU.png)
 
# Properties of Fourier Transform

1. Shift Invariance - Shifting the image does not change the magnitude of the Fourier transform
	- ![|400](https://remnote-user-data.s3.amazonaws.com/dwdjV_8xK3_HGrHFcXP5b5U1rMDUETVux2avnq7Hor26SYXrYnilaHmljZy9eO1ZRlSeHs9CuypnE4lJ8tql27XglqqPxN1iqVr-YWpSC6IDMWpE3Rh-wFsa36RT68Au.png)
2. Rotation - When you rotate an image, the frequency components rotate
	- ![|400](https://remnote-user-data.s3.amazonaws.com/YRBtb9Z6HdQaNlPZ-bhSonoFTVeN5LoZCzwO4JJrLHFbOyXN0TgMSh_zir6hbV_qmfTI8rNXnDRot4nyAm9UFlFV9leUJqMSUs4_pjNkB_vUpP4VPatlN0AoDfbKe3GF.png)
3. Filtering - Fourier transforms provide access to different frequency components
	- ![|400](https://remnote-user-data.s3.amazonaws.com/yqiR6v19Ot4jnNXRtmCUZ5rSL8-xGafcKdfGzjEkASn-z5Ji9mQ8H-zmgdH6_8B_X-F-zn12QHwR0pPk7QYmd74mS5VPI6xoJTnuCTplb1HwZd0HDfFt8vgb1XXa9HRv.png)

# Applications of 2D Fourier Transforms

- Understanding and analysis
- Representation (invariance)
- Speeding up algorithms
- Recognition/Understanding
- Coding
