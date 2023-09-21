---
title: "Radio Fundamentals"
---
# Concepts

- [Bluetooth](concepts/Bluetooth.md)
- [WiFi](WiFi.md)
- [GSM](GSM.md)
- [Modulation](Modulation.md)
- [LoRaWAN](LoRaWAN.md)

---
# **Radio Spectrum**
- Generally used for broadcasting 
	- Centre frequency determines characteristics of the channel we're creating
	- Using a greater frequency  
		- Send more data 
		- More easily use the bandwidth
	- Using a greater bandwidth  
		- Greater the width around the centre frequency
		- Greater data rate achievable
## **Different frequencies are allocated for different purposes**  
- IEEE 802.15.4, Bluetooth etc  
	- 2 .4GHz 
- WiFi  
	- 2 .4, 5 GHz and now 60 GHz
- ISM license free bands, sub-GHz  
	- 433, 868 MHz
- GSM-900  
	- Mobile: 890-915 MHz
	- Base: 925-960 MHz
- GSM-1800  
	- Mobile: 1710-1785 MHz
	- Base: 1805-1880 MHz
- 3G  
	- Base: 2210-2170 MHz
	- Mobile: 1920-1980 MHz
- 4G  
	- 800MHz, 1800, 2.6 GHz
## **Radio Propagation** 
- Changing voltage in a wire causes radio waves to be emitted
- These waves are detected by the receiving antenna
- Some data is expected to be lost

- Link Budget  
	- The summary of the gains/losses in a radio system
- Simplified, the received power is   
	- $P_{RX}=P_{TX}+G_{TX}+G_{RX}-\text{Losses}$
		- Where
		- $P_{RX}$ - Received power
		- $P_{TX}$ - Transmitter output power
		- $G_{TX}$ - Transmitter antenna gain
		- $G_{RX}$ - Receiver antenna gain 
## **Modulation**
- In order to transmit digital information, we need to send a sequence of bits. 
- This is hard to do over a radio link as you can't just change the radio signal on and off repeatedly
	- This is hard to do over a radio link as you can't just change the radio signal on and off repeatedly
	- Instead, we modulate a carrier frequency
### Attributes of the carrier frequency that we can modulate  
#### Amplitude
- e.g.
	- A=0 for 0 and A=1 for 1
#### Frequency
- e.g.
	- F=500 for 0 and F=1000 for 1
#### Phase
- e.g.
	- $\theta$=0 for 0 and $\theta$=$\frac{\pi}{2}$ for 1 
### Amplitude Shift Keying
- Used in AM radio
- Simple, but {{prone to interference}} 

### Frequency Shift Keying  
- Weather Faxing uses FSK modulation
 
### Phase Shift Keying 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220821184050.png|400]]
### Quadrature Phase Shift Keying
- Sends multiple bits simultaneously by using multiple phase shifts
- GPS uses Binary Phase Shift Keying

### Quadrature Amplitude Modulation
- Amplitude modulate two carrier frequencies with 90° (quadrature) phase shift
	- Combines different modulation schemes
#### Advantages   
- Packs more bits in
#### Disadvantages   
- Becomes more sensitive to noise as you increase its complexity
---

 - QAM64 is used in US cable TV

### Lora Modulation  
- Sends sweeps of frequencies
#### Advantages   
- Robust
- Good for long range
#### Disadvantages   
- Slow 
#### LORA Factors
- The max bitrate in Semtech's LORA depends on the "spreading factor"
	- There is a lower {{spreading factor}} for a higher {{data rate}} 
- The spreading factor also affects the {{sensitivity}} and {{range}} 

## **Applications of Modulation Schemes** 
### Bluetooth  
- GMSK - Minimum possible frequency shift and a Gaussian filter
- DQPSK - Differential encoding uses data to change rather than set the phase
### WiFi  
- BPSK and QPSK
- 16 and 64 QAM 
### GSM  
- GMSK
### Universal Mobile Telecommunications System (UMTS)  
- QPSK
### LORA  
- Low power LoRaWAN

## **Multiple Access**
- How can multiple devices use the same bands?
### Frequency Division Multiple Access 
- Divide frequency band into channels
- Assign each user a different channel
	- Uplink and downlink may be on different channels
- Used in analogue radio systems
- Bandwidth is wasted whenever a user is offline 

### Time Division Multiple Access
- Divide access to the frequency band into a number of distinct time slots 
- Used by GSM
- Requires time synchronisation
	- Difficult with mobile transceivers 
		- Base station informs mobiles of delay required depending on distance
		- Single slot available for registering with base station
####  Dynamic TDMA
- Users with different requirements may be allocated multiple time slots
- Used in Bluetooth

### Code Division Multiple Access
- User has access to the whole bandwidth for the entire duration
- Different CDMA codes are used to distinguish between different users
-  _**Used by 3G/UMTS**_   
	- Chip rate much higher than bit rate (256 chips/bit)
	- bandwidth only used when actually sending
