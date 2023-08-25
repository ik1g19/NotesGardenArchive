---
title: Point Operators
---
 
# Histogram of an image

![|400](https://remnote-user-data.s3.amazonaws.com/7nH4rPBAlVRDXasCRZ7E8V-j856Rf8aR1ubAnmlUt3Dx6Mr_7d5D1hiNqwZ19WyFLem-H_kreDbEt8vMvwJnLmfaZlw6TVl1H3dbYcKJ7pOfj5_YsRJqDXFCOO9MbpKa.png)

The histogram shows the contrast
 
# Brightening an Image
$N_{x,y}=k\cdot O_{x,y} + l$

Where
- x and y are the coordinates 
- l is the level
- O is the old image
- N is the new image
- k is the gain
To change the brightness of an image, add or subtract to the level at each point

So to change the brightness of an image, choose values for $k$ and $l$

![|400](https://remnote-user-data.s3.amazonaws.com/CiQZ-oRyPwBVULu09_OrWcge-BtvEUGHrBLiY2_yVqSTGAURvksb7nx5micxvMTds84ccaSZJqg7g6u7JU-vWthi9ckuJg3liu-vqqi9SYMdawxdZYGI4N-FZU3fYHts.png) 
 
# Intensity Mappings
## Copy
![|400](https://remnote-user-data.s3.amazonaws.com/CduIDJwfhy1oPGyckj7iwy_Xt9fUXsSsZcC1U-KJGUNqqdeOeTWijhY_9sL-vgQ7v1YaDcnPyblitg1emrGPVhje10lnGCdnXLtL6OuxRhtAt7YGMOIWj9flyDuKiPVR.png)

What is the Mapping? - White becomes white and black becomes black 
## Brightness Inversion
![|400](https://remnote-user-data.s3.amazonaws.com/fh8KAus9iEHcOtKZwctf2jjeD-53-OIytUtEBQK4m0xh_x7bQNijHoK720JnOvSz-lGN_27D4WILLWmPYlBEEtlBhLyS9u8TQU7y6xXZCGWeO3f7Ias5FVWKyGErdLVn.png) 

What is the Mapping? - White values are swapped for black and black values are swapped for white

## Brightness Addition

![|400](https://remnote-user-data.s3.amazonaws.com/12DUf-6MAZAJGrt_67T2P7YY9d7nLq8w3mWk9L8WPc8om8cBbAjszZca5GSLIaiJNJWJJv9tJi-hFRlJJKejAYlkQGp77_aa36n31O7-11yM-cNEQoKcdEWXc4sMFrr9.png) 

What is the Mapping? - Involves a clipping process, as you cannot get whiter than white or blacker than black

## Brightness Scaling by Multiplication
What is the Mapping?
![|400](https://remnote-user-data.s3.amazonaws.com/aRx9GBtDCrd1CMietuO3TVUPmOk4JwoY1K6KGTPsKO3ZJ10TKlXkXMHsY-caSzE2zoSUFACQ3NAc_l1jCMoPIzgsHLzt494lukNfo0vmCkgZhd1yVdqyJylAEXcC-4UI.png) 

# Exponential and Logarithmic Point Operators
## Logarithmic Compression
### Brightness compression
![|200](https://remnote-user-data.s3.amazonaws.com/AWyiLa8PGwiJ9vz93oeum51FfNoRFXHMgxgk8Kye27-wMSl21Ym76YckETwKGI96Ms9NcXuJNrILBf7xeof_tcDcHR3jggkP0ckLjzW9louxQvfgxZJ3m2a1wpxwhNaW.png) 

$$N_{x,y}=log(O_{x,y}) $$

What does it do? - Replaces the value by the logarithm of its value
## Exponential Expansion
### Brightness expansion
 ![|200](https://remnote-user-data.s3.amazonaws.com/Qm-ubI-EKmOpbQUxHFbtKRSPGKMvg2nBbQuJPidU42OwWJVMQv__uSk_QfIdAleg8wtFz0QHyxj9-BFyjZ5UePDRf-tQAqzVB3FjH6VqIjZNtkoF3gfsV9j1l7oUA7D3.png) 

$$N_{x,y}=exp(O_{x,y})$$

What does it do?→Performs an exponential operation on each point

# Intensity Normalisation
Intensity [[Normalisation]] - Aim is to use all available grey levels for display
## Intensity Normalisation Process
Original Histogram

![|400](https://remnote-user-data.s3.amazonaws.com/BkS2MmNLNKwYmph3wyYTn8LFLXEeJ2NM42JFJHOGmrWFFusOa69MonNbhesv8SiJXkFuU2mUWVv-DINQGYF4LvUiKdGPP2l5lIptdSzqpvx67Dif_GiIXIIFtfYakRpi.png)

1. Shift the origin to zero (subtract the minimum value)

![|400](https://remnote-user-data.s3.amazonaws.com/N05Thqptywelz0hCsb1R2D07E2-YAK0zBnt4Xfh5GZqU-_fY5beROvWR1pgT7CqvyxPm5gDNyoYM9tbA6xMOIiplkYcswpdEZ3E0JUUAMzR4Km-eZ8p3OrFGPtDNz8CP.png) 
 
2. Scale brightness to use whole range

![|400](https://remnote-user-data.s3.amazonaws.com/PhSveFC1gJqeASuEnw7V6WrL1os9riWX8H9fx9Tk5fmYzAERNVzFY3WsVdZuILMJpQIlHDpW1sOC6QIoHRhyGGjiB5csPrtQkXMyRKBHvDP_FiPRnBPsejiniwGmuVNl.png) 

$$N_{x,y}=\frac{N_{max}-N_{min}}{O_{max}-O_{min}}\cdot (O_{x,y}-O_{min})+N_{min}$$
Where
- N - New image 
	- $N_{max}$ - Maximum output
	- $N_{min}$ - Minimum output
- $x,y$ - Coordinates
- O - Old image 
	- $O_{min}$ - Minimum input
	- $O_{max}$ - Maximum input

# Intensity Normalisation vs Histogram Equalization
## Intensity Normalised
- Used in Matlab's  imagesc
- Grey levels all weigh the same
- Grey levels all weigh the same

![|200](https://remnote-user-data.s3.amazonaws.com/VdyLwKK15lcZ9vtE932fIxY3N0U-GUlnvJ0nu5WJBmYp9wZa3F7vLukyNSHTucuI--XxGSpnXjLQJThDGR0NZSuqFdh3fDw30zSPu_cmX_qCfGej4NimJIPen8TOQ-pZ.png) 

![|200](https://remnote-user-data.s3.amazonaws.com/VdyLwKK15lcZ9vtE932fIxY3N0U-GUlnvJ0nu5WJBmYp9wZa3F7vLukyNSHTucuI--XxGSpnXjLQJThDGR0NZSuqFdh3fDw30zSPu_cmX_qCfGej4NimJIPen8TOQ-pZ.png)  

![|400](https://remnote-user-data.s3.amazonaws.com/KPYQI0jECosgTBzWl5nL27dtco3NfgBRrJ1kkBfDL2JoykqBR1yHPngsC7N7Hq-of6ieYwLUrC42-ZO9X9daPUvgjNPyWLSY8j1LoaGuMYxsxxGUaTrNNpEq02hTIwZc.png)  

![|400](https://remnote-user-data.s3.amazonaws.com/KPYQI0jECosgTBzWl5nL27dtco3NfgBRrJ1kkBfDL2JoykqBR1yHPngsC7N7Hq-of6ieYwLUrC42-ZO9X9daPUvgjNPyWLSY8j1LoaGuMYxsxxGUaTrNNpEq02hTIwZc.png) 

Used in Matlab's imagesc

## Histogram Equalized

![|200](https://remnote-user-data.s3.amazonaws.com/oGpaO2EnZMsttjm7KNod9enMGcHWbbHl_GIrWB9BQE8qjfXCo81aFZkf0F3MSEKT58nyzFSyipD1q8yXMxe-3axAHY1xudsvaVTT_pEzO7i2hbKr8-V7l8St5GRGtq36.png)  

- Grey levels have different weights
- Grey levels have different weights
- Aimed for human vision

![|400](https://remnote-user-data.s3.amazonaws.com/e7iUlWwaeED5t08N9fl4-KwF1sB8YQUx8oqKqAGkzGh3Pxv_XnMOVnLUt6UWLjTCQ_cTRPXDOL_18peVxGpCEMkQ-dVJgpksCWdbxxt0xUNZ_ecIm2Lkm6BTbnv4DYvU.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/e7iUlWwaeED5t08N9fl4-KwF1sB8YQUx8oqKqAGkzGh3Pxv_XnMOVnLUt6UWLjTCQ_cTRPXDOL_18peVxGpCEMkQ-dVJgpksCWdbxxt0xUNZ_ecIm2Lkm6BTbnv4DYvU.png)  

![|200](https://remnote-user-data.s3.amazonaws.com/oGpaO2EnZMsttjm7KNod9enMGcHWbbHl_GIrWB9BQE8qjfXCo81aFZkf0F3MSEKT58nyzFSyipD1q8yXMxe-3axAHY1xudsvaVTT_pEzO7i2hbKr8-V7l8St5GRGtq36.png) 

# Histogram Equalisation

![|200](https://remnote-user-data.s3.amazonaws.com/lojllLfXhNlF9c-tNV8kpFVLDHv5CDBkOE1azZHw1hdS25LBoE8G_Ra-r2jGNFPTqc6ZMWPaeGuzJF7lTJJgNAL9J1hP2XqQ0Jng7Y_3XlbCzykkA-hK3zKbn4Tsv_j2.png) 

The aim is a flat histogram

## Deriving the equation
The number of points (N^2) in the transformed and original image should be the same
- The sum of points per level is equal in the equalised and original image
$$\sum\limits_{l=0}^{M}O(l)=\sum\limits_{l=0}^{M}N(l)$$
The cumulative histogram up to the level p should be transformed to cover up to the level q
- This is the stage that gives us the equalisation function, that then takes us to the equalised image
$$\sum\limits_{l=0}^{p}O(l)=\sum\limits_{l=0}^{q}N(l)$$
The number of points per level in the output picture is N(l) = \frac{N^2}{N_{max}-N_{min}}
This can be rearranged into a mapping function for the output pixels at level q  
$$q=\frac{N_{max}-N_{min}}{N^2}\cdot \sum\limits_{l=0}^p O(l)$$
- Can be used as a lookup function
- Effective but non-linear and significant problems with noise
- Often used in medical image analysis
Calculating a cumulative histogram of the output picture
$$\sum\limits_{l=0}^{M}N(l)=q\cdot \frac{N^2}{N_{max}-N_{min}}$$ 

# Thresholding an Image
What is it?
- Set the point to white if above a certain threshold, otherwise black

$$N_{x,y}=\begin{cases}255 & if & N_{x,y}>threshold\\0 & otherwise\end{cases}$$

[[Thresholding]] at level 160

![|200](https://remnote-user-data.s3.amazonaws.com/G5arlwbtidFIklArByboCOSPTzjKoLiLiTV_zc_rTs1LaLrs-XF_9u0_pwVDKW98N3nCxvrxtZmZ25XiUM_G4JKriKEP0N2nkP1XLxjB2nUBpFc8wF_InxDPV70WZ4x3.png) 

[[Thresholding]] at level 127

![|200](https://remnote-user-data.s3.amazonaws.com/nnLhSsmAFeImLUVie9DSrhVuK-QwxWduhOnhHG2kpmcEfc4lpnVOPA1PBmWuuPIHOO4mx2u7RYKh2WOQbURTCoBrFxJDYQvJfWcyRUK0kbLaVSVF8Ts8uhpXwiLO4WMB.png) 
