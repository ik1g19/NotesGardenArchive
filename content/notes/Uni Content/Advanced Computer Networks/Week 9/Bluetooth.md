---
title: "Bluetooth"
---

# **Personal Area Networks**  
- Short-range
- Body area networks
- Personal devices
# **2.4GHz Spectrum Band** 
- Globally unlicensed part of the spectrum
- Interference needs to be appropriately handled
- Aims to maximise bandwidth and minimise RF interference while operating at a very low power
# **Bluetooth**
## **Bluetooth 1.0**  
- Open specification
	- Publicly available
	- Royalty free
- 2.4GHz  
- Support multiple devices
- Low data rates and low duty cycles
	- < 1Mbit/s
- Low power
	- Intended for battery powered devices
## **Bluetooth Radio**
- Divides 2.4GHz radio in 79 channels
	- 1MHz per channel
- Uses Phase Shift Keying Modulation 
## **Frequency Hopping** 
- Transmissions frequently hop between channels to reduce interference
- Communication divided into slots
- Only one channel is working per time slot
- Each slot uses a random channel
- Reduced RF interference
	- Power is spread across the entire frequency band
## **Adaptive Frequency Hopping** 
- Reduces interference with WiFi competing for the same band
## **Piconets and Scatternets**  
- One master may connect up to 7 slaves
- No slave can communicate directly with another slave
- Master determines frequency hopping pattern
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819191522.png|300]]
#### Piconet  
- Network of multiple wireless devices connected using Bluetooth technology
#### Scatternet  
- Network of multiple Piconets using Bluetooth 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819191538.png|300]]
## **Packets**
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819191616.png|300]]
- Access Code - Which master or active slave should receive this package 
### Time Division Multiple Access 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819191651.png|300]]
### Multi-Slot Packets
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819191717.png|300]]
## **Frame Types**
- Bluetooth supports different frame types depending on the application
### Synchronous Connection Oriented
- Real time data
- Fixed slot in each direction
- Slots are reserved
- Not retransmitted
####  Throughput
- 240 bits of data
- For single slave and master pair, each getting 800 slots/second and using an 80 bit payload, this is 64kbps
- Sufficient for digital voice communication
### Asynchronous Connectionless Link
- Packet switched data
- Error correction using Hamming code
- Retransmission of failed frames
#### Throughput
- In slots not used for SCO links on a per-slot basis to any slave
	- 433.9 kbps
# **Bluetooh LE**  
- Designed for low energy devices (not voice)
- All slaves put in sleep mode unless a connection is initiated
# **Tags**
FILE TAGS: Bluetooth