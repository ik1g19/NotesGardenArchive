
# Grouping points to find shapes
## **Template Matching**

### Process of Template Matching

We store a count of the matching points

Where the match is best, we've found the shape

![|400](https://remnote-user-data.s3.amazonaws.com/Gwx6FL5lJT5-R68EQS3v3U5oIJ3KJG5gFAmmNWhbqBSDoH6ljvmR0eDkPKzZJFmLNqz5pmzsdXHdmrUQ7XCdel8ZjIOEYTin_AIP2-_UlYznUeKPCQspsdgH4UPYeDo2.gif) 

Take a template of what we want to find and match it to the image

![|400](https://remnote-user-data.s3.amazonaws.com/sGWWCr_gFjUmJfTeVqK5_ez7HxkG2Qlyil1fKdz7gWCo7deItS3FM2m8W95K93k1sQbypDdNJWvdXo2sPL4iR_Hwoje05D2nyFL6xfEyg9LxuUUJ7QvsoBQMrijGdB02.png) 

Where the match is best, we've found the shape

This process can be improved by just matching the edges

But if only the edges are being matched, then only the text and symbols on the sign will be matched, producing much less noise

In the example the template could match with some points in the road or the sky, producing some noise
## **Template Matching in Occluded and Noisy Images**
### Occluded Images

Template matching is optimal in occlusion

Shapes can be found even when partially occluded

![|400](https://remnote-user-data.s3.amazonaws.com/E5ZRNk2lASpAiMExr36jFzVufj2J5vJPtyZHI30y-Yf61geZR2A7HdhJ86tOHXQuZpSpRHmsa-EbYcEOnFEsOnBwTknG14IwPGDGDPsZd9aJHt-xOlmFAwQaVQv-X69W.png)

![|400](https://remnote-user-data.s3.amazonaws.com/E5ZRNk2lASpAiMExr36jFzVufj2J5vJPtyZHI30y-Yf61geZR2A7HdhJ86tOHXQuZpSpRHmsa-EbYcEOnFEsOnBwTknG14IwPGDGDPsZd9aJHt-xOlmFAwQaVQv-X69W.png) 

Shapes can be found even when partially occluded

Template matching is optimal in occlusion
### Noisy Images

Shapes can be found in noise that is challenging for human vision

![|400](https://remnote-user-data.s3.amazonaws.com/uxyf5JnOhSbcw0Mc1KnAZrpcaoU6FBbKx4jqsgv9ucicqs2JPc8jloRUhuJZPp1QSwBvQltYSNe92WDrEqxZhFJi6KcqZDvlle2QuJdQeQwaZGmUT09xw8vTDiKnNhbQ.png) 

Template matching is optimal in noise

Shapes can be found in noise that is challenging for human vision
## **Convolution and Correlation**

Correlation is about matching templates

You are just shifting the template across the image, looking for a match

$I\otimes T=\sum_{(x,y)\in W}I_{x,y}T_{x+i,y+j}$

So we need to flip the Fourier template

$I \otimes T=\mathscr{F}^{-1}(\mathscr{F}(I)\cdot \times \mathscr{F}(-T))$

Convolution is about application of a template

It involves flipping the template
- $I\cdot T = \sum_{(x,y)\in W}I_{x,y}T_{x-i,y-j}$
- This is very slow with large templates
- Can be sped up by multiplying the transforms

OR by multiplying the transforms
- $I\cdot T = \mathscr{F}^{-1}(\mathscr{F}(I)\cdot \times \mathscr{F}(T))$
## **Application of Correlation using FFT**

![|200](https://remnote-user-data.s3.amazonaws.com/t2hyTF8GQh35R3r2_M7PIURlCI3BoAHx-Im3Zz6bs3BgP1k_pO_mRWysK-IqBu5M0hGIFaotDa27ittn7CaKKcKGL8wkvfCX4UEFAzsCO_FFalFdfEfZK95VZtiLOwCy.png) 


![|200](https://remnote-user-data.s3.amazonaws.com/ilXxdB9Lcxy7JvhwrXeOYz8Dn2ppWyVEfiX0H3CuMk0A-wNjqzjvw7SBS0g4SHF4QIkVCuhVPNHrML--q9FO45xwqBLV7jxyJBC_AIUQW9cmv8mHu5WYzyIYOR39olRS.png) 


![|200](https://remnote-user-data.s3.amazonaws.com/iXsKbmEs87ZdlnkMYTqV4sZfvXP2xhajPsb9f4Os8wlv_pn4UkHUZZDOmEr1wSa1fEirFrlCJCPJiDUG4NtA2BQ5GPqJ31F7h8OBnetlsMAlI6bJO-1eXUNnaVI8UMfG.png)

![|200](https://remnote-user-data.s3.amazonaws.com/HviOFqUtqEDihHOD4Ekii9EumAU71I3ljjXWPKf_OaGSia19PfyMT41VzRHXj_nbAJiD8aC9nvLTXcV-4OFZsOpMWc4gVc_P6dZ5ylmEdqzKas3byjncq_JXuXlywHF0.png) 

![|200](https://remnote-user-data.s3.amazonaws.com/_dEO7MoIfwIdrFgY9DEVTouLtq8yjGiAjotUcuKT_vmpZ7fv6QIcCuuF3rxUTnVcgkDgEccRLRX95N_aPrWST39LuQrwfY4_DAy7yoxPzLtM-zwAZdXaH2uN29375pMh.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/H4BYSTKkSNksltu5eE7EGVZtEPwaGYPCxNNmsjwAW2U_41qZ1vWMEfWe_S0CULEDUzVlcmkW7IpWod375nvmhXfgNoAUE7kQA24S-pp-N2xIp0XZm-z1QHqq4FdIKjWn.png) 

No sliding of templates

Cost is 2xFFT plus multiplication
## **[[Hough]] Transform**

Performs the same as template matching, but is faster
### The Principle of Duality 

A line has
- points x,y
- gradient m
- intercept c
- y=mx+c

A line can also be represented as
- points m,c
- gradient -x
- intercept y
- c=-xm +y

![|400](https://remnote-user-data.s3.amazonaws.com/zTUFQ23V8KtxBkz2EXZJe2sLdQHFPWUGWl4n5LX-pn2z_2G2wWmPle9-HwogSWl0l9_oN9IFVEx1sYZ3BjwZc87Vpgf_XEIHCyuTWDMqEsbKhkYl4OLgVaMOJtCV_WSO.png) 

If you apply this process to a set of points on a line in one space, you can generate a set of lines in another space. The crossing of these lines will be the values of m and c of the line in the original space

This is called the principle of duality
## **Pseudocode for [[Hough]] Transform**

If a point is an edge, then the corresponding line for that point is plot in the accumulator space

The crossing can be found by finding the point in the accumulator space with the highest value

The code checks through all points in the image
## **Applied [[Hough]] Transform**

![|400](https://remnote-user-data.s3.amazonaws.com/pULoNjuq99lzfswOd68QhSbjSVgTwM9MhRMsDWt9tWZCYIN6aarcLvDQgTBNIvaWR78wj4iyVA4pN7dYoBg7Xi3ey8CT8i6i1LGHim3aHx3B3oT4NJqgsPfh1d_gZhP5.png) 

This version of the [[Hough]] transform does not detect vertical lines
- Because the gradient of the line would tend to infinity, so we would need infinite accumulator space
## [[Hough]] Transform for all Lines

![|400](https://remnote-user-data.s3.amazonaws.com/D4lLuxt763s1AbgaTqr9Yqslgb-M3QzdeNI5kF21L7yTCRNfyxOyfz6HmKGF6f0ErH6UoWIsIZOT_JF0_myNPhUAe4XSxU1L7HyTNeZxQ_m_YC4xM7jjhhLEjQWy_Zjm.png) 

The crossing in the accumulator space represents the line in the original image

Use foot of normal to represent a line

![|400](https://remnote-user-data.s3.amazonaws.com/lyLGdw4Z7LWAVXvUw0M14iDiScP-2WVKNWsH-2ZOzSEajxWEJv6mgiq7S_AZZ850BSRwy8hLvjxA87F_bRdxXIHEEtydfJhXqtL7saJnpft54OQCVCMDVkevnKw3yjvU.png)  

$\rho = x\cos\theta + y\sin\theta$

![|400](https://remnote-user-data.s3.amazonaws.com/D4lLuxt763s1AbgaTqr9Yqslgb-M3QzdeNI5kF21L7yTCRNfyxOyfz6HmKGF6f0ErH6UoWIsIZOT_JF0_myNPhUAe4XSxU1L7HyTNeZxQ_m_YC4xM7jjhhLEjQWy_Zjm.png)  

Use foot of normal to represent a line

![|400](https://remnote-user-data.s3.amazonaws.com/lyLGdw4Z7LWAVXvUw0M14iDiScP-2WVKNWsH-2ZOzSEajxWEJv6mgiq7S_AZZ850BSRwy8hLvjxA87F_bRdxXIHEEtydfJhXqtL7saJnpft54OQCVCMDVkevnKw3yjvU.png) 

The crossing in the accumulator space represents the line in the original image