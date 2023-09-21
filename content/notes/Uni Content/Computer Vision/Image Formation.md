---
title: Image Formation
---

# Inverse Fourier Transformation

![|400](https://remnote-user-data.s3.amazonaws.com/UYGkq5xc9QjoeOtbV6kE7dPGvk1Pu8M76GmCNipB_IheLBf_Wo494PqC_ohxoFMbCX2IMCbX65e2ZRW_2JzMoLamowVsqS1FQY-og3fflaEwttqsxMXHzrlbwzsF5ZLv.png)  

Reconstructing a signal from its Fourier Transformation

![|400](https://remnote-user-data.s3.amazonaws.com/Y-TYs3gCUHiXJyGQ8AJ3DznFvV1hkY1nsaIYOH90E4oP28z18dQMbiA0_BsPHywTKOlrSeTtmUV8L3Cl6EEmH9qh9GBkSVhDRTRyf6Q7iWIlklCcwV2CWW0aIHyQ3K7d.png)  

![|400](https://remnote-user-data.s3.amazonaws.com/5uniLhK1OOzXyhDn23tTLb-hdlXII0mqFWv5DRebl-nJgpodlh8OQGeNCfsP-hHRFSJnP9gYHJVov_YN9qDqwIDoxWuWLsFvGHnCA3GpOwXk8wOMzYBL6Zi79F0GgGYC.png)

![|400](https://remnote-user-data.s3.amazonaws.com/osGP5L8-xsMRUBVvgCYWNqHC0AP3ja4ghxu_ophJatd1BOEkERZR3cr0uVde9-N2Qs3xX08nkGhv1gLy1MQlkmi9qymT0azn_o5jsQ-8RZcoiQ6BXvz8l-YNzwo6H8w5.png)  

Rectangular pulse is not reconstructed perfectly as the limits used are -6 to 6, if $-\infty$ to $\infty$ were used then the pulse would've been reconstructed perfectly 
Inverse Fourier transform is used for Reconstruction
## Decomposing an Image into Bits 
The Most Significant Bit carries the most information where as bit 0 is noise

![|400](https://remnote-user-data.s3.amazonaws.com/6tbj-umtqI9sre8wocOPv6ACbNCpBM7UFa-FM-vpPqiP5t0YFduBqxigNZ5XVifRY7GlE3eb-QDrRuoOoulDZ9zLStnRLgICKpt_OqqMtDowWe9Ee3DUN1o3cy2LvGdR.png) 

And here, bit 4 is the lighting
Images don't just have to be represented as integers, floating point values are also commonly used

![|400](https://remnote-user-data.s3.amazonaws.com/A-TC-l9NFw9Uqj432itokNYFck2y8VNQ2XsPQnupd6CHTpdfN21zhlb-tHgyhoGL3t_a_WWN_4lJLmxdNOaYD-8GvcGwJY6ejqPqTz9Jg-vgntW1o9Th_EaCB0ZhulQ8.png)  
## Image in terms of Frequency
Pixels in an image vary in intensity

![|200](https://remnote-user-data.s3.amazonaws.com/Hu-hJ9V492-kClk_tpaGrJ466x0JL1PtoJhvYzvYVX76MzdYvFG__u-ODeOiANOtCyGODem7MiRvMfBmkkfhi2No57nvIpBedA5WE02vDz9kJbInHffQCMFbzkeIgSL9.png) 

In this example image, there are lots of vertical structures, so there are horizontal frequencies where the intensity changes a lot travelling from left to right
Intensity varies depending on which direction you travel across an image
- High frequencies→are where the intensity changes a lot
- Low frequencies→are where the intensity doesn't change much
## Fourier Transformation of a Rectangular Pulse
![|400](https://remnote-user-data.s3.amazonaws.com/ziiB58lQn2ljA1bnxV2ph5Rt9ZnbCAZopP5js9FPktPvGVWf__Coy8XqCaEt8R6oPpTGGFLaxDdbHie93cojMWid_qLj_7THJAG9ryf1qL-C9gUypR7QjmSDGWsk9Tph.png)  
![|400](https://remnote-user-data.s3.amazonaws.com/2taCqxtQDTbrwPi5P4--KZzHE12AeRyARYCVxOgguWOiUuiGeuxNepNMFYsxxXDc2htbLPy0_sSXmRt00z81fsW-UNQTscB5y1eBmHDN_geKdRPhsSqiCkvPUpZVPXGg.png)  
## Magnitude and Phase of Fourier Transformation of a pulse 
![|400](https://remnote-user-data.s3.amazonaws.com/Hrq-_jNh4H-o3BH8SBfcV5OeEVuPDYLeeoJuUKkzX_YpdPZzJyPCUx56NRU49OZnmmJFTWuAVGnsXvc1atU9p0A95FGCfSN7oNdE2noawh2WrauqRmRfo2a9gqKgvypE.png)  
## Effects of Differing Image Resolution 
![|400](https://remnote-user-data.s3.amazonaws.com/ZA9t7uzW_i1aU2pIC251UOHOTv51rGDDlv8sVOZk0W6ECvW4ucz6H_S2gzpbtfJQDGdpWkMsYo7ugI1nwcnasIrMOGIuO3zzttrBC6oN-SqoCD1qeIRgynUC0syH4iOT.png)

Low resolution→Lose information
- But NxN points implies a lot of storage
	- How to choose an appropriate value for N?
## What does the Fourier Transformation Do?
![|400](https://remnote-user-data.s3.amazonaws.com/Zsu0D23pe2JV9V5B01rY9BgL77Xp4gz9_tqe3jvFpeQM14lqU-KWaYlFfXrtBGAr1vGIuvDHUzuujq23WpXHura_4bx0H_3OpXOEpPNMt1rw7hvzojtnRg2xhZ5C4zb9.png)   
The Fourier Transform can separate a complex signal into its fundamental frequencies, which when added together will give the original signal
Fourier's treatise - Periodic function is the result of adding up sine and cosine waves of different frequencies
## The Importance of Phase
![|400](https://remnote-user-data.s3.amazonaws.com/HG2aG7xeGNTtASIm2Xz2i4EarfDekc1BhECtECyGuGIMbDUOFnxakX2gNpQ1ZTccBmG_AbQDtslM-_x42_1A_SiYiV-Kr1tHgymMrUQJqGH8I0ONSQZCBvF-jdob9XsB.png)  
 
## Jean Baptiste Joseph Fourier   
- Invented transforms
- Basis of the Fourier Transformation - Any periodic function is the result of adding up sine and cosine waves of different frequencies
- Found a way to understand the sine waves and cosine waves that make up the original signal

## Fourier Transformation Formula
1. The Fourier Transformation is a function $a( )$ of a time-variant signal $p(t)$
2. The Fourier Transform is then $Fp=a(p(t))$ 
3. The transform is a function of frequency
4. So $Fp(f) = a(p(t))$ 
5. $\mathscr{F}$ stands for the Fourier transform
6. So $Fp(f) = \mathscr{F}(p(t)) = a(p(t))$ 
7. The function $a()$ is actually an integral of cosine and sine waves, $cas(t)$
8. So $Fp(f) = \mathscr{F}(p(t)) = \int_{-\infty}^{\infty} p(t)cas(t)dt$
9. $cas$ = 'cosine and sine' and $e^{-jft} = cos(ft)-jsin(ft)$ 
10. So $Fp(f) = \mathscr{F}(p(t)) = \int_{-\infty}^{\infty}p(t)e^{-jft}dt$
11. Where $j$ is the complex number $j = \sqrt{-1}$ 

![|400](https://remnote-user-data.s3.amazonaws.com/A-TC-l9NFw9Uqj432itokNYFck2y8VNQ2XsPQnupd6CHTpdfN21zhlb-tHgyhoGL3t_a_WWN_4lJLmxdNOaYD-8GvcGwJY6ejqPqTz9Jg-vgntW1o9Th_EaCB0ZhulQ8.png)  

## Inverse Fourier Transformation

Inverse Fourier Transformation - Reconstructing a signal from its Fourier transformation

![|400](https://remnote-user-data.s3.amazonaws.com/UYGkq5xc9QjoeOtbV6kE7dPGvk1Pu8M76GmCNipB_IheLBf_Wo494PqC_ohxoFMbCX2IMCbX65e2ZRW_2JzMoLamowVsqS1FQY-og3fflaEwttqsxMXHzrlbwzsF5ZLv.png)  