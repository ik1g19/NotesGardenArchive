---
title: Building Machines that See
---

# Types of Computer Vision
## Vision in the Wild - Used in everyday life

e.g. Scanning pictures at a museum to find out more information about them
## Robot Vision

Used to feed robots information about their environment
## Industrial Vision

Used for checking products made in mass manufacture
# Key Terms in Designing Vision Systems

What you want your system to be
- Robust
- Repeatable

Achieved by designing your system to be
- Invariant
- And applying Constraints
# Robustness

The vision system must be robust to changes in its environment
e.g. Changes in lighting, angle or position of the camera
# Repeatability

Repeatability is a measure of robustness

Means the system must work the same over and over, regardless of environmental changes
# Invariance

Hardware and software can be designed to be invariant to certain environmental changes
- e.g. You could design an algorithm to be invariant to illumination changes

What you design into your system to make it more robust and repeatable

Invariance to environmental factors helps achieve robustness and repeatability
# Constraints

Constraints are what you apply to the hardware, software and wetware (people) to make your computer vision system work in a robust, repeatable fashion
- e.g. You constrain the system by putting it in a box so there can't be any illumination changes
# Constraints in Industrial Vision

![|400](https://remnote-user-data.s3.amazonaws.com/ODajJMej4bd2oz0CyYz_nlxUTCauZt6-eYUUAM7Xk4hkRqx6MPbQC9PUzCQeHrCtVfhqXXt8FbTEUdBY7Khq_eA6ydByqGJPQfq_XjyznF2E9wyKs_oh5s4Sl2GIIHvm.png) 
# Software Constraints

Production algorithms need to be fast

Intelligent use of colour
- Colour can help detect if something is wrong

Simple, but incredibly fast algorithms
- Hough transform is popular
# Colour-Spaces

There are many ways of numerically representing colour
- A single representation of all possible colours is called a colour-space
- It is generally possible to convert from one colour-space to another by applying a mapping
# RGB Colour-Space

Most physical image sensors capture RGB
- Most widely known space
- "Couples" brightness (luminance) with R, G and B channels, meaning illumination invariance is difficult
# **HSV Colour-Space**
## Hue, Saturation, Value

![|400](https://remnote-user-data.s3.amazonaws.com/h-whMTyDC02QmUaoomZcwhnrb44OBfony4R1TV9bvGKXT_Wimv5IfdP2_VCs4ZnI7lqHWnF7OcuH9DVS7eKN3yN5LrTw0Pdoq3Owa-ioKa6_Q38bYay4Ibxa0HJoYm__.png) 

Hue encodes the pure value as an angle
- e.g. Red = 0° = 360°

Saturation is how vibrant the colour is

Value encodes the brightness

Simple way to achieve invariance to lighting is to use just the H or H & S components
# **Physical Constraints**

Example in Mobile Vision
- QR-codes are designed to be robust
- But most software requires (constrains) the user to operate in a certain way
	- Within a certain area
	- Orientation - Approximately upright
	- Approximately stationary
## Industrial vision is usually solved by applying simple computer vision algorithms and lots of physical constraints
### Acquisition Hardware

- Expensive camera
- Optics filters
### Environment

- Enclosure
- Lighting
- Mounting
## Example in Industrial Vision

Illuminating a room of products travelling through it so the camera can better see the products
## Example in Vision in the Wild
### ANPR Constraints
#### License plates are constrained in design

- Material which reflects IR well
- Dimensions
- Easily recognisable font for camera

License plate styles are different across the world, so most ANPR systems will only work with plates from a single country
# **Unconstrained Vision**

As computers become more powerful and software techniques are developed to deal with invariance the need for constraints become less
However, will always be the problem of optimising costs, and constraints can always help reduce costs