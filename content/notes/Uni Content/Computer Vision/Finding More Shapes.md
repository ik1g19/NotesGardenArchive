---
title: Finding More Shapes
---

# Hough Transform for Circles
Has duality, similar to line equations
OR
Points x_0,y_0
Radius r
- Centre x,y
$$(x-x_0)^2+(y-y_0)^2=r^2$$
OR
$$(x-x_0)^2+(y-y_0)^2=r^2$$
- Radius r
- Centre $x_0,y_0$
- Points x,y
## Circle Voting and Accumulator Space
Illustrations courtesy of Mark Nixon
#### Accumulator
 ![|150](https://remnote-user-data.s3.amazonaws.com/Xh747k5sUlB3PbfyJANIIc8w7rVzcA0R3_cYFPEJt_Tb3rrnwhQ72t3y7fMoZJdRFbcOCjgO4qcPbSm7dBoFZDzjCYDQjCbLa8XrrCXYGILPr9c2Qafuq4hyR5kNQ-ci.png) 
#### Image
![|150](https://remnote-user-data.s3.amazonaws.com/f4wCMbV9KIQbeV4XcQC0c_DY5zTJJCvd4gX5vG4Mp08eApJ0AAKCXM3ww9LrcHvyvlQoSEJBKztBIlljQUfzIc0GvqnTmLhPqf9tFwcCU_3OcI_t4Y6zkWljiP7KP-C4.png) 
An edge point in the image corresponds to a circle in the accumulator space. Every point on the circle in the accumulator space is considered a vote
Same process as line voting
The accumulator space is actually third dimensional, the third dimension represents the radius of the circle
The point in the accumulator with the most votes will be an intersection of the cones where the circles have the same radius as they did in the original image, and the point will be the crossing of all of the circles
So we are actually generating cones of votes
![|400](https://remnote-user-data.s3.amazonaws.com/j6dAdtJPCYmYRyNQhfkTh6GDhlpNrqqaMQc6a5eZs-VaXXWCOPRSeJdvAeKEtog1vSCPKpVYPev8VljX312UCpGqIG9L8xdXuOempc5Ihit1L_v5hoV8RanjBxZalDUK.png)
## Pseudocode for Circular Hough Transforms

## Applying the Hough Transform for Circles
![|400](https://remnote-user-data.s3.amazonaws.com/KIZuwV-JzFSX6EqlEYY4W40CDa_NP3o78rOFrkCEMLT7QkP3kk9ba_RgEOPfvJ5yTzwzhJuxHSvqNwe1_yulF0pie4DcMMGZEmmOnFg_2IBc6iGf0BfgNqw8Y2qJMJUM.png)
## Extensions into Conic Sections
### Ellipse
$$\frac{(x-x_0)^2}{a^2}+\frac{(y-y_0)^2}{b^2}=1$$
Ellipses are described by 4 parameters
Accumulator size increases rapidly as the range of values increases
Memory size becomes impractical
Motivates approaches to save memory and improve speed
## Improving Circular Hough Transform Performance
Differentiating (x-x_0)^2+(y-y_0)^2=r^2 
Gives $\frac{dy}{dx}=-\frac{(x-x_0)}{(y-y_0)}$
The final circle equation only has two parameters, which reduces accumulator space greatly, increasing performance 
Rearranging
$$y-y_0=\frac{r}{\sqrt{1+(\frac{dy}{dx})^2}}$$
$(\frac{dy}{dx})^2$ is the edge direction 

Substituting for (x-x_0) back into the circle equation
$$(\frac{dy}{dx})^2(y-y_0)^2+(y-y_0)^2=r^2$$
## Arbitrary Shapes
How to recognise shapes which are sections
Use a generalised Hough transform
And vote via the look-up table
Form a discrete look-up table (R-table)
## R-table Construction
Then store those combinations of r and \alpha and index them by the edge direction
Then measure the edge direction at the points on the outside of the shape
Firstly find the reference (centre) point of the shape, which can be found by averaging the x and y points of the shape
Edge direction is not unique so there will be multiple entries in the tables at certain values
- This eventually gives noise in the accumulator where multiple values are stored at the same index
Using this, we then determine the length r and direction \alpha to the outside points from the reference point
## Procedure for Generalised Hough Transform
### Preparation
Form r-table (list of points, indexed by edge direction)
Determine centre of template shape
### Application
Use r-table to vote for points in the real image
Take maximum from accumulator to find centre co-ordinates of the shape

## Scaling for Generalised Hough Transform
Accounting for shapes being different distances from the camera
If you want to find a shape regardless of the scale of the shape (any size)
- We then have an accumulator in terms of x_0, y_0, centre coordinates and the scale
- We scale the vector of the voting, we vote for scales of the distance from the point to the centre
- This gives a three dimensional accumulator array, which will find shapes whatever size they appear
## Orientation for Generalised Hough Transform
Add another dimension to the accumulator space
We can then rotate the vector in the r table, and then vote for different rotations 
## Active Contours
For unknown arbitrary shapes
- Extract by evolution
Shape is placed on image and contracts until it finds the desired shape
### ![|400](https://remnote-user-data.s3.amazonaws.com/E1DhNW3SkqoDyi97zqV9rDm9QC8UVhnHQ4JlsWM8jR99PTVQVrxTRKwrDuevQyOB_qUcNAWiLwIZn8m9RlwwxVJ_BI7ZRyAUhVRnCkd2zDXp1LIC0MccIistS_GEF-H8.png) 
## Geometric Active Contours
![|400](https://remnote-user-data.s3.amazonaws.com/6ybzufr_PzCsE4uqOmLASxvukwViDqtUTFhm1CJpPT9bRU5Y0ZkpsFIs4gu9n6TTNwvkEYPyiApsvQG9pbYIK-q-oTAKq7k8gHyQjjn-eRPqXJdzWlsGr6R4G7v3aCpg.png)
Extracts a shape by using information from a segment of the image