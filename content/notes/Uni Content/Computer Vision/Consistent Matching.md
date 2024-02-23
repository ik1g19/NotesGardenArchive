---
title: Consistent Matching
---
# Concepts

- [[Image Matching]]
- [[Transforms]]

---
# Constrained Matching

Assume we are given a number of correspondences between the interest points in a pair of images

![|400](https://remnote-user-data.s3.amazonaws.com/eaiIjWPdu_I8cqT5l2Cx_FcUPLRmVowmdKTV0HVUFXehJVHviybk3ke3U4zrnYqrhaG-7f13aeUNAVaW4tkrje0cTfqMModRNqULHmCe2BacS5LM8OGYo5vWAZZEekJK.png) 

We estimate which of the correspondences are inliers (e.g. correct) or outliers (e.g. incorrect/mismatches)

We assume there is a geometric mapping between the two scenes, that can help us eliminate the mismatches 

#### Geometric Mappings

![|400](https://remnote-user-data.s3.amazonaws.com/s_ded5ZwlepxfNXL0upv6LEcv1XdAC2f7DntDbQmxthAdI0akbGF7JUAuEK2MunQKLWa5A8v-Cj2_e-lsO27bidg97zlED8VHHvEcwwNtLW168zk4hgOIog-bmuoOKee.png) 

# Point Transforms

We use point transforms of the form
$$x'=Tx$$

Where
- $x$ - the original coordinate
- $x'$ - the transformed coordinate
- $T$ - the transform matrix
## Similarity Transform

Has 4 Degrees of Freedom
- Translation + Rotation + Scale
## Aspect Ratio

![|400](https://remnote-user-data.s3.amazonaws.com/9_Ls2O4_CLThyLytQtG2tzbakOPk-NAKLxiAqzKO-dsSNRQe81taqzye6MNjR2wxt3ft7UXupH2h4LT0fy7pqwMUctqZQRo5X3v543cWvWykC--ZkY1Sl4NAqNHeCVLe.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/kI7es1GN4mbQjcSwEvjIWjuy_rl_jMnEIiCFfvNGYftRfTVjVbLp8GPhaCs-CB3WHGj4m86FfK3mGPuHxwNE_Ljp11FDdCXyrzeChK7MHCbN53Yelm56ZYdRE7OfEkKO.png) 
## Affine Transform

Has 6 Degrees of Freedom

Translation + Rotation + Scale + Aspect Ratio + Shear
## The Affine Transform

It is more convenient to write this as a single transform matrix by adding an extra dimension to each vector

![|400](https://remnote-user-data.s3.amazonaws.com/Pavhub8UGazgnMcKT7eoopwbI6jcdn0oxfqWbgzvL04qlYd7SQayjQLdjstGB4Xpco18_sAbAkV0vXC0wgSJwKcyWftD9m9ILZQBOjjltUJFZXOIZppvaQ9mxyHAoThH.png) 

**Defined as**

![|400](https://remnote-user-data.s3.amazonaws.com/RUa3QjasjqgjwQMMmm8MFS3qShOjRWWCZXAxeeFMopes4jQ9ZRre_LdYwn2lEGotwHeE5dzV29rKBo8yP3sHDNx3jmY960NGbkr5zxoxQu6077WIEIIqHfeCCR1PfdEw.png) 
$$x'=Ax+b$$
## Translation and Rotation

![|400](https://remnote-user-data.s3.amazonaws.com/EGziOPVB4v7X9N4Wu58tE_BowSWrwVKRkA1iL1FiO05-gpMApn1WyHCZMzitVsUCmoKYq3A-vNFbZrdPgwYv01EhGI4YgAHBVWVCTZy8XCB9R1auL-YMAxzvK6QHlaKn.png) 
![|400](https://remnote-user-data.s3.amazonaws.com/UZIGqWE3ZOKwSFsRoWC5wCLjG6bXHT0pVeNFJ87J93YDVn9NlBoaPoGM2fW1jd_ReN-NlNCvvwhR8lwPcWGsekq2BYaAJReTjV1h7LMqBKaeWfmOzoYx_gNgE7chhyzN.png) 
## Translation

![|400](https://remnote-user-data.s3.amazonaws.com/O27tW1bJ7ufWHowGCPjMfeEmo8S0608R80L5EwPHT1LKPk37ZfgE7IIWRF4BDZgSen_d_dYmb_42edflYmCqH4N0IV5UEA-cFMeiFnGnPdWLNGQTUwLs1usggwKLd7Sd.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/Iw5e_LhS-eEQ0vUFL2P1QqWS96vI3NPDV5_zjOH-qUXGfntunXPaWY99GE4kXNIiKF5oNgvQyh0vh9328DFVkhCTj80XgelzKOXHulQdQMltR-2ZARjeSnBA6XqhwQoL.png) 
## Shear

![|400](https://remnote-user-data.s3.amazonaws.com/6o_BDxRdcYDo0ujXj0aj3weUlVdUsuJCrAhbuPjQod1hRyq0TFK7SDn156kfJGtSfOD10nyLyRx0beCO6v9_juTgCHvIhhDSbhzcgJHYZ7Ia3a-nmc1P70VFqymGMwlC.png) 
 
![|400](https://remnote-user-data.s3.amazonaws.com/VXQk6r-6gevZ2RdLsYhZ4s8dGn3VR8qcvlGUOizPTPwGdWVx0fUCOVlqQDY1U14Qe2Jhy_ehcIXK7A4ShmY72escOi3YcEcM3_otoIFq5edKDkbpqVqZDFLdlFrWTH1-.png) 
## Scaling

![|400](https://remnote-user-data.s3.amazonaws.com/mMkcdsWQhspsAYfdMtrr429BexwUjFaBcQTura-yPHaYoHL1EyCRqJ7crOE2d4pUEKAY5TLz2m8uVgCCAfCDsepHuIH_YG1ul6RJ3v048VC83wSfoD8Vzs607N2VMhBp.png) 
![|400](https://remnote-user-data.s3.amazonaws.com/SOumd9ejjNadlsEedpGefhBIqJneSM6-MzQZpVrh5kyTvpZ4_pe5z4Jqa-x5xtkLWQWUHKfWhj1IVTKdqd0wMstv_etIJcjIg8Sc2Pw4OgJiuYHppYLzXubWmVes-Det.png) 

Geometric Transforms change the content of an image by applying a mapping
- To Incorporate more Degrees of Freedom
# Homogeneous Coordinates

Coordinates are called homogeneous when they are modelled like this
$$\begin{bmatrix}
wx'\\
wy'\\
w
\end{bmatrix}$$
$$y'=v/w$$

We normalise by w so that the transformed vector is $$\begin{bmatrix}
\cdot & \cdot & 1
\end{bmatrix}$$
$$x'=u/w$$
g and h will allow us to model perspective

![|400](https://remnote-user-data.s3.amazonaws.com/T_idr1Ky53aBsKv2qN1rh29Y9Anu3v6HjmmEQARDhlUmDW6n-Zxq5m_U1HIeck-I8hBpvKsork7Mh2NP8GS8-jLJKhkKxdQ2PpcCjxfr2oZJEY-Ey4q102JdEE504GKL.png) 
 
The Planar Homography (Projective Transformation)

![|400](https://remnote-user-data.s3.amazonaws.com/T_idr1Ky53aBsKv2qN1rh29Y9Anu3v6HjmmEQARDhlUmDW6n-Zxq5m_U1HIeck-I8hBpvKsork7Mh2NP8GS8-jLJKhkKxdQ2PpcCjxfr2oZJEY-Ey4q102JdEE504GKL.png) 
$$x'=u/w$$
$$y'=v/w$$
$g$ and $h$ are the keystone distortions

They squish one side of the image to simulate a perspective change

![|400](https://remnote-user-data.s3.amazonaws.com/ZB25yPRaMp214_rEXnE6jF9mwAz5G1LRws1LGsSmC0rmHQB0slpXzvt_b0qlS6_bkpP1B-9HkhmbXqIzkz8f5w9QOY3cRtU_CpwF2pTH3GYvq_iM29XhWQj_1YVRjtSb.png) 

# Recovering a Geometric Mapping
## Simultaneous Equations
### Least Squares

![|400](https://remnote-user-data.s3.amazonaws.com/ng9x_dID0F7wLEYAYDfF4NpeKzlc3DiecM8ZuIQcLq421k589f7oVDqLRhIrxO7AMyCe_cc02HIAm1cwS5RAtgCdg5emUtEUDdwccPW6DMLwQouvLJnnXo0KhXxnQnix.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/xQgpVj6qXDEhZtiCzIDfFRrk9giF8s3f5TplVZ8dWXqtwfmK41-Rxik-o5SW0Er0Ska8_sxoBkDTzwLa-2lTv2d3MML1HiTHO_YCVhRhpgnXXC509axfYUyLQCfszzkv.png) 

We need to seek the minimum error, or least squares solution

In the presence of noise, and with potentially more matches than required, we have to solve an overdetermined system

It is possible to estimate a transform matrix from a set of point matches by solving a set of simultaneous equations

We need at least 4 point matches to solve a homography or 3 to solve an affine transform
## Robust Estimation
### RANSAC - RANdom SAmple Consensus
#### We assume

- M data items required to estimate model T
- N data items in total
#### Algorithm

- Repeat steps 1 to 4 n times
- If k is large enough, either accept T
	- Or compute the least-squares estimate using all inliers, and exit with success 
- Select M data items at random
- Estimate model T
- Fail - no good T fit of data
- Find out how many of the N data items fir T within tolerance tol, call this k
	- The other points are the outliers
	- The points that have an absolute residual less than tol are the inliers
	- i.e. Compute how many times the absolute residual is less than tol

Need a way to deal with estimating a model (i.e. a transform matrix) in the presence of high amounts of noise (i.e. mis-matches)

Least squares will be sub-optimal and find a very bad solution
 
# Applications of Robust Local Matching
## 3D Reconstruction

Possible to estimate depth, and ultimately build a complete 3d scene from sets of point correspondences formed from matching local features
## Matching Music/Sounds
### How Shazams aglorithms work

A recording of a piece of music is turned into an image called a spectrogram

Local image features can be extracted, described and matched from the spectrogram images
## Object Recognition & AR
### Object Recognition

Image of object is matched against scene, and recognised if there is a consistent match
### Augmented Reality

Data can be added to a scene on the basis of a match

# Problems with Direct Local Feature Matching
## Local feature matching is slow

Typical image may have ~2000 interest points/sift descriptors

Each sift descriptor is 128 dimensions
- Assuming your matching a query against a database of images...
## Optimising
### Hashing

Locality Sensitive Hashing (LSH) creates hash codes for vectors such that similar vectors have similar hash codes
### Efficient Nearest Neighbour Search
#### K-D Trees

K-D Tree Problems
- Doesn't scale well to high dimensions
	- You end up needing to search most of the tree
- There are approximate versions, which won't return the exact answer, which do scale

Binary tree structure that partitions the space along axis-aligned hyperplanes
##### Searching

- Walk down the tree until a leaf is hit, then brute force search to find the best point in the leaf

![|400](https://remnote-user-data.s3.amazonaws.com/wqzjPYyTj1FT0ayVve_9BdEQDt0AahN3li1V6gr98QINfjbJSI2pkHoSvO2GyQQ3BhEt5rDyGwldrQZRHVY4dPRs-n3q8eshO2dgGzZkihfkW2MKmBKTByxelZDM4oof.png) 
![|400](https://remnote-user-data.s3.amazonaws.com/68gnUfNyW2xE3SV9ZmdSMNpdbf7LcKhNiGFPjY5D-MIdlqlQuf8UXMn-IMGBLf5_di6XQa9izD3H_3CLoBRvsBk3VnCPNl65BQeyx8hFL0I6Ho5z0S8tR18d4Cl3yc3C.png) 

Then backtrack and see if the next subtree needs checking

![|400](https://remnote-user-data.s3.amazonaws.com/FCC7HUmnpfsh9wg11FLIS27hd27K-s7UU5XtlrgFuI6SamgW3F4s8mWsYiOb0yGVDpWXRMNHL0Lf2QzmLQ0Pxw9C1vRW15U3qQsA6pb4wqdKyuxhBapRo_yZfpfn0VRX.png) 

- A subtree needs checking if the partition is closer to the query point than the current best found point
- Then repeat the brute force process in each partition you check

![|400](https://remnote-user-data.s3.amazonaws.com/wRxxlhhn_EkMc97cZ2mRBIg-uL84GSGiHcWnaCr-F-8VKhZdSytUAs9x7x6z-lPgj8U18r7OJtYGFP5xncaHaIjUXessKUkYz-oxKUL_TJ3zM3taob2elHqNleIVeQWU.png) 

Stop after a certain depth, or when the number of points in a leaf is less than a threshold

Typically take each dimension in turn and split it on the media of the points in the enclosing partition

![|400](https://remnote-user-data.s3.amazonaws.com/R5MoeeRg4pvhfRFE9NyAwvU83PJS4NSayFleq7Faady61upmXilr0BLV0lrNaTn2phNyDeAlw5IFSA6y_uct6jRCdOQaIJ0UZXfgaQcKC3LXNVe40IlbVY0jSVlR2u8w.png)
![|400](https://remnote-user-data.s3.amazonaws.com/Z_5j-0vw0DG3Ps8UYckeqow66lImGA9UkI3pvzF6tlwrpSSa0Tk28G503Gm5eztRcTpJXIKpqgn1SZgu5ysmLfcurnpnV7uhZn8GJQvgYjaB3UECNW8LWy6RF1y48Ry6.png) 
### Sketching

With the correct LSH function, the Hamming distance between a pair of sketches is proportional to the euclidean distance between the original vectors

Concatenates binary hashes into a bit string

Can compress sift features to 128 bits
- Hamming distance computation is cheap 
