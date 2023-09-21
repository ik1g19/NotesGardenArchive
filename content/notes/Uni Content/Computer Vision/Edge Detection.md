---
title: Edge Detection
---
# Concepts

- [Edge Detection](concepts/Edge%20Detection.md)

---
# What is an Edge

An edge is contrast

![|400](https://remnote-user-data.s3.amazonaws.com/sjzgE4trwlwrkAVA4R_0__PK9PfqVHk-JAnL9C0ro5ou59LGVZbOshNpAQgYacbuR2CWffld7-sEZrG18pcnsbsTYtLJsAkLaQaHWvMIpDKRZrLhtLVfyiIUfjFClfo3.png) 
 
# First Order Edge Detection
## Horizontal Differencing

![|400](https://remnote-user-data.s3.amazonaws.com/Sa8mSnJnkV2ZXL2zukAk2NJ48CkAsVfXT26AbQW7WhZ_ozP47Gq18_KSXeaPdT_uyQY4twh2mVwVnpxAoB4Tn6ylx7xGvt9q7W7_BpO0o3NyDz7zJAuac64Sg2NOkQWd.png) 

Detects vertical edges

Horizontal Differencing - Calculates the difference between the current point and the point to the right
## Vertical DIfferencing

![|400](https://remnote-user-data.s3.amazonaws.com/KLpQ4LDR9hc-RLSaOJKxY5KFWQz0-cr8yKdOS32FTFAPqattzNHRv_g8aC9X7kimWt40krDjNDOjxRS4NlXOuLF4TobPGMmSNbMOlt34OL7d5jdfzjf7ZCMM1-etUY2r.png) 

Detects horizontal edges

Vertical Differencing - Calculates the difference between the current point and the point below
## First order Edge Detection
The addition of the horizontal and vertical differences
![|400](https://remnote-user-data.s3.amazonaws.com/l9zVepydsn9hP4GKSf0Uqi7xY5550MlTCWm-0fpJIndWKodBjMJ0S3e3j5t4rhkCxb5J6pbEuAhwBpdShuSbjj6BouZ5x1HQaQES0esiqu5p4LmACTYIrvDSqWnkZvlf.png) 
## Vertical Edge Formula
$$Ex_{x,y}=|P_{x,y}-P_{x+1,y}|$$  
## Horizontal Edge Formula
$Ey_{x,y}=|P_{x,y}-P_{x,y+1}|$ 

## Vertical and Horizontal Edge Formula
$E_{x,y}=|2\cdot P_{x,y}-P_{x+1,y}-P_{x,y+1}|$  

This provides us a template
This is because it is 2 times the current point, minus one times the point to the right, minus one times the point below, and the other point is disregarded
### Vertical and Horizontal Edge Template
![|400](https://remnote-user-data.s3.amazonaws.com/KXshk05u4niLs68iUTPqWOZSChdrs-yNAoGTHmMW51avRDdqfXizfMm5WVRgzLwntUrb33rCINn1hvyjwRoQEkM2q_reywLov8zeSEy26bex1DtSa0gcqwkqormU6tIB.png) 
$$E_{x,y}=|2\cdot P_{x,y}-P_{x+1,y}-P_{x,y+1}|$$
In code this looks like
![|400](https://remnote-user-data.s3.amazonaws.com/KS1NSyj5Pw4gk7hpNH5_T91Q-SqKS6R-PPOHKmei5JrmT2Tv61ey__pioxYzbw6MB_KDx07MePvFlmwPbHe2GQ8etiU-Fhs8JCltOI_X1nn5uBaFznVkbxoi15_14Vdk.png) 
![|400](https://remnote-user-data.s3.amazonaws.com/l9zVepydsn9hP4GKSf0Uqi7xY5550MlTCWm-0fpJIndWKodBjMJ0S3e3j5t4rhkCxb5J6pbEuAhwBpdShuSbjj6BouZ5x1HQaQES0esiqu5p4LmACTYIrvDSqWnkZvlf.png) 

# Taylor Series
[[Taylor Series]] - Used to approximate a function at a point further than where we currently are
## Formula
$f(t+\Delta t)=f(t)+f'(t)\Delta t+\frac{f''(t)}{2!}(\Delta t)^2 +\frac{f'''(t)}{3!}(\Delta t)^3+...+\frac{f^n(t)}{n!}(\Delta t)^n$  

# Edge Detection Maths
Taylor expansion for $f(x+\Delta x)$
$$f(x+\Delta x)=f(x)+f'(x)\Delta x+\frac{f''(x)}{2!}(\Delta x)^2 +O(\Delta x^3)$$
This is equivalent to
The equivalent template is
![|400](https://remnote-user-data.s3.amazonaws.com/v9fVvJ9dxe0s1HsgxAw5KJZTzMqBaqewMyGvNF7clbw_U-RRfNmiZBlOIzVe2LezaxDWp68_URYMeOksJQZb-W8HtFWo2AkRWCtCoYwL6IWVcb9t2G1gekwYFX65-OQE.png) 
- The point minus the point to the right 
$$Ex_{x,y}=|P_{x,y}-P_{x-1,y}|$$
Expand $f(x-\Delta x)  o$
$$f(x-\Delta x)=f(x)-f'(x)\Delta x+\frac{f''(x)}{2!}(\Delta x)^2 -O(\Delta x^3)$$
Calculate $f(x+\Delta x)-f(x-\Delta x)$
$$f(x+\Delta x)-f(x-\Delta x) = \frac{f(x+\Delta x)-f(x-\Delta x)}{2\Delta x}-O(\Delta x^2)$$
This can be rearranged to
$$f'(x)=\frac{f(x+\Delta x)-f(x)}{\Delta x}-O(\Delta x)$$
This tells us
- If $\Delta x<1$, this error is smaller 
$$Ex_{x,y}=|P_{x+1,y}-P_{x-1,y}|  $$
![|400](https://remnote-user-data.s3.amazonaws.com/RI2KblfjrRq8jqnu-FCBDIqX-Yhtou79gykYbPZaxQbomzOwvFR8IMFlVZQa8NPpl2Ldc2XmwzpFYbnaIDgk9IJJa3bozTwcvb9uLoVhpX44rWI6vtRx1L8VpxOGyvRu.png) 

# Templates for Improved First Order Difference 
## My
![|150](https://remnote-user-data.s3.amazonaws.com/uAbQc8K29wW9r_v8s1Mm_ctUhzcO_7ztcxSKBhmAxX1JU6Dug2OzDyvCn_1qY3O2YUukogM_S3DVwmNRKovJPdtpnSyxB8in-ZS2Gw4h5Xxr4WAh0onWxJ3yEUfp6qb5.png) 
## Mx
![|250](https://remnote-user-data.s3.amazonaws.com/OFfqeVqcOwnRDy-lXW3bD38lOfxSao-N6t0tNzABzYrve9_FIWG-jOx8XZLPfl7zQyRtZfF_Fc8kzi8dgfVH3WjggcV6uS2XkGVcJEIyVi9otjrKLodJH3TkGDb85iLZ.png) 

# Edge Detection in Vector Format
![|400](https://remnote-user-data.s3.amazonaws.com/Y0JVAYqzxE15UxoJkmhS7Czf7j9IiVq8E2djXaLbt232j-wsoXEAPfToB550HnuxTyBl9UU6f9cAFTOdvIevoCowN2_j7Ix4ZMMxoefq-0VH26wohyN63QGVya07RrSq.png) 
#### Magnitude M
$$M=\sqrt{{M_x}^2+{M_y}^2}$$
#### Direction $\theta$
$$\theta=\tan^{-1}(\frac{M_y}{M_x})$$
# Templates for 3x3 Prewitt Operator
Averaging the improved horizontal and vertical operators over 3 rows/columns gives Prewitt templates
## Mx
![|400](https://remnote-user-data.s3.amazonaws.com/uLRzJCjzIwk41eoGZwEOt6rphTD7ITDJzBlit3ZP9HVByif789uRNK8E1OdY5s-mizPasi5h9tG-KOVPd0sqYV213LHIEAUTmsD9r0xaN6iZyLrvNebVY1Cm7oQbS4kG.png) 
## My
![|400](https://remnote-user-data.s3.amazonaws.com/dgjqyBxUm2wsIpyauvoHqglE9I1VG67wxt3oyeagwXuKn_A8j4pTiI-cQltxnJf18aqL3w2ISh2Dv7kWss5LZ1HAOdxg1sHfpU05aNlH0zlmb9LV3dAZBQc6_nF3yphx.png) 

The edge magnitude and direction is calculated for the centre point

# Applying the Prewitt Operator
## Original Image
![|400](https://remnote-user-data.s3.amazonaws.com/8LTigPhz30YwIJ9GJxQbC-mPxIuxWO7MXmwScK5rMvBBL-0A1OS4dOvydILmc99gfLgZBGa-7NRyJQrdrCHluJc1IRJa_Y0EvAo6fTYoU_o7qX4tz6QZnH5thLaawnAm.png) 
## Edge Magnitude
Blurred edges

![|400](https://remnote-user-data.s3.amazonaws.com/oA2rz975pYs27E--6qIumtOkqRbNevIN2wCNE_8g2hcNoQ1oe2mfOYRVTtxbDgpKPD602hnwp5JIIbs4cYHLJgr6CYxraiQbVWFP3_pEr26_TT9vojhjUhs2Zm7n2_wu.png) 

No double points
No missing points in the corner, unlike before
## Vector Format
![|400](https://remnote-user-data.s3.amazonaws.com/5UKBaQj1ZrJR-OKS9ER5U2YsSA_nxm0ta7oL_HGMdlCRfEN6p14qIb6-xctaodGCfNVQ-l6MvKcI4fOP5r-9sokOYrXRYLwmYyVnLN0FXg4p9FJq8Lrt7bHHAnbUrYRi.png) 
## Edge Direction
![|400](https://remnote-user-data.s3.amazonaws.com/TAowEoFGhOlLPNay9atPmct9XZ93KUem7mOUdrna7fVkN9HZ22-g4AwOuDoqzOGc04SWS2c3JPkFh8jSRz8suVAH2XylfJP1ZJgJF7b8hyGz2_j_wV4LQhZVLh-CnPDK.png) 

# Templates for Sobel Operator
Sobel is the most popular basic operator
It is an improvement of the Prewitt Operator
Double the centre coefficients of the Prewitt Operator
## Mx
![|400](https://remnote-user-data.s3.amazonaws.com/6LPbR-I4CmNhYGxcAzTUB_qZQwLi2gI4wnWlREmwh2fNBoXbQ0vTDaXmWeiOKrhVmjqHGCcAgFWsOFvxfAJuDu5t7X5O6MSQDxdhCMypQu4D6Y6-74wfC-BIHVRFLvCq.png) 
# My
![|400](https://remnote-user-data.s3.amazonaws.com/zQ643T-uxE2cgoF7KvY9C9Ydmv6GI7mtyCk-t318qYViy5xbvDfCz0bMXRyzdHBTHG0YIkH9FF-qMrLi7DEoFoJwJNWn5iTBIAwuxdLlLmtKq3dEKF1LMMqSpZt2TYxz.png) 