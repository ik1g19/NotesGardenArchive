---
title: "Low Power Wide Area Networks"
---

# **Where does LPWAN sit?**
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817175509.png|500]]
# **LoRa** 
### LoRa Modulation
- ISM 868/915MHz frequency
- Proprietary PHY layer (Semtech)
- Low data rate, simple low level links
	1. 3-50 kbit/s data rates

### Characteristics of LoRa
- Main gains of LoRa are Spread Spectrum and Chirp design 
#### Spread Spectrum and Chirp Design
- High immunity to interference
- Long range due to high sensitivity
- Doppler resistant
	- Good for fast moving things
- Multipath resistant
	- Better in urban environments with lots of reflecting surfaces
- Scalability
	- To lots of nodes transmitting on the same frequency

### LoRaWAN Architecture
![](https://remnote-user-data.s3.amazonaws.com/IktF8GGRSMcmYk43sB6QXPtHfDR_-Ia6f9SS7sVfaqLlHs7P7CDlS-8E9L1qia_Ku_4UhZu1sEd5iKDBf6AaitxrAFavCMySXcdhY0G4sTCtPp7qQ1ORF3oJmS-LViuw.png) 

### LoRaWAN Enabled Devices
- Vehicle detector
- Water meter
- CO$_2$
- Pressure
 
### Frequencies
- EU 863-870MHz
- USA 902-928MHz
- China 779-787 and 470-510MHz
- Channels and Restrictions 
	- In the EU, LoRaWAN typically utilises the 868MHz band
	- This band has restrictions limiting the amount of bandwidth which can be taken up by a single application
	- The most prevalent implemented solution is a duty cycle limitation
		- Longer packet = Less frequent
			- e.g.
				- 10 byte packet every 30 seconds
				- 250 byte packet every 10 minutes
			- A variable data rate means variable power consumption

### IDs
- Devices use a 64 bit DevEUI identifier
- And an Application ID - AppEUI
- When joining a device also gets a dynamic 32 bit DevAddr

### Frame Counter
- Network and device reject counters that are lower than expected
- Helps to prevent replay attacks

### LoRaWAN and The Things Network 
![](https://remnote-user-data.s3.amazonaws.com/r-Oc8J3eWREvYrd2HBDEhf_qv2UZkKa4Za_Fo59ukSuHDVjOwFt2h6i5qkBpTYWpow5SKfJA1fqrGpoCVUBOVF6vuhL5Gmn2Zes5CTSCwMhTq8IxLb3G0AyNDNMOtQbt.png) 

### Classes of Device
#### Class A
- Bidirectional
- Opens two receive windows after an uplink
 
#### Class b
- Time synchronised received windows for downlink messages
- Gateway sends beacons

#### class c
- Keeps receive windows open unless transmitting
- Low latency but high power use

### Typical LoRa Transceievers
- UART
- SPI

### Weightless
- Operates in ISM band (868MHz) and TV white space
- Intended for long range M2M communication
	- 5km range
	- Aims for 10 year battery life
	- $2 chip

### Nano Sat Comms
- Nano satellites are cheap to deploy and are an emerging possible LPWAN channel
- $5/month for global coverage
- 750 packets/device/month
- 200 bytes/packet
