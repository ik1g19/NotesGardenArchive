---
title: Further Edge Detection
---

[[Sobel]] is a good basic operator but has blurred and noisy edges
# Canny Edge Detection Operator
## Stages in Canny Edge Detection
1. Gaussian Smoothing
2. [[Sobel]] [[keywords/Edge Detection|Edge Detection]]
3. Non-maximum Suppression
4. Hysteresis [[Thresholding]]

![|400](https://remnote-user-data.s3.amazonaws.com/I_9Ei80WT3SUadCSbOGikQxLEc-FLZzWFWaTdTNHsq2dV03Lu2YZ8sGOsmrdwouKMyTs2YEh_Qb--fpD8wNWA46w6UKk8655Ey8AXJOschZr7XrfNOyEg-LH0uOcKHFm.png)  

![|400](https://remnote-user-data.s3.amazonaws.com/I_9Ei80WT3SUadCSbOGikQxLEc-FLZzWFWaTdTNHsq2dV03Lu2YZ8sGOsmrdwouKMyTs2YEh_Qb--fpD8wNWA46w6UKk8655Ey8AXJOschZr7XrfNOyEg-LH0uOcKHFm.png)

[[Canny]] gives thin edges in the correct places, but is a more complex process
## Objectives of the Canny operator
Optimal detection with no spurious responses (no responses to noise)
Single response to a single edge
Good localization with minimal distance between detected and true edge position (edges are in the right place)

The objectives made the operator un-implementable, so a set of approximations are used
- Threshold with hysteresis to connect the edge points together
- Use the Sobel operator
- Non-maximal suppression (getting rid of everything that isn't the maximum)
- Gaussian smoothing
# Interpolation in Non-maximum Suppression
![|400](https://remnote-user-data.s3.amazonaws.com/y2GV04Wur_kyNdjMCmj2FS0Vki7aE3fXoMWRfHUhhEVVyczKqVC3nAZmDiUahsYPnwa_QMLtSx9gIbbuXiGki29J_RtNXsF_k8js3T9uYXo7mHM-OHnGjkq8bYbKifL2.png) 
Uses linear interpolation, as you need to use points which are not on the image grid
# Hysteresis Thresholding Transfer Function
Has an upper and a lower threshold, for when the value is increasing or decreasing respectively

[[Thresholding]] with memory

Hysteresis thresholding takes into account that if you have found an edge, then you are likely to find another edge next to it, so the threshold for what is considered an edge decreases
![|400](https://remnote-user-data.s3.amazonaws.com/HpgegWKU6TetnzHqRvYmMn7hBM1AzyEv8z_MJ5Jf515Wc-1RBuVnd_ebVQ4Hs5ijtnNzddfEMmvVJiG0zIcCOFUIDIl4C96im7pMeDx6uXAC2E8WqOUi-bYuPChVFxLh.png) 
How does it work
- Has an upper and a lower threshold, for when the value is increasing or decreasing respectively
For edge detection, the lower threshold is the average {{noise }}and the upper threshold is the average feature boundary
# Action of Non-maximum Suppression and Hysteresis Thresholding
![|400](https://remnote-user-data.s3.amazonaws.com/lfvUh-kU6uW6wHWsM9xaNJ6UWo__vWQoMNARV2Bbm9xNT60Fd49gfOLK_8OrLQkEOWQ72AaSH39-GYoF2WNF4abwWYq2273c733jcf1StRhcQrUchhsXOLzjAUXzCZp4.png) 
# Comparing Hysteresis Thresholding and Uniform Thresholding
![|400](https://remnote-user-data.s3.amazonaws.com/ofUotIs1P6HTyc85G8Df9jxSX9mutRef3Gkr_PpsjYGiCJvyhser3kfZRJQb4_3WCa0RWBm7ZpngiaUyFc4w7Hl1-hnNYj8ww1KmKQW_JjEGFYwxkiNg9X16RBssTXxH.png)
AND any connected points > lower threshold
Hysteresis thresholding gives all points > upper threshold AND any connected points > lower threshold
# Comparing Canny and Sobel
![|400](https://remnote-user-data.s3.amazonaws.com/3aKroWSBaKU4E5OpMokfns7yqSb4_0S7ZEcJ9EfxQEGkh4ntfRPWduertyI_EhW0PIV2inkKtkId7XQ62CZLz3hPhUoL7yf13QDNHggg99KFlgRxezdydI1pRQ8g9L3e.png)
Canny gives thinner lines and less noise
# First and Second Order Edge Detection
![|400](https://remnote-user-data.s3.amazonaws.com/UUWAUWI67_sECkEpVdi57eG7QbkwzhRzgqCdWeEUVWtf3lscB6uNQqF3QGkEBDHAQ4FL602zZHbZ_Pd1ozhhoPOo0yPLHr8CXFPQNGF25B-wr7L2E4jLWrPSx07XN9p2.png) 
### First Order
Single differentiation→then threshold the function to find the edge (The red dotted line)
(The red dotted line)
Such as→Canny and Sobel
### Second Order
(The green dotted line)
Second derivative→then find the zero crossing (where the gradient of the first derivative is 0) (The green dotted line)
# Edge Detection via the Laplacian Operator
Where the numbers change from negative to positive there will be a 0 crossing so there is an edge
![|400](https://remnote-user-data.s3.amazonaws.com/AoCIrnaM__5MWV-gTScIsCPm0uPHvr-P7GhWXwPRsF3hImkVwfPFjVkrqiSvYgg5C4dUFy8DIeSnpyUJH42tEUauJMIQdXWpn39dvsb4-w0H-fxCaxhdUXPl730X74d5.png) 
## The Laplacian Operator
![|400](https://remnote-user-data.s3.amazonaws.com/AoCIrnaM__5MWV-gTScIsCPm0uPHvr-P7GhWXwPRsF3hImkVwfPFjVkrqiSvYgg5C4dUFy8DIeSnpyUJH42tEUauJMIQdXWpn39dvsb4-w0H-fxCaxhdUXPl730X74d5.png) 

The Laplacian operator is a second order operator
![|400](https://remnote-user-data.s3.amazonaws.com/mgYiymmW8Pyu3XW5mm78rvqfv0QvlD_fbIgSerHLbw9YrK5YbEnOjv3wl2XP4uvpKuO5cc6M0VpdgBNK3ctA5gX-uVq4-O-D0nm6i5lqWOFp7nNvfzX8Q66vmj_1geVz.png)
Since first order operators are sensitive to noise→second order operators will be even more sensitive to noise, which is why there is a -6 inside the image, which is not close to any edges
There is an edge where→the numbers change from negative to positive, as there will be a 0 crossing
# Laplacian of Gaussian
## Derivation
- Then differentiate again
$$\frac{\delta^2 g(x,y,\sigma)}{\delta x^2}=(\frac{x^2}{\sigma^2}-1)\frac{e^{}\frac{-(x^2+y^2)}{2\sigma^2}}{\sigma^2}$$
- Take the Gaussian function
$$g(x,y,\sigma)=e^{\frac{-(x^2+y^2)}{2\sigma^2}}$$
- In terms of x and y, the second derivative is
$$\Delta^2 g(x,y,\sigma)=\frac{\delta^2g(x,y,\sigma)}{\delta x^2}U_x + \frac{\delta^2 g(x,y,\sigma)}{\delta y^2}U_y$$
- Differentiate once
$$\frac{\delta g*x,y,\sigma)}{\delta x}=-\frac{x}{\sigma^2}e^{\frac{-(x^2+y^2)}{2\sigma^2}}$$
- Which simplifies to
$$\Delta^2 g(x,y,\sigma)=\frac{1}{\sigma ^2}(\frac{x^2+y^2}{\sigma^2}-2)e^{\frac{-(x^2+y^2)}{\sigma^2}}$$
- Substituting in the previous equations gives
$$\Delta^2 g(x,y,\sigma)=(\frac{x^2}{\sigma^2}-1)\frac{e^{}\frac{-(x^2+y^2)}{2\sigma^2}}{\sigma^2} + (\frac{y^2}{\sigma^2}-1)\frac{e^{}\frac{-(x^2+y^2)}{2\sigma^2}}{\sigma^2}$$

Formula→$\Delta^2 g(x,y,\sigma)=\frac{1}{\sigma ^2}(\frac{x^2+y^2}{\sigma^2}-2)e^{\frac{-(x^2+y^2)}{\sigma^2}}$ 
The Laplacian of Gaussian operator is called the Mexican Hat operator because of its shape when plotted
![|400](https://remnote-user-data.s3.amazonaws.com/sTTe5B7Bt4rK9J9R0tNl-6OA1MuDU9l2PRa2PhRpxCsl0Xu66JajKUKAZA4mDnNiTYKQijVugOqS621Q1LIO7e7KhoVLIkjb7ozx1rVPW6v3bCYocHlKINQ8vQpeYZj8.png) 
# Zero Crossing Detection
We take the average of each of the points in each quadrant
We split the 3x3 section into 4 2x2 sections
![|400](https://remnote-user-data.s3.amazonaws.com/TPCqF1Pt2k7f8bP3euPJQxuHg49sMPZgemDCHhMPUjZxcmwAr066QlVMMsBhC8vn8S5M-J6l8ptETGgFcTNy1dl2j1WFQdpAUlJ4DmgzVLEwQkEhr3x3FFBBmYZpekpc.png) 
If one of the quadrants has a negative average and one of the quadrants has a positive average, then there must be a zero crossing at the centre point
We split the 3x3 section into 4 2x2 sections
![|400](https://remnote-user-data.s3.amazonaws.com/TPCqF1Pt2k7f8bP3euPJQxuHg49sMPZgemDCHhMPUjZxcmwAr066QlVMMsBhC8vn8S5M-J6l8ptETGgFcTNy1dl2j1WFQdpAUlJ4DmgzVLEwQkEhr3x3FFBBmYZpekpc.png)  
If one of the quadrants has a negative average and one of the quadrants has a positive average, then there must be a zero crossing at the centre point
$$IF (max(1,2,3,4) > 0 \land min(1,2,3,4)<0) THEN f(x,y)=edge$$
We take the average of each of the points in each quadrant
# Examples of Second Order Edge Detection
## Marr-Hildreth Edge Detection
![|400](https://remnote-user-data.s3.amazonaws.com/vKrHyJK3OCYWlv4Sd5LbBvobuDGwZSnIQJZ_WrhKikyOnKfTo6hOFdnlZ0QPEL_wQNqKe0dNvYZtbJgP4Y7D9Q4A8A8sJelOb6Nb0CDhMOkBZZtSPDz1DF36UhnVUUR2.png) 
Window size and variance must be specified as input
# Comparison of Edge Detection Operators
![|400](https://remnote-user-data.s3.amazonaws.com/C-5TC3QerivbcQsrCfq40-DOEvlw9girIjm7IKBRKWufTYGB0yk0LIDO2tWDWC2b_G9Fhb252hpMlqj_0I7coMHXbLGBjaJXnGSA-S2NS7Ux1_TBdD0TOSiskbiQD1r-.png)