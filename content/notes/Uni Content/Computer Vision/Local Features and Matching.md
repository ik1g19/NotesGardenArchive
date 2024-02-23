---
title: Local Features and Matching
---
# Concepts

- [[SIFT]]
- [[Feature Vector]]
- [[Image Matching]]

---
# Local Features

Interest points are detected in the image and a feature is extracted from the surrounding pixels, represented by, usually just one, featurevector

Feature points are used for
- Robot navigation
- Camera pose estimation and camera calibration
- Motion tracking
- 3d reconstruction
- Image alignment
- Object recognition
- Indexing and database retrieval

# Matching with Features

- Detect feature points in both images
- Find corresponding pairs

![|400](https://remnote-user-data.s3.amazonaws.com/MgSq7AlBR3NJb86c8nrUBZ3FhQCyrJDYEWvEeyAeOqzzPEWWn0Nz_uSQeTjrUatItrdAeo9CLwSxjYDRKyqKOP-ChBfVT26iik46nCX-a0TSmELS_x4M6ZFMbtxVdYaq.png) 
## Issues with this method
### Problem 1

![|400](https://remnote-user-data.s3.amazonaws.com/pXvwDOMvt5qv3xoROYc_l87nvsdzZF2CRRbECnxl0aQRhqWQOqd_MuSFB94Jlh0syfqpsZWw2rLG7gECHVt4SiRA4Tbbn3vsib8E1b30Virp8WGI8p1gVnNBXE-tdXXC.png) 

- We need to detect the same points independently in both images
- We need a repeatable detector
### Problem 2

- We need an invariant, robust and distinctive descriptor of each point
- For each point, we need to able to recognise the corresponding point in the other image

![|400](https://remnote-user-data.s3.amazonaws.com/g9QJxvqJocrDxgQmeVjzb3KVnXIyidb5GvIOETOw3kx5QdI3MJ-D-6Qz2bkwC8siIbiLAbwRnVNiUqABPbP9L78ymfoY5mZdk6bsFBx7zDbwRkBwIOLW3zjRFvBKD9Nh.png) 

# Two Types of Matching Problem

In stereo vision there are two important concepts related to matching
## Narrow-baseline stereo

The camera has made a small movement between its two images of the recorded object

![|400](https://remnote-user-data.s3.amazonaws.com/YauNt3JRUpF3yu4YIUEkiGEEnQ0WBARSUISVAyEoeFmai-Jevi5tIiM4GUQXBYQ4laRAV0CA5o9NJ-xFpFhgCuOAxnX1K_2dgfZ1A-KDFf9xuYjCfmDA9F3bBz6VfnzA.png) 
## Wide-baseline stereo

![|400](https://remnote-user-data.s3.amazonaws.com/WepGxv2LlL5KbVUDi6liIcwWmC0uECnwuCXKQbRcm1Q5_isLnE9D6DtXYh1Z7scTz0Gw8Oo372tRovAG478BPPRxJGaWovl3ws2dSMVcCqHJ6YyY1CSxEekDjo_qyaPA.png) 

The camera has made a large movement between its two images of the recorded object

- These concepts extend to general matching
	- Techniques for wide-baseline stereo are applicable to generic matching tasks
		- e.g. Object recognition, panoramas, etc
	- Techniques for narrow-baseline stereo are applicable to tracking where the object doesn't move too much between frames

# Robust Local Description
## Descriptor Requirements
### Narrow Baseline

- Robustness to rotation and lighting are not so important
- Descriptiveness can be reduced as search is over a smaller area
### Wide Baseline

- Need to be robust to intensity change, invariant to rotation
- Robust to small localisation errors of the interest point
	- The descriptor should not change too much if we move it by a few pixels, but to change more rapidly once we move further away
- Need to be highly descriptive to avoid mismatches
	- But not so distinctive you can't find any matches
 
# Matching by Correlation (Template Matching)
## Narrow Baseline Template Matching
### Interest point in two images with a slight change in position

![|400](https://remnote-user-data.s3.amazonaws.com/hC87RA5XrBKiKxVkYJL7DC6YYWJeTF3ynedwDe-evZIrR55TbocCk5IzEQtAj7WSULvsWB5aPhJImNBsqPWVkdxEQPRmLQexyksW7Y1L8KIOi96K6a7JzFvRShM-PrCb.png)

### Local search windows, based on the interest point in the first image

![|400](https://remnote-user-data.s3.amazonaws.com/loMkCqQe3t6z76j-81Vc05xFKoUbd0oYznxHAuwPL4AOQcNUKCp3mgF-R8kpWim_m7ohHkSwCEqEQOz6zYpLMKoDVbnCQ2418xxEB99Gbd7IOHYl2mJX7mixUw1iL_yW.png)

### The template can then be matched against target interest points in the second image

![|400](https://remnote-user-data.s3.amazonaws.com/lXIvoWAFeuwJ1bdmkLcPrKw_FDxM2zocurvfBIkH-Qz048vmvf972Ezlg-577J9XoxKpAW9P09jxoxHFzT61RB2YYa64d1h8q7H2h8s7K3afvjF42mM4vDILLZz8YUxn.png) 
## Problems with Wider Baselines

- Sensitive to localisation of interest point
	- Not a problem with a small search window
- Not robust to rotation
- Can't assume a search area with wider baselines
	- Need to consider all the interest points in the second image
		- More likely to mismatch

# Local Intensity Histograms
## Use local histograms instead of pixel patches

1. Describe the region around each interest point with a pixel histogram

![|400](https://remnote-user-data.s3.amazonaws.com/BdtcXa7Kb81ptkrLcloRZ6BIZ-FkOWdvM11e9DNxixjl8fHr1PCmYyZ8cn9M5yG3Qtau7_xSbuKSTq14690JyNYZDsTfIkCmZWU9v634tyx2XCfEvEaP6I5kQUi7rImP.png) 

2. Match each interest point in the first image to the most similar point in the second image
	- i.e. In terms of Euclidean distance or some other measure between the histograms

![|400](https://remnote-user-data.s3.amazonaws.com/0GhfQcOe1cNcsG486ptg6GOaNnnpAsElQ3TMWaLibaE9va7XNCwM3WEFTfNa3FSJ0jL_6y8J9mT9J_FEFL5IZtGO4oBixjFR5bJNCzJ8bwHrVTnVUMTshXEhPLjxIgCC.png) 
## Problems

- Not invariant to illumination changes
- Sensitive to interest point localisation
- Not rotation invariant if the sampling window is square or rectangular
	- Can be overcome by using a circular window
- Not necessarily very distinctive
	- Many interest points are likely to have similar distribution of grey values
## Overcoming Localisation Sensitivity

Apply a weighting so that pixels near the edge of the sampling patch have less effect, and those nearer the interest point have more
- Common to use a Gaussian weighting centred on the interest point for this

We want to allow the interest point to move a few pixels in any direction without changing the descriptor
## Overcoming Lack of Illumination Invariance

Illumination invariance is potentially achievable by normalising or equalising the pixel patches before constructing the histogram
### Local Gradient Histograms

Instead of building histograms of the raw pixel values, we could instead build histograms that encode the gradient magnitude and direction for each pixel in the sampling patch
- The gradient magnitude and direction histogram is also more distinctive
- Gradient magnitudes and directions are invariant to brightness change
#### Building Gradient Histograms

- For each pixel in the sampling patch
	- Accumulate the gradient magnitude of that pixel in the respective orientation bin
- Quantise the directions (0°-360°) into a number of bins
	- Usually around 8 bins

![|400](https://remnote-user-data.s3.amazonaws.com/2ApfIGZrYEZC1Yra_ppqXtWJnZ7xbCIEiu1PV2hmi6WvWY5dIyW6j-iC6nFAHjrAmUEDkUipuqNR_3Dx6DRUaExJqRSe9Nra-YV5saOPUB5IFwxsiTCUTQXNqUzo55CN.png) 

You can compute the gradient orientations/directions and magnitudes of an image by using its partial derivatives

![|400](https://remnote-user-data.s3.amazonaws.com/jvLgv-gF2sU-0fvyNAnegWsEU8-Jkzk9aqvjHdVehahAYSbn_eu-1wcMYglFJBB0NFq3VpY92nX7I2VEORserATfFjrkKZCwZGgTCFToY-lH-JmACGKUn54oV-z2debO.png) 
#### Rotation Invariance

- By finding the dominant orientation
	- And cyclically shifting the histogram so the dominant orientation is in the first bin

![|400](https://remnote-user-data.s3.amazonaws.com/y9g-0vm-wkAkYyhZW7X98YsDoliicRCiz_6MfYL09Y8kChpyt35BFtIREyV_iQN3u4mGyZNqiS87sTnmk-V0Dw-eukKjrXEAiY3_ikEveVHPtckq6Or87FyPZ3sIcZq-.png) 

- Gradient histograms are not naturally rotation invariant
- But can be made invariant

# The SIFT Feature

Standard SIFT geometry appends a spatial 4x4 grid of histograms with 8 orientations

Leading to a 128-dimensional feature
- Which is highly discriminative and robust

- Built on local gradient histogram idea
	- Which effectively creates multiple gradient histograms about the interest point and appends them all together into a longer feature
- Incorporates spatial binning
- The Scale Invariant Feature Transform (SIFT) is widely used

# SIFT Construction
## Sampling

- Sampling patch around interest point
- Patch is either fixed size, or more commonly, proportional to the scale of the interest point

![|200](https://remnote-user-data.s3.amazonaws.com/5P2OQ570ccA_sUDgzsqDCBlcT1nZiSRg6eyTE9189-eqCQdIVricXJ0g7pJ61PVZQJs61fNkxKEb2HMQaYBKO59mFbLO7eIUJ69AC6yYI_1NEtdZuP2Op9VSKb74XdlS.png)
## Binning

![|200](https://remnote-user-data.s3.amazonaws.com/4aF8Cqvz_c4eMkYMTTUTVS4Sv6FgqoLQbrxAlr5CRGUCrMPfVbcmpZ6s7WboDBi9O1yu_svtuzUjhqRyUXp4HBsPkR3HMszgGSFUAOjHHTWaB8fkXXGc-FWF1MrAEIrv.png) 

Gradient histograms, taking into account the gaussian weightings, are created for each spatial bin
- Orientations are measured relative to the overall dominant orientation of the patch

There are usually 4x4 spatial bins, rather than the 2x2 shown
## Weighting

![|200](https://remnote-user-data.s3.amazonaws.com/O09a-SgiqIV1HKWV5_aTcJDeidpdxBX7Dqx7RunwyRvaZZ_eCU7rvnWKJo4ZCzS1NolHnQygiv2y-MocFabw4VcpavjCX4rY3cieYaykVGXqpy3xR1xXzqspFfghhWTk.png) 

The corners of the sampling square have zero weight, so in effect the sampling region is actually circular

A gaussian centred on the interest point weighs pixel contributions lower near the edges
 
# Matching SIFT Features
## Euclidean Matching

Take each feature in turn from the first image, and find the most similar feature in the second image
- Threshold can be used to reject poor matches
- Doesn't work too well and results in lots of mismatches

The simplest way to match features

## Improving Matching Performance

Only form a match if the ratio of distances between the closest and second closest matches is less than a threshold
- Threshold typically set to 0.8
- This means you can be more confident you have found the right point as you can see if there are any another similar points, that it could potentially be

Take each feature from the first image, and find the two closest features in the second image
